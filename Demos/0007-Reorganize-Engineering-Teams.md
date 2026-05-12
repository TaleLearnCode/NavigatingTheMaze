# Reorganize Engineering Teams into Platform and Product Squads

- **Status:** Accepted
- **Date:** 2025-11-20
- **Work Item:** ORG-789-Team-Structure

## Context and Problem

Our engineering organization has grown from 12 to 45 engineers over the past 18 months. We currently operate as a single, monolithic engineering team where all engineers work on all parts of the system (infrastructure, platform services, and product features).

**Pain Points Identified:**
1. **Infrastructure work is constantly deprioritized** in favor of product features, leading to technical debt accumulation
2. **Context switching is high** — engineers shift between platform-level work (Kubernetes configuration, CI/CD pipelines) and product features (user-facing functionality)
3. **Ownership is unclear** — when platform issues arise (e.g., deployment failures), no specific team owns the resolution
4. **Onboarding is slow** — new engineers must learn the entire system (infrastructure + product) to be effective
5. **Product delivery velocity is inconsistent** — platform issues block feature development unpredictably

**Trigger:** Three production incidents in Q3 2025 were caused by infrastructure issues that had been identified but not addressed due to lack of dedicated ownership.

## Decision Drivers

- **Separation of concerns** — infrastructure/platform work requires different skills and focus than product development
- **Ownership clarity** — clear accountability for platform stability vs. product feature delivery
- **Scalability** — current structure doesn't scale beyond 50 engineers (already feeling pain at 45)
- **Specialization** — allowing engineers to develop deep expertise in platform OR product (not both)
- **Delivery predictability** — reducing context switching to improve velocity and reliability
- **Retention** — engineers frustrated by constant context switching and lack of ownership
- **Hiring** — ability to hire specialists (platform engineers, SREs) vs. generalists only

## Considered Options

1. **Platform Team + Product Squads** (recommended)
2. **Keep single team, assign rotating infrastructure "buddies"**
3. **Fully federated teams** (each squad owns their own infrastructure)
4. **Hire external DevOps consultancy** (outsource platform work)

## Decision Outcome

Chosen option: **"Platform Team + Product Squads"**, because it provides clear ownership for infrastructure/platform concerns while allowing product squads to focus on feature delivery. This structure scales to 100+ engineers, improves delivery predictability, and enables specialization.

The organization will reorganize into:
- **1 Platform Team** (8-10 engineers): Owns infrastructure, CI/CD, observability, shared services
- **3 Product Squads** (10-12 engineers each): Own product features, customer-facing functionality, vertical product domains

This structure will be implemented over 6 weeks with careful change management to minimize disruption.

#### Consequences

- **Good, because** platform work gets dedicated ownership and consistent prioritization (no longer competes with product features)
- **Good, because** product squads can focus on delivering customer value without context-switching to infrastructure firefighting
- **Good, because** onboarding new engineers is faster (join a squad with a clear domain, not the entire system)
- **Good, because** we can hire specialists (SREs, platform engineers, infrastructure experts) instead of only generalists
- **Good, because** accountability is clear (platform issues → Platform Team, feature bugs → Product Squad)
- **Good, because** this structure scales (can add more product squads as we grow to 100+ engineers)
- **Bad, because** creates coordination overhead between Platform Team and Product Squads (requires ADRs, RFCs, regular sync meetings)
- **Bad, because** may create silos if not managed carefully (platform engineers lose touch with product context, product engineers lose infrastructure skills)
- **Bad, because** requires culture change (some engineers prefer generalist roles and may resist specialization)
- **Bad, because** transition period (6 weeks) will temporarily reduce velocity as teams reorganize and adjust
- **Neutral, because** we'll need to establish new communication patterns (platform RFCs, squad representatives in architecture meetings)

#### Implementation

**Phase 1: Planning (Weeks 1-2)**
1. Identify engineers for Platform Team (mix of infrastructure-focused engineers + volunteers)
2. Define Product Squad domains:
   - Squad A: Customer Management & Onboarding
   - Squad B: Billing & Payments
   - Squad C: Analytics & Reporting
3. Create RACI matrix (Responsible, Accountable, Consulted, Informed) for platform vs. product decisions
4. Document communication protocols (how product squads request platform work, SLAs, escalation paths)

**Phase 2: Reorganization (Weeks 3-4)**
1. Announce team assignments and rationale (all-hands meeting)
2. Conduct 1-on-1s with every engineer (address concerns, explain role expectations)
3. Establish Platform Team charter and roadmap (Q1 2026: focus on CI/CD improvements, observability, cost optimization)
4. Establish Product Squad OKRs (aligned with company product strategy)
5. Set up team spaces (Slack channels, project boards, documentation wikis)

**Phase 3: Transition (Weeks 5-6)**
1. Platform Team begins operating independently (daily standups, sprint planning, platform backlog)
2. Product Squads begin sprint planning with new team composition
3. Establish weekly Platform-Product sync meeting (share roadmaps, coordinate dependencies)
4. Conduct retrospective after 2 weeks (identify issues, adjust processes)

**Phase 4: Continuous Improvement (Ongoing)**
1. Monthly cross-team knowledge sharing sessions (platform engineers teach product squads about infrastructure, vice versa)
2. Quarterly team rotations (product engineers can spend 1 sprint with Platform Team to maintain infrastructure skills)
3. Measure success metrics (see Confirmation section below)

#### Confirmation

Success will be measured by:
1. **Platform stability:** Reduction in production incidents caused by infrastructure issues (target: <2 per quarter)
2. **Product velocity:** Increase in feature throughput per squad (target: +20% by Q2 2026)
3. **Engineer satisfaction:** Quarterly engagement surveys show improved ownership clarity and reduced context switching (target: >80% positive)
4. **Onboarding time:** New engineers productive within 3 weeks (down from 6 weeks currently)
5. **Platform roadmap delivery:** Platform Team ships at least 80% of planned infrastructure improvements on time
6. **Coordination effectiveness:** Platform-Product collaboration rated positively in retrospectives (>75% of squads report effective collaboration)

**Review Cadence:**
- **1-month check-in:** Retrospective on transition, identify early issues
- **3-month review:** Assess metrics, adjust team boundaries if needed
- **6-month review:** Decide whether to create additional product squads as team grows

#### Stakeholders

- **Engineering Team** (all 45 engineers affected by reorganization)
- **Engineering Leadership** (VPs, Directors — accountable for decision and change management)
- **Product Management** (needs clear interface to product squads, understand prioritization changes)
- **CTO** (final decision authority, accountable for org structure)
- **Recruiting Team** (hiring strategy changes to focus on specialists)
- **HR/People Ops** (support change management, address employee concerns)

## Pros and Cons of the Options

### Platform Team + Product Squads (Chosen)

- **Good, because** clear ownership (platform stability vs. product delivery)
- **Good, because** enables specialization (platform engineers, product engineers)
- **Good, because** scales well (can add product squads as organization grows)
- **Good, because** improves delivery predictability (reduced context switching)
- **Good, because** enables hiring specialists (SREs, infrastructure experts)
- **Bad, because** creates coordination overhead (requires communication protocols, RFCs, ADRs)
- **Bad, because** risk of silos if not managed (requires intentional knowledge sharing)
- **Bad, because** transition period reduces velocity temporarily (6 weeks of adjustment)

### Rotating Infrastructure "Buddies" (Keep Single Team)

- **Good, because** no organizational disruption (everyone stays in one team)
- **Good, because** maintains generalist skillset across all engineers
- **Good, because** simpler communication (no cross-team coordination overhead)
- **Bad, because** doesn't solve root problem (infrastructure work still deprioritized in favor of features)
- **Bad, because** "buddy" role is seen as burden, not desirable assignment (low morale)
- **Bad, because** doesn't scale beyond 50 engineers (already experiencing pain at 45)
- **Decision:** Rejected because it addresses symptoms, not root cause

### Fully Federated Teams (Each Squad Owns Infrastructure)

- **Good, because** complete ownership (no dependencies on other teams)
- **Good, because** fast decision-making (no cross-team coordination needed)
- **Bad, because** duplicates infrastructure work across squads (inefficient, inconsistent)
- **Bad, because** requires every squad to have infrastructure expertise (hiring becomes harder)
- **Bad, because** leads to infrastructure fragmentation (Squad A uses Docker, Squad B uses Kubernetes, Squad C uses serverless → operational nightmare)
- **Bad, because** doesn't leverage economies of scale (shared platform, shared tooling)
- **Decision:** Rejected due to duplication and fragmentation risks

### Hire External DevOps Consultancy (Outsource Platform)

- **Good, because** immediate expertise (consultants bring platform experience)
- **Good, because** no internal reorganization needed
- **Bad, because** expensive (consultancy costs 2-3x FTE salaries long-term)
- **Bad, because** creates dependency on external vendor (knowledge doesn't stay in-house)
- **Bad, because** cultural mismatch (consultants don't understand product context, team dynamics)
- **Bad, because** doesn't solve long-term ownership problem (what happens when contract ends?)
- **Decision:** Rejected due to cost and lack of long-term ownership

## More Information

### Related Decisions
- **ADR-0015:** Adopt Kubernetes for container orchestration (Platform Team will own this)
- **ADR-0022:** Standardize CI/CD pipeline across all services (Platform Team responsibility)

### References
- [Team Topologies](https://teamtopologies.com/) — Framework for organizing teams (Platform, Stream-Aligned, Enabling, Complicated Subsystem)
- [Spotify Model](https://engineering.atspotify.com/2014/03/spotify-engineering-culture-part-1/) — Squad structure inspiration
- Internal analysis: "Engineering Velocity Report Q3 2025" (identified context switching as top productivity issue)

### Assumptions
- We will continue hiring (plan to grow to 60 engineers by end of 2026)
- Product roadmap requires 3 parallel streams of work (justifies 3 product squads)
- Engineers are willing to specialize (confirmed via anonymous survey: 70% prefer focus over generalist role)
- Leadership commits to protecting Platform Team prioritization (won't pull them into product work during crunch times)

### Non-Technical Decision Note
**This is a non-technical ADR** — documenting an organizational structure decision rather than a technology choice. We're using the ADR format because:
- High impact (affects all 45 engineers)
- Hard to reverse (reorganizing again would be disruptive)
- Multiple stakeholders with competing priorities
- Requires clear documentation of rationale for future reference

## Follow-On Information

- **Next Review Date:** 2026-05-20 (6 months post-implementation)
- **Success Metrics Dashboard:** [Internal Link — Engineering Metrics Dashboard]
- **Team Roster:** [Internal Link — Team Structure & Assignments]

## Record History

* **Proposed**: 2025-11-05 (RFC shared with engineering team for feedback)
* **Accepted**: 2025-11-20 (decision finalized after 2 weeks of discussion and feedback)
* **Implemented**: 2025-12-31 (Phase 3 complete, teams operating in new structure)
* **Last Reviewed**: N/A
* **Deprecated**: N/A
* **Superseded by**: N/A
* **Date Superseded**: N/A
* **Archived:** N/A
