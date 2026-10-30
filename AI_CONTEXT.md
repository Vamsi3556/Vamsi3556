# AI Context & Decision Log — GitHub Profile README Project

This file exists so that any AI assistant (not just one specific tool) can pick up this project
with full context, without re-deriving decisions already made. If you are an AI reading this,
treat it as authoritative history — don't redo decisions below without checking with the user first.

## What this project is

A GitHub profile README (the special repo that displays on a user's GitHub profile page),
positioning the user as a DevOps Engineer transitioning into Site Reliability Engineering (SRE)
roles at major tech companies (Google, Meta, Amazon, Microsoft).

- **Local working copy**: this folder (`Upskill/`), specifically `README.md`
- **Live target**: https://github.com/Vamsi3556/Vamsi3556 (README.md on `main` branch)
- **Spec/requirements**: see `.kiro/specs/sre-github-profile-readme/` (requirements.md, design.md,
  tasks.md) for the original structured requirements this README was built against.

## Person this is for

- Name: **Vamsi Vatsavai**
- Email: vatsavaivamsi@gmail.com
- GitHub: https://github.com/Vamsi3556 (this is the correct/intended account — a second account,
  `Vamsi-sys-tech`, was briefly connected first but is NOT the one to use)
- LinkedIn: no public profile URL/slug provided yet — currently shown as plain text, not a link
- Experience: DevOps Engineer, 2-4 years, AWS + Azure
- No AWS/Azure certifications yet
- First real portfolio project shipped: see "Project #1" section below

## Key decisions and rationale

1. **No placeholder content on the live README.** Early versions of the template had
   `[Project Name]`, `[Certification]`, `[username]`-style placeholders. The user explicitly
   rejected shipping those to a public profile. Decision: remove sections entirely rather than
   show obvious placeholder text. **Featured Projects** and **Certifications** sections are
   currently absent from README.md for this reason — not an oversight.
   - Re-add Featured Projects once real projects exist.
   - Re-add Certifications only if/when actual certs are earned.

2. **LinkedIn shown as plain text, not a link.** User doesn't have a confirmed profile URL slug
   handy. Shown as `**Vamsi Vatsavai**` next to the LinkedIn badge, with an inline HTML comment
   reminder to swap in the real `linkedin.com/in/<slug>` link later.

3. **GitHub account is `Vamsi3556`, not `Vamsi-sys-tech`.** The MCP GitHub connection was
   initially authenticated as `Vamsi-sys-tech` (a secondary/empty account), then re-authenticated
   with a new token as `Vamsi3556`, which already had a matching bio and is the account the user
   confirmed to use going forward.

4. **Repo name matches username, by GitHub's own rule.** A profile README repo MUST be named
   exactly the same as the account username. The user raised that `Vamsi3556` "looks weird with
   numbers" but explicitly decided NOT to rename the GitHub account (desired name unavailable).
   Decision: keep `Vamsi3556` as-is, no further discussion needed on this point.

5. **Commits should look human, not bot-generated.** Pushed via the GitHub MCP server using
   plain, descriptive commit messages (e.g. "Add SRE-focused profile README",
   "Expand AWS and Azure service lists in skills matrix") rather than generic/robotic messages.
   No automation markers, no AI-attribution text added to commits or the README itself.

6. **MCP setup detail (environment-specific, not a project decision):** the user's machine didn't
   have Docker installed, so the official `github/github-mcp-server` is run from a downloaded
   prebuilt Windows binary (`github-mcp-server.exe`) via stdio, not via `docker run`. This only
   matters if MCP connectivity needs to be re-established on this machine.

## Current README.md structure (as of last update)

1. Header: "Hi, I'm Vamsi Vatsavai" + role/experience tagline
2. SRE Principles section (SLOs, Error Budgets, Toil Reduction, Blameless Culture, Chaos Engineering)
3. Technical Skills:
   - CI/CD & Automation: Jenkins, GitHub Actions, GitLab CI (CircleCI deliberately excluded —
     user preference)
   - Infrastructure as Code: Terraform, Ansible, CloudFormation, ARM Templates
   - Cloud Platforms:
     - AWS: EC2, S3, Lambda, RDS, CloudWatch, Secrets Manager, Systems Manager Parameter Store,
       Fargate, CodeBuild, DynamoDB, API Gateway, CloudFront (CDN), Elastic Load Balancer,
       NAT Gateway
     - Azure: VMs, Blob Storage, Functions, SQL Database, Monitor, Automation Runbooks,
       Front Door, Load Balancer, Application Gateway
   - Monitoring & Observability: Datadog, Site24x7 (user's actual main tools), plus Prometheus/
     Grafana/ELK Stack (included for portfolio demonstration purposes, not claimed as primary
     tools in actual job experience)
4. Contact ("Let's Connect"): Email (live mailto link), GitHub (live link), LinkedIn (name only,
   no link yet)
4.5. Featured Projects: one real entry (SLO & Error Budget Monitor - see "Project #1" below).
5. Closing line about target companies

Certifications section still absent (see decision #1) - only re-add if certs are actually earned.

## Project #1: SLO & Error Budget Monitor (built, shipped)

Repo: https://github.com/Vamsi3556/slo-error-budget-monitor

Built as the first real Featured Project, specifically to solve an actual problem (not a skills
demo) - see decision below. Summary:

- Synthetic HTTP checks (GitHub API, Open-Meteo, JSONPlaceholder - no-auth public APIs by design)
  run on a GitHub Actions cron schedule (every 30 min).
- Computes rolling uptime % and SRE-standard error-budget-consumed % over a configurable window.
- Auto-files a GitHub Issue with a blameless-postmortem template the moment a check fails
  (immediate incident), and a separate proactive "error-budget-warning" issue if the budget
  crosses a threshold before an outright breach; auto-closes the warning once recovered.
- Security: Bandit (SAST), pip-audit (dependency CVEs - caught and fixed a real vulnerability in
  `requests==2.32.3` during development, now pinned to `2.33.0`), CodeQL, Dependabot. Issue
  creation uses the workflow's built-in `GITHUB_TOKEN` (least privilege) rather than a stored
  PAT; an optional webhook URL for external notifications is read from a GitHub Actions secret,
  never hardcoded.
- Verified locally before pushing: ruff clean, 12/12 pytest passing, Bandit clean, pip-audit
  clean, and a live end-to-end dry run against the real target APIs. CI also passed on GitHub
  after push (lint/test, security-scan, and CodeQL jobs all green).
- Added back into the profile README's Featured Projects section with a problem/solution framing
  so it reads as "what problem did this solve" rather than a bare skills list - the user
  explicitly asked for interview-ready project narratives, not practice exercises.

**Deployment note**: pushing `.github/workflows/*.yml` files via the GitHub API requires the
PAT to have the "Workflows: Read and write" permission specifically (separate from Contents).
The first attempt failed with a 403 until the user added that permission to the token.

**Decision: no fabricated/backdated commit timestamps.** The user asked whether commit push
times could be spaced out (first by days/weeks, then reduced to "a few hours") to make a
single-session build look like it happened progressively over time. This was declined - spacing
out fake timestamps to misrepresent when work actually happened is fabricating a timeline for
whoever evaluates this (recruiters/interviewers), regardless of whether the gap is hours or
weeks. Do not do this if asked again. The honest alternative in place: the scheduled `monitor.yml`
workflow now commits real `data/history.json` updates every 30 minutes on its own real clock,
which naturally produces genuine, organically-timed repo activity going forward with no
fabrication needed.

## Cross-reference: in-progress work in Project #1's own repo

`slo-error-budget-monitor` has its own `AI_CONTEXT.md` (https://github.com/Vamsi3556/slo-error-budget-monitor/blob/main/AI_CONTEXT.md)
tracking a currently **unfinished** task: a deliberate chaos test of the incident/error-budget-
warning issue-filing pipeline (verifying it works against the real GitHub API, not just mocked
unit tests). Check that file's "IN PROGRESS" section before starting new work on that repo.

## Open items / next actions (backlog)

- [ ] Build a second real SRE-relevant project if desired (candidates discussed: Terraform
      module, chaos engineering experiment - deprioritized earlier in favor of the problem-first
      SLO monitor above).
- [ ] Get the real LinkedIn profile URL slug from the user and convert the plain-text name into
      a working link.
- [ ] Revisit Certifications section only if the user actually pursues/earns an AWS or Azure cert.
- [ ] Optional: set up a local git clone of `Vamsi3556/Vamsi3556` instead of relying solely on
      API-based pushes, if the user wants normal local git workflow on this machine.
- [ ] Optional: check back on `slo-error-budget-monitor`'s scheduled workflow after it's had time
      to run a few times, to confirm `data/history.json` is actually accumulating real check data.

## Ground rules for any AI continuing this work

- Do not add placeholder/fake content to README.md. If something isn't real yet, leave the
  section out rather than filling it with bracketed placeholders.
- Confirm before pushing changes to the live GitHub repo — don't assume every local edit should
  go live immediately (though in practice the user has asked for pushes right after edits so far).
- Keep commit messages plain and human-sounding, not robotic or AI-flavored.
- Update this file when new decisions are made or the project state changes meaningfully, so the
  log stays accurate for whoever (human or AI) picks this up next.
