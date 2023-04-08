# Packable website recommendations

There are often use cases for web content in situations where the original server is not available, such as:

* **Archive**: where a user wants to access web content after the original server 
is no longer available, or the content on the original server has been removed or changed. For example: a user wants to store a copy of a local government website
from a certain day.

* **Offline distribution**: where a user wants to access web content in an offline
context without any direct Internet access. For example a school wants to use a 
copy of an educational website by storing it on a local server.

Making a website packable (e.g. suitable for archive/offline distribution) 
can help to increase access.

## Goals

The goals of these recommendations are:

1. Provide simple steps that webmasters and webdevelopers can use to make their 
sites as accessible as possible
1. Provide a technical reference that can be used by those funding digital content
creation for the public good (e.g. donors, governments, foundations etc) that
they can include to require content created to be ready for archive and offline
distribution


## Website requirements

1. Provide a [sitemap](https://www.sitemaps.org/) to list any pages that would not normally be found by crawling and following links.

2. List any resources that are lazily loaded that would be required for the active URL to be used. For example if the URL has a slidehsow which loads as the user
goes through each slide, list the resources required to load so that an archiver
can download them. This can be done in three ways:

Link rel=archive tag:
```
<link rel="archive" href="slide10-background.jpg"/>
```

HTML5 Cache Manifest:

```
<html manifest="page.appcache">
```
The [HTML5 Cache Manifest](https://en.wikipedia.org/wiki/Cache_manifest_in_HTML5) is no longer used by browsers, however it provides a 
simple way to list resources required for the page to load. This can avoid the 
need for excessive number of link tags for pages that use many small resources.

Alternatively, the site can offer a pre-built archive:

```
<link rel="alternate" type="application/zip+wacz" href="page.wacz"/>
```
Webmasters who want to bundle resources themselves (e.g. using tools such as
webpack) e.g. to reduce server load as/when the site is archived or otherwise
build their own archives can provide a WACZ, WARC, ZIM, or WBN bundle.

3. If embedding content on external sites that prohibit or restrict downloads 
(e.g. Youtube), offer an alternate link that can be downloaded:

```
<link rel="archive-alternate" 
   data-original-href="https://www.youtube.com/watch?v=AAA
   href="/originalvideos/AAA.mp4"/>
```

4. Ensure that each "packable" page can load with the resources that are fetched
immediately after the page is opened and any additional resources the page 
references as above. Any features that require live connectivity with the
original server (e.g. social feeds) should degrade gracefully.

## Archiver requirements

1. If a prebuilt archive is offered by the site, download it.
2. If a prebuilt archive is not offered by the site, open the site using a modern
standards compliant browser (e.g. Chromium, Firefox) and store all URLs fetched
upon loading the page (wait until there has been no download activity for 5
seconds, or up to a maximum of 1 minute). Store all URLs listed as as link 
rel=archive and the appcache manifest.


