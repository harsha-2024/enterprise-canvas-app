
# Wiring flows in Canvas app

1. In Power Apps Studio, open your app → **Power Automate** pane → **Add flow** → select `PA_Approvals_Start` and `PA_Fraud_CheckTxn`.
2. Use these examples in control formulas:

```powerfx
// Approvals – Approve button
Set(resp, PA_Approvals_Start.Run(ThisItem.bkg_transactionid, "Approve", User().FullName));
If(resp.Outcome="Approve",
   Patch(bkg_transaction, ThisItem, { bkg_status: "Approved" })
)

// Fraud scoring – e.g., on a "Score" button
Set(fr, PA_Fraud_CheckTxn.Run(ThisItem.bkg_transactionid, ThisItem.bkg_amount, ThisItem.bkg_currency, ThisItem.bkg_customerid));
Patch(bkg_transaction, ThisItem, { bkg_fraudscore: fr.Score, bkg_isfraudrisk: fr.IsRisk })
```

> Add environment variable `pp_FraudApiUrl` in your solution and point it to your scoring endpoint before using the fraud flow.
