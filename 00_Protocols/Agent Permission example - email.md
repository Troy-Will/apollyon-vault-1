Troy 🤝🔑🌟 — concise first: I produced a developer-ready spec **and** a 600-px modal mock (HTML/CSS/JS) for the **Email Send** permission flow, plus exact typed-consent text, token naming, audit format, UX flow, security notes, and an implementation checklist with estimates. Copy/paste any part into your Small Steps or hand to your devs.

---

# 1) One-line summary (copyable)

Require explicit, typed consent before any agent sends email from a user account; create a scoped, short-TTL token, log the event, show an undo affordance (60s), and store audit records for 90 days.

---

# 2) Exact typed-consent string (use as requirement)

`I ALLOW <Agent-Name> TO SEND THIS EMAIL FROM <Account-IDENTIFIER>`

Example filled: `I ALLOW Sentinel-A1 TO SEND THIS EMAIL FROM troy@work`

User must enter this exact phrase (case-insensitive but trimmed) to permit send for medium/high risk.

---

# 3) Token naming & TTL

- Token name format: `token_agent_<agentId>_<action>_<YYYYMMDDHHMMSS>`  
    Example: `token_agent_SentinelA1_email_send_20250818T192500`
    
- Default TTL: **30 minutes** for email_send tokens.
    
- On grant: token created server-side, stored hashed, returned only to agent service for use; token auto-revokes when TTL expires or when user hits Kill/Undo.
    

---

# 4) Minimal developer spec (JSON schema)

```json
{
  "agent_id": "string",
  "agent_name": "string",
  "action_type": "email_send",
  "target_recipients": ["string"],
  "subject_preview": "string",
  "body_preview": "string",
  "attachments": [
    {"filename":"string","size_bytes":1234,"sha256":"hex"}
  ],
  "scopes_requested": ["email.send"],
  "token_ttl_minutes": 30,
  "user_consent_method": "typed_consent_modal",
  "typed_consent_string": "I ALLOW Sentinel-A1 TO SEND THIS EMAIL FROM troy@work",
  "token_id": "string",
  "audit_id": "string",
  "revoked": false,
  "timestamp": "ISO8601"
}
```

---

# 5) Sample audit log entry (copy/paste)

```
AUDIT_ID: audit_20250818T192501_7f3b
EVENT: PERMISSION_GRANTED
AGENT_ID: Sentinel-A1
ACTION: EMAIL_SEND
TARGETS: ["alice@example.com"]
SUBJECT_PREVIEW: "Re: Q3 budget"
ATTACHMENTS: ["report-q3.pdf (243KB, sha256:...)"]
SCOPES: ["email.send:troy@work"]
TOKEN_ID: token_agent_SentinelA1_email_send_20250818T192500
USER: troy@work
CONSENT_METHOD: typed_consent_modal
TYPED_CONSENT: "I ALLOW Sentinel-A1 TO SEND THIS EMAIL FROM troy@work"
TS: 2025-08-18T19:25:01Z
REVOCABLE_UNTIL: 2025-08-18T19:26:01Z  (60s undo window)
RETAINED_UNTIL: 2025-11-16T19:25:01Z  (90 days)
```

---

# 6) UX Flow (steps)

1. Agent requests permission → server creates a pending permission object (no token yet).
    
2. Modal shown with full preview (subject, body, attachments, token TTL) and explicit checkboxes.
    
3. User must check relevant boxes and **type** the typed-consent string.
    
4. On `Allow selected`:
    
    - Server validates typed string → creates scoped token `token_agent_...` with TTL.
        
    - Server records audit entry (permission_granted).
        
    - Agent performs send using token.
        
    - UI shows persistent unobtrusive banner: “Email sent by [Agent] — [Undo 60s] [View audit]”.
        
5. If user clicks Undo within 60s:
    
    - Client calls `POST /api/agents/actions/undo` with `audit_id`.
        
    - Server attempts best-effort rollback: revoke token, mark message as retracted (if provider supports recall), and record `UNDO` event in audit.
        
    - If rollback impossible (external provider already delivered), show explanation and next remediation steps.
        
6. After TTL expiry, token auto-invalidated.
    

---

# 7) API endpoints (recommended)

- `POST /api/agents/permissions` — create pending permission (returns `permission_id`)
    
- `POST /api/agents/permissions/:id/grant` — validate typed consent → create token + audit entry → returns `token_id`, `audit_id`
    
- `POST /api/agents/actions/send_email` — agent uses token to call send (server proxies send; logs response)
    
- `POST /api/agents/actions/undo` — undo request with `audit_id` (best-effort rollback)
    
- `GET /api/agents/audit/:audit_id` — return audit entry (for UI view/export)
    
- `POST /api/agents/tokens/:token_id/revoke` — manual revoke (Kill-switch path)
    

---

# 8) Modal mock (600px) — HTML/CSS/JS (copy/paste)

Below is a standalone modal you can drop into a UI demo. It includes typed consent validation, preview, checkboxes, and a mock POST to `/api/agents/permissions/:id/grant`. (No external libs required.)

```html
<!-- Email Send Permission Modal (600px) -->
<style>
  .modal { width:600px; max-width:95%; background:#fff; border-radius:10px; padding:20px;
           box-shadow:0 10px 30px rgba(0,0,0,0.15); font-family:system-ui,Segoe UI,Roboto,Arial; }
  .modal h2 { margin:0 0 8px; font-size:18px; }
  .muted { color:#555; font-size:13px; }
  .preview { background:#f7f7f8; padding:12px; border-radius:6px; margin:12px 0; font-size:14px; white-space:pre-wrap; }
  .checkbox-row { display:flex; gap:8px; align-items:center; margin:8px 0; }
  .consent { margin-top:12px; }
  .btn { padding:8px 12px; border-radius:6px; border:0; cursor:pointer; }
  .btn-primary { background:#0b63d6; color:#fff; }
  .btn-ghost { background:#f2f4f7; color:#111; }
  .banner { margin-top:12px; padding:10px; background:#eef6ff; border-radius:6px; display:flex; justify-content:space-between; align-items:center; }
  .error { color:#b00020; font-size:13px; margin-top:8px; }
</style>

<div class="modal" role="dialog" aria-labelledby="perm-title" aria-modal="true">
  <h2 id="perm-title">Approve automated email send</h2>
  <div class="muted">Agent <strong id="agent-name">Sentinel-A1</strong> requests permission to send this email from <strong id="acct">troy@work</strong>.</div>

  <div class="preview" id="email-preview">
<strong>To:</strong> alice@example.com
<strong>Subject:</strong> Re: Q3 budget
<strong>Body:</strong>
Hi Alice,

Please find the attached Q3 report. Let me know if you have questions.

Best,
Troy
  </div>

  <div><strong>Attachments:</strong> report-q3.pdf (243KB)</div>

  <div class="checkbox-row">
    <input type="checkbox" id="cb-read" />
    <label for="cb-read">I allow <strong>Sentinel-A1</strong> to read my draft & attachments (scoped)</label>
  </div>
  <div class="checkbox-row">
    <input type="checkbox" id="cb-send" />
    <label for="cb-send">I allow <strong>Sentinel-A1</strong> to send this email on my behalf</label>
  </div>

  <div class="consent">
    <label for="typed">Typed consent (required):</label><br/>
    <input id="typed" style="width:100%; padding:8px; margin-top:6px; border-radius:6px; border:1px solid #ddd" placeholder="Type the consent phrase here"/>
    <div class="muted" style="margin-top:6px; font-size:12px;">
      Type exactly: <code id="consent-string">I ALLOW Sentinel-A1 TO SEND THIS EMAIL FROM troy@work</code>
    </div>
    <div class="error" id="err" aria-live="polite" style="display:none"></div>
  </div>

  <div style="display:flex; gap:8px; margin-top:14px;">
    <button class="btn btn-primary" id="allow">Allow selected</button>
    <button class="btn btn-ghost" id="save">Save to Small Steps</button>
    <button class="btn" id="cancel">Cancel</button>
  </div>

  <div id="post" style="display:none" class="banner">
    <div>Automated action completed by <strong>Sentinel-A1</strong>.</div>
    <div>
      <button id="undo" class="btn btn-ghost">Undo (60s)</button>
      <button id="view" class="btn" style="margin-left:8px">View audit</button>
    </div>
  </div>
</div>

<script>
  const consentTemplate = 'I ALLOW Sentinel-A1 TO SEND THIS EMAIL FROM troy@work';
  document.getElementById('consent-string').textContent = consentTemplate;
  const err = document.getElementById('err');

  document.getElementById('allow').addEventListener('click', async () => {
    err.style.display='none';
    const typed = document.getElementById('typed').value.trim().toUpperCase();
    if (typed !== consentTemplate) {
      err.style.display='block'; err.textContent = 'Typed consent does not match required phrase.';
      return;
    }
    if (!document.getElementById('cb-send').checked) {
      err.style.display='block'; err.textContent = 'You must allow the send capability to proceed.';
      return;
    }

    // Mock POST to grant permission → create token & audit entry
    const payload = {
      agent_id: 'Sentinel-A1',
      action_type: 'email_send',
      targets: ['alice@example.com'],
      subject_preview: 'Re: Q3 budget',
      scopes_requested: ['email.send:troy@work'],
      user: 'troy@work'
    };

    // Replace with real API call in production
    console.log('POST /api/agents/permissions/:grant', payload);
    // show post-action banner + undo
    document.getElementById('post').style.display = 'flex';
    // set undo timer (60s)
    window._undoTimeout = setTimeout(()=> {
      document.getElementById('undo').disabled = true;
      document.getElementById('undo').textContent = 'Undo expired';
    }, 60000);
    // store audit_id mock
    window._lastAudit = 'audit_20250818T192501_7f3b';
  });

  document.getElementById('undo').addEventListener('click', async () => {
    clearTimeout(window._undoTimeout);
    // Mock undo API call
    console.log('POST /api/agents/actions/undo', { audit_id: window._lastAudit });
    document.getElementById('post').style.display='none';
    alert('Undo requested — server will attempt rollback and revoke token.');
  });

  document.getElementById('save').addEventListener('click', ()=> {
    // Save to Small Steps (client should call server or local vault)
    console.log('Save to Small Steps: Email send request saved for later review.');
    alert('Saved to Small Steps.');
  });

  document.getElementById('cancel').addEventListener('click', ()=> { alert('Request cancelled.'); });
  document.getElementById('view').addEventListener('click', ()=> { alert('Open audit view: ' + window._lastAudit); });
</script>
```

---

# 9) Security & privacy notes (must-haves)

- **Always show exact message preview and attachments.** No blind sends.
    
- **Tokenize payment/credentials** (never send full card numbers).
    
- **Scan attachments for malware before sending.**
    
- **Store audits for 90+ days**; provide export & admin review.
    
- **CAPTCHA / 2FA** triggered flows must pause and require manual intervention (non-bypassable).
    
- **Least privilege:** tokens limited to `email.send:<account>`, no broader scopes.
    

---

# 10) Implementation checklist & time estimates

- UX: modal design + copy → **60–90m** (owner: UX).
    
- Frontend: integrate modal + typed consent validation + undo banner → **90–180m** (owner: frontend).
    
- Backend: permission endpoints, token issuance, audit logging → **4–8h** (owner: infra/security).
    
- Token store & revocation + kill-switch endpoint → **3–6h** (owner: security).
    
- Attachments malware scan & preview pipeline → **4–8h** (owner: infra/security).
    
- QA: test typed consent, undo edge cases, audit export → **2–4h** (owner: QA).
    

---

# 11) Next tiny action (one click for you)

If you want me to file this into **Small Steps** now, copy/paste this one-liner into your Small Steps template:

`Draft Email-send permission modal & dev spec | Context: Voice of Reason / Agent Safety | Next step: Implement modal HTML + backend endpoint | Est: 120m | Priority: High | Review-by: 2025-08-23`

Say “Save to Small Steps” and I’ll add it where you want (or I can paste it formatted for your Obsidian template).

---

Troy — you said you need to begin wrapping up. If you want I’ll (a) save the “next tiny action” to your Small Steps now, or (b) hold until you say “Psyche — resume.” Which do you prefer?