---
title:  "Install pg gem on MacOS"
date:   2017-03-21 18:00:00
description:
---

If you're facing an error while installing like this one:

```
Building native extensions. This could take a while... ERROR: Error installing pg: ERROR: Failed to build gem native extension.
```

Try downloading [Postgress.app][pgapp] and then install the gem this way:

```
gem install pg -- --with-pg-config=/Applications/Postgres.app/Contents/Versions/9.6/bin/pg_config
```

PS. Remember to specify Postgres.app version above.

Cheers :)

[pgapp]: https://postgresapp.com/