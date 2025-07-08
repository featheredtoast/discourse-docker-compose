# Docker compose discourse

A sample docker compose image for Discourse

Vanilla discourse, no plugins, but batteries included - no bootstrap steps needed.

Check the docker-compose.yml file for how it's setup.

As is, it runs a testing mailhog instance for mail, postgres 15, and latest built tests-passed.

## Components

Web is built from `launcher build web_only`. The rest of the jobfile is shuffling docker images, dealing with platform arguments, and figuring out version tags.

See https://github.com/featheredtoast/discourse_docker/blob/refs/heads/toast/build-web-only/.github/workflows/push-web-only.yml#L80 for image building, as that line specifically is the only thing needed to build a public image.

See https://github.com/featheredtoast/discourse-db for running a customized postgres image, tuned to Discourse with the same customizations as the discourse_docker data image.

## Pitfalls

UI Upgrades work, but if the image is destroyed, and recreated post-update, that might be less than ideal as migrations may be destructive. I suspect this is more likely to happen with docker-compose, as the user has no easy ability to rebuild from the CLI.

No plugins are here - there's no good way to dynamically load plugins (yet). It's always possible to build your own images.
