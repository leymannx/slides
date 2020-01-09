<!-- .slide: data-background="#000000" -->

# Technical SEO – Lessons Learned

---

<!-- .slide: data-background="#000000" -->

* Norman Kämper-Leymann
* Senior PHP Developer at IBM IX – Aperto
* https://www.drupal.org/u/leymannx

---
<!-- .slide: data-background="#000000" -->

## What is technical SEO?

* Optimizing a website for the crawling and indexing phase <!-- .element: class="fragment" data-fragment-index="1" -->
* Providing search engine-friendly markup. <!-- .element: class="fragment" data-fragment-index="2" -->

---
<!-- .slide: data-background="#000000" -->

## HTTPS everywhere and mobile optimization

---
<!-- .slide: data-background="#000000" -->

## Remove `h`-tags from side-wide elements 

* Drupal block labels: replace `<h2>` 
* 
  ```twig
  <div{{ attributes.addClass(classes) }}>
    {{ title_prefix }}
    {% if label %}
      <h2{{ title_attributes }}>{{ label }}</h2>
    {% endif %}
    {{ title_suffix }}
    {% block content %}
      {{ content }}
    {% endblock %}
  </div>
  ```
* Card titles, regions etc. 
* Use `h`-tags only for structuring text 

---
<!-- .slide: data-background="#000000" -->

## Infinite scroll 

* Always also provide a pager, SEs don't execute Ajax-requests 
* relying on the sitemap is not enough, relevance gets calculated on-site 
* starting from page two add `<meta name="robots" content="noindex,follow"/>` 

---
<!-- .slide: data-background="#000000" -->

# What is link juice?

* value that's being passed from one page or site to another 
* consider a page on your site as an empty glass 
* every **external** site linking to this page fills the glass with a sip of juice 
* now consider this page has 4 links to other pages 
* every link spills 1/4 of the juice to the linked page 

---
<!-- .slide: data-background="#000000" -->

## Read more section

* latest articles 
* most read articles 
* strengthen your internal link graph 
* let strong pages inherit relevance 

---
<!-- .slide: data-background="#000000" -->

## Exclude category/taxonomy pages from indexing

* noindex,follow 
* no keyword optimised, no real text 
* you want visitors to find real pages with real content that then maybe link to other pages with real content 

---
<!-- .slide: data-background="#000000" -->

## One single `<nav>` for desktop and mobile

* Google bot needs to crawl many duplicate links 

---
<!-- .slide: data-background="#000000" -->

## Linkmasking irrelevant links

* internal links to unindexed pages 
* route link juice in the right direction 
* 
  ```javascript
  (function($) {
      $(document).ready(function() {
          var $base64 = $('.ix-base64');
          $base64.off('click');
          $base64.on('click', function(e) {
              e.preventDefault();
              window.location = atob($(this).attr('data-ix-base64'));
          });
      });
  })(jQuery);
  ```
* 
  ```html
  <div data-ix-base64="aHR0cDovL2Jsb2cuajEtdmlzYS1pbnRyYXguY29tLz9zPSZjYXQ9Mjc="
      class="ix-base64">Foobar</div>
  ```

---
<!-- .slide: data-background="#000000" -->

## Responsive image fallback image style

* 
  ```html
  <picture>
      <source srcset="/sites/default/files/styles/hero_image_lg/cats.jpg?itok=wZfQREu3 1x" media="(min-width: 1024px)" type="image/jpeg">
      <source srcset="/sites/default/files/styles/hero_image_md/cats.jpg?itok=HydRt7uw 1x" media="(min-width: 620px)" type="image/jpeg">
      <source srcset="/sites/default/files/styles/hero_image_sm/cats.jpg?itok=gRkfE67k 1x" media="(min-width: 400px)" type="image/jpeg">
      <source srcset="/sites/default/files/styles/hero_image_xs/cats.jpg?itok=5rZSb561 1x" media="(min-width: 0px)" type="image/jpeg">
      <img src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" alt="Beautiful cats" title="Beautiful cats">  
  </picture>
  ```
* This prevents having an transparent Pixel in base64 set as src attribute in responsive img tags inside `<picture>`. 
* They won't get indexed. Only have real images set as src. 

---
<!-- .slide: data-background="#000000" -->

## Cards

* always only link text 
* 
  ```html
  <div class="card my-box">
      blah blah blah.
      <a href="http://google.com">link</a>
  </div>
  ```
* 
  ```javascript
  $(".my-box").click(function() {
      window.location = $(this).find("a").attr("href"); 
      return false;
  });
  ```
* don't use image-links at all 

---
<!-- .slide: data-background="#000000" -->

## Structured data

* JSON-LD 
* Breadcrumb, FAQ 
* only elements that are visibile (show breadcrumbs also on mobile) 
* sample link to show SERP 
* https://www.drupal.org/node/2799067 

---
<!-- .slide: data-background="#000000" -->

## Remove node/ID shortlinks

* `<link rel="shortlink" href="https://example.com/node/ID">` 
* 301 forwarding causes link juice loss 

---
<!-- .slide: data-background="#000000" -->

## Remove self-referential links

* `<h1><a href="https://example.com/hello-world" rel="bookmark">Hello World</a></h1>` 
* single-post.php 

---
<!-- .slide: data-background="#000000" -->

# Language switcher

* Remove link to node/ID when no translation exist 
* https://www.drupal.org/project/language_switcher_extended 

---
<!-- .slide: data-background="#000000" -->

# Rabbit Hole

* https://www.drupal.org/project/rabbit_hole 
* prevent certain single nodes being visited or indexed (e.g. FAQs) 

---
<!-- .slide: data-background="#000000" -->

## 404 Links

* 301 forwarding 

---
<!-- .slide: data-background="#000000" -->

# Thank you!

* https://github.com/leymannx/slides
* Markdown to Slideshow MarkShow https://mark.show
