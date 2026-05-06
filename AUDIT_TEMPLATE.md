# Bainbridge Warning Diagnostic — Audit Template

**Purpose:** Identify governance gaps in AI deployments before they cause cascade failures.

**Time Required:** 2-3 hours
**Participants:** Technical lead, Product owner, Risk/compliance (if applicable)

---

## PHASE 1: CAPABILITY PROFILE

*What can your AI system do autonomously?*

### 1.1 Decision Autonomy
- [ ] List all decisions the AI makes WITHOUT human approval:
  1. 
  2. 
  3. 

### 1.2 Action Scope
- [ ] What actions can the AI execute directly? (e.g., send emails, modify databases, trigger payments)
  
### 1.3 Learning Capability
- [ ] Does the system learn from new data in production? [ ] Yes [ ] No
- [ ] If yes, what guardrails prevent drift?

### 1.4 Failure Impact Assessment
For each autonomous capability above, rate maximum impact:
- Financial: $_______
- Reputational: [ ] Low [ ] Medium [ ] High [ ] Catastrophic
- Regulatory: [ ] None [ ] Minor [ ] Major [ ] Existential

---

## PHASE 2: GOVERNANCE PROFILE

*What oversight mechanisms exist?*

### 2.1 Human-in-the-Loop
- [ ] Percentage of decisions reviewed by humans: _____%
- [ ] Average time between AI decision and human review: _____
- [ ] Who has authority to override? (List roles)

### 2.2 Monitoring & Alerts
- [ ] What metrics are tracked? (e.g., accuracy, drift, latency)
  
- [ ] What triggers an alert?
  
- [ ] Who receives alerts?

### 2.3 Documentation & Audit Trail
- [ ] Can you reconstruct WHY the AI made a specific decision? [ ] Yes [ ] No
- [ ] How long are decision logs retained? _____
- [ ] Are logs immutable? [ ] Yes [ ] No

### 2.4 Testing & Validation
- [ ] Frequency of model validation: [ ] Daily [ ] Weekly [ ] Monthly [ ] Quarterly [ ] Never
- [ ] Do you test for edge cases? [ ] Yes [ ] No
- [ ] Last penetration test date: _____

---

## PHASE 3: GAP ANALYSIS

*Calculate your Bainbridge Zone*

### 3.1 Capability-Governance Gap

For each autonomous capability from Phase 1:

| Capability | Autonomy Level (1-10) | Governance Strength (1-10) | Gap Score |
|------------|----------------------|---------------------------|-----------|
| Example: Auto-approve loans | 8 | 3 | 5 |
| | | | |
| | | | |

**Gap Score = Autonomy Level - Governance Strength**
- Gap ≥ 5: CRITICAL (R3 - High cascade risk)
- Gap 3-4: HIGH (R2 - Moderate risk)  
- Gap 1-2: MEDIUM (R1 - Low risk)
- Gap ≤ 0: LOW (R0 - Reversible)

### 3.2 R0-R3 Classification

**R0 (Reversible):** All gaps ≤ 0
- Decisions can be undone
- Human oversight is real-time
- No catastrophic failure modes

**R1 (Low Risk):** All gaps ≤ 2
- Minor failures contained
- Review happens within 24h
- Financial impact < $10K

**R2 (Moderate Risk):** Any gap = 3-4
- Failures could cascade
- Review delayed > 24h
- Financial impact $10K-$100K

**R3 (High Risk):** Any gap ≥ 5
- Cascade failure likely
- No meaningful human oversight
- Financial impact > $100K or existential

**Your Classification:** R___

---

## PHASE 4: CASCADE RISK ASSESSMENT

*Calculate Amplified Exposure Level (AEL)*

### 4.1 Probability of Failure (P)
Rate 0.0 - 1.0 based on:
- System complexity: [ ] Simple [ ] Moderate [ ] Complex
- Deployment maturity: [ ] New [ ] Tested [ ] Production-hardened
- Historical incidents: [ ] None [ ] Minor [ ] Major

**P = _____** (0.1 = low, 0.5 = moderate, 0.9 = high)

### 4.2 Consequence Magnitude (C)
If failure occurs, rate financial impact:
- Direct costs: $_______
- Regulatory fines: $_______
- Reputation loss: $_______
- Customer churn: $_______

**Total C = $_______**

### 4.3 Amplification Factor (A)
How fast does failure cascade?
- [ ] Contained to single system (A = 1)
- [ ] Spreads to 2-3 systems (A = 3)
- [ ] Enterprise-wide (A = 10)
- [ ] Ecosystem-wide (A = 30)

**A = _____**

### 4.4 Velocity (V)
Time from first failure to full cascade:
- [ ] > 1 week (V = 0.1)
- [ ] 1-7 days (V = 0.3)
- [ ] 1-24 hours (V = 0.7)
- [ ] < 1 hour (V = 1.0)

**V = _____**

### 4.5 AEL Calculation

**AEL = P × C × A × V**

AEL = _____ × $_____ × _____ × _____ = **$_____**

---

## PHASE 5: REMEDIATION ROADMAP

*Close the gaps*

### 5.1 Immediate Actions (This Week)
For each R3 classification:
1. 
2. 
3. 

### 5.2 Short-Term Actions (This Month)
For each R2 classification:
1. 
2. 
3. 

### 5.3 Medium-Term Actions (This Quarter)
For systemic gaps:
1. 
2. 
3. 

---

## NEXT STEPS

1. **Share results** with technical leadership
2. **Prioritize** R3 gaps for immediate remediation
3. **Schedule** re-assessment in 90 days
4. **Integrate** into deployment checklist

---

**Framework Reference:** [Bainbridge Warning](https://github.com/hillarynjuguna/bainbridge-warning)  
**Methodology:** Oscillatory Fields Intelligence Architecture  
**License:** MIT — Free for commercial and research use
