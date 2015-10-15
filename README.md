# dokku-faye-nginx-location

It's often tricky to get [faye][faye] running using it's default settings. Faye normally runs on port 9292 which is blocked on many firewalls. To get around this we configure [dokku][dokku] to route an application's "/faye" location to a container of a "faye" process type that is declared via a Procfile like

```
faye: bundle exec rackup faye.ru -E production
```

## Installation

```sh
# dokku 0.4+
dokku plugin:install https://github.com/abulava/dokku-faye-nginx-location.git
```

## Customization

It currently templates out an nginx configuration that is included in this plugin. If you'd like to provide a custom template for your application, you should copy the existing template into your "$DOKKU_ROOT/$APP" directory as the file "faye.conf.template". The next time you deploy, Nginx will use your template instead of the default.

[faye]: https://github.com/faye/faye
[dokku]: https://github.com/progrium/dokku
