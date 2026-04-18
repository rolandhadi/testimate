# Testimate

**Industry-standard test automation effort estimator and timeline planner. One HTML file. No install. Zero backend. Export to styled Excel, import to edit.**

[![No dependencies](https://img.shields.io/badge/dependencies-zero_install-brightgreen)](https://github.com)
[![Single file](https://img.shields.io/badge/deploy-single_html_file-blue)](https://github.com)
[![License: MIT](https://img.shields.io/badge/license-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Made for QA](https://img.shields.io/badge/built_for-Test_Automation_Architects-9cf)](https://github.com)

Testimate is a free, browser-based **test automation effort estimation tool** built for **QA leads, Test Automation Architects, Delivery Managers, and consultants** who need a defensible, repeatable way to estimate automation projects without spreadsheets full of hidden assumptions.

It follows the methodology used by mature QA organizations worldwide: step-based complexity classification, fixed vs variable cost decomposition, industry-standard phase breakdown, PERT three-point estimation, and ISTQB-aligned task categories.

## Table of Contents

- [Why Testimate?](#why-testimate)
- [Features](#features)
- [Quick Start](#quick-start)
- [Screenshots](#screenshots)
- [How the Estimation Works](#how-the-estimation-works)
- [Industry-Standard Methodology](#industry-standard-methodology)
- [Complexity Classification](#complexity-classification)
- [Advanced Factors](#advanced-factors)
- [PERT Three-Point Estimation](#pert-three-point-estimation)
- [Task Categories (8 Standard Phases)](#task-categories-8-standard-phases)
- [Save and Load](#save-and-load)
- [Formulas Reference](#formulas-reference)
- [Example Scenarios](#example-scenarios)
- [Unit Tests](#unit-tests)
- [Roadmap](#roadmap)
- [Frequently Asked Questions](#frequently-asked-questions)
- [Contributing](#contributing)
- [License](#license)
- [About the Author](#about-the-author)

## Why Testimate?

Most **test automation effort estimation** is done in private spreadsheets with hidden formulas, inconsistent units, and no traceability. Estimates vary wildly from estimator to estimator, and consumers of those estimates have no way to stress-test the assumptions.

Testimate solves this by making the math explicit, the methodology industry-standard, and the output shareable. It supports any test automation framework or tool, including:

- **Web:** Selenium, Cypress, Playwright, TestCafe, WebdriverIO, Puppeteer, Nightwatch
- **Mobile:** Appium, Espresso, XCUITest, Detox, Maestro
- **Desktop/Cross-platform:** Eggplant Functional, Ranorex, UFT/QTP, TestComplete
- **BDD:** Cucumber, SpecFlow, Behave, Robot Framework
- **API:** REST Assured, Postman/Newman, Karate, SuperTest
- **Unit/Integration:** JUnit, TestNG, pytest, Jest, Mocha, xUnit
- **CI/CD:** Jenkins, GitHub Actions, GitLab CI, Bamboo, Azure DevOps, CircleCI

The estimation model is tool-agnostic. You input **step counts per test case** and pick complexity rates; the math produces man-days, timelines, and Gantt charts.

## Features

### Core Estimation Engine
- **Per-test-case input:** name, steps, complexity, rate override, notes
- **Auto-complexity classification** by step count (configurable thresholds)
- **Manual complexity override** per test case
- **Per-test-case rate override** for exceptional cases
- **Work breakdown structure** (WBS) with fully editable task categories and items
- **Fixed vs Variable** cost model with automatic proportional allocation
- **Clustering discount** for amortization when test cases share setup
- **Risk/buffer** contingency
- **Multi-resource planning** with linear calendar scaling

### Industry-Standard Advanced Factors
- **Test Data Preparation** uplift percentage
- **Platform / Device Matrix multiplier** (cross-browser, mobile fleets)
- **Learning Curve** uplift for new teams
- **Framework Setup Uplift** for first-time projects
- **Maintenance** percentage per year + horizon in months
- **PERT three-point estimation** (best, expected, worst)

### Timeline and Visualization
- **Interactive Gantt chart** with weekly MD allocation
- **Collapsible tree view** by category
- **Filter bar** to search test items or categories
- **Sticky header and columns** for wide timelines
- **Expand all / Collapse all** controls
- **Virtual rows** for Framework Uplift and Maintenance (when applicable)
- **Colored bars** per category matching the UI color palette

### Save, Load, Share
- **Styled Excel export** (XLSX) with matching colors, auto-filter, collapsible row groups, frozen panes
- **CSV export** for quick review
- **Excel import** for round-trip editing (same template format)
- 4 sheets on export: `Summary`, `TestCases`, `TaskItems`, `Timeline`

### Quality and Reliability
- **60+ built-in unit tests** (run via `Run Tests` button or `?test=1` URL parameter)
- **Pure calculation functions** that can be unit-tested in isolation
- **Round-trip test** verifying export-to-import preserves every field
- **No external backend** - all computation happens in your browser

## Quick Start

1. Download `Testimate.html`
2. Double-click to open in Chrome, Firefox, Safari, or Edge
3. Start estimating

No install, no npm, no build. It is one self-contained HTML file that loads **ExcelJS** and **SheetJS** via CDN (the only two runtime dependencies, both MIT-licensed).

### Host it on GitHub Pages

```bash
git clone https://github.com/your-username/testimate.git
cd testimate
# Enable GitHub Pages in repo settings, pointing to main branch root
# Testimate is now live at https://your-username.github.io/testimate/Testimate.html
```

## Screenshots

> Add screenshots to a `/docs/screenshots` folder and reference them here

- **Test Cases table** with complexity tags, rate overrides, and live MD calculation
- **Task Items work breakdown** with category colors and fixed/variable tags
- **Estimation Summary** with result cards and PERT three-point band
- **Interactive Gantt timeline** with collapsible category grouping
- **Styled Excel export** with matching colors and Excel-native outline groups

## How the Estimation Works

Testimate uses a **bottom-up, step-based parametric model**:

### Step 1: Score each test case

```
tc.variable_md = steps × rate_for_complexity(steps)
```

Where complexity rate defaults to:
- Simple (1-50 steps): 0.25 MD/step
- Medium (51-150 steps): 0.20 MD/step
- Complex (151+ steps): 0.15 MD/step

### Step 2: Apply multipliers and adjustments

```
variable_after_multipliers =
    sum(tc.variable_md)
  × platform_matrix_multiplier
  × (1 + learning_curve_pct/100)
  × (1 + test_data_pct/100)

variable_net =
    variable_after_multipliers
  × (1 - clustering_discount_pct/100)
  × (1 + risk_buffer_pct/100)
```

### Step 3: Add fixed and advanced items

```
fixed_total        = sum(task_items where type=fixed)
framework_uplift   = fixed_dev_env_baseline × framework_uplift_pct/100
maintenance_md     = (variable_net + fixed_total + framework_uplift)
                   × maintenance_pct_per_year/100
                   × maintenance_months/12

grand_total_md     = fixed_total + variable_net + framework_uplift + maintenance_md
```

### Step 4: Convert to calendar time

```
calendar_weeks   = grand_total_md / (5 × resources)
calendar_months  = grand_total_md / (20 × resources)
```

## Industry-Standard Methodology

Testimate aligns with the methodology used by the major international testing and project management standards bodies:

- **ISTQB Advanced Test Automation Engineer** - step-based effort estimation, framework-aware categorization
- **ISO/IEC/IEEE 29119-3** (Software Testing Standards) - test planning and documentation
- **TMMi** (Test Maturity Model integration) - structured phase breakdown
- **PMBOK Guide** - work breakdown structure, three-point estimation (PERT)
- **Nesma Test Point Analysis (TPA)** - complexity-based test sizing

The 8 standard phases built into Testimate reflect the consensus phase structure used by Thoughtworks, Capgemini, Accenture, and major enterprise QA consulting playbooks.

## Complexity Classification

| Complexity | Step Range | Typical MD/Step | Example |
|---|---|---|---|
| Simple | 1 to 50 | 0.25 | Login flow, search, basic form submission |
| Medium | 51 to 150 | 0.20 | Multi-step checkout, account management, report generation |
| Complex | 151+ | 0.15 | Full E2E transaction, data-driven flows, multi-role workflows |

**Why the rate is lower for Complex test cases:** longer test cases have more step-level reuse (common setup, shared teardown, repeated interaction patterns), so marginal per-step cost decreases. This is the **economy-of-scale effect** documented in multiple industry studies and matches empirical project data.

You can override the complexity per test case (for example, a 30-step test with unusually complex logic can be manually classified as Medium or Complex).

## Advanced Factors

Testimate exposes the industry-recognized adjustment factors that most estimators either ignore or fudge into a generic "buffer":

| Factor | Typical Range | When to Use |
|---|---|---|
| **Test Data Preparation** | 10-20% | When fixtures, anonymized production data, or combinatorial data sets are needed |
| **Platform Matrix Multiplier** | 1.3-1.5x (2 browsers), 1.5-2x (mobile multi-device) | Cross-browser, cross-OS, cross-device execution |
| **Learning Curve** | 15-30% | Team is new to the automation tool or the product |
| **Framework Setup Uplift** | 50-100% (on Dev Env) | First-time automation project for the product |
| **Maintenance % per Year** | 20-30% | Long-lived automation with ongoing selector updates and framework upgrades |
| **Maintenance Horizon** | 12-36 months | Duration over which maintenance effort is amortized |

## PERT Three-Point Estimation

When enabled, Testimate computes the **PERT (Program Evaluation and Review Technique) weighted average**:

```
E_pert = (Best + 4 × Expected + Worst) / 6
```

With default deltas of `Best = Expected - 15%` and `Worst = Expected + 25%`, the PERT expected value is approximately 1.017x the point estimate, giving you a risk-adjusted number suitable for external commitments.

This approach is standard in:
- PMBOK Guide (Seventh Edition, Section on Estimating Activity Durations)
- ISO/IEC/IEEE 29148 requirements practice
- Accenture and Deloitte test estimation playbooks

## Task Categories (8 Standard Phases)

The default work breakdown structure follows the consensus phase model used in enterprise QA:

1. **Preparation and Planning** (5-10%) - Requirements review, automation strategy, feasibility, risk assessment
2. **Environment and Framework Setup** (10-20%) - Framework architecture (Page Object Model, Keyword-Driven, Data-Driven, BDD), tooling, CI/CD pipeline, source control
3. **Test Design** (5-10%) - Test scenarios, test data design, boundary/equivalence partitioning
4. **Test Script Development** (30-50%) - Script automation, common libraries, object repository, test data preparation, unit testing of automation code, code review, debugging
5. **Test Execution** (10-20%) - Smoke, regression, cross-browser runs, results analysis, evidence capture
6. **Defect Management** (5-10%) - Defect triage and logging, script recalibration after fixes, regression re-execution
7. **Reporting and Sign-off** (5-10%) - Automation metrics, coverage report, stakeholder walkthrough, closure report, lessons learned
8. **Handover and Documentation** (3-5%) - Runbook, wiki, knowledge transfer, training materials

Every category and task item is editable. The defaults exist only to give you a reasonable starting point; you can rename, add, remove, or reorder anything.

## Save and Load

### Excel Export (Styled)

Saves a fully styled `.xlsx` file with four sheets:

| Sheet | Content |
|---|---|
| `Summary` | Project, rates, advanced factors, results with colored section headers |
| `TestCases` | All test cases with complexity tags, rate, MD, notes; auto-filter, frozen header |
| `TaskItems` | Work breakdown with category colors, fixed/variable type tags |
| `Timeline` | Gantt chart with Excel-native collapsible row groups by category |

The exported Excel matches the UI's color palette exactly and can be opened in Microsoft Excel, Google Sheets, or LibreOffice Calc.

### Excel Import (Round-Trip)

Load any Excel file previously saved by Testimate. All project settings, rates, advanced factors, test cases (with overrides), and task items are restored. Perfect for iterative estimation where you save a baseline, adjust inputs, and reload.

### CSV Export

Single-file CSV export for quick review, email, or ingestion into other tools.

## Formulas Reference

For transparency, all formulas used by Testimate:

| Metric | Formula |
|---|---|
| Test case MD | `steps × rate` |
| Variable gross | `sum of all test case MDs` |
| Variable after multipliers | `variable_gross × platform × (1 + learning/100) × (1 + testdata/100)` |
| Variable net | `variable_after_multipliers × (1 - clustering/100) × (1 + buffer/100)` |
| Item MD (variable) | `variable_net × item_proportion / sum_of_proportions` |
| Item MD (fixed) | `item.value` |
| Framework uplift | `fixed_dev_env_total × uplift_pct / 100` |
| Maintenance | `(variable_net + fixed + framework_uplift) × maint_pct/100 × months/12` |
| Grand total | `fixed + variable_net + framework_uplift + maintenance` |
| Weekly capacity | `5 × resources` |
| Calendar weeks | `grand_total / weekly_capacity` |
| Calendar months | `grand_total / (working_days_per_month × resources)` |
| PERT expected | `(best + 4 × expected + worst) / 6` |

## Example Scenarios

### Small: 5 Simple test cases, 1 resource
- Total steps: 150
- Variable gross: 37.5 MD
- Fixed total: 22 MD
- Grand total: 59.5 MD
- Duration: **3.0 months** (1 resource)

### Medium: 10 mixed test cases, 2 resources
- Total steps: 593 (6 Simple, 3 Medium, 1 Complex)
- Variable gross: 117.5 MD
- Fixed total: 22 MD
- Grand total: 139.5 MD
- Duration: **3.5 months** (2 resources)

### Large: 40 test cases with 20% clustering, 3 resources, 12-month maintenance at 25%
- Total steps: ~2,400
- Variable net: ~450 MD
- Fixed: 22 MD + framework uplift
- Maintenance: ~120 MD over 12 months
- Grand total: ~600 MD
- Duration: **~10 months** (3 resources)

## Unit Tests

Testimate ships with 60+ built-in unit tests covering:

- Complexity classification boundaries
- Rate resolution precedence (per-TC rate > complexity override > auto-classify)
- Variable gross, net, and multiplier composition
- Fixed totals and Dev Env baseline detection
- Item MD calculation for fixed and variable items
- Framework uplift and Maintenance formulas
- PERT best, expected, worst
- Gantt week allocation and overlap math
- Virtual row insertion (Framework Uplift, Maintenance)
- Category grouping and filtering
- Default state sanity
- Full Excel export-import round-trip

Run via the `Run Tests` button in the header or by opening `Testimate.html?test=1`.

## Roadmap

Planned enhancements (community contributions welcome):

- [ ] Save estimates to localStorage for persistence across sessions
- [ ] Share-by-URL (estimate state encoded in URL parameters)
- [ ] Automation ROI calculator (vs manual testing effort)
- [ ] Multi-team coordination overhead modeling
- [ ] Historical estimate tracking and learning curve fitting
- [ ] Dark mode

## Frequently Asked Questions

### Is Testimate free?
Yes. MIT-licensed, no ads, no tracking, no backend.

### Do I need to install anything?
No. It is a single HTML file. Open it in any modern browser.

### Does it work offline?
After the first load (which fetches ExcelJS and SheetJS from CDN), the core estimator works offline. If you need fully offline operation, inline the two CDN scripts into the HTML file.

### Can I customize the default test cases and task items?
Yes. Add, edit, remove, or reorder anything. Save the customized version as your team's baseline and share it.

### How accurate are the rates?
The default rates (0.25 / 0.20 / 0.15 MD/step) are calibrated from industry benchmarks and real project data, but every project is different. Treat them as a starting point, calibrate from your historical data, and adjust.

### What if my test framework doesn't use "steps"?
Any unit of work can serve as the "step" count. For API tests, each endpoint call is a step. For BDD, each Given/When/Then is a step. For keyword-driven frameworks, each keyword invocation is a step. Just be consistent within a project.

### Can I use this for non-automation QA estimation?
Yes, the model applies to manual testing too. Adjust the rates and categories to match manual testing work.

## Contributing

Issues, pull requests, and discussions are welcome. If you use Testimate on a real project, I would love to hear how it worked for you. Please consider sharing:

- Calibrated rates from your domain or tech stack
- Additional default task items worth including
- New advanced factors you find useful
- UI improvements

## License

MIT License. See `LICENSE` file.

## About the Author

**Roland Ross Hadi** - Test Automation Architect

I build automation frameworks and estimation models for enterprise software delivery. Testimate is a free tool I built to make test automation estimation more transparent, defensible, and teachable.

Connect with me:
- GitHub: [rolandhadi](https://github.com/rolandhadi)
- LinkedIn: [linkedin.com/in/rolandhadi](https://www.linkedin.com/in/rolandhadi/)

If Testimate saves you time or helps you win a pitch, a star on the repo is the best thank-you.

---

## Keywords for Discoverability

test automation, test automation estimation, QA effort estimation, test estimation tool, automation planning, software testing estimation, test case estimation, QA project planning, Selenium estimation, Cypress estimation, Playwright estimation, Eggplant Functional, Appium mobile testing, test automation framework, Page Object Model, Keyword-Driven, Data-Driven testing, BDD estimation, Cucumber effort, Robot Framework estimation, CI/CD test estimation, Jenkins test pipeline, GitHub Actions QA, test automation ROI, test maintenance cost, PERT estimation, three-point estimation, ISTQB Advanced, ISO IEC IEEE 29119, TMMi, test maturity, test automation architect, QA lead tools, test effort calculator, man days calculator testing, test automation Gantt chart, test automation timeline, test script development estimate, regression testing effort, cross-browser testing effort, mobile test automation estimation
