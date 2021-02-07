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

Both CNAMES are proxies by Cloudflare to give access to statistics (how https://stats.athon.uk/ gets data).

## Hosting

### Static Content

The static websites are hosted by Netlify on the free tier and  you can find each of the sites build logs in their READMEs:

* https://app.netlify.com/sites/cranky-hermann-f72f70/deploys

### Generated Content

We store generated content in a GCloud bucket, with the following CORS settings:

```
[
    {
      "origin": ["https://stats.athon.uk", "http://localhost:8000"],
      "method": ["GET"],
      "responseHeader": ["Content-Type"],
      "maxAgeSeconds": 3600
    }
]
```

Currently we just have the statistics stored there: https://athon-uk.storage.googleapis.com/data.json

Future data like events will also be hosted in the same bucket. Probably as `events.json`.

### Compute

We have two scheduled jobs, which run by Github Actions:

* [Fetching stats from cloudflare](https://github.com/Athons/cfstats/actions?query=workflow%3A%22Update+Stats%22)
* [Querying Github for changes to organisations repositories](https://github.com/Athons/events/actions?query=workflow%3A%22Run+Tool%22)

We have no permanent servers.

#### GH Secrets

If writing a job to run as an action, you'll have access to the follow organisation wide secrets:

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
