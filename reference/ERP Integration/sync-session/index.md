---
title: Sync Session
excerpt: >-
  Manage GL entity sync sessions during onboarding. Start a session before
  pushing GL entities, then complete it when all entities have been synced.


  During onboarding, the ERP pushes GL entities (accounts, subsidiaries,
  currencies, etc.) to the Platform. The sync session mechanism lets the ERP
  explicitly signal 'I'm starting a sync' and 'I'm done syncing.' The UI holds
  on a loading/progress screen until the session is marked complete or expires,
  preventing users from seeing partially synced data.


  ### Key Points


  - Sessions are scoped per company — any valid API token for the company can
  start, complete, or poll a session.

  - Sessions have a **60-minute TTL**. If not completed within 60 minutes they
  expire automatically.

  - Entity creation calls are completely independent of sessions and remain
  backward compatible.

  - Sessions can only be started when the company is in GL onboarding
  (onboarding not yet completed).

  - **Completing the session is mandatory** — until the session is marked
  complete, the UI will continue to display a 'sync in progress' screen,
  preventing the user from proceeding with onboarding.
hidden: false
---