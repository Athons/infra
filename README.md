# Infrastructure

Documenting athon's infrastructure

## Domains

### athon.uk

#### Whois

```
    Domain name:
        athon.uk

    Data validation:
        Nominet was able to match the registrant's name and address against a 3rd party data source on 27-Oct-2019

    Registrar:
        Namecheap, Inc. [Tag = NAMECHEAP-INC]
        URL: https://www.namecheap.com

    Relevant dates:
        Registered on: 27-Oct-2019
        Expiry date:  27-Oct-2025
        Last updated:  27-Sep-2020

    Registration status:
        Registered until expiry date.

    Name servers:
        luke.ns.cloudflare.com
        sneh.ns.cloudflare.com

    WHOIS lookup made at 18:44:18 07-Feb-2021
```

(Ran on 2021-02-07)

#### Records

* CNAME `hack` to `cranky-hermann-f72f70.netlify.app`
* CNAME `stats` to `infallible-shirley-b1f453.netlify.app`

Those are both proxied to give access to statistics.

## Hosting

### Static Content

Static websites are hosted by netlify on the free tier, you can find each of the sites build logs in their READMEs

* https://app.netlify.com/sites/cranky-hermann-f72f70/deploys

### Generated Content

Currently the only dynamic content is the statistics, which is hosted in a GCloud bucket `https://athon-uk.storage.googleapis.com/data.json`.

Future data like events will also be hosted in the same bucket. Probably as `events.json`.

### Compute

We have two jobs current:

* Fetching stats from cloudflare
* Querying Github for changes to organisations repositories.

Both of which run as scheduled github actions.

We have no permanent servers.

#### GH Secrets

If writing a job to run on these, you'll have about the follow organisation wide secrets:

* `CF_TOKEN` - Read only token to the cloudflare API
* `GCLOUD_BUCKET` - Name of our Gcloud bucket (athon-uk), stored as a secret for simplicty.
* `GCLOUD_IAM_KEY` - Key to write to the previously mentioned bucket.
* `GCLOUD_PROJECT_ID` - GCloud project id.
* `GITTER_COMMUNITY` - hack.athon.uk, prefixed to all our gitter channels.
* `GITTER_TOKEN` - API token to post messages.
* `GH_TOKEN` - Github API token

##### Events Repo

* `GITTER_CHANNEL` - where to post the message

## Community

The main place to talk is gitter or github issues.
