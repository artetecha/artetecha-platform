# Modern WordPress development and deployment workflow

This repository hosts the codebase for two sites, both

- are built using [WordPress.org](https://wordpress.org)
- are deployed on [Platform.sh](https://platform.sh) in [Multi-App setup](https://docs.platform.sh/configuration/app/multi-app.html)
- have their codebase managed via [Composer](https://getcomposer.org), thanks to [`johnbolch/wordpress`](https://github.com/johnpbloch/wordpress) and [WordPress Packagist](https://wpackagist.org)
- have their dependencies automatically upgraded by [Dependabot](https://dependabot.com) and automatically merged by [Mergify](https://mergify.io) when builds pass
- have a [Cloudflare](https://www.cloudflare.com) CDN in front of them
- use [GitHub Actions](https://github.com/features/actions) as CI/CD and Cron Scheduler

Also, one of the two sites is not in English, and uses translation files for WordPress core, themes, and plugins for an optimal setup.

## WordPress

WordPress remains by far the CMS that is easiest to adopt, and that provides a fast time to market in the majority of use cases. There is so much high quality stuff out there for WordPress, be it OSS or Premium, that one can have beautiful sites powered by an easy-to-use CMS up and running in no time. 

## Platform.sh

***Disclaimer**: I am not affiliated with Platform.sh in any way, shape or form. I am simply a happy user.*

Platform.sh provide an incredibly flexible and powerful PaaS. As they like to call it, it is the Idea-to-Cloud PaaS. With a GitHub integration, you can have a child environment cloned from your production environment for each pull request, and a Status Check that runs a build on Platform.sh out of the new branch, so to verify that the changes do not break anything. 

Feel free to poke around the Platform.sh configuration file in this repo to see how the sites were set up with a multi-container deployment comprising of various services. 

## Dependabot

Now part of the GitHub family, it provides a free plan for public repositories, and it supports PHP+Composer. You can configure it to decide what kind of upgrades you want to perform on your dependencies, and the bot will issue pull requests periodically, avoiding stale depenencies. 

## Mergify

This service, too, provides a free plan for public repositories. Youn can configure it with a number of conditions that, when met, will trigger an automatic merge of your pull requests. 

## Cloudflare

Cloudflare is one of the CDNs best [supported by Platform.sh](https://docs.platform.sh/golive/cdn.html); it is also one that provides a good free plan.
When you combine that with the awesome plugin [WP Cloudflare Super Page Cache](https://wordpress.org/plugins/wp-cloudflare-page-cache/), choosing Cloudflare for your personal sites becomes really a no-brainer.

## WordPress translation files and Composer

WordPress Packagist does not provide such files at the moment. Thankfully, the OSS community never rests, and [`inpsyde/wp-translation-downloader`](https://github.com/inpsyde/wp-translation-downloader) is a great Composer plugin to manage WordPress translations.

## GitHub Actions

It seemed like the obvious choice. Currently no particular CI/CD task is implemented, as Platform.sh provide their own built-in CI/CD for builds and deployments. Moreover, I do not require particular testing at present, so I am not using Actions for that either. However, I am using it as Cron Scheduler, to perform regular tasks on my Platform.sh project. 

Although Platform.sh allow you to do that by defining Cron Jobs [on their own platform](https://docs.platform.sh/golive/steps.html#4-bonus-steps-optional), I chose to have this functionality decoupled from Platform.sh. 
