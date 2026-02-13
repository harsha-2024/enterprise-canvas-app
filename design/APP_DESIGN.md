
# App Design – Banking Operations (Enterprise)

## Personas & Roles
- **Teller**: capture deposits/withdrawals, quick KYC check, cash transactions
- **Relationship Manager (RM)**: 360° customer view, onboarding, upsell, approvals
- **Operations**: back-office processing, batch approvals, exception handling
- **Compliance**: KYC, AML alerts, SAR (suspicious activity) triage
- **Admin**: user access, environment variables, theming, feature flags

## Major Modules / Screens
1. **Dashboard** – KPIs, workload, tasks
2. **Customers** – search, view, edit, KYC panel, credit profile
3. **Accounts** – balances, statements, account actions
4. **Transactions** – create/approve, fraud score banner, attachments
5. **Cases** – service cases, escalations, timeline
6. **Approvals** – inbox, bulk actions, audit log
7. **Admin** – feature flags, env vars (pp_*), offline data policy
8. **Settings** – theme, accessibility (high-contrast, large text), language

## Data
- Dataverse tables in `/data-model/dataverse_tables.csv`
- Environment Variables: `pp_FraudApiUrl`, `pp_MinCreditScore`, `pp_MaxDebtToIncome`, `pp_FeatureFlags`

## Performance & Delegation
- Use `StartsWith`/`in` where supported for delegable search on Dataverse
- Use `With()` and local variables to avoid recomputation
- Paginate Galleries via `Concurrent()` + `Skip()/FirstN()`
- Preload reference sets with `ClearCollect()` on App start

## Resilience & Telemetry
- Global `Notify()` wrapper; log to Dataverse `bkg_apptelemetry` (optional)
- Guard network calls with retry (Power Automate flows) and circuit-breaker flags

## Security & RBAC
- Role-based visibility: `Visible = User().Email in colAdmins || LookUp(colRoles, Email = User().Email && Role="Compliance")`
- Field-level governance via Dataverse column security profiles

