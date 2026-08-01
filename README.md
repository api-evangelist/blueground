# Blueground

Blueground is a global proptech company that leases, furnishes and operates move-in-ready
apartments for stays of a month or longer, across cities in North America, Europe, the Middle
East, Asia and Latin America. It runs a consumer booking site and guest mobile apps, an internal
property/pricing/operations platform, and the **Blueground Partner Network** — an invite-only
marketplace where third-party furnished-rental operators list supply.

- Website — https://www.theblueground.com/
- Partner Network — https://partner-network.theblueground.com/
- GitHub — https://github.com/bluegroundltd
- Harvest source (secondary market) — https://forgeglobal.com/blueground_stock/

## API surface

**Blueground publishes no public API, developer portal, or machine-readable contract.**
Contract discovery on 2026-07-31 probed `theblueground.com`, `www.theblueground.com`,
`api.theblueground.com`, `docs.theblueground.com`, `partners.theblueground.com` and
`partner-network.theblueground.com` for `/openapi.json|.yaml`, `/swagger.json`,
`/v1/openapi.json`, `/api-docs`, `/docs`, `/redoc`, `/v3/api-docs`, `/graphql`, and the
`/.well-known/` discovery surface (`security.txt`, `openid-configuration`,
`oauth-authorization-server`, `oauth-protected-resource`, `api-catalog`, `ai-plugin.json`,
`agent-card.json`, `agent.json`). Every probe missed:

- `api.theblueground.com` is live (Go service, TLS 1.3) but answers `404 page not found` as
  `text/plain` on every path — an app backend, not a documented public API.
- `docs.theblueground.com` returns S3 `AccessDenied` (403) on every path.
- `partner-network.theblueground.com` is a Next.js SPA whose catch-all returns HTTP 200 with the
  same HTML shell for every path — recorded as a false positive, not a hit.
- No GraphQL endpoint, no MCP server, no A2A agent card, no AsyncAPI, no security.txt.

Partner connectivity is brokered through PMS / channel-manager platforms (SiteMinder, Rentals
United, NextPax, Avantio, Guesty, Hostify, Hostfully, Cloudbeds, Airbnb, Happy Star) rather than
a self-serve Blueground API — captured in `integrations/_index.yml` as listing-only entries.

## Artifacts

| Artifact | File | Method |
|---|---|---|
| llms.txt | `llms/blueground-llms.txt` | searched (verbatim, `https://www.theblueground.com/llms.txt`) |
| Packages | `packages/blueground-packages.yml` | searched (10 Maven Central + 2 npm, first-party OSS) |
| Well-known | `well-known/blueground-well-known.yml` | probed (all misses recorded) |
| Integrations | `integrations/_index.yml` | searched (PMS/channel-manager partners) |
| Domain security | `security/blueground-domain-security.yml` | probed (TLS 1.3, HSTS, DNSSEC, DMARC `p=reject`) |

The `bluegroundltd` GitHub org publishes engineering libraries (test fixtures, transactional
outbox, enum/JSON-schema codegen, logging MDC) to Maven Central under `io.github.bluegroundltd`
and to npm under `@blueground` — these are internal developer tooling, **not** API client SDKs,
so no `SDKs` pointer is wired.

No vulnerability-disclosure program, trust center, status page, or published certifications were
found (`0-working/probe-security-programs.py` → `vdp=none trust=none`).
