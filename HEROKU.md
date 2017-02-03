# Heroku deployment

```bash
heroku create wagon-db --region=eu
echo '{}' > composer.json
git add composer.json
git commit -m "add composer.json for PHP app detection"
heroku buildpacks:set heroku/php
heroku addons:create cleardb:ignite
$(ruby -e 'require "uri"; uri = URI.parse(ARGV[0]); puts "mysql -u#{uri.user} -p#{uri.password} -h#{uri.host} -D#{uri.path.gsub("/", "")}"' `heroku config:get CLEARDB_DATABASE_URL`) < backend/php-mysql/database.sql
git push heroku master
heroku domains:add db.lewagon.org
```
