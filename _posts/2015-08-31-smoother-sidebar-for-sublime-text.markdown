---
title:  "Smoother sidebar for Sublime Text"
date:   2015-08-31 11:00:00
description:
---

I mentioned here before that I work [Sublime Text 3][sublime-text-3] for my daily coding life! If there's something that I particularly don't like it is the sidebar theme. I think it contrasts too much with the current open tab one, unless you use a white based theme.

I love monokai and have been using it since the beginning.
Here is a simple trick to make the sidebar look better.

## Default sidebar
![zsh](/assets/images/sidebar/default-sidebar.png)

## Modified sidebar
![zsh](/assets/images/sidebar/modified-sidebar.png)

All you have to do is open your Sublime Text default configurations, if you're on MacOS it can be found here

```
/Users/<USER_NAME>/Library/Application Support/Sublime Text 3/Packages/User
```

and the file is named

```
Default.sublime-theme
```

in case you don't have it, just create one. The whole configuration can be found [here][monokai-theme].

In case you wan't to return to the original one, you can replace back with this [one][defaul-theme] or simply delete the file.

I hope it helps the SublimeText users out there.
Cheers.

[sublime-text-3]: http://www.sublimetext.com/3
[monokai-theme]: https://gist.github.com/fpgentil/f3d8bd1ead809839b88a
[defaul-theme]: https://gist.github.com/fpgentil/07d821db7094beafb7a3
