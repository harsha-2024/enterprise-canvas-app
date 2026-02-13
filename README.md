
# BankingOps Canvas App – Extended (Dataverse-aligned)

This package implements:
1) **Logical name alignment** to the `bkg_*` Dataverse schema used in the prior kit and plug-ins.
2) New **Screens**: Approvals Inbox, Case Timeline, Admin Feature Flags (paste into Code View).
3) **Power Automate Flows** (JSON) for Approvals and Fraud Checks + wiring samples (Power Fx) to call them via `Flow.Run(...)`.

> If your logical names differ, run a global find/replace on the YAML and flow JSONs. Key logical names used: `bkg_transaction`, `bkg_customer`, `bkg_case`, and their columns like `bkg_status`, `bkg_txndate`, `bkg_isfraudrisk`.
