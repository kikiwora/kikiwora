# Roman Suvorov

**Senior iOS Engineer · Apple Platforms · Software Architecture · Performance · Product Engineering**

Engineering software that is simple, maintainable, and designed to last.

Senior iOS engineer with professional experience since 2019, working primarily with Swift and UIKit on production iPhone and iPad applications.\
My work is strongest where application architecture, state management, concurrency, performance, reliability, and interaction quality meet.

I am particularly interested in designing clear architectures and reusable engineering systems that make codebases easier to understand and evolve.\
Performance, reliability, and user experience should be considered from the beginning rather than added later.

## Current focus

- **Software Architecture** — explicit state, clear ownership, strong boundaries, reusable components, and maintainable application structure.
- **Product Engineering** — treating responsiveness, reliability, interaction quality, and implementation quality as parts of the same product problem.
- **Performance** — profiling startup, rendering, data preparation, scrolling, caching, memory use, and application resource footprint.
- **Concurrency** — Swift Concurrency, actor isolation, cancellation, task scheduling, stale-data handling, and interoperability with older asynchronous code.
- **Native UI Engineering** — complex UIKit interfaces, animated structural updates, reusable components, and interaction behaviour.
- **Developer-facing systems** — type-safe abstractions, diagnostics, logging, debug capabilities, code generation, and APIs that make application code safer and easier to use.

### Current technical foundation

`Swift` · `UIKit` · `Foundation` · `Swift Concurrency` · `Swift Package Manager` · `OSLog` · `Instruments` · `Swift Testing` · `git`

I am also expanding into **SwiftUI**, **TCA** (The Composable Architecture) and broader development across **Apple platforms**.

---

# Experience

## ONSEO · LiveScore

**Senior iOS Engineer** · 2023 – Present  
**Product:** LiveScore — native iPhone and iPad sports application, iOS 15+

LiveScore presents scheduled and live sports events, scores and incidents, competitions, favourites, tournament structures, odds, advertising, and other continuously changing data.\
My work has focused on application architecture, performance, concurrency, complex UIKit behaviour, reusable engineering systems, and product quality.

### Main Scores screen — architecture, scalability, and performance

Designed and implemented a major evolution of LiveScore's main Scores screen, one of the largest and most state-heavy areas of the application.\
Observed daily workloads reached up to **250 sections and 1000 matches**, with independently changing scores, incidents, odds, advertisements, preferences, pagination, and user interactions.

Key work included:

- Moved loading, refresh, preferences, and rendering orchestration toward a **Redux-style unidirectional architecture** with clearer state ownership and effect handling.
- Separated list structure, domain entities, freshness, preferences, and presentation state so they could evolve independently.
- Introduced **table-of-contents and on-demand section loading**, allowing recorded initial structured loads of only a small batch faster even when the full date approached **1,000 matches**.
- Addressed **cancellation, stale and out-of-order responses, incomplete batches, changing list structures, and repeated-request loops**.
- Preserved usable content during refresh, runtime configuration changes, and endpoint fallback instead of unnecessarily interface blanking.
- Implemented persistent competition (section) **favouriting, hiding, collapsing, and prioritization**, consistently across dates, filters, and fallback loading.
- Coordinated animated collapse, expansion, movement, favorited reveal, contextual menus, tooltips and other user interactions / data updates.
- Batched rapid preference changes without delaying immediate controls or visual feedback.
- Corrected reuse, sizing, layout, and scrolling behaviour to improve scrolling performance.
- Added **sequence-based behavioral tests**, feature flags, runtime configuration, local slicing and frequent updates simulation support, and automatic endpoint fallback for safer rollout and regression testing.

### Measured Scores-screen performance

Measured loading across five **uncached dates** on a weakest supported device, the **iPhone SE, 2nd generation**:

| Measurement | Before | After | Improvement |
|---|---:|---:|---:|
| Average initial page loading | 2.28 s | 0.89 s | **61% reduction** |
| Average response-model preparation | 1.31 s | 0.17 s | **87% reduction** |
| Busy date with ~700 matches | 3.90 s | 1.07 s | **73% reduction** |

The work included profiling and optimization of date processing, task scheduling, actor-boundary waiting, resources caching/preloading, and diagnostic overhead.\
Network waiting itself remained broadly unchanged.

### Application-wide performance and footprint

- Reduced **application startup time by approximately 70%** by deferring and restructuring work on the first (cold) and consequential launch paths.
- Reduced application binary size by approximately **15 MB** through static linking, asset cleanup/optimization, and more efficient resource handling.
- Reworked networking resource caching around modern asynchronous APIs and memory-first reuse, reducing unnecessary disk/network work and making cached content appear immediately.
- Investigated and fixed memory leaks, unnecessary layout work, expensive Core Data access patterns, and rendering bottlenecks.
- Used older supported hardware as a practical performance baseline rather than optimizing only for flagship devices to achieve stable 60FPS during scrolling and avoid overheat on complex data sets or active user navigation across the app.

### Concurrency and reliability

- Migrated substantial production code from legacy callbacks/GCD toward **Swift Structured Concurrency**.
- Introduced and worked with **Dynamic Actor Isolation** to expose invalid isolation assumptions and eliminate crashes caused by those violations.
- Investigated and removed deadlocks involving dispatch queues, lifecycle/deallocation timing, and asynchronous work.
- Conducted reverse engineering of legacy third-party libraries written on Objective-C to find the root cause of deadlocks and negative performance impact caused by undocumented private behavior, like Google Ads.
- Fixed a long-standing **KVO crash affecting approximately 5% of users** of a few millions.
- Hardened failure paths around networking, storage, stale state, and partial updates.
- Improved diagnostic quality through structured logging and more explicit ownership of asynchronous operations.

### Tournament Draws

Designed a reusable architecture for tournament draw/bracket presentation.

Challenges included:

- non-linear tournament structures;
- variable competition formats;
- dynamic sizing;
- navigation between related entities;
- reusable rendering across sports and tournament configurations;
- responsive performance on constrained devices.

The work emphasised separating tournament/domain structure from its visual representation so that the UI could remain reusable as competition formats changed.

### Live incidents and interaction quality

- Implemented live incident presentation for events such as **goals, red cards, and VAR states**.
- Coordinated polling-driven updates with cell identity and animation continuity.
- Used both custom animation and **Lottie** where appropriate.
- Reduced unnecessary table rebuilds and progressively moved from reuse workarounds toward explicit targeted updates.
- Added haptic feedback and contextual navigation where it improved interaction clarity.
- Built and unified contextual tooltip/popup flows instead of duplicating one-off presentation logic.

### Reusable engineering systems

Designed or evolved reusable systems used across the application:

- **Tagged domain identifiers** to prevent accidental interchange of semantically different types. String does not mean everything should be interchangeable. PlayerName is not the same as ImageID.
- **Command** abstractions for typed synchronous/asynchronous work, including main-actor and non-main-actor execution.
- Structured **OSLog / Logger** conventions.
- Debug and QA menu capabilities.
- Production-like **Fake Release** configuration for validation.
- Resource and localisation code generation.
- Build/development scripts and automation.
- Runtime diagnostics and performance instrumentation.
- Reusable contextual-menu and presentation components.

### Technical influence

- Regularly contributed through architecture and implementation reviews.
- Presented internal engineering topics and shared debugging/performance techniques.
- Influenced backend/API decisions where client requirements exposed structural issues.
- Contributed to behaviour/design alignment with Android.
- Built capabilities used by QA to make environment, state, configuration, and diagnostics easier to inspect.
- Helped move the codebase toward safer concurrency, clearer architecture, and more explicit engineering conventions.

### Git contribution metrics

Across the analysed LiveScore repositories (`LiveScore` and `LiveScore_IntrospectServer`):

- **2,007 retained commits**
- **529,159 added lines**
- **342,053 deleted lines**
- **871,212 cumulative changed-line events**
- **187,106 net added lines**

These are cumulative Git diff statistics across tracked text, not the number of unique lines currently present in the codebase or a productivity measure.

### LiveScore stack

`Swift` · `UIKit` · `Foundation` · `Swift Concurrency` · `SnapKit` · `Core Data` · `OSLog` · `Instruments` · `Swift Package Manager` · `Lottie` · `Git`

---

## Patron Empowerment · Rhythmic Rebellion

**Middle iOS Engineer** · before 2023  
**Product:** Rhythmic Rebellion — music platform for artists and fans

Rhythmic Rebellion combined music listening with artist/fan functionality such as releases, direct purchases, and merchandise. The ecosystem included iOS, Android, and web clients.

This project was where I developed much of my practical understanding of state-driven application architecture, normalised data, asynchronous rendering, complex native interactions, and cross-client state.

### Architecture and state management

- Worked extensively in a **Redux-style, unidirectional architecture** with actions, state, effects, and services.
- Built features around explicit state transitions rather than controller-owned implicit behaviour.
- Worked with requested vs. already-loaded identifiers to drive incremental data acquisition.
- Used **normalised domain state**, storing albums, tracks, artists, and related entities independently and assembling presentation from identifiers.
- Designed code around reusable entities and shared state rather than duplicating complete nested models per screen.
- Worked with typed domain identifiers and command-style abstractions that later influenced similar systems in subsequent projects.

### Complex native interactions

Implemented and maintained interaction-heavy product UI, including:

- long-press expanding cards/tiles;
- scroll-responsive presentation;
- dynamically changing action sheets;
- multiple sheet positions/detents;
- static vs. scrollable content depending on data size;
- transitions involving views expanding or transforming between presentation states;
- custom animations across several product areas.

### Rendering and performance

- Worked with **Texture / AsyncDisplayKit** for asynchronous layout/rendering.
- Used a declarative layout abstraction over Texture for dynamic UI composition.
- Optimised view hierarchy and layout behaviour.
- Used **Reveal** to inspect running interfaces, identify unnecessary view recreation, and simplify hierarchy/constraint/layout work.
- Improved reuse and reduced unnecessary rebuilding of interface elements.
- Developed a deeper understanding of view-backed vs. layer-backed rendering and the relationship between layout complexity and scrolling performance.

### Networking and synchronisation

- Used **GraphQL** for client data requirements and query specification.
- Worked with **WebSocket-based synchronisation** for state shared between clients.
- Supported scenarios where player state could remain synchronised between iOS and other clients.
- Worked with preloading and progressive presentation of remote content.
- Integrated native and web-based areas of the product where required.

### Engineering growth

This project substantially expanded my experience in:

- data-driven architecture;
- state normalisation;
- concurrency and asynchronous work;
- rendering performance;
- reusable components;
- complex native interaction design;
- cross-platform/client coordination.

### Git contribution metrics

Across the analysed Rhythmic Rebellion repositories (`RhytmicRebellion_Main`, `RhytmicRebellion_Components`, and `RhytmicRebellion_Artist`):

- **249 retained commits**
- **102,086 added lines**
- **54,222 deleted lines**
- **156,308 cumulative changed-line events**
- **47,864 net added lines**

These are cumulative Git diff statistics across tracked text, not the number of unique lines currently present in the codebase or a productivity measure.

### Rhythmic Rebellion stack

`Swift` · `UIKit` · `Texture / AsyncDisplayKit` · `Redux-style state management` · `GraphQL` · `WebSockets` · `GCD` · `Reveal` · `Git`

---

## EPAM Systems · Regeneron / VelociGene

**Junior iOS Engineer → Middle-level promotion near the end** · started 2019  
**Project:** internal iPad application supporting laboratory workflows

My first large professional iOS project was a native iPad application used in a specialised laboratory environment.

A key interaction constraint was that personnel could be wearing protective clothing and gloves, so workflows were designed around **tap-based interaction** rather than assuming gesture-heavy input.

### Modular application development

- Worked within a strongly modular **VIPER** architecture.
- Progressed from bug fixing to implementing complete screens and independently structured modules.
- Implemented business logic, presentation, and native layouts while respecting explicit responsibility boundaries.
- Built functionality intended to remain independently testable rather than concentrating logic in view controllers.

### Testing and automation support

- Worked in a project with a **>95% unit-test coverage requirement**.
- Wrote tests alongside assigned business logic and modules.
- Supported a dedicated automated-testing team using **Appium**.
- Added or maintained configuration and accessibility-facing hooks required for automation.
- Learned early to treat testability as an architectural constraint rather than an afterthought.

### Custom laboratory UI

Implemented a scalable, animated editor representing a laboratory configuration involving mouse paws/digits.

The feature included domain-specific validation such as:

- preventing invalid adjacent selections;
- enforcing a maximum of **three selected digits across two paws**;
- adapting to configurable dimensions;
- providing animated visual feedback.

### Correctness and operating constraints

- Fixed issues involving **time-zone changes and date/time formatting**.
- Built interfaces around the actual physical operating environment, including tap-only interaction requirements.
- Worked with native Apple frameworks and **no third-party application libraries** on the project.
- Collaborated with backend, QA, and other engineers in a larger delivery organisation.

### Git contribution metrics

Across the analysed EPAM / VelociGene repository:

- **246 retained commits**
- **28,596 added lines**
- **12,256 deleted lines**
- **40,852 cumulative changed-line events**
- **16,340 net added lines**

These are cumulative Git diff statistics across tracked text, not the number of unique lines currently present in the codebase or a productivity measure.

### VelociGene stack

`Swift` · `UIKit` · `Foundation` · `VIPER` · `Unit Testing` · `Appium integration/support` · `Git`

---

# Selected engineering themes

Across these projects, the recurring work has been less about individual frameworks and more about a few consistent engineering problems:

### Architecture and state ownership

From independently testable VIPER modules, through Redux-style state and normalised music-domain entities, to the LiveScore Scores-screen architecture, I tend to work toward explicit ownership, predictable data flow, and boundaries that make behaviour easier to reason about.

### Performance as a design constraint

I prefer profiling and measurement over intuition alone. This has included launch-time work, response preparation, layout/rendering, table updates, memory, caching, Core Data access, binary size, and network/resource behaviour.

### Concurrency and correctness

Asynchronous code becomes difficult when data can arrive late, out of order, or after the state it belongs to has changed. Much of my recent work has involved making those cases explicit: cancellation, stale results, actor isolation, queue interactions, incremental updates, and recovery.

### Product and interaction quality

Architecture is useful when it supports the product. I care about how live updates appear, whether animations preserve continuity, whether controls react immediately, whether content remains usable during refresh, and whether the implementation makes future changes safer.

### Reusable engineering systems

I prefer small abstractions that remove real classes of mistakes: typed identifiers, explicit commands, reusable presentation systems, logging conventions, diagnostics, and shared components. An abstraction should make the system easier to understand—not merely make it more abstract.

---

# Professional engineering activity

<details>
<summary>Selected Git-history statistics</summary>

A local read-only analysis of selected professional Git histories across LiveScore, Rhythmic Rebellion, and VelociGene recorded:

- **2,502 retained commits**
- **659,841 added + 408,531 deleted tracked-text line events**
- **1,068,372 cumulative tracked-text change events**
- **460,209 added + 246,509 deleted Swift line events**
- **706,718 cumulative Swift change events**

The analysis excluded identified formatter-author commits, selected SwiftFormat-title commits, and selected-author merge commits.

These figures describe historical change activity. They are **not** unique lines authored, code currently retained, or a productivity metric.

</details>

---

# Current interests

- Apple Platforms
- Interaction Design
- Performance Engineering
- Technical Leadership
- SwiftUI
- Independent product development

---

# Links

- [LinkedIn](https://www.linkedin.com/in/kikiwora/)
- [GitHub](https://github.com/kikiwora)
