# stale-while-revalidate
An explainer to define Chrome's stale-while-revalidate behavior.

## Abstract

The [Design Doc](https://docs.google.com/document/d/1wqbhCdf3eCv-VuUoV34xD2KfMinOCxH4fRe5EDCtXIo/edit) covers
some of the technical details of how this is implemented in Chrome. This document's audience is more
for web developers to understand how stale-while-revalidate works and how to conduct an origin-trial
with it enabled.

## Motiviation

The motivation for implementing stale-while-revalidate inside the browser is to allow fast update lifecycles
of resources while allowing these resources to be used as stale for a limited number of times. These properties
allow pages to load quickly using stale content but having the cached resource be update shortly thereafter.

CSS fonts served from fonts.google.com contain stale-while-revalidate directives so handling this directive
should help improve prove handling of these files.

## Sub Resources

Stale-While-Revalidate handling will only have effect on sub-resource requests. Stale-While-Revalidate
processing will not be handled on the document (whether top-level or iframe), media, download requests or
requests initiated from the [Fetch API](https://fetch.spec.whatwg.org/). The resources were it is not handled
will have handling that appears the same as if the value was not specified.

## Invalidation Contract

When a resource is returned as stale from the HTTP cache in the browser it needs to be revalidated within
60 seconds otherwise subsequent requests for that resource will be treated as stale and will cause a blocking
revalidation. This implementation detail is helpful to limit the amount of usage a stale resource
receives after being provided to the page. Attempts are made so that the revalidation requests are sent at
the most optimal time to avoid blocking any of the page.

## Service Worker

Original requests will still be seen via the Service Worker API. However the revalidation of the request
will not be seen to the Service Worker. This is consistent with other cache operations. 

## HTTP headers

Stale while revalidate is set via the `Cache-Control` header.

Example:
`Cache-control: private, max-age=3000, stale-while-revalidate=2592000`

This specifies that the resource is only cacheable by the browser, has a maximum age of 50 minutes and can
be returned stale for 30 days.

## Origin trial

The `Origin-Trial` HTTP header must be used when specifying the origin trial for this feature. Note that
the `meta` tag `http-equiv` approach does not work since timings of preload document parsers.


## How to file issues with Chrome

Create a new issue with "Stale-While-Revalidate" in the title. Optionally assigning the "Blink>Loader" component.
