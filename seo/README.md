<!-- .slide: data-background="#000000" -->

# Technical SEO 
### Lessons Learned

Norman Kämper-Leymann / @leymannx

---
<!-- .slide: data-background="#000000" -->

## What is technical SEO?

* Provide search engine-friendly markup. <!-- .element: class="fragment" data-fragment-index="1" -->

---
<!-- .slide: data-background="#000000" -->

## HTTPS everywhere and mobile optimization

---
<!-- .slide: data-background="#000000" -->

## Remove `h`-tags from side-wide elements 

* Drupal block labels: replace `<h2>` <!-- .element: class="fragment" data-fragment-index="1" -->
* <!-- .element: class="fragment" data-fragment-index="2" -->
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
* Card titles, regions etc. <!-- .element: class="fragment" data-fragment-index="3" -->
* Use `h`-tags only for structuring text <!-- .element: class="fragment" data-fragment-index="4" -->

---
<!-- .slide: data-background="#000000" -->

## Infinite scroll 

* Always also provide a pager, SEs don't execute Ajax-requests <!-- .element: class="fragment" data-fragment-index="1" -->
* relying on the sitemap is not enough, relevance gets calculated on-site <!-- .element: class="fragment" data-fragment-index="2" -->
* starting from page two add `<meta name="robots" content="noindex,follow"/>` <!-- .element: class="fragment" data-fragment-index="3" -->

---
<!-- .slide: data-background="#000000" -->

# What is link juice?

* value that's being passed from one page or site to another <!-- .element: class="fragment" data-fragment-index="1" -->
* consider a page on your site as an empty glass <!-- .element: class="fragment" data-fragment-index="2" -->
* every **external** site linking to this page fills the glass with a sip of juice <!-- .element: class="fragment" data-fragment-index="3" -->
* now consider this page has 4 links to other pages <!-- .element: class="fragment" data-fragment-index="4" -->
* every link spills 1/4 of the juice to the linked page <!-- .element: class="fragment" data-fragment-index="5" -->

---
<!-- .slide: data-background="#000000" -->

## Read more section

* latest articles <!-- .element: class="fragment" data-fragment-index="1" -->
* most read articles <!-- .element: class="fragment" data-fragment-index="1" -->
* strengthen your internal link graph <!-- .element: class="fragment" data-fragment-index="2" -->
* let strong pages inherit relevance <!-- .element: class="fragment" data-fragment-index="2" -->

---
<!-- .slide: data-background="#000000" -->

## Exclude category/taxonomy pages from indexing

* noindex,follow <!-- .element: class="fragment" data-fragment-index="1" -->
* no keyword optimised, no real text <!-- .element: class="fragment" data-fragment-index="2" -->
* you want visitors to find real pages with real content that then maybe link to other pages with real content <!-- .element: class="fragment" data-fragment-index="1" -->

---
<!-- .slide: data-background="#000000" -->

## One single `<nav>` for desktop and mobile

* Google bot needs to crawl many duplicate links <!-- .element: class="fragment" data-fragment-index="1" -->

---
<!-- .slide: data-background="#000000" -->

## Linkmasking irrelevant links

* internal links to unindexed pages <!-- .element: class="fragment" data-fragment-index="1" -->
* route link juice in the right direction <!-- .element: class="fragment" data-fragment-index="2" -->
* <!-- .element: class="fragment" data-fragment-index="3" -->
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
* <!-- .element: class="fragment" data-fragment-index="4" -->
  ```html
  <div data-ix-base64="aHR0cDovL2Jsb2cuajEtdmlzYS1pbnRyYXguY29tLz9zPSZjYXQ9Mjc="
      class="ix-base64">Foobar</div>
  ```

---
<!-- .slide: data-background="#000000" -->

## Responsive image fallback image style

* <!-- .element: class="fragment" data-fragment-index="1" -->
  ```html
  <picture>
      <source srcset="/sites/default/files/styles/hero_image_lg/cats.jpg?itok=wZfQREu3 1x" media="(min-width: 1024px)" type="image/jpeg">
      <source srcset="/sites/default/files/styles/hero_image_md/cats.jpg?itok=HydRt7uw 1x" media="(min-width: 620px)" type="image/jpeg">
      <source srcset="/sites/default/files/styles/hero_image_sm/cats.jpg?itok=gRkfE67k 1x" media="(min-width: 400px)" type="image/jpeg">
      <source srcset="/sites/default/files/styles/hero_image_xs/cats.jpg?itok=5rZSb561 1x" media="(min-width: 0px)" type="image/jpeg">
      <img src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7" alt="Beautiful cats" title="Beautiful cats">  
  </picture>
  ```
* This prevents having an transparent Pixel in base64 set as src attribute in responsive img tags inside `<picture>`. <!-- .element: class="fragment" data-fragment-index="2" -->
* They won't get indexed. Only have real images set as src. <!-- .element: class="fragment" data-fragment-index="3" -->

---
<!-- .slide: data-background="#000000" -->

## Cards

* always only link text <!-- .element: class="fragment" data-fragment-index="1" -->
* <!-- .element: class="fragment" data-fragment-index="2" -->
  ```html
  <div class="card my-box">
      blah blah blah.
      <a href="http://google.com">link</a>
  </div>
  ```
* <!-- .element: class="fragment" data-fragment-index="3" -->
  ```javascript
  $(".my-box").click(function() {
      window.location = $(this).find("a").attr("href"); 
      return false;
  });
  ```
* don't use image-links at all <!-- .element: class="fragment" data-fragment-index="4" -->

---
<!-- .slide: data-background="#000000" -->

## Structured data

* JSON-LD <!-- .element: class="fragment" data-fragment-index="1" -->
* Breadcrumb, FAQ <!-- .element: class="fragment" data-fragment-index="2" -->
* only elements that are visibile (show breadcrumbs also on mobile) <!-- .element: class="fragment" data-fragment-index="4" -->
* sample link to show SERP <!-- .element: class="fragment" data-fragment-index="4" -->
* https://www.drupal.org/node/2799067 <!-- .element: class="fragment" data-fragment-index="5" -->

---
<!-- .slide: data-background="#000000" -->

## Remove node/ID shortlinks

* `<link rel="shortlink" href="https://example.com/node/ID">` <!-- .element: class="fragment" data-fragment-index="1" -->
* 301 forwarding causes link juice loss <!-- .element: class="fragment" data-fragment-index="2" -->

---
<!-- .slide: data-background="#000000" -->

## Remove self-referential links

* `<h1><a href="https://example.com/hello-world" rel="bookmark">Hello World</a></h1>` <!-- .element: class="fragment" data-fragment-index="1" -->
* single-post.php <!-- .element: class="fragment" data-fragment-index="2" -->

---
<!-- .slide: data-background="#000000" -->

# Language switcher

* Remove link to node/ID when no translation exist <!-- .element: class="fragment" data-fragment-index="1" -->
* https://www.drupal.org/project/language_switcher_extended <!-- .element: class="fragment" data-fragment-index="2" -->

---
<!-- .slide: data-background="#000000" -->

# Rabbit Hole

* https://www.drupal.org/project/rabbit_hole <!-- .element: class="fragment" data-fragment-index="1" -->
* prevent certain single nodes being visited or indexed (e.g. FAQs) <!-- .element: class="fragment" data-fragment-index="2" -->

---
<!-- .slide: data-background="#000000" -->

## 404 Links

* 301 forwarding <!-- .element: class="fragment" data-fragment-index="1" -->

---
<!-- .slide: data-background="#000000" -->

# Thank you

* Follow me on Twitter: https://twitter.com/leymannx
* Markdown to Slideshow MarkShow: https://mark.show
