
# DSA Lead Qualification Workflow

**Project status:** Prototype concept  
**Category:** AI Automation · Workflow Design

> This document describes a proposed workflow architecture. Live integrations, automated execution, and business results have not yet been verified.

## 1. Project Overview

The DSA Lead Qualification Workflow explores how AI-assisted automation could help organise incoming leads, suggest a priority category, and prepare relevant follow-up messages for human review.

The proposed workflow uses Google Sheets as a lead-data source, n8n to coordinate workflow steps, and an AI model to assist with classification.

The goal is to reduce repetitive administrative work while keeping people in control of communication decisions.

## 2. Problem Statement

When lead information is handled manually, it can be difficult to:

- Keep lead records organised.
- Identify which enquiries may need attention first.
- Maintain consistent follow-up processes.
- Prepare relevant messages efficiently.
- Track the status of each lead.

A structured workflow could help address these challenges, provided that the classification rules and integrations are properly implemented and tested.

## 3. Proposed Architecture

```text
Lead Source
    |
    v
Google Sheets
    |
    v
n8n Workflow
    |
    v
Input Validation
    |
    v
AI-Assisted Classification
    |
    +---- HOT
    +---- WARM
    +---- COLD
    |
    v
Prepare Follow-Up Draft
    |
    v
Human Review and Approval
    |
    v
Optional Messaging Integration
```

**Important:** This is a proposed architecture, not proof of a working deployment. WhatsApp or other messaging integrations are future possibilities and are not confirmed as connected.

## 4. Tools and Their Proposed Roles

| Tool | Proposed role |
|---|---|
| Google Sheets | Store and organise lead records |
| n8n | Coordinate workflow steps and data movement |
| AI model | Suggest a lead category and help draft a message |
| Human reviewer | Check classifications and approve messages |
| Messaging API | Potential future delivery of approved messages |

The final tool selection will depend on implementation requirements, access permissions, costs, and testing.

## 5. Example Lead Data

The following records are fictional examples created for documentation.

| Lead ID | Enquiry | Follow-up requested | Example category |
|---|---|---|---|
| DEMO-001 | Requests product details | Yes | HOT |
| DEMO-002 | General information enquiry | Yes | WARM |
| DEMO-003 | Says there is no current interest | No | COLD |

These classifications are illustrative only. Actual rules must be defined and evaluated against reviewed examples.

The workflow should not infer sensitive personal traits or make unsupported assumptions about a person.

## 6. Proposed Workflow Steps

### Step 1: Receive lead information

Read an authorised lead record from the approved source.

### Step 2: Validate the record

Check that required fields are present and correctly formatted. Flag incomplete records instead of silently processing them.

### Step 3: Suggest a category

Use documented business rules and, where appropriate, AI assistance to suggest HOT, WARM, or COLD.

The output should include a brief explanation and should be checked when uncertain.

### Step 4: Prepare a follow-up draft

Create a message appropriate to the enquiry and the person's communication preferences.

Do not send the message automatically in the prototype design.

### Step 5: Request human review

A person checks the category, supporting information, and draft message before approving any external communication.

### Step 6: Record the outcome

If implemented, record the review status and workflow outcome while avoiding unnecessary personal information in logs.

### Step 7: Consider future integration

Only after implementation and testing should an authorised messaging integration be considered. Appropriate consent and opt-out handling must be in place.

## 7. Human Review and Privacy

A responsible implementation should:

- Require human approval before messages are sent.
- Respect communication preferences and opt-outs.
- Contact people only when there is an appropriate basis and required consent.
- Collect only information needed for the workflow.
- Restrict access to lead records.
- Avoid including personal data in logs unnecessarily.
- Use fictional records for demonstrations.
- Store API credentials securely outside the source code.
- Provide a way to correct incorrect categories.

## 8. Error Handling and Duplicate Prevention

A future implementation should address the following cases:

- Missing or invalid fields.
- Duplicate lead records.
- Spreadsheet access failures.
- API rate limits and timeouts.
- Temporary service outages.
- Invalid or unexpected AI output.
- Low-confidence or ambiguous classifications.
- Repeated workflow execution.
- Failed message-draft creation.
- Attempts to process opted-out contacts.

Possible safeguards include stable lead identifiers, processing-status fields, bounded retries, clear error logs, and manual review of failed records.

These safeguards are recommendations and are not claimed to be implemented yet.

## 9. Testing Plan

Before the workflow is considered operational, test it with fictional records.

- [ ] Valid examples for all three categories.
- [ ] Missing required fields.
- [ ] Ambiguous enquiries.
- [ ] Invalid AI responses.
- [ ] Duplicate records.
- [ ] Spreadsheet access errors.
- [ ] API timeouts and retry behaviour.
- [ ] Opted-out contacts.
- [ ] Message drafts awaiting approval.
- [ ] Confirmation that no message is sent before approval.
- [ ] Confirmation that failures are visible and recoverable.

No test results or performance metrics are claimed in this document.

## 10. Current Limitations

- The workflow is documented as a prototype concept.
- A live n8n deployment has not been verified.
- Google Sheets and AI provider connections have not been verified.
- A WhatsApp or other messaging API integration has not been verified.
- Classification accuracy has not been measured.
- Time saved and business impact have not been measured.
- Error-handling and duplicate-prevention mechanisms remain implementation considerations unless separately demonstrated.

## 11. Future Development Roadmap

1. Define the lead fields and business classification rules.
2. Build the initial workflow in n8n using fictional data.
3. Add input validation and duplicate checks.
4. Test AI-assisted classification against reviewed examples.
5. Add a human approval step for follow-up drafts.
6. Implement error handling and workflow-status tracking.
7. Evaluate output quality and document actual test results.
8. Consider a messaging integration after permissions, consent, and safeguards are addressed.
9. Update the project status only when implementation evidence supports the change.

## 12. Conclusion

This project explores how AI-assisted classification and workflow automation could make lead handling more organised and consistent.

Its focus is on clear workflow design, responsible use of AI, human oversight, and a practical path from prototype concept to a testable implementation.
