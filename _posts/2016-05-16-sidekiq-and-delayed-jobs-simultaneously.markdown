---
title:  "Using Sidekiq and DelayedJob simultaneously"
date:   2016-05-16 08:00:00
description: "How to deal with both implementation of `delay` method"
---

I'm working on a project at the moment in which DelayedJob was the one responsible for doing all the background job. For a new feature, we have decided to use Sidekiq instead.

It was going well until I remembered that both of them implements the method `delay`.

It is known that DelayedJob stores the job into a MySQL database (in our case) and process it later. On the other hand, Sidekiq uses redis for handling the jobs.

It is our intention to move all the backgound work to Sidekiq one day, but that's a whole another story.

Just to mention, in order not to worry about the `delay` method in DelayedJob, we can setup like this:

```ruby
Delayed::Worker.delay_jobs = false
```

This will ignore everytime you call a method through `delay` and your specs are good to go.

```ruby
my_object.delay.my_method
```

If you prefer, you can disable it only for the test environment.

```ruby
Delayed::Worker.delay_jobs = !Rails.env.test?
```

After adding Sidekiq gem to Gemfile I realized that a huge amount of tests broke!

Fortunately, we can _disable_ the `delay` method in order not to conflict with the ones implemented by DelayedJob.

```ruby
Sidekiq.remove_delay
```

This will disable all the `delay_` method that Sidekiq implements:

```
- delay
- delay_for
- delay_until
```

If you still want them to be used by both Sidekiq and DelayedJob, you can still make it happen.

```ruby
Sidekiq.hook_rails
```

This will give you the opportunity to use them as:

```
- sidekiq_delay
- sidekiq_delay_for
- sidekiq_delay_until
```

You can read more about it [here][sidekiq-doc]

Cheers.

[sidekiq-doc]:https://github.com/mperham/sidekiq/wiki/Delayed-extensions#disabling-extensions
