<!-- .slide: data-background="#000000" -->

# DDEV, BLT and Lightning

---
<!-- .slide: data-background="#000000" -->

### Requirements (Mac)

* Docker
* Homebrew
* DDEV
* https://gist.github.com/leymannx/ca3a1a6298a796a185c9735e3c821f58

---
<!-- .slide: data-background="#000000" -->

### Drupal

* `mkdir -p ~/Sites/foobar && cd ~/Sites/foobar</pre>` <!-- .element: class="fragment" data-fragment-index="1" -->
* `ddev config --project-type php` <!-- .element: class="fragment" data-fragment-index="2" -->
* `ddev composer create drupal-composer/drupal-project:8.x-dev` <!-- .element: class="fragment" data-fragment-index="3" -->
* `ddev config --project-type drupal8 && ddev start` <!-- .element: class="fragment" data-fragment-index="4" -->
* `ddev exec drush -y site:install --account-name=admin --account-pass=admin` <!-- .element: class="fragment" data-fragment-index="5" -->
* `http://foobar.ddev.site` <!-- .element: class="fragment" data-fragment-index="5" -->

---
<!-- .slide: data-background="#000000" -->

### Commands

* `ddev help` <!-- .element: class="fragment" data-fragment-index="1" -->
* `ddev exec` <!-- .element: class="fragment" data-fragment-index="2" -->
* `ddev ssh` <!-- .element: class="fragment" data-fragment-index="3" -->
* `ddev export-db` <!-- .element: class="fragment" data-fragment-index="4" -->
* `ddev import-db` <!-- .element: class="fragment" data-fragment-index="5" -->

---
<!-- .slide: data-background="#000000" -->

### DDEV and BLT

* https://github.com/lcatlett/blt-ddev
* `composer create-project --no-interaction acquia/blt-project mysite`
* `cd mysite` && `composer require lcatlett/blt-ddev`
* `blt recipes:ddev --no-interaction`
* `ddev blt setup` – Setup Drupal, init Git, init Behat
* `ddev blt behat`

---
<!-- .slide: data-background="#000000" -->

### Lightning

* Well ...
* Layout, Preview, Workflow, Media, [API-First](https://github.com/acquia/lightning#api-first)
* We have also embedded hundreds of automated tests allowing developers to implement continual integrations pipelines that monitor major functionality, essentially providing a safe environment to innovate with their own custom code additions to Lightning.
* https://github.com/acquia/lightning/tree/8.x-4.x/tests
* `drush site:install lightning --existing-config`

---
<!-- .slide: data-background="#000000" -->

### What else I wanted to mention

* https://circleci.com/docs/2.0/circleci-images/
* https://jenkins.io/doc/book/pipeline/jenkinsfile/
* https://github.com/leymannx/drupal-circleci-behat
* [GitHub Actions](https://github.com/marketplace/actions/setup-php-action)

---
<!-- .slide: data-background="#000000" -->

# Thank you!
