# Interview Prep — Truelogic | Senior QA Engineer - E-commerce - Colombia
**Report:** #039 | Score: 3.8/5 | Applied: 2026-05-17

---

## Company Context

- **Quiénes son:** Truelogic Software LLC — nearshore consultancy LATAM fundada ~2018, especializada en equipos dedicados para clientes US. Conocida en el mercado QA de Colombia y LATAM.
- **Modelo:** Equipos dedicados embebidos en cliente. Similar a Gorilla Logic — el engineer trabaja directamente con el equipo del cliente, no en proyectos internos de Truelogic.
- **Cliente:** E-commerce (sector no confirmado — puede ser retail, marketplace, DTC). USD pay, 100% remote, Colombia-targeted.
- **Nota importante:** El JD completo no fue accesible vía Ashby. Si en la entrevista técnica aparecen requisitos no previstos, mantén calma — tu stack cubre el 90% de lo que cualquier empresa e-commerce necesita.

---

## Formato esperado del proceso

| Ronda | Tipo | Qué esperar |
|-------|------|-------------|
| 1 | HR / Recruiter Screening (30 min) | Fit, availability, salary, English level, Colombia confirmation |
| 2 | Technical Interview (60 min) | Test strategy, automation live demo o discusión, Playwright/Selenium |
| 3 | Client Interview | Fit con el equipo de e-commerce del cliente |

---

## Ronda 1 — HR Screening

**"Tell me about yourself"** (60 segundos)
> "I'm a Senior QA Engineer based in Bogotá, Colombia, with 11 years of experience across automation, API testing, and CI/CD integration. My current role is at Gorilla Logic — a nearshore consultancy like Truelogic — where I own QA for US enterprise SaaS clients using Playwright and TypeScript. Before that I built an automation framework from scratch at Thales Group that reduced testing time by 75%. I'm ISTQB certified, including the GenAI module, and I actively use AI tools in my daily test workflow. The Truelogic Colombia position caught my eye because the model matches how I already work, and e-commerce is a domain where strong automation coverage has a direct revenue impact."

**"Why Truelogic?"**
> "I'm targeting companies where QA is embedded in delivery, not bolted on afterward. Truelogic's dedicated team model — engineers working directly with US clients, remote from Colombia — is exactly the setup I'm used to at Gorilla Logic. The Colombia-specific posting was the deciding factor: no timezone friction, no location ambiguity."

**"What's your salary expectation?"**
> "$3,500–$4,500/month USD. Open on structure — contractor or full-time both work for me."

**"When can you start?"**
> "Within two weeks of an offer."

---

## Ronda 2 — Technical Interview

### Preguntas probables para un rol QA E-commerce

**"What's your approach to testing an e-commerce platform?"**
> "I'd break it down by risk and revenue impact. The highest-priority flows for automation are checkout (payment processing, cart calculations, discount application), user authentication, product search and filtering, and inventory sync. These directly impact revenue — a bug in checkout costs money every minute it's live. Secondary priority: account management, order tracking, email notifications. I'd also add API-layer tests for the integration points — payment gateway, inventory service, shipping API — because those tend to be where silent failures happen. For performance I'd identify the pages with highest traffic (homepage, product listing, checkout) and run load tests against realistic concurrency."

**"How do you handle test data management for e-commerce tests?"**
> "Test data isolation is critical in e-commerce because orders, users, and inventory have state that bleeds between tests. My approach: each test creates its own data via API (not UI) and cleans up after. For products and categories I use a dedicated test catalog that's seeded once and treated as read-only. For payment flows I use sandbox/test payment methods provided by the payment gateway — never hit real payment APIs in test. For user accounts I use a factory pattern that generates unique emails per test run."

**"Walk me through how you'd set up CI/CD for a QA suite from scratch."**
> "I'd start with GitHub Actions — it's what I use at Gorilla Logic and it's become the LATAM nearshore standard. Pipeline structure: on every PR, run a smoke suite (critical paths, under 3 minutes). On merge to main, run full regression in parallel across multiple workers. On release branch, run regression plus a performance smoke. I'd configure PR annotations so test failures show directly in the code review. Results go to a test management tool — TestRail if the client has it, otherwise I'd use Playwright's built-in HTML reporter with artifacts in Actions. The key metric to track: flaky test rate. I target under 2%."

**"Tell me about your API testing experience."**
> "At IDEMIA I scripted Postman collections to validate REST API data flows across 15+ integrated endpoints in government identity systems — strict data integrity requirements, zero tolerance for mismatches. I used pre-request scripts for auth token handling and test scripts for schema validation and field assertions. For E-commerce the same discipline applies but the endpoints are different: product catalog API, cart/checkout API, payment status API, inventory webhook validation. I also use Playwright's `request` fixture for API tests within the same automation suite — keeps the stack unified."

**"How do you prioritize when there's not enough time to test everything?"**
> "Risk-based testing: I map features to revenue impact and user frequency, then prioritize coverage accordingly. For e-commerce: checkout and payment always get full coverage regardless of timeline. Cosmetic issues in low-traffic pages can wait. I also communicate the risk explicitly — 'I covered these 5 flows fully, these 3 flows have smoke coverage only, and these 2 were not tested due to timeline — here's the risk.' That puts the release decision with product and business, not silently with QA."

**"What's your experience with Selenium?"**
> "I built a Selenium + Groovy framework from scratch at Thales Group and maintained Selenium test suites at Leanware for core banking workflows. I know Selenium well — WebDriverManager, explicit waits, Page Object Model, TestNG runner, Jenkins integration. My current primary tool is Playwright because it's faster, more reliable, and the DX is better — but if the client's existing suite is Selenium, I can work in it without friction. Migrating from Selenium to Playwright is also something I've done — it's worth evaluating if the suite has significant flakiness."

**"What testing tools have you used for test management?"**
> "TestRail is my primary — I used it at IDEMIA for government client test lifecycle management (test plans, test runs, traceability reports). Also JIRA for defect tracking and Confluence for test documentation. I've used Zephyr and QMetry as well. For automated test reporting I use Playwright's built-in HTML reporter, Allure for more detailed reports, and NewmanReporter for Postman/Newman runs in CI."

---

## Sobre el sector E-commerce (preparación)

No tienes background directo en e-commerce, pero puedes bridgearlo así:

**Si preguntan "¿tienes experiencia en e-commerce?":**
> "My background is in enterprise SaaS and government identity systems — different sector, same discipline. The core automation challenges in e-commerce — checkout flows, API integrations, data integrity, performance under load — are structurally identical to what I've solved in banking and biometric systems. The domain knowledge on cart mechanics and payment flows I can ramp on quickly; the automation engineering I bring from day one."

**Términos e-commerce a conocer:**
- Cart abandonment flow, checkout funnel, payment gateway (Stripe, PayU, MercadoPago)
- SKU management, inventory sync, out-of-stock handling
- Order lifecycle: placed → confirmed → shipped → delivered → returned
- CDN, page load performance (Core Web Vitals)
- A/B testing integration (feature flags)

---

## Ronda 3 — Client Interview

**"How do you ramp up on a new codebase and domain quickly?"**
> "I start with the happy path — I run through the product as a user before reading a line of code. That gives me the mental model of what matters to the end user. Then I look at existing tests (if any) to understand what the team has already decided is important. Then I map the critical paths to the codebase. Within the first week I try to get one meaningful test written and merged — not to prove myself, but because shipping something real is the fastest way to learn the toolchain."

**"How do you collaborate with developers who don't have QA experience?"**
> "I work alongside them, not after them. I join sprint planning to flag testability concerns before code is written. I do code reviews with a QA lens — 'this path has no error handling, how do we test it?' I make the automation visible — PR annotations, Slack notifications on test failures. When developers see their PRs blocked by a test I wrote, they start caring about testability from day one."

**"What does quality mean to you beyond test coverage?"**
> "Quality is confidence in the release, not a checklist. I care about: are the right things tested (coverage of critical paths), are the tests reliable (flaky rate under 2%), and is the feedback fast (CI under 5 minutes for smoke). High coverage numbers with slow, flaky tests don't give anyone confidence. I'd rather have 100 reliable tests than 1000 tests that fail 30% of the time for no reason."

---

## Preguntas a hacer

**Para HR:**
- "Can you tell me more about the e-commerce client — what kind of platform is it? B2C, B2B, marketplace?"
- "Is this role building a new QA suite from scratch or joining an existing team?"
- "What's the team composition — how many developers, any other QA engineers?"

**Para Technical:**
- "What's the current state of test automation on this project?"
- "What's the primary tech stack on the client side — what framework are they using?"
- "What's the biggest QA pain point the team is experiencing right now?"

**Para Client:**
- "What does a successful first 30 days look like for this role?"
- "How integrated is QA in the release process — do you do feature flags, canary releases, or straight deploys?"

---

## Salary Negotiation

- **Piso:** $3,000/month USD (no aceptar menos)
- **Target:** $3,500–$4,000/month USD
- **Techo:** $4,500/month USD
- **Ancla:** "Based on market rates for senior QA roles in LATAM nearshore consulting and my current compensation, I'm targeting $3,500–$4,000/month USD."
- **Si preguntan antes de hacer oferta:** "I'm in the $3,500–$4,500 range. What's the budget for this role?"

---

## Diferenciadores clave vs otros candidatos

1. **Contexto nearshore ya vivido** — trabajas en Gorilla Logic hoy, el modelo es idéntico. No es teoría.
2. **Stack actual = stack requerido** — Playwright/TypeScript, Selenium, Postman, GitHub Actions, todos en uso activo.
3. **Framework desde cero** — Thales -75% testing time es un proof point concreto y memorable.
4. **AI + ISTQB GenAI** — diferenciador real en 2026, pocos candidatos QA lo tienen certificado.
5. **Colombia-based** — eliminates timezone risk for the client completely.

