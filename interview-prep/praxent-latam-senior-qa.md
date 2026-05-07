# Interview Prep — Praxent — LATAM Senior QA Automation Engineer

**Report:** [#020](../reports/020-praxent-senior-qa-2026-04-28.md) | Score: 4.0/5 | Status: Interview  
**Current round:** Round 2 — Technical Interview (~60 min, Technical Director)  
**Next round:** Round 3 — Final Client Interview (fintech client)  
**Updated:** 2026-05-07

---

## 1. Company Intelligence

### What Praxent Does

Praxent is a **digital product agency specialized exclusively in fintech** — banking, lending, wealth management, and insurance. They build custom digital products for financial services companies that can't or won't build in-house.

- **Model:** Nearshore staff augmentation + product development for US fintech clients — identical to Gorilla Logic's model. Zero ramp time needed to understand this.
- **Size:** 120+ consultants. Austin, TX headquarters.
- **Clients:** Nymbus, Plinqit, Locality Bank, WealthBlock, Insurance Systems Inc., Fintegra
- **Services:** Product design, engineering (React/.NET, Angular/.NET, React/Node.js), QA

### Culture Signals

- **Best Places to Work in Fintech** (Built In), Clutch Top Company, Comparably Best Culture
- **Hard 40-hour week limit** — explicitly stated in JD. Not a "try to respect balance" clause — a firm policy
- **Remote-first since founding** — not forced remote
- **Learning budget** — courses, certifications, tech conferences
- **Hiring philosophy:** "hire good people who are great at their craft, give them fun problems to solve, and trust them"
- Interview experience rated 60% positive, 3.2/5 difficulty on Glassdoor — moderate process, not a grinder

### Fintech Domain

Understanding what Praxent's clients do helps you pass the Round 3 client interview. Their clients:
- Build **digital banking platforms** (Nymbus, Locality Bank)
- Build **lending and wealth products** (Plinqit, WealthBlock)
- Require **data integrity, compliance, and security** in every feature
- Are **mid-market fintech companies** that rely on Praxent for product and engineering muscle

**William's fintech proof point:** Leanware (banking SaaS, financial transaction validation, compliance protocols, PostgreSQL + Oracle, Jenkins shift-left). This maps directly to what Praxent's clients need.

---

## 2. Round 2 — Technical Interview (NOW)

### Format

- **~60 minutes with Technical Director**
- Expect one of:
  - **Live coding** — Playwright/TypeScript test written on-screen
  - **Take-home** — Playwright/TypeScript scenario sent before/after call
  - **Technical deep-dive** — walk through your past automation work in detail + scenario questions

### What the Technical Director Will Assess

1. Can you write Playwright code clean and fast?
2. Do you design frameworks, not just scripts?
3. Do you think about CI/CD integration from the start?
4. Can you communicate technical decisions clearly (you'll do this with their clients)?

---

## 3. Technical Prep — Playwright / TypeScript

### Core Playwright Patterns to Have Ready

**Fixtures (custom context setup):**
```typescript
// test.extend — share browser state across tests
const test = base.extend<{ authenticatedPage: Page }>({
  authenticatedPage: async ({ page }, use) => {
    await page.goto('/login');
    await page.fill('[data-testid="email"]', process.env.TEST_EMAIL!);
    await page.fill('[data-testid="password"]', process.env.TEST_PASSWORD!);
    await page.click('[data-testid="submit"]');
    await use(page);
  },
});
```

**Page Object Model:**
```typescript
class LoginPage {
  constructor(private page: Page) {}
  
  async login(email: string, password: string) {
    await this.page.fill('[data-testid="email"]', email);
    await this.page.fill('[data-testid="password"]', password);
    await this.page.click('[data-testid="submit"]');
    await this.page.waitForURL('/dashboard');
  }
}
```

**API test via Playwright:**
```typescript
test('POST /api/transactions creates record', async ({ request }) => {
  const response = await request.post('/api/transactions', {
    data: { amount: 500, currency: 'USD', accountId: 'acc_123' }
  });
  expect(response.status()).toBe(201);
  const body = await response.json();
  expect(body.id).toBeDefined();
});
```

**GitHub Actions integration:**
```yaml
- name: Run smoke tests
  run: npx playwright test --grep @smoke
- name: Run full regression
  if: github.ref == 'refs/heads/main'
  run: npx playwright test
```

### Questions They'll Likely Ask

**Framework design:**
- "How would you structure a Playwright test suite for a fintech web app from scratch?"
- "Walk me through your Page Object Model approach."
- "How do you handle test data management? Shared fixtures vs. isolated test data?"

**CI/CD:**
- "How do you integrate Playwright into a CI/CD pipeline?"
- "What's your strategy for smoke vs. regression? How do you gate PRs?"
- "How do you handle flaky tests?"

**Strategy:**
- "How do you decide what to automate vs. test manually?"
- "How do you prioritize test coverage in a new project?"
- "How do you communicate test results to non-technical stakeholders?"

**Fintech-specific:**
- "How do you test financial transaction flows where the UI and database must stay in sync?"
- "How do you approach testing in compliance-sensitive environments?"

---

## 4. Behavioral Questions — With Story Mappings

| Question | Story to Use | Key Detail to Lead With |
|----------|-------------|------------------------|
| "Tell me about yourself" | Thales → Leanware → Gorilla Logic arc | Framework from scratch → shift-left → AI-augmented |
| "Biggest technical achievement" | Thales -75% | Built from zero, POM, 75% reduction, Top 10 Employee |
| "How do you integrate QA into Agile?" | Leanware shift-left | Jenkins PR-blocking, sprint planning participation |
| "Example of catching a critical bug" | Acsendo SQL data layer | Bug not visible in UI, caught at data layer with SQL |
| "How do you handle cross-platform testing?" | IDEMIA mobile campaign | 15+ device/OS, zero UAT failures |
| "Tell me about mentoring or leading a QA team" | Thales team lead | Led validation team, defined methodology, trained 2 engineers |
| "How do you work with developers?" | Leanware shift-left | Framed testing as ally, not gate — "this catches your bugs before review" |
| "Why Praxent?" | See below | Nearshore fintech model matches current Gorilla Logic work; hard 40h limit; learning budget |

### "Why Praxent?" — Answer Framework

> "The model is identical to what I'm doing at Gorilla Logic — senior QA embedded in client product teams at US companies, from Colombia. What stands out to me about Praxent is the fintech specialization. My strongest work is in data-critical systems — banking transaction validation at Leanware, biometric data flows at IDEMIA. Those contexts demand the same rigor fintech clients need: data integrity, compliance, zero tolerance for transaction bugs. The 40-hour hard limit and the learning budget are things I look for — I want to stay sharp on tooling, not burn out."

---

## 5. Technical Red Flags to Pre-empt

These gaps from the JD are unlikely to come up in Round 2, but have a framing ready:

| Gap | Framing |
|-----|---------|
| **Appium** listed in JD but IDEMIA story covers it | "I've run mobile campaigns with Appium at IDEMIA — 15+ device/OS combinations for biometric apps" |
| **Java** listed alongside TypeScript | "My earlier automation was Selenium + Java (Thales, Acsendo). Current stack is Playwright + TypeScript at Gorilla Logic — I'm comfortable in both." |
| **Client-facing communication** | "At Thales I was the primary QA contact with government clients during FAT and UAT — delivered test results and sign-off documentation directly to stakeholders." |

---

## 6. Round 3 Preview — Client Interview

The third round is with Praxent's **fintech client** directly. This is the "cultural and technical fit with the actual team" stage.

### How to prepare:
- Ask at the end of Round 2: "What can you tell me about the client team I'd be working with? Any domain context that would help me prepare?"
- The client is likely in **banking, lending, or wealth management** based on Praxent's portfolio
- Frame your Leanware experience as direct sector overlap

### What the client assesses:
- Can this person communicate with our engineers and product managers?
- Do they understand our domain (financial services)?
- Do they ask smart questions?

### Questions to ask the client:
1. "What does the current test coverage look like — what's automated vs. manual today?"
2. "What's the biggest quality challenge your team is facing right now?"
3. "How does QA fit into your sprint cadence?"

---

## 7. Questions to Ask at Round 2

1. "Is there a specific project this role would slot into, or are you building a bench for upcoming client work?"
2. "What does the first 90 days look like for a senior QA joining a new client team?"
3. "What testing tools and CI/CD stack does the client team use today?"
4. "How does Praxent handle knowledge transfer between projects — do QAs move between clients?"
5. "What's the learning budget applied toward — do engineers use it for certifications, conferences, both?"

---

## 8. Salary Positioning

If comp comes up in Round 2:

> "I'm targeting $3,500–$4,500/month USD equivalent as a full-time employee. That's consistent with senior QA automation rates in LATAM for US-based product companies. I'm more interested in the right project than in squeezing the number, but that's my range."

**Do not go below $3,500/month.** The hard 40-hour limit is a signal this isn't a grind role — hold the floor.

---

## 9. Logistics

- **Comp target:** $3,500–$4,500/month USD
- **Employment type:** Full-time in Colombia (not contractor) — includes local benefits
- **Start:** Unclear — pipeline role. Ask directly in Round 2.
- **Work hours:** COT (UTC-5), confirmed overlap with US East and Central mornings
