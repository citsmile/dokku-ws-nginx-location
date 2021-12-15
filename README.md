# dokku-ws-nginx-location

It is quite challenging to run WebSockets as a separate service on the same server with the web application. [AnyCable][anycable] suggests creating a separate app in a Heroku-style deployment.

To get around this and deploy AnyCable to the same app (yet another containter) we configure [dokku][dokku] to route an application's "/ws" location to a container of a "ws" process type that is declared via a Procfile like

```
ws: bundle exec rake anycable:start
```

The rake task is defined as:
```
namespace :anycable do
  desc 'Start any cable'
  task :start do
    exec 'bundle exec anycable --server-command="anycable-go --host=0.0.0.0 --port=8080 --path=/ws/cable --health-path=/ws/health"'
  end
end
```

## Installation

```sh
# dokku 0.4+
dokku plugin:install https://github.com/citsmile/dokku-ws-nginx-location.git
```

## Customization

It currently templates out an nginx configuration that is included in this plugin. If you'd like to provide a custom template for your application, you should copy the existing template into your "$DOKKU_ROOT/$APP" directory as the file "ws.conf.template". The next time you deploy, Nginx will use your template instead of the default.

[anycable]: https://docs.anycable.io/deployment/heroku
[dokku]: https://github.com/progrium/dokku
