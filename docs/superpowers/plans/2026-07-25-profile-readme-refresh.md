# Profile README Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Refresh the GitHub profile README with current professional information, live projects, a portfolio link, GitHub-compatible Bitcount typography, and no GitHub statistics cards.

**Architecture:** Keep the profile as a single `README.md` using GitHub-supported Markdown and HTML. Preserve the red capsule-render identity and Pacman graph, use `readme-typing-svg` for Bitcount Grid Double typography, and organize the content into hero, current projects, about, featured work, stack/tools, and contribution sections.

**Tech Stack:** GitHub Flavored Markdown, sanitized HTML, Shields.io, Skill Icons, Capsule Render, Readme Typing SVG

## Global Constraints

- Preserve the current red capsule-render header and footer.
- Keep the Contribution Game / Pacman section.
- Remove the complete GitHub Stats section, including stats, top languages, streak, and trophy images.
- Remove the MRB Group / Company badge.
- Use HTTPS for every external destination.
- Do not expose the phone number or email from the resume.
- Keep native Markdown headings and meaningful image alt text.
- Do not use `<style>` or `@import`; use the SVG service's `font=Bitcount Grid Double` parameter.

---

### Task 1: Refresh the Profile README

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: Content and constraints from `docs/superpowers/specs/2026-07-25-profile-readme-refresh-design.md`
- Produces: A GitHub-renderable profile page linking to the portfolio and four requested live projects

- [ ] **Step 1: Record the pre-change requirements check**

Run:

```powershell
rg -n "Company|GitHub stats|wavify\.ir|asman-web\.ir|rudo-quest|indigo-accessories|ilya-aghaei-portfolio|pacman" README.md
```

Expected: Company and GitHub stats are present; Wavify and Pacman are present; Asman, Rudo Quest, Indigo Accessories, and the portfolio are absent.

- [ ] **Step 2: Rewrite the README content**

Use the following structure:

```text
red capsule hero
Front-End Developer introduction
GitHub + location + portfolio badges
Bitcount Grid Double typing SVG
Current Projects: Asman + Wavify
About Me: resume-backed summary
Featured Projects: Asman, Wavify, Rudo Quest, Indigo Accessories
Tech Stack
Tools I Use
Contribution Game / Pacman
red capsule footer
```

Project copy must describe Asman as a dealership management platform and Wavify as a Persian music streaming platform. Rudo Quest and Indigo Accessories must use neutral descriptions such as "Live web project" so unsupported product claims are not invented.

- [ ] **Step 3: Verify required and forbidden content**

Run:

```powershell
$readme = Get-Content -Raw README.md
$required = @(
  'https://asman-web.ir/',
  'https://wavify.ir/',
  'https://rudo-quest.vercel.app/',
  'https://indigo-accessories.vercel.app/',
  'https://ilya-aghaei-portfolio.vercel.app/',
  'Bitcount+Grid+Double',
  'pacman-contribution-graph'
)
$forbidden = @(
  '## GitHub stats',
  'github-readme-stats.vercel.app',
  'streak-stats.demolab.com',
  'trophy-output/trophy.svg',
  'Company-MRB',
  '<style>',
  '@import'
)
$missing = $required | Where-Object { -not $readme.Contains($_) }
$unexpected = $forbidden | Where-Object { $readme.Contains($_) }
if ($missing -or $unexpected) {
  throw "Missing: $($missing -join ', '); Forbidden: $($unexpected -join ', ')"
}
'README content checks passed.'
```

Expected: `README content checks passed.`

- [ ] **Step 4: Check link reachability and Markdown structure**

Run:

```powershell
$urls = @(
  'https://asman-web.ir/',
  'https://wavify.ir/',
  'https://rudo-quest.vercel.app/',
  'https://indigo-accessories.vercel.app/',
  'https://ilya-aghaei-portfolio.vercel.app/'
)
foreach ($url in $urls) {
  $response = Invoke-WebRequest -Uri $url -Method Head -MaximumRedirection 5
  if ($response.StatusCode -ge 400) { throw "$url returned $($response.StatusCode)" }
}
$readme = Get-Content -Raw README.md
foreach ($tag in 'p','div','a') {
  $opens = ([regex]::Matches($readme, "<$tag(?:\s|>)")).Count
  $closes = ([regex]::Matches($readme, "</$tag>")).Count
  if ($opens -ne $closes) { throw "$tag tags are unbalanced: $opens open, $closes close" }
}
'Link and HTML checks passed.'
```

Expected: `Link and HTML checks passed.` If a site rejects `HEAD`, retry that site with `GET` and accept any status below 400.

- [ ] **Step 5: Review the final diff**

Run:

```powershell
git diff --check
git diff -- README.md
```

Expected: No whitespace errors; the diff changes only the intended README content.

- [ ] **Step 6: Commit the refreshed README**

Run:

```powershell
git add README.md
git commit -m "feat: refresh profile readme"
```

Expected: One commit containing only `README.md`.
