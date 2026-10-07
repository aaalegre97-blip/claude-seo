# Claude SEO: Universal SEO Analysis Skill

## Project Overview

This repository contains **Claude SEO**, a Tier 4 Claude Code skill for comprehensive
SEO analysis across all industries. It follows the Agent Skills open standard and the
3-layer architecture (directive, orchestration, execution). 26 sub-skills (22 core +
1 orchestrator + 1 framework integration + 2 extension mirrors), 19 sub-agents (16 core +
1 framework integration + 2 extension mirrors), and an extensible reference
system cover technical SEO, content quality,
schema markup, image optimization, sitemap architecture, AI search optimization,
local SEO (GBP, citations, reviews, map pack), maps intelligence, semantic topic
clustering, search experience optimization (SXO), SEO drift monitoring, e-commerce
SEO, and international SEO with cultural adaptation profiles. Matomo is available
as an optional extension for self-hosted analytics.

## Architecture

```
claude-seo/
  CLAUDE.md                          # Project instructions (this file)
  CONTRIBUTORS.md                    # Community credits (Pro Hub Challenge)
  AGENTS.md                          # Multi-platform agent instructions (Cursor, Antigravity)
  .claude-plugin/
    plugin.json                    # Plugin manifest (v2.4.1)
    marketplace.json               # Marketplace catalog for distribution
  skills/                            # 26 sub-skills (auto-discovered)
    seo/                           # Main orchestrator skill
      SKILL.md                     # Entry point, routing table, core rules
      references/                  # On-demand knowledge files (13 files)
    seo-audit/SKILL.md            # Full site audit with parallel agents
    seo-page/SKILL.md            # Deep single-page analysis
    seo-technical/SKILL.md       # Technical SEO (9 categories)
    seo-content/SKILL.md         # E-E-A-T and content quality
    seo-content-brief/SKILL.md   # Content brief generation
    seo-schema/SKILL.md          # Schema.org markup detection/generation
    seo-sitemap/SKILL.md         # XML sitemap analysis/generation
    seo-images/SKILL.md          # Image optimization analysis
    seo-geo/SKILL.md             # AI search / GEO optimization
    seo-agentic/                 # Agent readiness (Lighthouse Agentic Browsing, WebMCP)
      SKILL.md
      references/                # Lighthouse category, access policy, discovery, WebMCP, vendor matrix
    seo-local/SKILL.md           # Local SEO (GBP, citations, reviews, map pack)
    seo-maps/SKILL.md            # Maps intelligence (geo-grid, GBP audit, reviews, competitors)
    seo-plan/SKILL.md            # Strategic SEO planning
    seo-flow/SKILL.md            # FLOW framework integration
    seo-programmatic/SKILL.md    # Programmatic SEO at scale
    seo-competitor-pages/SKILL.md # Competitor comparison pages
    seo-hreflang/SKILL.md       # International SEO / hreflang
    seo-google/                  # Google SEO APIs
      SKILL.md
      references/                # API reference files (11 files)
    seo-backlinks/SKILL.md      # Backlink profile analysis
    seo-cluster/                 # Semantic topic clustering (v1.9.0, by Lutfiya Miller)
      SKILL.md
      references/                # Clustering methodology, architecture, workflow
      templates/                 # cluster-map.html interactive visualization
    seo-sxo/                     # Search Experience Optimization (v1.9.0, by Florian Schmitz)
      SKILL.md
      references/                # Page-type taxonomy, user stories, personas, wireframes
    seo-drift/                   # SEO drift monitoring (v1.9.0, by Dan Colta)
      SKILL.md
      references/                # Comparison rules (17 rules, 3 severity levels)
    seo-ecommerce/               # E-commerce SEO (v1.9.0, by Matej Marjanovic)
      SKILL.md
      references/                # Marketplace API endpoints
    seo-dataforseo/SKILL.md     # Live SEO data via DataForSEO MCP (extension mirror)
    seo-image-gen/              # AI image generation for SEO assets (extension mirror)
      SKILL.md
      references/                # Image gen reference files (7 files)
  agents/                          # 19 subagents (auto-discovered)
    seo-technical.md             # Crawlability, indexability, security
    seo-content.md               # E-E-A-T, readability, thin content
    seo-schema.md                # Structured data validation
    seo-sitemap.md               # Sitemap quality gates
    seo-performance.md           # Core Web Vitals, page speed
    seo-visual.md                # Screenshots, mobile rendering
    seo-geo.md                   # AI crawler access, GEO, citability
    seo-agentic.md               # Agent readiness, Lighthouse Agentic Browsing
    seo-local.md                 # GBP, NAP, citations, reviews, local schema
    seo-maps.md                  # Geo-grid, GBP audit, reviews, competitor radius
    seo-google.md                # Google API analyst (CrUX, GSC, GA4)
    seo-backlinks.md             # Backlink profile analyst (Moz, Bing, CC, verify)
    seo-dataforseo.md            # DataForSEO data analyst
    seo-image-gen.md             # SEO image audit analyst
    seo-cluster.md               # Semantic clustering analysis
    seo-sxo.md                   # Search experience optimization
    seo-drift.md                 # SEO drift monitoring
    seo-ecommerce.md             # E-commerce SEO analysis
    seo-flow.md                  # FLOW framework integration
  hooks/                           # Quality gate hooks
    hooks.json                   # PostToolUse schema validation
  scripts/                         # 60 Python execution scripts
    google_auth.py               # Credential management (OAuth, SA, API key, 4-tier detection)
    backlinks_auth.py            # Backlink API credential management (Moz, Bing)
    moz_api.py                   # Moz Link Explorer API (DA/PA, spam, domains, anchors)
    bing_webmaster.py            # Bing Webmaster Tools API (registered-site links/comparison)
    commoncrawl_graph.py         # Common Crawl web graph parser (PageRank, in-degree)
    verify_backlinks.py          # Backlink existence verification crawler
    pagespeed_check.py           # PSI v5 + CrUX API
    crux_history.py              # CrUX History API (25-week trends)
    gsc_query.py                 # Search Console (queries, pages, sitemaps, sites)
    gsc_inspect.py               # URL Inspection (single + batch)
    indexing_notify.py           # Indexing API v3 (URL_UPDATED/URL_DELETED)
    ga4_report.py                # GA4 organic traffic reports
    matomo_auth.py               # Matomo credential management (extension)
    matomo_report.py             # Matomo Reporting API client (extension)
    keywordseverywhere_api.py    # Keywords Everywhere (Open PageRank) backlinks fallback
    google_report.py             # PDF/HTML report generator (WeasyPrint + matplotlib)
    youtube_search.py            # YouTube Data API v3
    nlp_analyze.py               # Cloud Natural Language API
    keyword_planner.py           # Google Ads Keyword Planner
    fetch_page.py                # Page fetcher with UA rotation
    parse_html.py                # HTML parser for SEO elements
    capture_screenshot.py        # Playwright screenshots
    analyze_visual.py            # Visual analysis helper
    drift_baseline.py            # SEO drift baseline capture (SQLite)
    drift_compare.py             # SEO drift comparison engine (17 rules)
    drift_report.py              # SEO drift HTML report generator
    drift_history.py             # SEO drift history query
    dataforseo_costs.py          # DataForSEO cost estimation and budget tracking
    dataforseo_merchant.py       # Google Shopping / Amazon data fetching
    dataforseo_normalize.py      # DataForSEO response normalization utility
    sync_flow.py                 # FLOW prompt library sync (GitHub API, CC BY 4.0 headers, --dry-run, --ref)
    url_safety.py                # Canonical URL/SSRF safety module (validate, DNS-pin, safe fetch)
    render_page.py               # Shared headless renderer (SPA-aware, Playwright)
    lcp_subparts.py              # LCP subparts breakdown via CrUX API
    preload_check.py             # Speculation Rules / bfcache / prerender / preload detector
    agent_ux_check.py            # Agent-friendly page auditor
    agentic_check.py             # Agent-readiness HTTP auditor (robots, llms.txt, Markdown, ARD, well-known, WebMCP)
    agentic_fix.py               # Agent-readiness fix drafter (robots Content-Signal, llms.txt, ai-catalog, WebMCP)
    lighthouse_agentic.py        # Lighthouse Agentic Browsing fraction reader (PSI or saved JSON)
    content_quality.py           # QRG-aligned content quality detector
    metadata_template.py         # Templated title/description detector (title echo + stock CTA)
    content_humanize.py          # AI-pattern remover (rewrites AI-typical phrasing)
    content_verify.py            # Claim extractor + citation-gap detector
    schema_generate.py           # JSON-LD generators for high-leverage v2 schema types
    schema_ecommerce_validate.py # Product schema validator (merchant-listing requirements)
    iptc_ai_label.py             # IPTC DigitalSourceType audit/injection for AI imagery
    parasite_risk.py             # Parasite-SEO risk scanner
    gbp_deprecation_lint.py      # GBP feature-deprecation linter
    domain_history.py            # Expired-domain heritage check
    seo_updates.py               # Primary-source Google updates query tool
    indexnow_submit.py           # IndexNow submitter
    ucp_check.py                 # UCP (Universal Commerce Protocol) profile auditor
    unlighthouse_run.py          # Unlighthouse CLI wrapper (site-wide Lighthouse)
    validate_backlink_report.py  # Backlink report validation
    portability_check.py         # Cross-platform portability lint for SKILL.md files
    consistency_check.py         # Reference-graph gate: dead refs, routing, lock, orphans
    release_sign.py              # SHA-256 manifest generator for release signing
    verify_release.py            # Verify checkout integrity against a release manifest
    sitemap_discovery.py         # Sitemap discovery (robots.txt, common paths)
    runtime.py                   # Managed runtime behind the claude-seo launcher
  schema/                          # Schema.org JSON-LD templates
  extensions/                      # Optional add-on install helpers
    dataforseo/                  # DataForSEO MCP install scripts
    firecrawl/                   # Firecrawl MCP install scripts
    banana/                      # Banana MCP install scripts
    ahrefs/                      # Ahrefs MCP install scripts
    bing-webmaster/              # Bing Webmaster and IndexNow install scripts
    profound/                    # Profound MCP install scripts
    seranking/                   # SE Ranking MCP install scripts
    unlighthouse/                # Unlighthouse install scripts
  docs/                            # Extended documentation
```

## Commands

| Command | Use Case |
|---------|----------|
| `/seo audit <url>` | Full website audit with parallel subagents |
| `/seo page <url>` | Single page analysis |
| `/seo technical <url>` | Technical SEO across 9 categories |
| `/seo content <url>` | E-E-A-T and content quality |
| `/seo content-brief <topic>` | Detailed content brief: keywords, outline, internal links |
| `/seo schema <url>` | Schema markup detection, validation, generation |
| `/seo sitemap <url>` | Sitemap validation |
| `/seo sitemap generate` | Create new sitemap with industry templates |
| `/seo images <url>` | Image optimization |
| `/seo geo <url>` | AI search optimization (GEO) |
| `/seo agentic <url>` | Agent readiness (Lighthouse Agentic Browsing, AI agent access, WebMCP) |
| `/seo local <url>` | Local SEO (GBP, citations, reviews) |
| `/seo maps [command]` | Maps intelligence (geo-grid, GBP audit, competitors) |
| `/seo backlinks <url>` | Backlink profile analysis |
| `/seo cluster <seed>` | SERP-based semantic clustering |
| `/seo sxo <url>` | Search Experience Optimization |
| `/seo drift baseline\|compare\|history <url>` | SEO drift monitoring |
| `/seo ecommerce <url>` | E-commerce SEO |
| `/seo hreflang [url]` | Hreflang and international SEO |
| `/seo plan <type>` | Strategic planning by industry |
| `/seo programmatic [url\|plan]` | Programmatic SEO analysis |
| `/seo competitor-pages [url\|generate]` | Competitor comparison pages |
| `/seo flow [stage] [url\|topic]` | FLOW framework prompts |
| `/seo google [command] [url]` | Google SEO APIs (GSC, PSI, CrUX, GA4) |
| `/seo dataforseo [command]` | Live SEO data (extension) |
| `/seo image-gen [use-case] <desc>` | AI image generation (extension) |
| `/seo firecrawl [command] <url>` | Full-site crawling (extension) |
| `/seo ahrefs [command] <url>` | Backlinks, organic keywords, and content data via the official Ahrefs MCP (extension) |
| `/seo seranking [command]` | AI Share-of-Voice across ChatGPT, Gemini, Perplexity, AI Overviews, AI Mode (extension) |
| `/seo profound [command]` | LLM citation tracking with time-series data (extension) |
| `/seo bing [command] <url>` | Bing Webmaster Tools + IndexNow URL submission (extension) |
| `/seo unlighthouse <url>` | Multi-page Lighthouse runner, runs locally (extension) |

## Development Rules

- Keep SKILL.md files under 500 lines / 5000 tokens
- Reference files should be focused and under 200 lines
- Scripts must have docstrings, CLI interface, and JSON output
- Follow kebab-case naming for all skill directories
- Agents invoked via Agent tool, never via Bash
- Bundled tools run through `"${CLAUDE_PLUGIN_ROOT}/scripts/claude-seo" run`; plugin state uses `CLAUDE_PLUGIN_DATA`
- Manual Python dependencies install into `~/.claude/skills/seo/.venv/`
- Test with `python3 -m pytest tests/` after changes (if applicable)

## Security Rules

- **Never commit credentials**: `.env`, `client_secret*.json`, `oauth-token.json`, `service_account*.json` are all in `.gitignore`
- **URL validation**: All scripts that connect to user-supplied URLs must use `scripts/url_safety.py` (`validate_url_strict()` plus the pinned safe request helpers). This blocks private IPs, loopback, metadata endpoints, redirect rebinding, and DNS rebinding.
- **OAuth tokens**: Never store `client_secret` in the token file. Read it from the client_secret.json file at runtime.
- **No hardcoded paths**: Use `os.path.dirname(os.path.abspath(__file__))` for relative paths, never a user-specific absolute path
- **Config location**: `~/.config/claude-seo/google-api.json` and `~/.config/claude-seo/backlinks-api.json` (user-space, not in repo)

## Report Generation Rules

- **All SEO reports must use `scripts/google_report.py`** as the canonical report generator
- **Dependencies**: `matplotlib>=3.8.0` (charts) + `weasyprint>=70.0` (HTML-to-PDF), both in `requirements.txt`
- **Format**: A4 PDF via WeasyPrint + matplotlib charts at 200 DPI
- **Style**: Clean white title page with navy (#1e3a5f) accent, Times New Roman body font
- **Color palette**: Navy #1e3a5f (headers), dark gold #b8860b (accents), forest green #2d6a4f (pass), warm amber #d4740e (warnings), deep red #c53030 (fail), warm cream #faf9f7 (backgrounds)
- **Structure**: Title page → TOC with scores → Executive Summary → Data sections → Recommendations → Methodology
- **Charts**: 85% width, max-height 120mm, figure captions on every chart, saved to `charts/` at 200 DPI
- **No `page-break-inside: avoid`** on any element (causes white gaps in WeasyPrint)
- **Post-generation review**: `_review_pdf()` runs automatically, checking for empty images, thin sections, duplicates
- **Before presenting any PDF to the user**: verify the review passes (`"status": "PASS"`)
- **Cross-skill enforcement**: After completing ANY analysis command (audit, page, technical, content, schema, geo, local, maps), offer: "Generate a PDF report? Use `/seo google report`"
- **Google logo** appears on title page when using Google API data ("Powered by Google APIs")

## Ecosystem

Part of the Claude Code skill family:
- [Claude Banana](https://github.com/AgriciDaniel/banana-claude) -- standalone image gen (bundled as extension here)
- [Claude Blog](https://github.com/AgriciDaniel/claude-blog) -- companion blog engine, consumes SEO findings
- [AI Marketing Claude](https://github.com/zubair-trabzada/ai-marketing-claude) -- community marketing suite (copy, emails, ads, funnels, CRO)

## Key Principles

1. **Progressive Disclosure**: Metadata always loaded, instructions on activation, resources on demand
2. **Industry Detection**: Auto-detect SaaS, e-commerce, local, publisher, agency
3. **Parallel Execution**: Full audits spawn up to 17 subagents simultaneously
4. **Extension System**: DataForSEO, Firecrawl, Banana, Ahrefs, SE Ranking, Profound, Bing Webmaster, and Unlighthouse extensions

## Repository Topology (public + private)

This project is mirrored across two GitHub remotes with shared historical
ancestry. Reviewed back-ports, private-only research, and marketplace branding
mean their release commits can have different SHAs. Neither repository is a
GitHub fork of the other.

| Remote | URL | Visibility | Role |
|---|---|---|---|
| `origin` | `https://github.com/AgriciDaniel/claude-seo` | **Public** | Published distribution. Users discover, clone, and install from here. `main` only reflects released history. |
| `aimh` | `https://github.com/AI-Marketing-Hub/claude-seo` | **Private** | Working repo inside the AI Marketing Hub org. Daily development. v2 branch + post-release work lives here before promotion to public. |

### Workflow

Daily development:
- Work on `v2` (or feature branches off `v2`) locally.
- `git push aimh <branch>` to publish work-in-progress to the private repo
  (Dependabot, Actions, and CI run there).

Promoting reviewed release changes:
1. Use an isolated clean worktree from the target repository branch.
2. Fast-forward only when ancestry proves it is safe. Otherwise cherry-pick
   the exact reviewed commits with `-x` and resolve only documented divergence.
3. Run the full validation suite and compare the private/public release trees.
4. Create an annotated repository-specific tag after validation.
5. Push private changes first. Push public changes only with explicit release
   authorization, with the public tag available before the installer moves.
6. Create the GitHub Release and release post on the public repository only.

### Safety rules

- **Never push to `origin/main` autonomously.** The public is release-only;
  pushes are user-authorized per-release.
- **`aimh` accepts day-to-day pushes.** No release-gate ceremony required
  for the private remote.
- **v2.2.5 is tagged on both repositories.** Each tag points to that
  repository's reviewed release commit.
- **Never force-sync the histories.** Preserve reviewed divergence and never
  rewrite either remote without explicit per-operation authorization.

### Verifying the topology

```bash
# Both remotes configured
git remote -v        # expects: origin (public) + aimh (private)

# Compare heads and then audit the documented divergence. Equal SHAs are not
# expected after repository-specific back-ports.
git ls-remote --heads aimh main
git ls-remote --heads origin main
```

Full workflow reference: `docs/WORKFLOW-public-private.md`.

## Release Blog Post

After cutting a new release (git tag + `gh release create`), run:

```
/release-blog
```

This generates a blog post on https://claude-seo.md/blog/, handles cover image generation, SEO metadata, FAQ schema, internal linking, sitemap/llms.txt updates, Vercel deployment, and Google indexing.

## Which Marketing Tool to Use (Alegre Solutions routing rule)

Three repos handle marketing work. Pick by **where the problem lives**, then say in one line which tool you're using and why before starting.

- **claude-ads** (`aaalegre97-blip/claude-ads`): the **ad account manager**. Anything inside Ads Manager.
- **claude-seo** (`aaalegre97-blip/claude-seo`): the **SEO technician**. Anything about ranking on Google or in Maps.
- **marketingskills** (`aaalegre97-blip/marketingskills`): the **marketer**. The offer, the words, the landing page, and the follow-up after a lead comes in.

**Rule of thumb:** inside Ads Manager → claude-ads. Rankings, Google Business Profile, site health → claude-seo. Offer, copy, page conversion, or lead follow-up → marketingskills.

### Paid ads

| The user says or needs… | Use | Skill / command |
|---|---|---|
| New client, brand, account setup | claude-ads | `/ads setup` |
| "What's wrong with this account?", audit, wasted spend | claude-ads | `/ads audit meta` (or other platform) |
| Budget, campaign structure, channel plan | claude-ads | `/ads plan`, `/ads budget` |
| Fatigue, pacing, overspend, "is it still working?" | claude-ads | `/ads monitor` |
| Kill / keep / scale decisions | claude-ads | `/ads optimize --draft` |
| A/B test design or readout | claude-ads | `/ads test` |
| Pixel, conversions API, tracking broken | claude-ads | `/ads tracking` |
| Review a finished ad before launch | claude-ads | `/ads creative` |
| Client ad performance report | claude-ads | `/ads report` |
| Hooks, headlines, primary text, static ad layouts | marketingskills | `ad-creative` |

### SEO

| The user says or needs… | Use | Skill / command |
|---|---|---|
| Full website SEO audit | claude-seo | `/seo audit <url>` |
| Google Business Profile, map pack, reviews, citations | claude-seo | `/seo local <url>`, `/seo maps` |
| One page not ranking | claude-seo | `/seo page <url>` |
| Site speed, indexing, crawl problems | claude-seo | `/seo technical <url>` |
| Search Console, PageSpeed, GA4 data | claude-seo | `/seo google` |
| SEO plan for a client | claude-seo | `/seo plan <business-type>` |
| Keyword groups, service-area or city pages | claude-seo | `/seo cluster`, `/seo programmatic` |
| Content brief for a blog or service page | claude-seo | `/seo content-brief` |
| Schema markup | claude-seo | `/seo schema <url>` |
| Showing up in AI answers (ChatGPT, AI Overviews) | claude-seo | `/seo geo <url>` |
| Before/after tracking when changing a site | claude-seo | `/seo drift baseline`, `/seo drift compare` |

marketingskills also has `seo-audit`, `ai-seo`, `schema`, `programmatic-seo` and `site-architecture`. Use claude-seo first for SEO because it runs real crawls and data pulls. Fall back to the marketingskills versions only if claude-seo isn't attached.

### Offer, copy, conversion, follow-up

| The user says or needs… | Use | Skill / command |
|---|---|---|
| Offer is weak (guarantee, bonus, urgency, pricing) | marketingskills | `offers`, `pricing` |
| Website or landing page copy | marketingskills | `copywriting` |
| Landing page not converting | marketingskills | `cro` |
| Speed-to-lead texts, lead follow-up | marketingskills | `sms` |
| Email nurture for leads that didn't book | marketingskills | `emails` |
| Sales scripts, objection handling | marketingskills | `sales-enablement` |
| Hiring cleaners or techs | marketingskills | `recruiting` |

### Full flows

- **Static ad:** `offers` → `ad-creative` (copy + layout) → build the image as HTML and export to PNG → `/ads creative` (pre-launch check) → after launch, `/ads audit meta` → `sms` / `emails` for follow-up.
- **Local SEO for a new client:** `/seo audit` → `/seo local` → fix the Google Business Profile → `/seo programmatic` for service-area pages → `copywriting` for the page words → `/seo drift baseline` before changes go live.

### Rules

- **If the needed repo isn't in this session:** say which repo and skill is the right one and offer to attach it. Don't silently fall back to the wrong tool.
- **Known gap:** none of the three has contractor-specific ad kill/scale thresholds or cost-per-booked-job targets. Flag this when giving kill/scale advice and judge against cost per booked job, not cost per lead.
