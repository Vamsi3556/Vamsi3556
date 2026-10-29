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
- No dedicated portfolio/SRE projects built yet (as of this writing)

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
5. Closing line about target companies

No Featured Projects or Certifications sections currently (see decision #1 above).

## Open items / next actions (backlog)

- [ ] Build 1-2 real SRE-relevant projects (e.g. Terraform module, monitoring/alerting automation,
      CI/CD pipeline with rollback, chaos engineering experiment). Once they exist, add a
      "Featured Projects" section back into README.md with real names/descriptions/links.
- [ ] Get the real LinkedIn profile URL slug from the user and convert the plain-text name into
      a working link.
- [ ] Revisit Certifications section only if the user actually pursues/earns an AWS or Azure cert.
- [ ] Optional: set up a local git clone of `Vamsi3556/Vamsi3556` instead of relying solely on
      API-based pushes, if the user wants normal local git workflow on this machine.

## Ground rules for any AI continuing this work

- Do not add placeholder/fake content to README.md. If something isn't real yet, leave the
  section out rather than filling it with bracketed placeholders.
- Confirm before pushing changes to the live GitHub repo — don't assume every local edit should
  go live immediately (though in practice the user has asked for pushes right after edits so far).
- Keep commit messages plain and human-sounding, not robotic or AI-flavored.
- Update this file when new decisions are made or the project state changes meaningfully, so the
  log stays accurate for whoever (human or AI) picks this up next.
