# Flatmate HQ project handover

## Purpose and team

A household organiser for three collaborators to develop together. Keep the existing look and features. Work lives in the ChatGPT project “Flatmate HQ”. Unrelated project material is intentionally excluded.

## Current app

- Overview: household summary, recent activity, expenses, chores, shopping and upcoming events.
- Expenses: equal splits in NZD, exact allocation to the cent, balances and suggested repayments. Recording a repayment does not transfer money.
- Receipts: optional JPEG, PNG, WebP or PDF attachments up to 1 MB each. Existing expenses can also receive or replace a receipt. Images have a preview and files can be downloaded.
- Chores: weekly rotation, completion, reassignment and shuffling unfinished jobs.
- Shopping: items, quantities, who added them, and bought/needed status.
- Calendar: flat events, inspections, bills and bin days.
- Reminders: one-off, weekly or fortnightly reminders. Marking a repeating reminder done advances it one interval. Calendar-file download includes an alert one hour before. The user must import it into their calendar; the app does not send background push notifications.
- Fines and weekly crown: separate from shared expense balances.
- Activity: newest updates first, category filters, and an Overview preview. Logs expenses, repayments, shopping changes, receipt updates, chore completions/reopening, reminders, events, fines, flatmates and weekly awards. Keeps the latest 500 logged changes. Existing expenses, repayments and fines appear as existing records; older shopping and chore actions cannot be reconstructed.
- Settings: flat name, flatmates, JSON backup export/import.

## Architecture

Buildless static app in `dist/index.html`, `dist/style.css`, `dist/app.js`. No framework, package manager or server database. Navigation uses URL hashes. Money is stored as integer cents. Dates use Pacific/Auckland; currency is NZD.

All household data is in localStorage under `flatmate-hq-v1`. Receipts are stored as data URLs inside the same data. Browser storage can fill; uploads and saves surface errors. Backups include receipts, reminders and activity. Older supported backups gain empty reminders/activity arrays during validation.

Activity is captured by comparing state with a snapshot on successful save. Logs store descriptive text rather than user authentication identities. This is a browser-local history, not a shared or tamper-proof audit log.

## Relevant conversation decisions

1. User opened Flatmate HQ and established this chat as the place to develop it.
2. Discussed making it an iPhone app and eventually distributing through the App Store. No native project, Apple developer account setup or App Store submission has been done.
3. Chat was moved from the general coding project into its own Flatmate HQ project.
4. User requested household reminders such as rubbish collection, and receipt attachments under expenses. Implemented and published.
5. User requested recent purchases, expenses and other updates in an Activity section. Implemented and published.
6. User requested this standalone pack for moving to GitHub and developing with three people. No GitHub repository has been created or collaborator invitations sent as part of this pack.

## Next development priorities

The main missing capability for a real shared flat is accounts, flat invitations, shared server storage and access control. Code collaboration on GitHub is separate from shared app data. Other potential work: native/mobile packaging, background notifications, larger receipt storage, edit/delete flows and more detailed activity tracking. These are future ideas, not completed features.

## Checks performed

JavaScript syntax checks; targeted tests for receipt validation and backup migration, recurring calendar-file generation, activity logging and duplicate prevention, filtering, HTML escaping and backup roundtrip. Browser checks covered reminders advancing and persisting after reload, receipt entry controls, and Activity rendering with existing records. This is not a comprehensive automated test suite, native-device test, or multi-user test.

## Current source identity

Site project ID: appgprj_6ad491bc1ebc8191b83e1376e571fb02

Branch: main

Latest commit: b001369ceedf7e2edb748d677bfdbd1d8038b2a2

Live URL: https://flatmate-hq-benjamin.grassycup1.chatgpt.site/
