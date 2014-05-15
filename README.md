# Ahoy

:fire: A foundation of knowledge and libraries for awesome analytics

Best practices for:

- tracking visits, events, emails, and referrals
- scaling storage
- funnels, cohorts, and LTV calculations
- experiments like split tests
- and much more

Designed to work with any progamming language and any device.

Never build an analytics platform from scratch again.

This is a work in progress, built for the open-source community.  If you have great practices, articles, or videos, [please share](https://github.com/ankane/ahoy_guide/issues/new).

:warning: Everything below is scattered and probably makes no sense

## Outline

- Intro
- The Perfect Platform
- People, Not Page Views
- Web
  - Landing page
    - Acquisition
    - Funnels
    - Experiments
  - Product
    - Same as above
- iOS
  - Same as above
- Android
  - Same as above
- Emails
- Referrals
- Load Times
- Storage
- HTTP Spec

## Web

### Visitors

There are two ways to tell where a visitor has come from:

- the `Referer` header
- query parameters, like `utm_source`

When a user clicks on a link, most browsers set the `Referer` header with the URL of the previous page.  From this, you can extract:

- the page
- search keywords - thanks to [great libraries](https://github.com/snowplow/referer-parser)

**TODO:** Explain how different browsers handle redirects and note about HTTPS -> HTTP

There are a few things you can calculate about the visitor:

- estimated location from IP address
- browser, OS, and device model from user agent

Client libraries have access to more information, like:

- screen size
- pixel density (retina) - does this really matter?

Be sure to exclude bots from your metrics - some like Googlebot run JavaScript.

### Landing Page

The landing page is one of the most important pages of your website.

When an unauthenticated visitor lands on your site, there are a few things that could happen:

- register (success!)
- sign in
- bounce

**TODO:** Note about multiple authentication strategies (email, Facebook, Google, etc)

**Best practice:** For third-party services, ask for the miminum number of permissions needed

#### Authenticated Visitors

If a visitor is authenticated, do **not** show them the landing page with a “Customer Login” link.  Drop them right into your product.

**Best practice:** Keep users signed in between visits - unless you run a banking website of course

#### Funnel

Intent is key

Segment by:

- mobile vs desktop
- channel
- experiment

#### Experiments

Commonly called split tests or A/B tests

- [How Not To Run An A/B Test](http://www.evanmiller.org/how-not-to-run-an-ab-test.html)
- [Why multi-armed bandit algorithm is not “better” than A/B testing](http://visualwebsiteoptimizer.com/split-testing-blog/multi-armed-bandit-algorithm/) - time is $$$

Start with big changes (exploration) before changing button colors

Use same tracking as events for conversions

## iOS

- [Link to App Store](http://stackoverflow.com/a/2337601/1177228)
- [Smart App Banners](https://developer.apple.com/library/ios/documentation/AppleApplications/Reference/SafariWebContent/PromotingAppswithAppBanners/PromotingAppswithAppBanners.html)

## Android

- [Link to Play Store](http://developer.android.com/distribute/googleplay/promote/linking.html)
- [Link with referrer](https://developers.google.com/analytics/devguides/collection/android/v2/campaigns#google-play-implement)

## Storage

Start simple and scale as needed - “premature optimization is the root of all evil”

- logs (not queryable)
  - backup to [S3]
- database
  - PostgreSQL, Redis, Logstash, Fluentd
- distributed data stores
  - Hadoop, Cassandra, [Amazon Redshift]

[not open source]

**TODO:** Recommendations for starting, scaling, and scaling again

## Privacy

Things not to do

- [supercookies](http://mashable.com/2011/09/02/supercookies-internet-privacy/)
- [device fingerprinting](https://panopticlick.eff.org/)

## HTTP Spec

### Visits

A `POST` request is sent with:

- visit_token
- visitor_token
- referrer
- landing_page

The server can capture:

- ip
- user_agent
- user - from app authentication

And calculate things like:

- referring_domain and search_keyword from referrer
- utm_source, utm_medium, utm_term, utm_content, and utm_campaign from landing_page
- city, region, and country from ip
- browser, os, and device_type from user_agent

### Events

A `POST` request is sent with:

- name
- properties
- time

The server can capture:

- visit_token - from cookies
- user - from app authentication

As a precaution, the server should reject times that do not match:

```
1 minute ago < time <= now
```

## Libraries

### Client Tracking

Works with any backend

- [JavaScript](https://github.com/ankane/ahoy.js)
- iOS (soon)
- Android (soon)

### Server Tracking + Backend

- [Ruby](https://github.com/ankane/ahoy)
- Others (help make this possible)

### Email

- [Ruby](https://github.com/ankane/ahoy_email)
- Others (help make this possible)

### Experiments, Funnels, Cohorts, More

- Coming soon

## Great Content

- [Startup Metrics for Pirates](https://www.youtube.com/watch?v=irjgfW0BIrw)
