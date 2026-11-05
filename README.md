# Cloudflare DDNS for UniFi OS

[![CodeQL](https://github.com/willswire/unifi-ddns/actions/workflows/github-code-scanning/codeql/badge.svg)](https://github.com/willswire/unifi-ddns/actions/workflows/github-code-scanning/codeql)
[![Code Coverage](https://github.com/willswire/unifi-ddns/actions/workflows/coverage.yml/badge.svg)](https://github.com/willswire/unifi-ddns/actions/workflows/coverage.yml)
[![Dependabot Updates](https://github.com/willswire/unifi-ddns/actions/workflows/dependabot/dependabot-updates/badge.svg)](https://github.com/willswire/unifi-ddns/actions/workflows/dependabot/dependabot-updates)
[![Deploy](https://github.com/willswire/unifi-ddns/actions/workflows/deploy.yml/badge.svg)](https://github.com/willswire/unifi-ddns/actions/workflows/deploy.yml)

Cloudflare Worker that lets UniFi devices (UDM-Pro, USG, etc.) update Cloudflare DNS A/AAAA records. UniFi has no built-in Cloudflare DDNS option.

## 1. Deploy the Worker

**Button:** [![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/willswire/unifi-ddns)

**Wrangler:** clone this repo, install [Wrangler](https://developers.cloudflare.com/workers/wrangler/install-and-update/), then:

```sh
npm i
wrangler login
wrangler deploy
```

Note the `*.workers.dev` route.

## 2. Create a Cloudflare API token

[Cloudflare Dashboard](https://dash.cloudflare.com/) > **Profile > API Tokens** > create with the **Edit zone DNS** template, scoped to one zone.

## 3. Configure UniFi OS

**Settings > Internet > WAN > Dynamic DNS** > Create New:

- **Service:** `custom`
- **Hostname:** `subdomain.example.com` or `example.com`
- **Username:** Cloudflare account email
- **Password:** Cloudflare User API token (not an Account API token)
- **Server:** `<worker-name>.<worker-subdomain>.workers.dev/update?ip=%i&hostname=%h` (no `https://`)

## Troubleshooting

See [docs/faq.md](docs/faq.md). Otherwise ask on [discussions](https://github.com/willswire/unifi-ddns/discussions/new?category=q-a) or open an [issue](https://github.com/willswire/unifi-ddns/issues).
