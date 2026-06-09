# Rapta AI Platform — Manual QA Test Plan
**Product:** Rapta AI Platform — AI Supercoach  
**Prepared by:** Fatima Alfred  
**Date:** June 2026  
**Role:** Manual QA Tester  

---

## 1. Objective
Verify that Rapta's AI Platform correctly guides factory 
workers through assembly steps, detects defects reliably, 
and behaves consistently across real world factory floor 
conditions before deployment to customer sites.

---

## 2. About Rapta
Rapta builds an on AI powered computer vision 
platform that guides factory workers through assembly 
processes in real time, catches quality defects as they 
happen, and provides supervisors with analytics to 
improve production workflows.

The platform runs on edge hardware with no internet 
connection, making thorough pre deployment testing 
critical since there is no remote fix once deployed 
at a customer site.

---

## 3. Platform Features In Scope

| Feature | Description |
|---|---|
| AssemblyAI | Verifies parts placed in correct position |
| OCR Verification | Reads and verifies labels and serial numbers |
| Torque Verification | Verifies bolts tightened correctly |
| Scan Region | Camera scans area detecting defects |
| QA Inspection | General quality inspection steps |
| QA Dwell | Camera pauses for detailed inspection |
| Video Instructions | Guides workers through assembly steps |
| Data Capture | Records serial numbers and assembly data |
| Serial Number Capture | Captures and verifies serial numbers |

---

## 4. Out of Scope
- Hardware installation and configuration
- AI model training process
- Network infrastructure setup
- Customer site deployment

## 5. Test Approach

Rapta's platform uses AI computer vision a non 
deterministic system that makes judgment calls rather 
than returning fixed outputs. Testing approach focuses 
on evaluating consistent and reliable behavior across 
real world conditions rather than checking exact 
expected outputs.

**Testing Types:**
- Functional Testing
- Negative Testing
- Boundary Testing
- Exploratory Testing
- Consistency Testing
- Regression Testing
- Compliance and Audit Trail Testing


## 6. Test Scenarios by Feature

---

### 6.1 AssemblyAI — Part Placement Verification

**Happy Path:**
- Part placed correctly in good lighting
- System shows DETECTED IN POSITION
- Step advances to next step

**Negative Testing:**
- Part missing — NOT DETECTED — step holds
- Wrong part placed — DETECTED NOT IN POSITION
- Step does not advance — operator alerted

**Boundary Testing:**
- Part placed at edge of tolerance area
- Tolerance too tight — false failures?
- Tolerance too loose — missed defects?

**Real World Conditions:**
- Poor lighting and shadows
- Different camera angles
- Worker's hand partially blocking part
- Similar looking parts near each other
- Part placed at different orientations

**Consistency Testing:**
- Same scenario run 10 times
- Results consistent every time?

---

### 6.2 OCR Verification — Label and Serial Number Reading

**Happy Path:**
- Correct label in good lighting
- OCR reads correctly and confirms part

**Negative Testing:**
- Wrong serial number — system flags mismatch
- Step does not advance

**Edge Cases:**
- Poor lighting and shadows on label
- Label partially obscured
- Similar looking characters — 0 vs O, 1 vs I
- Damaged or worn label
- Label slightly tilted or rotated

**Consistency Testing:**
- Same label read 10 times
- Consistent result every time?

---

### 6.3 Torque Verification — Bolt Tightening

**Happy Path:**
- Correct torque applied
- System confirms and step advances

**Negative Testing:**
- Insufficient torque applied
- System flags and step holds

**Edge Cases:**
- Torque applied to wrong bolt
- Tool not correctly positioned
- Multiple bolts — all must pass before step advances

---

### 6.4 Video Instructions — Worker Guidance

**Happy Path:**
- Video plays correctly at each step
- Worker can follow instructions clearly

**Edge Cases:**
- Video paused mid step — does system handle gracefully?
- Video skipped — does system allow or prevent?
- Different screen resolutions — video displays correctly?

---

### 6.5 Audit Trail and Compliance Testing

**Critical for DOD and regulated customers:**
- Every step recorded with timestamp
- Failed attempts recorded
- Corrections recorded
- Final pass recorded
- Complete traceable record of entire assembly
- Data saved locally — no internet required

---

### 6.6 Air Gapped Environment Testing

**Critical for on premises deployment:**
- All features work correctly without internet
- No error messages related to connectivity
- Data saved locally on edge device
- System recovers cleanly after restart
- No data corruption after power interruption

---

## 7. Entry Criteria
- Platform build stable and deployed in test environment
- Test hardware available in lab
- Camera correctly positioned and configured
- AssemblyAI steps configured with anchors and parts
- Test cases reviewed and ready

---

## 8. Exit Criteria
- All critical and high severity test cases passed
- No open release blockers
- Consistent behavior verified across multiple runs
- Audit trail recording verified
- Air gapped operation verified
- Regression suite passed after any model update
- Test results documented

---

## 9. Key Test Cases Summary

| ID | Feature | Scenario | Expected Result | Severity |
|---|---|---|---|---|
| TC_001 | AssemblyAI | Part correct — good lighting | DETECTED IN POSITION | Critical |
| TC_002 | AssemblyAI | Part missing | NOT DETECTED | Critical |
| TC_003 | AssemblyAI | Wrong part placed | DETECTED NOT IN POSITION | Critical |
| TC_004 | AssemblyAI | Part at tolerance boundary | Correct status | High |
| TC_005 | AssemblyAI | Part missing — poor lighting | NOT DETECTED | Critical |
| TC_006 | OCR | Correct label — good lighting | Label confirmed | Critical |
| TC_007 | OCR | Wrong serial number | Mismatch flagged | Critical |
| TC_008 | OCR | Label partially obscured | Flagged or alerted | High |
| TC_009 | Torque | Correct torque applied | Step advances | Critical |
| TC_010 | Torque | Insufficient torque | Step holds | Critical |
| TC_011 | Audit Trail | Complete assembly sequence | Full trail recorded | Critical |
| TC_012 | Air Gapped | No internet connection | All features work | Critical |
| TC_013 | Air Gapped | Power loss mid assembly | Clean recovery | High |

---

## 10. Risk Register

| Risk | Impact | Mitigation |
|---|---|---|
| Lighting variations on factory floor | High | Test across multiple lighting conditions |
| Hardware differences across customer sites | High | Test on multiple edge device configurations |
| AI model updates affecting existing detections | High | Full regression after every model update |
| Part variants not trained correctly | Medium | Test all known variants |
| Power interruptions on factory floor | High | Test system recovery scenarios |
| DOD compliance requirements | High | Verify audit trails and access controls |

---

## 11. Defect Severity Definitions

| Severity | Definition | Example |
|---|---|---|
| Critical | Directly affects product quality or safety | Missing part passes detection |
| High | Significant impact on functionality | False positive slows production |
| Medium | Moderate impact — workaround exists | Variant detection inconsistent |
| Low | Minor impact — cosmetic or edge case | UI label misaligned |

---

## 12. Tools
- Test Management: JIRA and Confluence
- Bug Tracking: JIRA
- Screen Recording: Visual bug artifacts
- Camera Setup: Factory floor test lab hardware
- Edge Device: On premises edge computer

---

## 13. Testing Environment
- On premises edge hardware
- No internet connection — air gapped
- Factory floor test lab with camera setup
- Multiple lighting conditions simulated

---

*This test plan was independently created by Fatima Alfred 
as part of a computer vision QA testing portfolio — 
demonstrating a manual QA approach to testing AI powered 
manufacturing software.*

*GitHub: github.com/FatimaQA-Eng*
