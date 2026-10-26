# Blueground

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
