# Interview Intel: Lifted — Senior QA Engineer (Contract, LATAM)

**Evaluation report:** [#004](../reports/004-lifted-2026-04-15.md) | Score: 3.8/5
**Researched:** 2026-04-22
**Sources:** 0 Glassdoor reviews (company too small), 0 Blind posts — all intel inferred from JD + archetype patterns. Every question is labeled accordingly.

---

## Process Overview

- **Rounds:** 4 stages (confirmed from JD)
- **Format:** Recruiter screening (60 min) → Culture fit (30 min) → Technical assessment → Hiring manager (60 min)
- **Difficulty:** Unknown — insufficient data
- **Positive experience rate:** Unknown
- **Known quirks:** Contract-only modality — comp discussion happens early
- **Sources:** JD text (Greenhouse posting)

---

## Round-by-Round Breakdown

### Round 1: Recruiter Screening — 60 min

- **Conducted by:** Recruiter / HR
- **What they evaluate:** Background fit, LATAM eligibility, contract comfort, availability, English level, salary expectation
- **Likely questions:**
  - "Walk me through your QA background." `[inferred from JD]`
  - "Are you comfortable with contract work? What's your rate expectation?" `[inferred — contract role]`
  - "What's your current availability / notice period?" `[inferred]`
  - "What's your experience with Playwright specifically?" `[inferred from JD — it's their #1 requirement]`
  - "Have you worked in Agile/Scrum teams before?" `[inferred from JD]`
- **How to prepare:**
  - Have your rate target ready: **$3,500–$4,000/month**. Say it confidently, not apologetically.
  - Lead with Gorilla Logic + Playwright as the opening line — that's what they want to hear first.

---

### Round 2: Culture Fit — 30 min

- **Conducted by:** Team lead or engineering manager
- **What they evaluate:** Communication style, async work habits, how you handle feedback and ambiguity, team fit
- **Likely questions:**
  - "How do you communicate defects to developers who push back?" `[inferred — collaborative culture signal]`
  - "Tell me about a time you disagreed with a dev on a bug priority." `[inferred from behavioral pattern]`
  - "How do you work in a distributed, async team?" `[inferred — LATAM remote role]`
  - "What does quality mean to you beyond test coverage?" `[inferred — culture screen]`
- **How to prepare:**
  - Lifted is a smaller company — they care about attitude as much as skill. Show curiosity about their product (contingent workforce platform).
  - Mention your distributed experience explicitly: "I've been fully remote across all my last three roles, English-only async communication."

---

### Round 3: Technical Assessment

- **Format:** Unknown — could be take-home or live coding
- **Conducted by:** Senior engineer or QA lead
- **What they evaluate:** Playwright proficiency, test structure quality, TypeScript comfort, how you handle edge cases
- **Likely scenarios:** `[inferred from JD requirements]`
  - Write Playwright tests for a given URL or feature
  - Review existing test code and identify improvements
  - Live debug a flaky test
  - Design a test plan for a described feature
- **How to prepare:**
  - Review Playwright patterns: `test.describe`, `page.locator`, `expect` assertions, `beforeEach`/`afterAll` hooks
  - Practice Page Object Model (POM) structure — you list it in your CV, be ready to implement it live
  - If take-home: prioritize readable, maintainable code over clever solutions. Add a short README explaining your decisions.
  - If asked about BrowserStack/LambdaTest: "I use Playwright's built-in multi-browser support (Chromium, Firefox, WebKit). BrowserStack same-day onboarding."

---

### Round 4: Hiring Manager — 60 min

- **Conducted by:** Hiring manager / Lifted leadership
- **What they evaluate:** Senior judgment, ownership mindset, proof points, fit for the specific client project
- **Likely questions:**
  - "Tell me about a time you built or improved a QA process from scratch." `[inferred — JD says 'develop and maintain testing strategies']`
  - "How do you decide what to automate vs. keep manual?" `[inferred — hybrid manual/automation role]`
  - "Tell me about a significant bug you caught before release." `[inferred — standard senior QA]`
  - "How do you handle sprint pressure when testing time gets cut?" `[inferred — sprint collaboration req]`
  - "What's your approach to cross-browser testing?" `[inferred from JD nice-to-have]`
  - "Why this role? Why Lifted?" `[standard]`

---

## Likely Questions — Full List

### Technical `[inferred from JD]`

**Q: Walk me through how you structure a Playwright test suite.**
Best answer: POM pattern. `pages/` directory for page objects, `tests/` for specs, `fixtures/` for reusable setup. Gorilla Logic context: "I organize by feature module — each page object encapsulates selectors and actions, tests stay declarative. I run via GitHub Actions on every PR."

**Q: How do you handle flaky tests?**
Best answer: "First, I quarantine them — tag as `@flaky`, exclude from blocking CI. Then investigate: async timing issues get explicit waits (`waitForSelector`, not `sleep`), environment issues get retry logic. Root cause first, band-aid second." IDEMIA context: flaky tests on mobile/OS variants.

**Q: How do you integrate automation into CI/CD?**
Best answer: Leanware story — Jenkins pipeline, shift-left, PR-blocking test gates. "Tests run on every push, results in Jira, blocking only the critical path suite to keep builds fast."

**Q: What's the difference between E2E, integration, and unit testing? When do you use each?**
Best answer: Standard pyramid answer, but anchor to your experience: "At IDEMIA I owned the E2E and integration layers — unit tests belonged to devs. My job was validating the full system path, especially the API-to-UI flow for biometric enrollment."

---

### Behavioral `[inferred from JD + archetype patterns]`

**Q: Tell me about a time you improved a QA process significantly.**
→ **Use: Thales -75% story** (see Story Bank below)

**Q: Tell me about a time you found a critical bug before production.**
→ **Use: Acsendo -50% bugs story** — or any IDEMIA biometric system defect catch

**Q: Tell me about a conflict with a developer over a bug.**
→ Build from: Leanware context — banking compliance, when a bug is "by design" vs. actually wrong. Frame: "I escalate with data — reproduce rate, customer impact estimate, compliance risk. I make it easy for the dev to say yes to fixing it."

**Q: How do you handle being told there's no time to test properly?**
→ "I triage. I identify what's highest risk — new code paths, changed integrations, areas with no existing coverage. I document what I'm NOT testing and why, so the team owns the risk decision consciously."

---

### Role-Specific `[inferred from JD]`

**Q: How do you approach testing a feature you know nothing about?**
→ "First I read the acceptance criteria and any design specs. Then I ask one question: what's the worst thing that could happen if this is wrong? That gives me the highest-risk paths to test first. I do exploratory testing before writing automation — you can't automate what you haven't understood manually."

**Q: How do you work with developers to ensure testability?**
→ Leanware story: "At Leanware I participated in sprint planning to raise testability concerns early — before code was written. I'd flag things like missing error states, inconsistent API responses, or UX flows that would be hard to automate. That's the shift-left mindset."

**Q: What's your experience with Jira vs. Linear for defect tracking?**
→ "Jira is my primary — used it at Leanware, IDEMIA, Thales, Gorilla Logic. I've used it for full defect lifecycle: creation, triage, sprint boards, retrospective metrics. Linear I haven't used but it follows the same workflow paradigm — I'd be up to speed immediately."

---

### Background Red Flags

**Q: Why are you leaving Gorilla Logic after less than a year?**
→ "I'm not leaving — I'm open to the right opportunity in parallel. Gorilla Logic is a staff augmentation model, so I have flexibility to take on a contract engagement that's a strong technical fit. Lifted's Playwright+TypeScript stack is exactly my current day-to-day."

*(If that's not accurate — adjust based on your actual situation with Gorilla Logic.)*

**Q: You've worked in biometrics and identity — why contingent workforce software?**
→ "The domain is different, but the testing challenge is the same: a SaaS platform where bugs affect real business operations. At IDEMIA a defect in enrollment affected thousands of people. At Lifted, a defect in workforce management affects clients' business. Same rigor applies."

**Q: You have banking, biometrics, government — that's specialized. Can you adapt to a SaaS product company?**
→ "All of my work has been SaaS or enterprise software at the application layer. The biometric hardware was the client's system — I was always testing software integration and APIs, not hardware. Gorilla Logic right now is pure SaaS product engineering."

---

## Story Bank — Built for This Interview

### [Automation from Scratch] Thales Framework — 75% Time Reduction
**S:** At Thales Group (identity document systems), all QA was manual. No automation existed. The team was spending 80% of test cycles on repetitive regression runs for passport and ID card issuance software.
**T:** I was tasked with building an automated testing framework from zero to reduce regression time and improve reliability before major release cycles.
**A:** I chose Selenium + Java + Groovy, designed a modular framework with POM pattern, trained two validation engineers on maintaining it, and integrated it into the release sign-off process. Wrote tests covering the full enrollment-to-issuance flow.
**R:** Reduced testing time by 75%. What took 4 weeks of manual regression now ran in under a week. Recognized as Top 10 Employee for this contribution.
**Reflection:** I'd now add CI/CD integration from day one — we ran it manually at first. Automation without pipeline integration is only half the job.
**Best for:** "Tell me about a time you built something from scratch" / "How have you improved a QA process?" / "What's your biggest achievement?"

---

### [Shift-Left & CI/CD] Leanware — Sprint-Integrated Testing
**S:** At Leanware (banking SaaS), the QA function was post-development — tests ran after features were "done," finding bugs too late and slowing releases.
**T:** I was asked to improve the QA integration with the dev process to catch bugs earlier and reduce rework cycles.
**A:** Integrated automated test suites into the Jenkins CI/CD pipeline. Set up PR-blocking tests for critical paths. Participated in sprint planning to raise testability concerns before code was written. Defined acceptance criteria alongside product.
**R:** Measurably reduced manual testing effort. Bugs were caught at PR stage, not in staging. Sprint velocity improved because integration issues surfaced earlier.
**Reflection:** Getting buy-in from devs was the hardest part. I learned to frame testing as their ally, not a gate — "this catches your bugs before your code review."
**Best for:** "How do you implement shift-left?" / "Tell me about CI/CD integration" / "How do you collaborate with developers?"

---

### [Bug Prevention] Acsendo — 50% Bug Reduction
**S:** At Acsendo (SaaS HR platform), production bugs were high and recurring. The team was reactive — fixing bugs after users reported them.
**T:** Introduce systematic testing to catch bugs in the development phase, not production.
**A:** Combined manual exploratory testing with automated regression using Java + JUnit. Used SQL queries to validate data integrity at the backend, not just UI. Set up test coverage metrics to track progress.
**R:** 50% reduction in production bugs over the testing phase. Customer satisfaction improved measurably.
**Reflection:** The SQL validation was the key insight — many bugs weren't visible in the UI but showed up in the data. Testing at the data layer catches things UI testing misses.
**Best for:** "Tell me about a time you prevented bugs" / "How do you measure QA impact?" / "What's your approach to quality?"

---

### [Cross-Platform Testing] IDEMIA — Mobile Campaign
**S:** At IDEMIA, biometric enrollment apps needed to work across a wide range of mobile devices and OS versions used in government deployments (not controlled environments).
**T:** Design and execute a cross-platform test campaign to validate application behavior across the full device matrix.
**A:** Set up an Appium-based mobile test suite. Defined the device matrix based on client deployment requirements. Led a campaign across 15+ device/OS combinations. Documented and triaged OS-specific bugs separately from application bugs.
**R:** Identified 8 OS-specific compatibility issues before client delivery. Zero reported compatibility failures during UAT.
**Reflection:** Device matrix definition is as important as the tests — you can't test everything, so you have to be strategic about what represents the actual deployment environment.
**Best for:** "Cross-browser / cross-platform testing" / "How do you handle testing at scale?" / "Tell me about mobile testing"

---

---

## Round 2 Deep Prep — Technical Assessment (2026-04-29)

> Format unknown — prepare for both live coding and take-home. If live: share your screen and think out loud. If take-home: clean code + short README wins over clever code.

---

### Topic 1: Playwright Fundamentals

**Q: Walk me through how you structure a Playwright test suite.**

> "I use Page Object Model. The `pages/` directory holds page classes — each one encapsulates locators and actions for a given screen. The `tests/` directory holds the specs, which stay declarative: they call page methods and make assertions, never touching selectors directly. I add a `fixtures/` folder for reusable setup like authenticated state or test data. At Gorilla Logic this is my current setup — I run it through GitHub Actions on every PR."

Key things to say: POM, `pages/`, `tests/`, `fixtures/`, CI on every PR.

---

**Q: How do you locate elements in Playwright? Walk me through your strategy.**

> "I follow Playwright's recommended priority: user-facing locators first. `getByRole()` and `getByLabel()` are my defaults because they reflect what a real user sees, and they're resilient to DOM refactors. `getByTestId()` when the team has added `data-testid` attributes — I advocate for this in sprint planning. `page.locator()` with CSS or XPath is last resort, only when nothing else is stable. I avoid absolute XPaths — they break on any DOM change."

Priority order to mention: `getByRole` → `getByLabel` → `getByTestId` → `locator()` CSS → XPath never.

---

**Q: Write a Playwright test for a login flow.**

Be ready to write this from memory:

```typescript
// pages/LoginPage.ts
import { Page, Locator } from '@playwright/test';

export class LoginPage {
  readonly page: Page;
  readonly emailInput: Locator;
  readonly passwordInput: Locator;
  readonly submitButton: Locator;
  readonly errorMessage: Locator;

  constructor(page: Page) {
    this.page = page;
    this.emailInput = page.getByLabel('Email');
    this.passwordInput = page.getByLabel('Password');
    this.submitButton = page.getByRole('button', { name: 'Sign in' });
    this.errorMessage = page.getByRole('alert');
  }

  async login(email: string, password: string) {
    await this.emailInput.fill(email);
    await this.passwordInput.fill(password);
    await this.submitButton.click();
  }
}

// tests/auth/login.spec.ts
import { test, expect } from '@playwright/test';
import { LoginPage } from '../../pages/LoginPage';

test.describe('Authentication', () => {
  let loginPage: LoginPage;

  test.beforeEach(async ({ page }) => {
    loginPage = new LoginPage(page);
    await page.goto('/login');
  });

  test('successful login redirects to dashboard', async ({ page }) => {
    await loginPage.login('user@example.com', 'validPassword');
    await expect(page).toHaveURL('/dashboard');
  });

  test('invalid credentials shows error message', async () => {
    await loginPage.login('user@example.com', 'wrongPassword');
    await expect(loginPage.errorMessage).toBeVisible();
    await expect(loginPage.errorMessage).toContainText('Invalid');
  });

  test('empty fields prevents submission', async () => {
    await loginPage.submitButton.click();
    await expect(loginPage.emailInput).toBeFocused();
  });
});
```

Things they'll evaluate: POM class structure, typed Locators, `beforeEach` setup, happy path + negative + edge case, `getByLabel`/`getByRole` usage.

---

### Topic 2: Flaky Tests

**Q: You've inherited a test suite with several flaky tests. What's your approach?**

> "First I quarantine them — tag with `@flaky` and exclude from the blocking CI gate so they don't stop everyone's work. Then I investigate one by one. Most flakiness falls into three categories: timing issues, where the test acts before the UI is ready; environment issues, like test data that changes between runs; and selector instability, where the locator breaks on minor DOM changes.
>
> For timing: Playwright's auto-wait handles most cases, but if I need explicit waiting I use `waitForResponse()` or `waitForURL()` tied to a real event, never `page.waitForTimeout()`. For environment: isolate test data per test or seed it in `beforeEach`. For selectors: move to `getByRole` or `getByTestId`. Root cause first — retries are a band-aid, not a fix."

Key things to mention: quarantine first, three categories (timing/environment/selector), `waitForResponse` not `waitForTimeout`, retries are band-aids.

---

**Q: When is `waitForTimeout` acceptable?**

> "Almost never in production test suites. It's only acceptable as a temporary debugging aid while diagnosing a timing issue — never committed. I've seen `sleep(2000)` scattered through suites and it's always a sign the root cause was never investigated. The real fix is almost always waiting for a specific network response, URL change, or element state — things Playwright can detect deterministically."

---

### Topic 3: TypeScript in Tests

**Q: How do you use TypeScript specifically in your Playwright work?**

> "I use interfaces to type test data and API response shapes — it catches mismatches between what the test expects and what the actual payload returns before the test even runs. I type all page object constructor parameters and return values so IDE autocompletion works across the suite. I use enums for things like user roles or test environments so magic strings don't leak into tests. And async/await everywhere — no promise chains."

Show you know: interfaces for test data, typed page objects, enums over magic strings, async/await.

---

**Q: Write a TypeScript interface for test data.**

```typescript
interface UserCredentials {
  email: string;
  password: string;
  role: 'admin' | 'manager' | 'worker';
}

interface WorkerProfile {
  id: string;
  name: string;
  status: 'active' | 'inactive' | 'pending';
  contractStart: Date;
}

// Usage in test
const testUser: UserCredentials = {
  email: 'worker@example.com',
  password: 'Test@1234',
  role: 'worker'
};
```

---

### Topic 4: CI/CD Integration

**Q: How do your Playwright tests plug into CI/CD?**

> "In GitHub Actions I have a workflow triggered on every PR. It installs dependencies, runs `npx playwright install --with-deps`, then runs the suite. I separate runs by tag: `@smoke` runs on every push (fast, < 2 min), `@regression` runs only before merges to main. Test results go to the Actions summary as HTML report artifacts. On failures, the job blocks the PR merge — that's the shift-left gate. I've done the same architecture with Jenkins at Leanware."

Structure to mention: trigger on PR, install browsers, smoke vs. regression tags, HTML report artifacts, blocking gate.

---

**Q: How do you handle browser installation in CI?**

> "`npx playwright install --with-deps` installs the browser binaries and their OS-level dependencies. In Docker-based CI I cache the browsers layer to avoid reinstalling on every run. Playwright also supports running tests against a remote browser grid — useful when you want to test across browser versions without managing local installs."

---

### Topic 5: Test Plan Design (if asked to design, not code)

**Q: Design a test plan for a shift assignment feature in a contingent workforce platform.**

Answer structure:

> "I'd start with the acceptance criteria and map out the user flows. For shift assignment, the main scenarios would be:
>
> **Happy path:** Manager creates shift → assigns worker → worker receives notification → worker accepts → shift shows as confirmed.
>
> **Negative cases:** Assign to unavailable worker (conflict check), assign past the worker's contracted hours, assign to inactive/terminated worker, assign with missing required fields.
>
> **Edge cases:** Two managers assigning the same worker simultaneously (race condition), shift spanning midnight, worker in different timezone, bulk assignment to 100+ workers.
>
> **Data integrity:** Verify the assignment is correctly persisted (SQL query to backend if accessible), not just visible in UI.
>
> **I'd automate** the happy path and the critical negative cases first. The race condition and bulk scenarios I'd flag for load/stress testing separately. Manual exploratory testing covers the UX edge cases that are hard to predict from requirements."

---

### Topic 6: Code Review / Identify Issues

If they show you an existing test and ask what you'd improve, watch for these common issues:

| Anti-pattern | What to say |
|---|---|
| `page.waitForTimeout(3000)` | "I'd replace with `waitForResponse()` or `waitForSelector()` — arbitrary sleeps make tests slow and still flaky" |
| Raw CSS selectors like `div.btn-primary` | "I'd move to `getByRole('button', { name: '...' })` — more resilient and semantically clear" |
| No page objects, selectors in spec files | "I'd extract to a page object — specs should read like a user story, not like DOM traversal" |
| `test.only` committed | "This blocks the rest of the suite in CI — should never be committed" |
| No assertions on API responses | "I'd add `expect(response.status()).toBe(200)` and validate the response body, not just the UI reaction" |
| Magic strings repeated across tests | "I'd extract to constants or a TypeScript enum to avoid drift" |

---

### If It's Take-Home Format

**README template to include:**

```markdown
## Approach

- POM structure: `pages/` for page objects, `tests/` for specs
- Locator strategy: getByRole/getByLabel first, getByTestId for dynamic content
- Test coverage: happy path, key negative cases, one edge case per feature
- What I'd add with more time: API-level test data setup, visual regression with Playwright screenshots
```

**How to present your code:**

- Use `test.describe` to group by feature, not by file
- Add a comment on any non-obvious decision (e.g., why you used `waitForResponse` instead of `waitForSelector`)
- Run `npx tsc --noEmit` before submitting — no TypeScript errors in submission

---

### Quick-fire Q&A Cheat Sheet

| Question | One-line answer |
|---|---|
| `page.locator` vs `getByRole`? | `getByRole` is preferred — semantic, resilient, Playwright-recommended |
| How do you share auth state across tests? | `storageState` saved after login, loaded in `playwright.config.ts` as `use.storageState` |
| How do you test API responses? | `page.route()` to intercept, or `request` fixture for direct API calls without browser |
| Parallel test execution? | `workers` in `playwright.config.ts`, ensure tests are isolated (no shared state) |
| What's a fixture in Playwright? | Extended `test` object via `test.extend()` — provides reusable setup like logged-in page |
| How do you run only one browser? | `--project=chromium` flag, or configure in `playwright.config.ts` |
| Screenshot on failure? | `use: { screenshot: 'only-on-failure' }` in config |
| How do you mock an API? | `page.route('**/api/endpoint', route => route.fulfill({ json: mockData }))` |

---

## Technical Prep Checklist

- [ ] **Playwright API fundamentals** — `page.locator()`, `expect()`, `waitFor*`, `route()` for API mocking — why: *it's their #1 requirement, expect live coding or take-home*
- [ ] **Page Object Model implementation** — you claim it in your CV; be ready to write it from memory — why: *standard senior QA bar*
- [ ] **TypeScript in test context** — interfaces for test data, type-safe selectors, async/await patterns — why: *JD requires TypeScript proficiency*
- [ ] **Test plan design** — given a feature, identify test cases (happy path, edge cases, negative, performance) — why: *"develop and maintain effective testing strategies" is in JD*
- [ ] **Flaky test debugging** — timing issues, environment issues, selector instability — why: *this comes up in every senior QA interview*
- [ ] **CI/CD integration** — how tests plug into GitHub Actions or similar — why: *JD lists CI/CD familiarity as required*
- [ ] **Defect lifecycle in Jira** — severity vs. priority, how to write a good bug report — why: *Jira is listed as required tool*
- [ ] **Browser DevTools** — network tab for API validation, console errors, performance panel basics — why: *web/backend testing requires this*

---

## Company Signals

**Values to demonstrate (from JD language):**
- "Collaborative" — mention cross-team work explicitly; Lifted wants QA embedded in the team, not siloed
- "Ownership" — frame your stories as "I decided" and "I led", not "I was asked to"
- Contract mindset — they want someone who hits the ground running, no onboarding runway. Lead with readiness.

**Vocabulary to use:**
- "Sprint sign-off" and "release gates" — maps to their release cycle language
- "Shift-left" — shows QA philosophy alignment
- "Playwright selectors" and "locator strategies" — signals hands-on, not theoretical

**Things to avoid:**
- Don't over-explain the biometric background — they don't need the full IDEMIA story for every question. Use it sparingly as a "systems that can't fail" framing.
- Don't mention BrowserStack as a gap — say "Playwright handles cross-browser natively; BrowserStack is additive."

**Questions to ask them:**
1. "What does the current test coverage look like for the platform — are we starting from scratch or extending an existing suite?"
2. "How is QA embedded in the sprint process today — do I participate in planning and refinement, or is my touchpoint mainly at the testing phase?"
3. "What's the biggest quality challenge on the product right now?" *(Shows strategic thinking, not just execution focus)*

---

---

## Mock Scenarios — Live Coding Practice

> Run these as real drills: open VS Code, set a 20-minute timer, write the solution from scratch. Then compare. Do each one at least twice before Friday.

---

### Scenario 1 — Fix the Broken Test

**Prompt:** "Here's a test a junior wrote. It's flaky and keeps failing in CI. Find everything wrong with it and fix it."

```typescript
// BROKEN — find all the issues
import { test, expect } from '@playwright/test';

test('worker shift assignment', async ({ page }) => {
  await page.goto('https://app.lifted.com/dashboard');
  
  await page.waitForTimeout(3000);
  
  await page.click('div.btn > span.label');
  
  await page.waitForTimeout(2000);
  
  await page.fill('#worker-search', 'John Smith');
  
  await page.waitForTimeout(1000);
  
  await page.click('.dropdown-item:first-child');
  
  const text = await page.textContent('.confirmation-banner');
  expect(text).toBe('Shift assigned');
});
```

**Issues to find (spot all 7 before reading the fix):**

1. No `beforeEach` — navigating inside the test, not isolated
2. Three `waitForTimeout` calls — arbitrary sleeps, not event-driven
3. `div.btn > span.label` — fragile CSS combinator, breaks on markup change
4. `#worker-search` — ID selector acceptable but `getByLabel` is more semantic
5. `.dropdown-item:first-child` — index-based selector, no guarantee it's John Smith
6. No assertion that the dropdown populated before clicking
7. `textContent()` returns `string | null` — not typed, `expect` may receive null

**Fixed version:**

```typescript
import { test, expect } from '@playwright/test';
import { DashboardPage } from '../../pages/DashboardPage';

test.describe('Shift Assignment', () => {
  let dashboard: DashboardPage;

  test.beforeEach(async ({ page }) => {
    // assumes storageState handles auth — no login inside the test
    dashboard = new DashboardPage(page);
    await dashboard.goto();
  });

  test('assigns a shift to an available worker', async ({ page }) => {
    await dashboard.openShiftAssignment();

    const search = page.getByLabel('Search worker');
    await search.fill('John Smith');

    // wait for dropdown to populate — not a timeout
    const dropdown = page.getByRole('listbox');
    await expect(dropdown).toBeVisible();

    await page.getByRole('option', { name: 'John Smith' }).click();

    // wait for the network call that confirms assignment
    await page.waitForResponse(resp =>
      resp.url().includes('/api/shifts/assign') && resp.status() === 200
    );

    const banner = page.getByRole('status');
    await expect(banner).toContainText('Shift assigned');
  });
});
```

**What to say out loud during this drill:**
> "First thing I notice is three `waitForTimeout` calls — that's always a red flag. They slow the suite and still fail when the network is slower than the hardcoded delay. I'll replace each one with a deterministic wait. Second: the selectors are implementation-coupled — if a developer renames the CSS class, the test breaks for no functional reason. I'll move to role-based locators. Third: I'd extract this to a page object, but if time is limited I'll at least put the locators in variables with meaningful names."

---

### Scenario 2 — Write From Scratch

**Prompt:** "Write Playwright tests for a worker profile update form. The form has: Full Name (text), Availability (dropdown: Full-time / Part-time / Weekends only), Skills (multi-select checkboxes), and a Save button. After save, a success toast appears and the new values persist on page reload."

**Your solution:**

```typescript
// pages/WorkerProfilePage.ts
import { Page, Locator } from '@playwright/test';

export class WorkerProfilePage {
  readonly page: Page;
  readonly nameInput: Locator;
  readonly availabilitySelect: Locator;
  readonly saveButton: Locator;
  readonly successToast: Locator;

  constructor(page: Page) {
    this.page = page;
    this.nameInput = page.getByLabel('Full Name');
    this.availabilitySelect = page.getByLabel('Availability');
    this.saveButton = page.getByRole('button', { name: 'Save' });
    this.successToast = page.getByRole('status');
  }

  async goto() {
    await this.page.goto('/profile');
  }

  async skillCheckbox(skill: string): Promise<Locator> {
    return this.page.getByRole('checkbox', { name: skill });
  }

  async save() {
    await this.saveButton.click();
    await this.page.waitForResponse(resp =>
      resp.url().includes('/api/profile') && resp.status() === 200
    );
  }
}

// tests/profile/profile-update.spec.ts
import { test, expect } from '@playwright/test';
import { WorkerProfilePage } from '../../pages/WorkerProfilePage';

test.describe('Worker Profile Update', () => {
  let profile: WorkerProfilePage;

  test.beforeEach(async ({ page }) => {
    profile = new WorkerProfilePage(page);
    await profile.goto();
  });

  test('updates name and shows success toast', async ({ page }) => {
    await profile.nameInput.fill('Maria González');
    await profile.save();

    await expect(profile.successToast).toBeVisible();
    await expect(profile.successToast).toContainText('saved');
  });

  test('persists changes after page reload', async ({ page }) => {
    await profile.nameInput.fill('Carlos Ruiz');
    await profile.availabilitySelect.selectOption('Part-time');
    await profile.save();

    await page.reload();

    await expect(profile.nameInput).toHaveValue('Carlos Ruiz');
    await expect(profile.availabilitySelect).toHaveValue('Part-time');
  });

  test('selects multiple skills', async ({ page }) => {
    const skills = ['Forklift', 'Logistics', 'Safety Certified'];
    for (const skill of skills) {
      await (await profile.skillCheckbox(skill)).check();
    }
    await profile.save();

    await page.reload();

    for (const skill of skills) {
      await expect(await profile.skillCheckbox(skill)).toBeChecked();
    }
  });

  test('save button is disabled when name is empty', async () => {
    await profile.nameInput.clear();
    await expect(profile.saveButton).toBeDisabled();
  });

  test('shows validation error for name exceeding 100 characters', async () => {
    await profile.nameInput.fill('A'.repeat(101));
    await profile.save();

    const error = profile.page.getByRole('alert');
    await expect(error).toContainText('100');
  });
});
```

**Coverage you hit:** happy path, persistence (reload), multi-select, disabled state, validation error. That's the full expected set for a senior.

---

### Scenario 3 — Refactor to POM

**Prompt:** "Refactor this working test suite into Page Object Model. Don't change behavior, only structure."

```typescript
// BEFORE — all selectors inline
import { test, expect } from '@playwright/test';

test('login success', async ({ page }) => {
  await page.goto('/login');
  await page.fill('[data-testid="email"]', 'admin@lifted.com');
  await page.fill('[data-testid="password"]', 'Admin@1234');
  await page.click('[data-testid="submit"]');
  await expect(page).toHaveURL('/dashboard');
});

test('login fails with wrong password', async ({ page }) => {
  await page.goto('/login');
  await page.fill('[data-testid="email"]', 'admin@lifted.com');
  await page.fill('[data-testid="password"]', 'wrong');
  await page.click('[data-testid="submit"]');
  await expect(page.locator('[data-testid="error-msg"]')).toBeVisible();
});

test('login fails with empty email', async ({ page }) => {
  await page.goto('/login');
  await page.fill('[data-testid="password"]', 'Admin@1234');
  await page.click('[data-testid="submit"]');
  await expect(page.locator('[data-testid="email-error"]')).toContainText('required');
});
```

**Your refactored version:**

```typescript
// pages/LoginPage.ts
import { Page, Locator } from '@playwright/test';

export class LoginPage {
  readonly page: Page;
  readonly emailInput: Locator;
  readonly passwordInput: Locator;
  readonly submitButton: Locator;
  readonly errorMessage: Locator;
  readonly emailError: Locator;

  constructor(page: Page) {
    this.page = page;
    this.emailInput = page.getByTestId('email');
    this.passwordInput = page.getByTestId('password');
    this.submitButton = page.getByTestId('submit');
    this.errorMessage = page.getByTestId('error-msg');
    this.emailError = page.getByTestId('email-error');
  }

  async goto() {
    await this.page.goto('/login');
  }

  async login(email: string, password: string) {
    await this.emailInput.fill(email);
    await this.passwordInput.fill(password);
    await this.submitButton.click();
  }
}

// tests/auth/login.spec.ts
import { test, expect } from '@playwright/test';
import { LoginPage } from '../../pages/LoginPage';

test.describe('Login', () => {
  let loginPage: LoginPage;

  test.beforeEach(async ({ page }) => {
    loginPage = new LoginPage(page);
    await loginPage.goto();
  });

  test('success redirects to dashboard', async ({ page }) => {
    await loginPage.login('admin@lifted.com', 'Admin@1234');
    await expect(page).toHaveURL('/dashboard');
  });

  test('wrong password shows error', async () => {
    await loginPage.login('admin@lifted.com', 'wrong');
    await expect(loginPage.errorMessage).toBeVisible();
  });

  test('empty email shows field validation', async () => {
    await loginPage.passwordInput.fill('Admin@1234');
    await loginPage.submitButton.click();
    await expect(loginPage.emailError).toContainText('required');
  });
});
```

**What changed:** selectors centralized in one class, `beforeEach` eliminates repeated `page.goto`, `login()` method removes duplicated fill+click, specs read like plain English.

---

### Scenario 4 — API Mocking

**Prompt:** "The workers list endpoint is slow and returns 500 records in staging. Write a test for the dashboard workers table without hitting the real API."

```typescript
import { test, expect } from '@playwright/test';

const MOCK_WORKERS = [
  { id: '1', name: 'Ana Torres', status: 'active', role: 'Forklift Operator' },
  { id: '2', name: 'Luis Pérez', status: 'inactive', role: 'Warehouse Associate' },
];

test.describe('Workers Table (mocked API)', () => {
  test.beforeEach(async ({ page }) => {
    // intercept before navigation so the mock is in place when the page loads
    await page.route('**/api/workers', async route => {
      await route.fulfill({
        status: 200,
        contentType: 'application/json',
        body: JSON.stringify({ workers: MOCK_WORKERS, total: 2 }),
      });
    });

    await page.goto('/dashboard/workers');
  });

  test('displays worker names from API', async ({ page }) => {
    const table = page.getByRole('table');
    await expect(table).toBeVisible();
    await expect(page.getByRole('row', { name: /Ana Torres/ })).toBeVisible();
    await expect(page.getByRole('row', { name: /Luis Pérez/ })).toBeVisible();
  });

  test('shows inactive badge on inactive workers', async ({ page }) => {
    const luisRow = page.getByRole('row', { name: /Luis Pérez/ });
    await expect(luisRow.getByText('inactive')).toBeVisible();
  });

  test('handles empty workers list gracefully', async ({ page }) => {
    // override the route for this specific test
    await page.route('**/api/workers', route =>
      route.fulfill({
        status: 200,
        contentType: 'application/json',
        body: JSON.stringify({ workers: [], total: 0 }),
      })
    );

    await page.reload();

    await expect(page.getByText('No workers found')).toBeVisible();
  });

  test('handles API error — shows error state', async ({ page }) => {
    await page.route('**/api/workers', route =>
      route.fulfill({ status: 500 })
    );

    await page.reload();

    await expect(page.getByRole('alert')).toContainText('Something went wrong');
  });
});
```

**Key points to say:**
> "I set up `page.route()` before `page.goto()` so the intercept is in place before the browser makes the first request. The mock lets me test specific states — empty list, error 500 — that are hard to reproduce against the real API. The last two tests override the route inside the test itself; that works because `page.route()` stacks and the last registered handler wins."

---

### Scenario 5 — Debug a Flaky Test Live

**Prompt:** "This test passes locally 9/10 times but fails in CI almost every run. Diagnose and fix it."

```typescript
// FLAKY
test('search filters workers by name', async ({ page }) => {
  await page.goto('/workers');
  
  await page.fill('[data-testid="search-input"]', 'Maria');
  
  const rows = page.locator('table tbody tr');
  const count = await rows.count();
  
  expect(count).toBeGreaterThan(0);
  
  const firstRowText = await rows.first().textContent();
  expect(firstRowText).toContain('Maria');
});
```

**Diagnosis process — say this out loud:**

> "First question: what's different between local and CI? Local is fast, CI has network latency. So the test fills the search input, then immediately counts rows — but the table hasn't had time to re-render after the search request returns. There's no wait between filling the input and asserting results.
>
> Second issue: `rows.count()` captures a snapshot. If I call it before the search response arrives, it returns the pre-filter count. The assertion passes with the wrong data.
>
> Third: `textContent()` returns `string | null` — if the row is still rendering, it can return null."

**Fixed version:**

```typescript
test('search filters workers by name', async ({ page }) => {
  await page.goto('/workers');

  // wait for the initial table to load before searching
  await expect(page.getByRole('table')).toBeVisible();

  const searchInput = page.getByTestId('search-input');
  await searchInput.fill('Maria');

  // wait for the search API response before asserting results
  await page.waitForResponse(resp =>
    resp.url().includes('/api/workers') &&
    resp.url().includes('search=Maria') &&
    resp.status() === 200
  );

  const rows = page.locator('table tbody tr');

  // assert the row count changed (not zero)
  await expect(rows).not.toHaveCount(0);

  // assert content — Playwright retries until the element is stable
  await expect(rows.first()).toContainText('Maria');
});
```

**Key fix:** `waitForResponse()` tied to the actual search request. `toContainText()` retries automatically until the assertion passes or times out — no `textContent()` null risk.

---

### Drill Schedule Before Friday

| Day | Task | Time |
|-----|------|------|
| Today | Write Scenario 1 fix from memory (no peeking) | 20 min |
| Tomorrow | Write Scenario 2 from scratch (login + 3 test cases) | 25 min |
| Wednesday | Write Scenario 3 refactor — start from the BEFORE code | 20 min |
| Thursday | Write Scenario 4 API mock + Scenario 5 fix | 30 min |
| Friday morning | Re-read the Quick-fire cheat sheet, then rest | 10 min |

**Rule for all drills:** Write in a real editor. Run `npx tsc --noEmit` to check types. Don't look at the answer until you're done.

---

## Rate Negotiation Script

When they ask about expectations:
> "I'm looking at $3,500–$4,000/month for a contract engagement of this scope. That reflects my Playwright+TypeScript experience and the fact that I can contribute from day one without a ramp period. Is there a budget range you're working within?"

If they push back on the upper end:
> "I understand. The lower end of my range is $3,500 — for a strong match like this I'm willing to start there and revisit after 90 days based on delivery."
