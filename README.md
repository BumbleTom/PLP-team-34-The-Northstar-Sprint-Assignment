# PLP---Team-34---The-Northstar-Sprint---Assignment
 Power Learn Project Northstar Sprint  assignment, contains our Team Charter, project board, and collaborative chatbot prototype.  It also Includes commit/edit logs and audit trail to prove balanced contributions. The final deliverables is MVP demo, go‑live readiness note, and self assessments.

# Team-Charter
## 1. Purpose

 This Charter is the governing agreement for how this team will communicate, meet deadlines, resolve conflict, and hold one another accountable during the Northstar Sprint. All members agree to abide by these terms for the full duration of the engagement. This document, together   with the audit log and project board, constitutes the record of good-faith collaboration required for delivery.

## 2. Communication Norms

| Item              | Agreement                                                              |
|--------------------|-------------------------------------------------------------------------|
| Primary channel    | Use WhatsApp for daily updates and Google Meet for daily meetings.     |
| Response time      | All members respond to direct questions within 4 working hours        |
| Daily check-in     | Each member posts a status update by 8:00 PM EAT daily                 |
| Standing meetings  | Day 1 Charter workshop (90 min); daily 15-min standup; Day 4 checkpoint review |
| Blockers           | Any member stuck more than 2 hours posts to the channel immediately    |

## 3. Deadlines and Work Standards
•	All project board tasks represent no more than 4 hours of work; larger tasks are split before being added to the board.
•	Board status is updated the same day the work occurs. Batched or end-of-week updates are not permitted.
•	Every commit or edit follows the required convention: <type>: <what changed> - <why it matters>. Non-descriptive messages (e.g. "wip", "updates") are not acceptable.
•	A task is marked Done only when it fully satisfies its stated Definition of Done.
•	All deliverables are due by 11:59 PM EAT on the assigned day. Anticipated delays must be flagged in the team channel at least 3 hours before the deadline.

## 4. Conflict Resolution
This team resolves disagreements in the following order:
•	Step 1 — Direct conversation. Members involved discuss the disagreement directly within 24 hours of it arising.
•	Step 2 — Team discussion. If unresolved, the issue is raised at the next standup and settled by majority vote.
•	Step 3 — Escalation. If still unresolved, or if the delay threatens a deadline, the issue is raised to the course instructor/facilitator with a brief written summary of the disagreement and the resolution steps already attempted.
All discussion remains respectful and focused on the work product, not on individuals.

## 5. Escalation Path — Inactivity
Per the sprint's non-negotiable rules, zero visible activity (no commits, edits, or board movement) from any member for two or more consecutive days triggers immediate escalation.

# Project Board
The project board is the single source of truth for tracking work across the sprint. Every task carried out by the team is logged here, along with the member responsible for it and its current status — **To Do**, **In Progress**, or **Done**.
Status is updated in real time as work happens, so the board always reflects an accurate picture of who is doing what and how far along each task is. A task only moves to Done once it fully meets its stated Definition of Done, as agreed in the team's Working Charter.

Board link - https://github.com/users/BumbleTom/projects/2

## Defined Tasks and Definition of Done

| Task                                | Definition of Done                                                                 |
|-------------------------------------|-----------------------------------------------------------------------------------|
| Draft Team Charter Document         | Charter uploaded to repo as TEAM_CHARTER.md                                        |
| Set Up GitHub Repository            | Repo created, initialized with README, visible to team                            |
| Create Project Board (Kanban)       | Board created with To‑Do, In‑Progress, Done columns                               |
| Add 10+ Tasks to Board              | Tasks listed, each ≤4 hours, with owners assigned                                 |
| Configure Communication Channels    | WhatsApp group created, all members added                                         |
| Write Order Status Chatbot Flow     | Bot responds correctly to "Where is my order?" queries                            |
| Write Returns/Refunds Chatbot Flow  | Bot explains return steps and refund timeline                                     |
| Add Fallback Response to Chatbot    | Bot replies with escalation message when query not matched                        |
| Test Chatbot Flows                  | Each flow tested with sample queries, responses verified                          |
| Document Go‑Live Note               | One‑page summary of what works, what's incomplete, and next steps added to repo   |



# Collaborative Delivery

Tracks each member’s contribution with name, email, allocated tasks, and commit link.  
Captures the final sprint board state for transparency and traceability.  
Ensures balanced collaboration and provides audit evidence for client validation.

## Evidence for client validation

| Member Name                | Email                        | Tasks Owned                                                                                          | Priority            |
|-----------------------------|------------------------------|------------------------------------------------------------------------------------------------------|---------------------|
| Erick Odiwuor              | erickodiwuor014@gmail.com    | Add 10+ Tasks to Board · Configure Communication Channels · Document Go-Live Note                     | High / Medium / High |
| Belinda Awinja             | belindahtom@gmail.com        | Set Up GitHub Repository · Create Project Board (Kanban) · Test Chatbot Flows                         | High / Medium       |
| Asivhannzhi Muofhe         | vhannjee@icloud.com          | Write Order Status Chatbot Flow · Test Chatbot Flows                                                  | Medium              |
| Emmanuel Argut             | emmaargut@gmail.com          | Write Returns/Refunds Chatbot Flow · Add Fallback Response to Chatbot                                 | Medium              |
| Rodah Mwikali              | makalicaroh@gmail.com        | Draft Team Charter, Add Fallback Response                                                             | High                |

# Audit Log

This is the evidence trail that shows each team member’s contributions and links them to actual work in the project.
It captures the member identity, task, commit link, and timestamps

Audit Log link - https://github.com/BumbleTom/PLP-team-34-The-Northstar-Sprint-Assignment/commits/main/

## Chatbot Decision Tree flow Overview

This file documents the branching logic for the MVP chatbot.  
It covers **Order Status** and **Returns/Refunds**  questions, **Fallback Response** and **Chatbot Testing flow**

### 1. Order Status Decision Tree Flow

Everything that happens when a customer sends a message about their order status. It covers every decision point, every possible outcome, and the exact reply text the bot sends.

Order Status link - https://github.com/BumbleTom/PLP-team-34-The-Northstar-Sprint-Assignment/blob/main/AssignmentsFolder/order-status-flow.md

### 2. Returns & Refunds Decision Tree Flow

This is designed to guide the chatbot in handling customer queries about returning items or requesting refunds. It ensures the bot explains the return steps clearly and provides the refund timeline so customers get direct, automated answers without needing a human intervention.

Returns & Refunds link - https://github.com/BumbleTom/PLP-team-34-The-Northstar-Sprint-Assignment/blob/main/AssignmentsFolder/Return_refund_decision_tree_flow

### 3. Fallback Response

This is what the bot says when it doesn’t understand or can’t match a user’s query to any of the defined intents.

Fallback link - https://github.com/BumbleTom/PLP-team-34-The-Northstar-Sprint-Assignment/blob/main/Fallback%20Responce%20Decision%20Tree

### 4. Chatbot Testing Flow

This document explains how the chatbot will be tested before it's considered ready to demo or hand off. It focuses on the order status, returns and fallback response branches from the Chatbot Decision Flow.

Testing flow link - https://github.com/BumbleTom/PLP-team-34-The-Northstar-Sprint-Assignment/blob/main/AssignmentsFolder/chatbot-testing-flow%202.md

## GO-LIVE-Note

This is the final handover document for the project sprint. It captures what was delivered, what remains incomplete, and the next steps, giving the client a clear snapshot of the project’s readiness.

Note Link - https://github.com/BumbleTom/PLP-team-34-The-Northstar-Sprint-Assignment/blob/main/GO_LIVE_NOTE%20md

# Challenges Faced and Solutions rendered

## Challenges

1. Task dependency confusion - Two people working on the same task without a clear handoff point, which caused duplicated efforts and conflicting versions of the same deliverable.
2. Availability differences - Different schedules from the rest of the team which slowed down the chatbot testing phase.

## Solutions rendered
1. We resolved to using the GitHub project board itself as our tasks communication tool. Each task task card was moved visibly from to-do to in-progress to done so everyone could see what was ready for the next person.
2. We agreed on the 24-hourvresponse rule, whereby, any update, file or review request had to be acknowledged within 24-hours. We also used the WhatsApp group to send quick status updates.





