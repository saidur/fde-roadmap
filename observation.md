# Observation

Assignment: responsive landing page for an FDE (Forward Deployed Engineer) service, HTML and CSS.

Pages:

- Claude: `20261006/claude/index.html`
- Grok 4.7: `20261006/grok/index.html`

Both models received the same prompt, in separate runs, and were told not to read other files in the repo.

## 1. AI Models Used

Model 1: Claude Sonnet 5.5 (high)

A first attempt with Claude Opus 5 (thinking, high) failed before it wrote a file (`resource_exhausted`). The page below is from the Sonnet retry, not from Opus.

Model 2: Grok 4.7 (high, fast)

## 2. Prompt Used

The same prompt was given to both models:

> Create a responsive landing page for an FDE service using HTML and CSS.

FDE was defined for both as: an engineer embedded with a customer to deploy software, integrate systems, and solve operational problems on site.

Output constraints, also the same for both: one self-contained HTML file, CSS in a `<style>` tag, no external stylesheets, no image files, no frameworks. A small script was allowed only for a mobile menu.

## 3. Code Quality Observation

Both files are valid single-page sites. Desktop and a 390px-wide layout were checked in a browser. Navigation, FAQ disclosure, and the mobile menu were exercised on both.

| | Claude Sonnet 5.5 | Grok 4.7 |
| --- | --- | --- |
| File | 590 lines | 996 lines |
| Look | Standard blue SaaS page: hero, trust strip, six service cards, comparison, four steps, three tiers, industry chips, FAQ, contact form, four-column footer | Editorial page: cream and pine, serif headlines, role definition, four duties, method, three engagements, FAQ, email brief |
| Responsive | Stacks to one column. Mobile menu opens. A hidden menu checkbox is about 390px wide and starts 22px in from the left, so a 390px viewport scrolls sideways by about 22px | Stacks cleanly. No horizontal overflow at 390px. Menu opens and the icon switches to a close mark |
| Accessibility | Focus rings and reduced motion. No skip link. The visible menu control is `aria-hidden`; the real control is a checkbox with `opacity: 0` | Skip link, `aria-expanded` on the menu, Escape closes it, links close it, focus rings, reduced motion |
| Dead ends | Contact form uses `action="#"` and `method="post"`, so a submit does not reach a server. Footer “Privacy · Terms” are plain text. Four footer “Services” links all go to `#services` | Contact is a `mailto:hello@fieldline.example` link. No form to wire up |
| CSS | Familiar class names. One rule sets every process step’s top border to the brand color and overrides the earlier gray border, so that first declaration does nothing | Longer, sectioned CSS. The 900px breakpoint is written twice. A short script only updates the menu’s accessibility state |

Claude is easier to scan if you have seen a lot of marketing templates. Grok is longer, and the structure matches the sections on the page. Grok’s menu and landmarks are the more careful of the two.

## 4. AI Hallucination Observation

The prompt did not name a company, give an email, list customers, or describe a product CLI. Both models invented a company anyway.

Shared assumption: both named the company **Fieldline**. The pages are not copies of each other (layout, copy, and sections differ), so this looks like the same invented brand from the word “field,” not one model pasting the other’s file.

Claude invented more that a reader could mistake for fact:

- A terminal mock that runs `fieldline status --site main`, with lines such as “legacy ERP connector live” and “data sync across 3 systems.” There is no such command.
- A badge that calls the Embedded Team tier “Most common,” with no basis.
- Service claims written as fact: cloud, on-premise, and air-gapped deployment; least-privilege access; shipping fixes daily.
- An industry list under “Where we work” (manufacturing, healthcare, public sector, and others) with no customers behind it.
- Form copy: “We will only use your details to respond to this request.” The form does not send the details anywhere.
- “© 2026 Fieldline. All rights reserved.” and “Privacy · Terms,” which are not real pages.

Grok invented less, and marked the contact address as a placeholder:

- Company name Fieldline.
- Email `hello@fieldline.example`. The `.example` domain is reserved for examples, so it does not look like a live inbox.
- Engagement names (Site embed, Rollout, Resident) and a four-step method. These are framing, not statistics.
- No customer names, testimonials, prices, phone numbers, street addresses, or API URLs.
- The site log is a list of the work (“Embed with the team…”, “Deploy into the live environment”), not a fake command.

## 5. Final Decision

Grok 4.7 produced the better page.

- **Accuracy.** It stays inside the definition of a forward deployed engineer and does not invent a CLI, a “most common” plan, or a promise that a form will be answered. Claude’s page reads as a finished company site, including several claims that are not true.
- **Understanding of the requirement.** The prompt asked for an FDE service. Grok’s sections are deploy, integrate, solve, and hand back. Claude turned the same prompt into a general consultancy: six services, eight industries, and a lead form.
- **Code quality.** Both are responsive and usable. Grok has no sideways scroll at 390px, a working close state on the menu, and a skip link. Claude’s hidden checkbox causes a small horizontal scroll, and the visible menu button is hidden from assistive tech.
- **Maintainability.** Claude’s class names are conventional, but the next edit has to replace a form, a privacy line, and footer links that point at nothing. Grok’s file is longer, and the content can be edited without inventing a backend.

Claude Sonnet 5.5 is the better reference if the goal is a familiar, high-volume marketing layout. For this assignment, Grok 4.7 is the stronger result because more of what it shows is something a person could stand behind.
