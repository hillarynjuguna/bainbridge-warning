# The Bainbridge Warning: Diagnostic Framework

## Four-Stage Diagnostic Process

### Stage 1: Capability Profile

Map the current AI agent deployment landscape. For each deployed agent or pipeline:

- What actions can it take?
- Which of those actions interact with external systems, data stores, or counterparties?
- What is the semantic domain (the business meaning of what the agent does)?
- What is the deployment velocity (how quickly are new agents and capabilities being added)?

The Capability Profile is not a judgment. It is a measurement. The goal is an accurate inventory of what the AI systems in your organization can do right now.

### Stage 2: Governance Profile

Map the current governance infrastructure against the four primitives.

**Bounded Verifiability Latency:** Has every agent action been classified by reversibility (R0 through R3)? For R3 actions, does a pre-execution validation mechanism exist? For R2 actions, are synchronous validation thresholds defined? Is there a reversibility registry, and when was it last updated?

**Explicit Compositional Contracts:** Do agents in pipelines carry behavioral specifications? Are composition violations detectable between pipeline stages? Is there drift detection on agent output distributions?

**Continuous Deterministic Layer Regression:** Are the policy and context layers version-controlled? Do Tier A deterministic checks run on every policy modification? Do Tier B regression tests run on a defined schedule? Are Tier C invariants monitored in production? Is Tier D semantic drift monitoring active?

**Dual Ownership:** Is semantic authority (Context Steward) defined and staffed? Is execution governance (CRE) defined and staffed? Does the CRE have emergency halt authority? Is there an escalation architecture for disputes? When did the Governance Council last meet?

### Stage 3: Gap Analysis

The gap between the Capability Profile and the Governance Profile is the Bainbridge Zone. The size of the gap is measured along each of the four primitive dimensions.

**Scoring (per primitive):**

- **Level 0: Absent.** The primitive does not exist. No classification, no contracts, no regression testing, no defined ownership.
- **Level 1: Partial.** Some elements of the primitive exist but coverage is incomplete. Common state: R3 classification exists for some pipelines but not all. Policy version control exists but regression tests do not.
- **Level 2: Operational.** The primitive is deployed across all active agent pipelines. Coverage is maintained as new deployments are added. Metrics are measured and reviewed.
- **Level 3: Mature.** The primitive is integrated into development and deployment workflows. It operates as production-critical infrastructure with SLAs, monitoring, and continuous improvement.

Most organizations beginning this assessment score Level 0 or Level 1 across all four primitives. This is not a condemnation. It is the starting position from which the remediation plan is built.

### Stage 4: Predictability Assessment

For each gap identified in Stage 3, assess the predictable failure mode:

- What class of incident becomes possible when this primitive is absent?
- What is the cascade amplification potential (how far can an error propagate before detection)?
- What is the reversibility of the most consequential unvalidated action?
- What is the time horizon before the gap is likely to produce an incident (based on deployment velocity and action volume)?

The Predictability Assessment converts the abstract gap measurement into a concrete risk surface. The output is a prioritized remediation sequence: which primitive to build first, based on which gap produces the most consequential predictable failure.

## The R0-R3 Reversibility Classification

### R0: Fully Reversible
Read-only operations. Advisory outputs. Log entries. Analysis that informs but does not execute. Zero cost to reverse because nothing has changed in the world.

**Validation requirement:** Advisory. Can be asynchronous, post-hoc, or absent without governance risk.

**Examples:** Querying a database without writing. Generating a summary for human review. Producing a classification that requires human approval before action.

### R1: Reversible With Overhead
Actions that produce state changes that can be reversed, but reversal requires deliberate effort and carries bounded cost.

**Validation requirement:** Asynchronous. Validation must complete within the reversal window.

**Examples:** Creating a draft document before publication. Updating an internal record with version history. Scheduling a communication not yet delivered.

### R2: Reversible With Significant Overhead
Actions that can technically be reversed, but reversal carries substantial cost: financial, reputational, operational, or regulatory.

**Validation requirement:** Synchronous for high-stakes instances, asynchronous for lower-stakes. Thresholds defined in advance as governance artifacts.

**Examples:** Sending external communication to a large audience. Committing a contract modification requiring counterparty acknowledgment to reverse. Changing a live system configuration.

### R3: Effectively Irreversible
Actions that cannot practically be reversed, or that trigger downstream effects before reversal is possible.

**Validation requirement:** Mandatory pre-execution. The pipeline blocks on validation. The action cannot execute without a validation response. This is an architectural constraint, not a monitoring constraint.

**Examples:** Executing a financial transaction above a defined threshold. Sending a regulatory filing. Triggering irreversible data deletion. Executing a binding commitment.

### The Asymmetry Principle
The cost of a spurious halt (validating an R3 action and blocking it unnecessarily) is bounded: a delay, a missed opportunity, a review process. The cost of an unvalidated R3 failure is not bounded in the same way. This asymmetry is the core justification for mandatory pre-execution validation of R3 actions.

## The Annual Expected Loss Formula

For each unvalidated R3 action class:

```
AEL = P(failure) x C(direct) x A(cascade) x V(annual volume)
```

Where:
- **P(failure)** = probability of a governance-relevant failure per action
- **C(direct)** = direct cost of a single failure
- **A(cascade)** = cascade amplification factor (typically 3x to 15x)
- **V(annual volume)** = number of R3 actions of this class per year

The AEL calculation makes the cost of the governance gap concrete. It converts "we should probably build governance infrastructure" into "the expected annual cost of not building it is [number]."

## Minimum Viable Entry Point

Start with R3 classification. Identify every action in your current agent deployments that has irreversible external consequences. Name it R3. Build the pre-execution validation mechanism for it.

The classification exercise will surface the governance gaps that are most urgent. The act of naming them creates the organizational pressure to address them.

Everything else in this framework follows from that starting point.
