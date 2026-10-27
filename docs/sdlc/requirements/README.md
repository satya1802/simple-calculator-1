# Product Requirements

> Maintained by QuorQ AI SDLC. Text between `sdlc:auto` markers is regenerated; anything outside them is yours and is kept.

<!-- sdlc:auto:start narrative -->
## Summary

### REQ-TECHSTACK · approved · source: requirements:tech-stack

Product owner approved a fixed technology stack (FastAPI 0.115, AWS, PostgreSQL 16, React 19) to be used as-is, with no substitutions, despite the product needing almost no backend or database.

Decision: Backend = FastAPI 0.115, Cloud = AWS, Database = PostgreSQL 16, Frontend = React 19. Rationale given: calculation is entirely client-side with no accounts or stored data, so FastAPI is named only to satisfy the requirement for a server layer and to serve the static page (platform default, lightest fit); AWS is the platform default for cheap, reliable hosting of a free public single-page app at modest traffic; PostgreSQL is named only because a database choice is required even though nothing is persisted today, and is the default to adopt later if history/settings are added; React is chosen because the whole product is a responsive, instantly-updating single-page calculator with button and keyboard input, and is the platform default. Explicitly approved by the product owner; design must use exactly these, no substitutions.

**Related:** US-010, US-011, US-012, US-013

- ⚠ Database and backend are named for policy/platform-default reasons only, not functional need -- confirm with architecture phase that no incidental persistence or API surface gets introduced beyond serving the static page.

### REQ-SCOPE · draft · source: requirements:scope

Requirements version 4 defines a lightweight-delivery, free, anonymous, client-side-only calculator covering the four basic arithmetic operations, on-screen and keyboard input, decimal entry, sign toggle, clear/reset, error handling, and responsive desktop/mobile layout.

In scope: addition, subtraction, multiplication, division; on-screen button number entry; running result display; clear/reset; decimal point entry; sign toggle; division-by-zero error handling; keyboard input alongside on-screen buttons; responsive layout for desktop and mobile; anonymous use with no accounts/login; free use with no payments/billing. Out of scope -- explicitly excluded from design and build: scientific functions (powers, roots, trigonometry, logarithms, parentheses) and calculation history/memory keys. Delivery scope is marked 'lightweight'.

**Related:** US-001, US-002, US-003, US-005, US-006, US-007, US-008, US-009, US-010, US-011, US-012, US-013, US-014

- ⚠ No explicit approval status recorded for the scope document itself (only the technology stack is stated as approved by the product owner).

### EPIC-007 · draft · source: requirements:EPIC-007

Covers the core arithmetic engine: the four basic operations, chained multi-step calculations, decimal entry, and graceful handling of division-by-zero and invalid-input errors. All calculation is client-side; scientific functions and percent/memory are explicitly out of scope.

US-001 (critical): add, subtract, multiply, divide two numbers, verified by AC-001 (6*7=42), AC-050 (10-4=6), AC-051 (8/2=4), AC-052 (5+9=14). US-002 (high): continue calculating on a running result without re-entering it -- AC-053 (next operator applies to current result of 10), AC-054 (2+3 then *4 gives 20, i.e. running result 5 * 4). US-003 (high): decimal entry -- AC-055 (1.5+2.25=3.75), AC-056 (a second decimal point in the same number is ignored). US-005 (high): divide-by-zero / invalid-input error state -- AC-057 (dividing by zero shows a clear error message, app does not crash), AC-058 (clear/reset exits the error state back to ready-at-zero). Assumption stated at epic level: scientific functions (powers, roots, trig, logs, parentheses) and percent/memory keys are out of scope for this version.

**Related:** US-001, US-002, US-003, US-005

- ⚠ No requirement addresses numeric overflow or very long numbers (e.g. display width limits) beyond the divide-by-zero case -- only that one error condition is specified.
- ⚠ No acceptance criteria cover chained calculations combined with decimals or negative numbers together.

### EPIC-008 · draft · source: requirements:EPIC-008

Defines the calculator's interface: a live entry/result display, full on-screen button set, keyboard parity, clear/reset, sign toggle, and a responsive layout for desktop and mobile. Single-page web app, no history/memory keys per epic assumption.

US-006 (critical): display shows 0 on load (AC-005), updates live as digits are entered (AC-059), and shows the computed result on request (AC-060). US-007 (critical): full on-screen button input for digits, operators, decimal and commands (AC-061); buttons must exist for digits 0-9, add, subtract, multiply, divide, equals, decimal point, clear/reset and sign toggle (AC-062). US-008 (high): keyboard parity -- number keys and +,-,*,/ register like on-screen buttons (AC-007); Enter or = computes the result, Escape or Delete clears (AC-063). US-009 (high): clear/reset returns display to 0 and discards pending operation and error state (AC-064). US-014 (medium): sign toggle flips between positive/negative, e.g. 5 -> -5 and back (AC-065, AC-066). US-010 (high): responsive layout -- legible, mouse/keyboard-usable on desktop (AC-009); on mobile, buttons large enough to tap with no content cut off (AC-067). Epic assumption: single-page web app, no history/memory keys.

**Related:** US-006, US-007, US-008, US-009, US-010, US-014

- ⚠ No specific breakpoints, minimum tap-target size, or device matrix defined for the responsive layout (US-010) -- left to design phase.
- ⚠ No specification of keyboard behavior for the sign-toggle or decimal keys (only digit/operator/Enter/Escape/Delete keys are specified).

### EPIC-009 · draft · source: requirements:EPIC-009

Establishes that the calculator is free, anonymous, and fully client-side with no server-side storage of any calculation data or history, and no accounts or billing at any point.

US-011 (high): page is immediately usable on load with no sign-up, login or identity required (AC-068). US-012 (medium): no payment, subscription or billing is ever requested while using any feature (AC-011). US-013 (high): all computation occurs client-side with nothing sent to or stored on a backend (AC-069); closing or reloading the app retains no prior calculation or history, always starting fresh at 0 (AC-070). Epic assumptions: no login/accounts, free with no billing, client-side only with no backend database.

**Related:** US-011, US-012, US-013

- ⚠ No requirement states how the approved FastAPI/PostgreSQL layers (named for policy reasons only) will be kept entirely inert from a privacy standpoint -- worth confirming in architecture phase that no telemetry or logging inadvertently captures calculation data.

### REQ-NFR · draft · source: requirements:non-functional

Five non-functional requirements govern privacy, cross-device compatibility, performance, zero-friction usability, and stability under invalid input.

NFR-001 (privacy, applies to US-013): all calculation happens in-browser, nothing sent to or stored on a backend, calculator always starts fresh at 0. NFR-002 (compatibility, applies to US-010): layout adapts to screen size, legible and usable on desktop (mouse/keyboard) and mobile (tappable buttons, no cut-off content). NFR-003 (performance, applies to US-006, US-007, US-008): display updates immediately on every tap or keystroke. NFR-004 (usability, applies to US-011): calculator is ready to use immediately on load, no sign-up/login/identity needed. NFR-005 (availability, applies to US-005): invalid actions such as divide-by-zero show a clear error message rather than crashing, recoverable via clear/reset.

**Related:** US-005, US-006, US-007, US-008, US-010, US-011, US-013

- ⚠ NFR-005 only names divide-by-zero as the invalid-input example; no other invalid-input scenarios (e.g. malformed keyboard sequences) are enumerated.
- ⚠ No explicit performance budget (e.g. max latency in ms) given for 'instantly' in NFR-003 -- qualitative only.
<!-- sdlc:auto:end narrative -->

<!-- sdlc:auto:start summary -->
**Requirements version:** v4  
**Delivery scope:** lightweight  
**Approved:** 2026-10-27

**Capabilities in scope:** Addition, subtraction, multiplication and division, On-screen button number entry, Running result display, Clear / reset, Decimal point entry, Sign toggle (positive / negative), Division-by-zero error handling, Keyboard input alongside on-screen buttons, Responsive layout for desktop and mobile browsers, Anonymous use with no accounts or login, Free to use with no payments or billing

**Approved technology stack:**

| Layer | Choice | Rationale |
|---|---|---|
| backend | FastAPI | You were explicit that all calculation happens client-side with nothing stored and no accounts, so this product genuinely needs no backend logic. FastAPI is named only to satisfy the requirement to choose a server layer and to serve the static page; it is the platform default and the lightest sensible fit for a near-empty role here. |
| cloud | AWS | A free, public calculator needs reliable, inexpensive hosting that scales to anyone who visits without you managing machines. AWS is the platform default and comfortably serves a responsive single-page app to the general public worldwide, with low cost at the modest traffic a free utility page attracts. |
| database | PostgreSQL | You confirmed no data is stored and no history is persisted, so this product has nothing to put in a database. PostgreSQL is named only because a choice is required for this layer; it is the platform default and the one to adopt if you ever add saved history or settings later. |
| frontend | React | The whole product lives in the browser: a responsive single-page calculator with button and keyboard input, no accounts, no saved data. React handles exactly this kind of interactive single-page screen that updates instantly as someone taps digits, and it adapts cleanly to both desktop and mobile. It is also the platform default, so it is the lowest-friction path to the free, public page you described. |
<!-- sdlc:auto:end summary -->

<!-- sdlc:auto:start epics -->
## EPIC-007: Core Arithmetic Calculation

The calculator performs the four standard arithmetic operations (addition, subtraction, multiplication and division) on numbers entered by the user, supports decimal entry and chained multi-step calculations, and handles error conditions such as division by zero gracefully. Assumption: scientific functions (powers, roots, trigonometry, logarithms, parentheses) and percent/memory keys are out of scope for this version; all calculation is performed client-side.

### US-001: Perform addition, subtraction, multiplication and division

**Priority:** critical

> As a member of the general public using the calculator, I want to add, subtract, multiply and divide two numbers, so that I can carry out everyday arithmetic.

| ID | Given | When | Then |
|---|---|---|---|
| AC-001 | the number 6 has been entered | I select the multiply operator, enter 7 and request the result | the display shows 42 |
| AC-050 | the number 10 has been entered | I select the subtract operator, enter 4 and request the result | the display shows 6 |
| AC-051 | the number 8 has been entered | I select the divide operator, enter 2 and request the result | the display shows 4 |
| AC-052 | the number 5 has been entered | I select the add operator, enter 9 and request the result | the display shows 14 |

### US-002: Chained multi-step calculations

**Priority:** high

> As a member of the general public using the calculator, I want to continue calculating on a result without re-entering it, so that I can perform multi-step calculations and see a running result.

| ID | Given | When | Then |
|---|---|---|---|
| AC-053 | a calculation has produced the result 10 | I select an operator and enter another number without clearing | the next operation is applied to the current result of 10 |
| AC-054 | I enter 2 plus 3 then immediately select the multiply operator | I enter 4 and request the result | the running result of 5 is multiplied by 4 to show 20 |

### US-003: Decimal number entry

**Priority:** high

> As a member of the general public using the calculator, I want to enter numbers that include a decimal point, so that I can calculate with non-whole values.

| ID | Given | When | Then |
|---|---|---|---|
| AC-055 | the calculator is ready for input | I enter 1.5 add 2.25 and request the result | the display shows 3.75 |
| AC-056 | a number already contains a decimal point | I attempt to enter a second decimal point in the same number | the additional decimal point is ignored and the number remains valid |

### US-005: Divide-by-zero and invalid-input error state

**Priority:** high

> As a member of the general public using the calculator, I want clear feedback when a calculation cannot be completed, such as dividing by zero, so that I understand the result is invalid and can recover without the app breaking.

| ID | Given | When | Then |
|---|---|---|---|
| AC-057 | a number has been entered | I divide it by zero and request the result | the display shows a clear error message instead of a number and the app does not crash |
| AC-058 | the calculator is showing an error state | I use the clear/reset control | the error is cleared and the calculator returns to a ready state showing zero |

## EPIC-008: Calculator Interface and Input

The calculator presents a result display and accepts input via on-screen buttons and the keyboard, including a clear/reset control and a sign toggle. The layout is responsive so it is usable on desktop and mobile browsers. Assumption: the product is a single-page web application with no history/memory keys.

### US-006: Current entry and result display

**Priority:** critical

> As a member of the general public using the calculator, I want to see the number I am entering and the running result on a display, so that I can follow what I am calculating.

| ID | Given | When | Then |
|---|---|---|---|
| AC-005 | the calculator has loaded | I view it before entering anything | the display shows 0 |
| AC-059 | I am entering digits | I press number buttons or keys | the display updates to show the number as I build it |
| AC-060 | I complete a calculation | I request the result | the display shows the computed result |

### US-007: On-screen button input

**Priority:** critical

> As a member of the general public using the calculator, I want to enter digits, operators, decimal point and commands using on-screen buttons, so that I can operate the calculator entirely by tapping or clicking.

| ID | Given | When | Then |
|---|---|---|---|
| AC-061 | the calculator is displayed | I tap or click the digit and operator buttons | the corresponding digits and operators are registered and reflected on the display |
| AC-062 | the calculator provides on-screen controls | I inspect the layout | buttons exist for digits 0-9, add, subtract, multiply, divide, equals, decimal point, clear/reset and sign toggle |

### US-008: Keyboard number and operator input

**Priority:** high

> As a member of the general public using the calculator on a device with a keyboard, I want to enter numbers and operators using the keyboard, so that I can calculate faster without using the mouse or touchscreen.

| ID | Given | When | Then |
|---|---|---|---|
| AC-007 | the calculator is in focus | I press number keys and the +, -, *, / keys | the corresponding input is registered the same as the on-screen buttons |
| AC-063 | the calculator is in focus | I press Enter or = for equals and Escape or Delete for clear | the result is computed or the calculator is cleared accordingly |

### US-009: Clear and all-clear

**Priority:** high

> As a member of the general public using the calculator, I want to clear the current entry or reset the whole calculation, so that I can correct mistakes or start over.

| ID | Given | When | Then |
|---|---|---|---|
| AC-064 | a number or calculation is in progress | I use the clear/reset control | the display returns to 0 and any pending operation and error state are discarded |

### US-014: Sign toggle (positive / negative)

**Priority:** medium

> As a member of the general public using the calculator, I want to switch the sign of the number currently shown between positive and negative, so that I can work with negative numbers.

| ID | Given | When | Then |
|---|---|---|---|
| AC-065 | the display shows 5 | I use the sign toggle control | the display shows -5 |
| AC-066 | the display shows -5 | I use the sign toggle control again | the display shows 5 |

### US-010: Responsive desktop and mobile layout

**Priority:** high

> As a member of the general public using the calculator on different devices, I want the calculator layout to adapt to my screen size, so that it is usable on both desktop and mobile browsers.

| ID | Given | When | Then |
|---|---|---|---|
| AC-009 | the calculator is opened on a desktop browser | I view it | the display and buttons are laid out legibly and usable with mouse and keyboard |
| AC-067 | the calculator is opened on a mobile browser | I view it | the layout adapts so buttons are large enough to tap and no content is cut off |

## EPIC-009: Access, Privacy and Delivery

The calculator is freely available to anonymous users with no accounts, no payments and no server-side data storage. All computation happens in the browser and no calculation data or history is persisted. Assumptions: no login or accounts; free with no billing; client-side only with no backend database.

### US-011: Anonymous use with no login

**Priority:** high

> As a member of the general public, I want to use the calculator without creating an account or logging in, so that I can start calculating immediately with no barriers.

| ID | Given | When | Then |
|---|---|---|---|
| AC-068 | I navigate to the calculator | the page loads | it is immediately usable with no sign-up, login or user identity required |

### US-012: Free to use with no payments

**Priority:** medium

> As a member of the general public, I want to use the calculator entirely free of charge, so that I am never asked to pay or enter billing details.

| ID | Given | When | Then |
|---|---|---|---|
| AC-011 | I use any feature of the calculator | I perform calculations | no payment, subscription or billing is requested at any point |

### US-013: Client-side operation with no stored data

**Priority:** high

> As a member of the general public concerned about privacy, I want all calculation to happen in my browser with nothing stored or persisted, so that no calculation data or history is retained after I leave.

| ID | Given | When | Then |
|---|---|---|---|
| AC-069 | I perform calculations | the operations are computed | all computation occurs client-side with no data sent to or stored on a backend |
| AC-070 | I close or reload the calculator | I return to it | no previous calculation or history is retained and the calculator starts fresh at 0 |
<!-- sdlc:auto:end epics -->
