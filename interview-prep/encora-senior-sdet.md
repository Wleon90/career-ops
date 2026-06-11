# Interview Prep — Encora | Senior SDET
**Report:** #037 | Score: 4.2/5 | Applied: 2026-05-17

---

## Company Context

- **Quiénes son:** Encora = global nearshore technology services (~10,000 engineers), antes llamada Nearsoft. LATAM-headquartered, clientes Fortune 500.
- **Modelo:** SDETs embedded en equipos de producto del cliente — exactamente como Gorilla Logic. Zero cultura shock.
- **Tech culture:** Engineering-first, CI/CD-native, clients expect senior engineers who own quality end-to-end.
- **Diferenciador clave para mencionar:** "Your model mirrors how I already work at Gorilla Logic — I don't need to learn the consulting cadence, I live it daily."

---

## Formato esperado del proceso

| Ronda | Tipo | Qué esperar |
|-------|------|-------------|
| 1 | HR Screening (30 min) | Fit, availability, salary expectation, English level |
| 2 | Technical Interview (60-90 min) | Live coding / Playwright, framework design, CI/CD discussion |
| 3 | Client Interview | Fit with specific client team, project context |

---

## Ronda 1 — HR Screening

**Preguntas típicas y respuestas:**

**"Tell me about yourself"** (60 segundos, en inglés)
> "I'm a Senior QA Engineer and SDET based in Bogotá, Colombia, with 11 years of experience. My current daily stack is Playwright and TypeScript at Gorilla Logic, where I build automated test suites for US-based enterprise SaaS clients — E2E, regression, API-layer testing, all integrated into GitHub Actions CI/CD. Before that, I built an automation framework from scratch at Thales Group that cut testing time by 75%. I'm ISTQB certified including the new GenAI v1.0 module, and I use AI tools like Claude Code and Cursor actively in my test workflow. I'm targeting roles like Encora's SDET position because the nearshore model and the engineering culture match exactly how I already work."

**"What's your salary expectation?"**
> "$4,000–$4,500/month USD as contractor, or equivalent as employee. I'm open to discussing structure."

**"Why are you leaving Gorilla Logic?"**
> "I'm not leaving under pressure — Gorilla Logic is a good company. I'm selectively exploring roles that offer stronger technical challenges or long-term client relationships. Encora came up because of the stack alignment and the caliber of client work."

**"When can you start?"**
> "I can start within two weeks of an offer."

**"English level?"**
> Respond entirely in English. Demonstrate, don't claim.

---

## Ronda 2 — Technical Interview

### Playwright / TypeScript — Preguntas probables

**"Walk me through how you structure a Playwright test suite."**
> "I use Page Object Model as the base — each page gets its own class with locators and actions, tests stay clean and readable. For fixtures I follow Playwright's native fixture pattern to handle auth state, shared test data, and teardown. I organize by feature, not by test type — so login/, checkout/, dashboard/ rather than e2e/, smoke/. CI/CD-wise: smoke suite on every PR (headless, fast), full regression on merge to main with parallelization across multiple workers. I also keep an API test layer using Playwright's `request` fixture — it's faster than UI for data setup and validation."

**"How do you handle flaky tests?"**
> "First I identify the pattern — is it a timing issue, a test data dependency, or environment instability? For timing: I avoid arbitrary waits and use Playwright's built-in auto-waiting with explicit `waitFor` conditions only when needed. For data: I isolate test state — each test creates and cleans up its own data, never shares state with other tests. For environment: I flag flaky tests with a retry=2 in CI and a Flaky label in the test suite, then track them in a dedicated backlog. I treat flaky tests as bugs — they erode trust in the suite faster than having fewer tests."

**"How do you integrate tests into a CI/CD pipeline?"**
> "At Gorilla Logic I set up GitHub Actions workflows: one workflow for PRs runs the smoke suite in under 3 minutes — it's a PR-blocking check. The main branch merge triggers the full regression suite with parallelization across 4 workers. Results publish to the PR as annotations. I also use Playwright's built-in reporter plus HTML report artifacts uploaded to Actions for debugging failures. The key principle: tests in CI should never be slower than the developer's patience — if CI takes 20 minutes, engineers start bypassing it."

**"What's your approach to API testing?"**
> "I use Playwright's `request` fixture for API-layer tests within the same suite — it keeps everything in one framework. For more complex API validation I use Postman scripted collections: pre-request scripts for auth tokens, test scripts for assertions, Newman for CI execution. At IDEMIA I validated 15+ REST endpoints in government identity pipelines this way — zero-tolerance data integrity. For E2E flows I combine UI and API: UI triggers the action, API validates the resulting state — faster and more reliable than checking everything through the UI."

**"Tell me about a time you built a framework from scratch."**
→ Use the **Thales STAR story** from the story bank:
> "At Thales Group I inherited a manual-only QA process for passport and ID issuance systems. I designed and built a Selenium + Groovy framework with Page Object Model from zero — no template, no existing code. I chose the stack based on what the team could maintain, not just what I knew. Trained two engineers on it. Result: 75% reduction in testing time. What took 4 weeks of manual regression ran in under a week. I was recognized as Top 10 Employee that year. If I were doing it today I'd add CI integration from day one — we ran it manually at first, which was the one thing I'd change."

**"Do you have experience with BDD / Cucumber?"**
> "I've worked extensively with the BDD mindset — defining acceptance criteria in Gherkin-style language in sprint planning, writing tests that map to user stories rather than implementation details. On tooling: I haven't used Cucumber directly, but the syntax is minimal — Given/When/Then maps closely to how I already write Playwright test descriptions. I can ramp on Cucumber in a day or two. The hard part of BDD is the collaboration process, not the tool."

**"What's your experience with Docker?"**
> "At IDEMIA I ran test campaigns against infrastructure on Oracle DB, Kubernetes, and Docker — validating biometric data pipelines. I know Docker well enough to run test environments locally, debug container networking issues, and work with Docker Compose for multi-service test setups. I don't have deep DevOps experience on the infra side, but I'm comfortable using Docker as a test execution and environment tool."

---

### Live Coding — Preparación

Si hay ejercicio en vivo, espera algo como:
- Escribir un test Playwright para un flujo de login o e-commerce
- Refactorizar un test frágil
- Diseñar la estructura de un test suite para una feature nueva

**Cheat sheet mental:**
```typescript
// Fixture para auth reutilizable
test.beforeEach(async ({ page }) => {
  await page.goto('/login');
  await page.fill('[data-testid="email"]', 'user@test.com');
  await page.fill('[data-testid="password"]', 'password');
  await page.click('[data-testid="submit"]');
  await expect(page).toHaveURL('/dashboard');
});

// API test dentro de Playwright
test('API returns correct user data', async ({ request }) => {
  const response = await request.get('/api/users/1');
  expect(response.status()).toBe(200);
  const data = await response.json();
  expect(data).toMatchObject({ id: 1, role: 'admin' });
});
```

---

## Ronda 3 — Client Interview

El cliente probablemente preguntará sobre:
- Cómo trabajas con developers y PMs (no solo QA técnico)
- Cómo manejas plazos ajustados sin bajar la calidad
- Cómo priorizas qué testear

**"How do you decide what to automate vs what to test manually?"**
> "Risk-based approach: I automate what's stable, high-frequency, and high-risk — regression paths, critical workflows, smoke checks. I keep manual for exploratory testing, new features before they stabilize, and edge cases that are expensive to automate for their frequency. The ratio shifts over time — as the product matures, more goes into automation. I also factor in maintenance cost: a flaky automated test is worse than no test."

**"How do you handle pushback from developers who don't want to slow down for QA?"**
> "I reframe it: my job is to make their job faster, not slower. When I add PR-blocking tests at Gorilla Logic, developers initially pushed back. After two sprints of catching regressions at PR stage instead of during UAT, they became advocates. I make the value visible: 'this caught 3 bugs this sprint before they reached code review.' Numbers convert skeptics faster than arguments."

---

## Preguntas a hacer (al final de cada ronda)

**Para HR:**
- "What's the typical client engagement duration for SDET roles at Encora?"
- "Is the Colombia-based role tied to a specific client, or is it a general pool placement?"
- "What does the onboarding look like for new SDETs?"

**Para Technical:**
- "What's the current state of the test automation at the client I'd be joining — are we building from scratch or extending an existing suite?"
- "What's the tech stack on the client side — same Playwright + TypeScript, or different?"
- "How do you measure QA success on client engagements at Encora?"

**Para Client:**
- "What's the biggest QA challenge the team is facing right now?"
- "How embedded is QA in the sprint process — do you do TDD, BDD, or traditional QA gates?"

---

## Salary Negotiation

- **Piso:** $3,500/month USD
- **Target:** $4,000–$4,500/month USD
- **Techo:** $5,000/month USD (push if they ask for a range)
- **Ancla:** "Based on my current compensation and market rates for senior SDET roles in LATAM nearshore, I'm targeting $4,000–$4,500/month USD."
- **Si presionan por el número exacto:** "$4,200 is the number I have in mind."
- **Si dicen "that's above budget":** "What's the budget range? I want to make sure we're in the same ballpark before going further."

---

## Red Flags a vigilar

- Si el cliente es de India o requiere horario Asia-Pacific → preguntar timezone requirement explícitamente
- Si mencionan "occasional on-site visits" → clarificar frecuencia y quién paga
- Si no responden sobre salario en la primera llamada → ok, pero es señal de que puede estar bajo

