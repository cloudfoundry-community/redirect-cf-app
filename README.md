# Redirect old app to new path route

We previously hosted our blog at https://blog.starkandwayne.com but once Cloud Foundry supported path-based routes we moved it to https://www.starkandwayne.com/blog. That's great, except all the old URLs are being used/stored/documented around on the internets.

This little Cloud Foundry application is now run at https://blog.starkandwayne.com and returns an HTTP redirect to the https://www.starkandwayne.com/blog/path/that/was/requested.

It uses the [staticfile buildpack](https://github.com/cloudfoundry/staticfile-buildpack) to deploy a bespoke `nginx.conf`. That's it.

## Deploy

To map any requests sent to `blog.yourcompany.com` to the base URL `https://www.yourcompany.com/blog`:

```
cf push redirect-cf-app --no-start -n blog -d yourcompany.com
cf set-env redirect-cf-app REDIRECT_URL https://www.yourcompany.com/blog
cf start redirect-cf-app
```
