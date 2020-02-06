<!-- .slide: data-background="#000000" -->

# Local Drupal/PHP development with DDEV

Norman Kämper-Leymann

Senior PHP Developer at IBM iX – Aperto

https://twitter.com/leymannx

---
<!-- .slide: data-background="#000000" -->

## Requirements

Docker

Homebrew/Linuxbrew/Chocolatey

`brew tap drud/ddev && brew install ddev` OR `choco install ddev`

---
<!-- .slide: data-background="#000000" -->

## Quickstart

`mkdir foobar && cd foobar` <!-- .element: class="fragment" data-fragment-index="1" -->

`ddev config --project-type php` <!-- .element: class="fragment" data-fragment-index="2" -->

`ddev composer create drupal-composer/drupal-project:8.x-dev` <!-- .element: class="fragment" data-fragment-index="3" -->

`ddev config --project-type drupal8 && ddev restart` <!-- .element: class="fragment" data-fragment-index="4" -->

`ddev exec drush -y site:install --account-name=admin --account-pass=admin` <!-- .element: class="fragment" data-fragment-index="5" -->

https://foobar.ddev.site <!-- .element: class="fragment" data-fragment-index="6" -->

---
<!-- .slide: data-background="#000000" -->

## Under the hood

`.ddev/config.yaml` 

`web/sites/default/settings.ddev.php`

`.ddev/homeadditions/.bash_aliases`

---
<!-- .slide: data-background="#000000" -->

## Git Clone Example

`git clone git@github.com:acme/foobar.git && cd foobar`

`ddev composer install -n` OR `composer install -n && ddev start`

`ddev exec drush -y si --account-name=admin --account-pass=admin` OR `--existing-config` 

`ddev exec drush -y cset system.site uuid 2afd7494-a2d0-4c49-a4d5-8c36905b3e7b`

`ddev exec drush -y ev '\Drupal::entityTypeManager()->getStorage("shortcut_set")->load("default")->delete();'`

`ddev exec drush -y cim`

https://foobar.ddev.site`

---
<!-- .slide: data-background="#000000" -->

## Commands

`ddev help` <!-- .element: class="fragment" data-fragment-index="1" -->

`ddev exec` <!-- .element: class="fragment" data-fragment-index="2" -->

`ddev ssh` <!-- .element: class="fragment" data-fragment-index="3" -->

`ddev export-db` <!-- .element: class="fragment" data-fragment-index="4" -->

`ddev import-db` <!-- .element: class="fragment" data-fragment-index="5" -->

`docker ps` <!-- .element: class="fragment" data-fragment-index="6" -->

---
<!-- .slide: data-background="#000000" -->

## Thank you!

https://ddev.readthedocs.io/en/latest/users/cli-usage/#drupal-8-quickstart

https://github.com/drud/ddev/pull/2071/files

https://ddev.readthedocs.io/en/stable/users/performance/#using-nfs-to-mount-the-project-into-the-container
