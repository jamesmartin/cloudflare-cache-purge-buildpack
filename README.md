# ☁️ 🔥 💵 🔪

Purges your Heroku application's Cloudflare cache on deployment.

This buildpack makes use of Heroku's built-in [multi
buildpack](https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app)
functionality to make a HTTP DELETE request to the [Cloudflare purge all files
API](clou://api.cloudflare.com/#zone-purge-all-files). Each time you deploy
your Heroku app, the cache will be cleared.


## Configuration

You will need:

1. Your [Cloudflare API key and email address](https://api.cloudflare.com)
1. The [Zone ID](#getting-your-zone-id) of the site that Cloudflare is caching

Run the following against your Heroku application:

```
heroku config:set CF_EMAIL=email@example.com
heroku config:set CF_ZONE_ID=my_zone_id
heroku config:set CF_AUTH_KEY=my_cloudflare_api_key

heroku buildpacks:add https://github.com/jamesmartin/cloudflare-cache-purge-buildpack.git
git push heroku master
```

## Getting your Zone ID

The Cloudflare Zone ID for your site can be obtained via the API:

1. Clone this repository locally
1. Edit the [cf](./cf) file to include your Cloudflare API key and email address
1. Run the `zones` command:
  ```
    $ ./cf bin/zones
  ```
Find the Zone ID of your site in the JSON output of `zones`. E.g:

```json
{
  "result": [
  {
    "id":"this-is-your-zone-id",
    "name":"example.com",
    "status":"active",
    ...
```
