# Task 2: Patient Care & Communication System

## Step 1: Message Type Classification (One-Time Setup)
All outgoing patient messages are first classified to determine whether **doctor input is required** or not.

### Message Classification Table

| Message Type              | Example                         | Doctor Input Needed |
|--------------------------|----------------------------------|---------------------|
| Follow-up reminder       | “Please visit on Aug 5”          | No                  |
| Post-procedure care      | “Mild swelling is normal”        | No                  |
| Side-effect advisory     | “Nausea may occur”               | No                  |
| Custom instruction       | “Avoid sun exposure for 7 days”  | Yes                 |
| Patient question response| “Is itching normal?”             | Yes                 |

This classification is done once and reused consistently to avoid unnecessary doctor interruptions.

---

## Step 2: Care Control Sheet (Daily Working Sheet)
A single Google Sheet named **`Care_Control`** tracks all patient communication.

### Care_Control Sheet Structure

| Patient  | Phone | Visit Type | Message Type | Message Text | Doctor Approval | Status  |
|--------|-------|-----------|-------------|--------------|----------------|---------|
| Ramesh K | 9XXXX | OPD       | Follow-up   | Auto-filled  | Not required   | Pending |
| Sita P   | 9XXXX | Procedure | Post-procedure | Auto-filled | Not required   | Pending |
| Arjun M  | 9XXXX | OPD       | Custom      | Blank        | Required       | Waiting |

This sheet acts as the **single source of truth** for all patient communication.

---

## Step 3: Doctor Review Window (Every 3–4 Hours)
I filter the Care_Control sheet to show only entries where:

- **Doctor Approval = Required**
- **Status = Waiting**

I then block a short **10-minute review window** with the doctor.

During this time:
- The doctor dictates or approves responses
- I update the approved message directly in the sheet
- The doctor does **not** open WhatsApp or reply individually

This keeps doctor involvement focused and time-bound.

---

## Step 4: Handling Patient Questions Without WhatsApp Interruptions
Instead of allowing patients to message the doctor directly on WhatsApp, all **non-urgent patient questions** are routed through a simple **Google Form**.

### Form Captures:
- Patient name
- Phone number
- Question
- Urgency level

Form responses automatically populate a sheet called **`Patient_Questions`**, allowing:
- Questions to be reviewed in batches
- Full context during doctor review windows
- Reduced interruptions throughout the day

**Urgent cases** are flagged separately and handled immediately by clinic staff.

---

## Step 5: Controlled Message Dispatch Process
Messages are sent **only when**:
- Message content is finalized
- Status is marked as **Pending**
- Doctor approval is either **not required** or **already given**

Once sent:
- Status is updated to **Sent**
- Later marked as **Closed**

This ensures:
- Clear ownership
- Approval traceability
- No missed or duplicate messages

---

## Step 6: End-of-Day Closure Check
At the end of the clinic day, I filter the Care_Control sheet to find any entries still marked as **Pending**.

This final check ensures:
- No follow-ups are missed
- No patient questions are accidentally carried forward to the next day

---

## Step 7: Automation (Optional)
If required, **Google Apps Script** can be used to:
- Read pending rows
- Send messages via a WhatsApp API
- Update message status automatically

Automation **supports** the process but does **not replace human judgment**.

---

## Key Outcome
This system:
- Reduces doctor interruptions
- Improves response consistency
- Creates a clear audit trail
- Ensures every patient message is tracked, approved, and closed
