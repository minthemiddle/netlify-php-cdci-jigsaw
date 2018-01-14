# Test Netlify's continuous deployment using PHP + Jigsaw

- This repo is a demo project, using the `PHP` static page generator [Jigsaw by Tighten Co](https://github.com/tightenco/jigsaw)

## Build locally
- `git clone git@github.com:minthemiddle/netlify-php-cdci-jigsaw.git`
- `cd netlify-php-cdci-jigsaw`
- `composer require` to install all required PHP packages locally
- `vendor/bin/jigsaw init`
- `npm install` or `yarn` to install all required Javascript packages
- `gulp watch` will compile the source to static pages
- Alternatively, you can manually generate your page with Jigsaw's CLI: `vendor/bin/jigsaw build local` and `vendor/bin/jigsaw build production`

## How to customize the content

- `source` is where your content lives
- `Jigsaw` uses [`Laravel's Blade Template Engine`](https://laravel.com/docs/5.5/blade)
- All `*.blade.php` in `source` will be transformed to `/*/` on your live site, so `about.blade.php` will become `domain.com/about/`
- The pre-installed templates all extend `source/_layouts/master.blade.php`


## Build on Netlify

- Netlify's build image installs `php5-cli` and `php5-cgi` via `apt-get` ([https://github.com/netlify/build-image/blob/master/Dockerfile](see l.23), but unfortunately no `php7`
- All Laravel based tools need at least [https://laravel.com/docs/5.5/installation](`php7.0.0`)
- Netlify's build image uses `phpbrew` and installs `5.6` (which was released on 28 August 2014 and will be supported only until 31 December 2018 )
- To use your tools, you need to install a newer version with `phpbrew`
- `phpbrew install 7.1.3 +default && phpbrew switch 7.1.3` will work, for example, but the build time is _~ 10 minutes_
- A working `netlify.toml` build commands reads like this

```toml
[build]
command = "source /opt/buildhome/.phpbrew/bashrc && phpbrew install 7.1.3 +default && phpbrew switch 7.1.3 && phpbrew app get composer && composer require tightenco/jigsaw && ./vendor/bin/jigsaw build"
publish = "/build_local"
```

## Next steps

- Suggest Netlify to upgrade to `PHP7` (it is downward compatible and x-times faster and safer)