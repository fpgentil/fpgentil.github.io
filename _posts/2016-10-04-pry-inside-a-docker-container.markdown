---
title:  "Using binding.pry inside a Docker container"
date:   2016-10-04 18:00:00
description:
---

Quick tip for Ruby developer who are using Docker and can't debug their code with pry.
For those who don't know, [pry][pry] is an awesome IRB shell for Ruby.

This is a simple `.docker-compose.yml` file with a web app and a MySql database.

```
web:
  build: .
  volumes:
    - .:/myapp
  ports:
    - "3000:3000"
  links:
    - db:db
db:
  image: mysql
  environment:
    MYSQL_ROOT_PASSWORD: abc123
  ports:
    - "3306:3306"
```

All you have to do is run your container with the following command:

```
$ docker-compose run --service-ports web
```

This is my `HomeController`

```
class HomeController < ApplicationController
    def index
        binding.pry
    end
end
```

Trying things out

```
$ curl localhost:3000
```

```
From: /myapp/app/controllers/home_controller.rb @ line 3 HomeController#index:

    2: def index
 => 3:     binding.pry
    4: end

[1] pry(#<HomeController>)>
```

Hope it helps :)

[pry]:http://pryrepl.org/
