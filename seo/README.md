
# Technical SEO 
## Lessons Learned

Norman Kämper-Leymann / leymannx

---

# What is technical SEO?

* Provide search engine-friendly markup.

---

# HTTPS everywhere and mobile optimization

---

# Remove `h`-tags from side-wide elements 

* Drupal block labels: replace `<h2>`
* Card titles, regions etc.
* Use `h`-tags only for structuring text

---

# Infinite scroll 

* Always also provide a pager, SE don't execute Ajax-requests
* relying on the sitemap is not enough, relevance gets calculated on-site
* starting from page two add `<meta name="robots" content="noindex,follow"/>`

---

# Read more section

* latest articles
* most read articles
* strengthen your internal link graph
* let strong pages inherit relevance

---

# Exclude category/taxonomy pages from indexing

* noindex,follow
* no keyword optimised, no real text
* you want visitors to find real pages with real content that then maybe link to other pages with real content

---

# Linkmasking irrelevant links

* internal links to unindex pages
* route link juice in the right direction
* ```javascript
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
* ```html
  <div data-ix-base64="aHR0cDovL2Jsb2cuajEtdmlzYS1pbnRyYXguY29tLz9zPSZjYXQ9Mjc=" class="ix-base64">Foobar</div>
  ```

---

# Responsive image fallback image style

* This prevents having an transparent Pixel in base64 set as src attribute in responsive img tags inside `<picture>`.
* They won't get indexed. Only have real images set as src.

---

# Cards

* always only link text
* ```html
  <div class="card myBox">
      blah blah blah.
      <a href="http://google.com">link</a>
  </div>
  ```
* ```javascript
  $(".myBox").click(function() {
      window.location = $(this).find("a").attr("href"); 
      return false;
  });
  ```
* don't use image-links

---

# One single `<nav>` for desktop and mobile

* prevent duplicate links (link juice)

---

# Structured data

* JSON-LD
* Breadcrumb, FAQ
* only elements that are visibile (show breadcrumbs also on mobile)
* sample link to show SERP
* https://www.drupal.org/node/2799067

---

# 404 Links

* 301 forwarding

---

# Remove node/ID shortlinks

* `<link rel="shortlink" href="https://example.com/node/ID">`
* 301 forwarding causes link juice loss

---

# Remove self-referential links

* `<h1><a href="https://example.com/hello-world" rel="bookmark">Hello World</a></h1>`
* single-post.php

---

# Rabbit Hole

* prevent certain single nodes being visited or indexed (e.g. FAQs)

---

# Language switcher

* Remove link to node/ID when no translation exist
