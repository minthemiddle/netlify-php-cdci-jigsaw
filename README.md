# Test Netlify's continuous deployment using PHP + Jigsaw

- This repo is a demo project, using the `PHP` static page generator [Jigsaw by Tighten Co](https://github.com/tightenco/jigsaw)

## Getting started
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