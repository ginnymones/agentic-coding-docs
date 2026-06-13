# Vibe Coding Template

Use this template at the start of any AI-assisted coding session to front-load decisions and reduce rework.

---

## Phase 0: Project Brief (fill this out before coding starts)

### What am I building?
> You are building a resource matchmaker tool that will enable users (subject matter experts/SME, manager, senior leader, admin) find the users they need who have the right amount of time for the work required, as well as the skillset and proficiency level to deliver the output at the highest quality.

### Who is it for?
> The primary users are subject matter experts (SME) and managers (L4, L5), and administrators (any level). Secondary users are senior leaders (L6+). The initial build will be used by the Content Generation Hub (CGH) organization (~500 headcount) first, then we are aiming to scale up to the whole eShop organization (~2000+ headcount).

### What are the 3 core things a user must be able to do in v1?
> 1. The user must be able to see the following employee data: time spent per user, per process per day; current skillset; proficiency level; trainings taken; and success indicators (i.e. deployed in x process y # of times).
> 2. The user must be able to see which employees are available for cross-utilization in other projects, with "matches" coming from the correlation across the data identified in #1.
> 3. The user must be able to request to cross-utilize employees with skills and bandwidth capacity matching their need.

### What can wait for v2?
> Proficiency matrix (competency level per process and per manager, training need signal)
> Process alert levels and forecast (volume availability, SLA breach, human capacity overload/underload)
> Human capacity forecast (overload/underload, poor/good task complexity mix)

---

## Phase 1: Infrastructure Decisions (decide before writing code)

### Working with AI — Ground Rules
- If something is ambiguous, ask before guessing
- If the AI proposes something you don't understand, ask "why?"
- If a feature feels like scope creep, say "that can wait for v2"
- Test each deploy yourself — don't assume it works because the build passed
- If something fails twice, ask for a different approach rather than incremental patches
- State your constraints upfront (timeline, hosting, team size) so the AI can calibrate

### Authentication
> Pick one. Don't change mid-build.

| Option | When to use |
|--------|-------------|
| None | Demo, proof of concept, internal tool with no sensitive data |
| PIN/passphrase | Personal tool, small group, no email needed |
| OAuth (Google/GitHub) | Team tool, need real identity, org-level |
| Email magic link | User-facing product, no password friction |
| Full credentials | Enterprise, compliance requirements |

**My choice:** For MVP, PIN/passphrase. For actual product, Full credentials utilizing Amazon SSO
**Reason:** The goal for the MVP is to help stakeholders and senior leadership visualize the intent behind the project and the possibilities. The MVP should also be able to communicate to the app manager/developer how the whole intrastructure should be built. Meanwhile, the goal for the actual product is to have a working resource matchmaker tool.

### Database
> Pick one. Confirm free tier limits cover your use case.

| Option | When to use |
|--------|-------------|
| None (in-memory/localStorage) | Demo only, no persistence needed |
| JSON file in repo | Solo tool, git-based persistence, no multi-user |
| Supabase (PostgreSQL) | Multi-user, relational data, free tier generous |
| Vercel KV (Redis) | Simple key-value, session storage |
| PlanetScale / Neon | MySQL/PostgreSQL alternatives |

**My choice:** Supabase, Vercel
**Connection string format confirmed?** Yes
**Special characters in password?** None

### Hosting
> Pick one. Confirm it supports your stack.

| Option | When to use |
|--------|-------------|
| Vercel | Next.js, zero-config, free tier |
| Netlify | Static sites, serverless functions |
| Railway / Render | Docker, long-running processes |
| Internal (Protozoa, etc.) | Org-specific, may need Docker |
| Static file host | Single HTML file, no server needed |

**My choice:** Vercel (with private GitHub), Protozoa for internal security and initial build
**Root directory (if monorepo):** _______________
**Environment variables needed:** Please suggest the variables necessary for the tool.

### Framework & Stack
> Confirm versions. Pin them. -- Not defined yet, please suggest.

| Layer | Choice | Version |
|-------|--------|---------|
| Framework | | |
| Language | | |
| Styling | | |
| Charts/UI libs | | |
| ORM/data layer | | |
| Auth library | | |

---

## Phase 2: Visual Direction (decide before building UI)

### Theme
- [ ] Light mode
- [ ] Dark mode
- [x] Both (toggle) - light mode primarily, with option to switch to dark mode

### Vibe
> Pick 2-3 adjectives: minimalist, straightforward, not intimidating

### Colors (define upfront, verify WCAG AA contrast)
```
Background:    #FAF9F7
Card:          #FFFFFF
Text primary:  #111111
Text muted:    #2F3162
Accent:        #6970EB
Button:        #3E47E7
Success:       #2CC156
Warning:       #E47927
Danger:        #E34848
```

### Key screens to build
> List the pages/views. Prioritize.
> 1. Resource Matchmaker (Check for available associates for cross-utilization based on bandwidth and skillset. Results will appear below the matchmaker panel. For approvers, they will also see the pending resource requests for approval/rejection.)
> 2. Resource Request Intake Form (Once user selects associates, user will be taken to a form where user can request to "reserve" the chosen associates.)
> 3. Resource Climate (Displays current workload per user, per team, per process)

### UX Principles
- Use realistic content in all user-facing flows (no placeholder text)
- Accessible by default (WCAG AA contrast, semantic HTML, aria labels)
- Mobile-first: design for smallest screen, scale up
- Loading states and error states for every async action
- Feedback on every user action (success messages, disabled states during submission)
- Pointer cursor on all interactive elements

---

## Phase 3: Build Order (follow this sequence)

```
1. Scaffold project with chosen stack
2. Set up database schema + push to remote
3. Set up auth (even if minimal)
4. Verify: can I sign in and hit the database? ✓
5. Build core data flow (create, read, update, delete)
6. Verify: can I CRUD data through the API? ✓
7. Build UI skeleton (layout, routing, empty states)
8. Wire UI to real data
9. Verify: full flow works end-to-end? ✓
10. Polish (charts, animations, responsive, accessibility)
11. Deploy
12. Test on real device (mobile + desktop)
13. Fix issues found in testing
14. Document
```

**Key principle:** Verify at each checkpoint before moving forward. Don't build UI on top of broken infrastructure.

---

## Phase 4: Deployment Checklist

- [ ] Environment variables set in hosting platform
- [ ] Database schema pushed to production database
- [ ] Auth callback URLs registered (if OAuth)
- [ ] `.gitignore` covers: `node_modules`, `.next`, `.env.local`
- [ ] No secrets in committed files
- [ ] Build passes locally before pushing
- [ ] Tested on mobile viewport

---

## Phase 5: Post-Deploy Testing Script

Run through these manually after first deploy:

- [ ] Can I access the app at the URL?
- [ ] Can I sign in / create account?
- [ ] Can I create data?
- [ ] Can I read data back?
- [ ] Can I edit data?
- [ ] Can I delete data?
- [ ] Does it work on my phone?
- [ ] Does the public/shared view work (if applicable)?
- [ ] Are error states handled (wrong password, network failure)?

---

## Lessons Learned (fill after each project)

### What went well?
>

### What took longer than expected?
>

### What would I do differently next time?
>

### New patterns/tools discovered?
>

---

## Quick Reference: Common Gotchas

| Issue | Prevention |
|-------|-----------|
| `node_modules` committed to git | Use `node_modules` (no leading `/`) in `.gitignore` |
| Supabase port 6543 unreachable locally | Use port 5432 for CLI, 6543 for serverless |
| "prepared statement does not exist" | Add `?pgbouncer=true` to connection string |
| Password special chars break URL | URL-encode before putting in connection string |
| OAuth redirect URI mismatch | Register full callback URL including `/api/auth/callback/[provider]` |
| Prisma version mismatch | Pin major version, check compatibility with framework |
| Chart hover shows light background | Add `cursor={false}` to Recharts Tooltip |
| Legend overlaps chart on mobile | Use `verticalAlign="bottom"` with padding |
| Build fails on Vercel but works locally | Check env vars are set, check root directory setting |
