
# Using this kit

## 1) Create a starter .msapp (optional)
You can generate a starter Canvas app with **PAC CLI** (e.g., from a custom connector):

```powershell
pac auth create --url "https://YOUR-ENV.crm.dynamics.com" --name Dev
pac auth select --name Dev
# Generate a basic app (replace with your connector if desired)
pac canvas create --msapp .\Starter.msapp --connector-display-name "Sample Connector"
```

> The **pack/unpack** commands are **preview/deprecated**. Use **Power Platform Git Integration** for source control of Canvas apps.

## 2) Assemble the app in Studio
- Open **Power Apps Studio** → Create a Canvas app (Tablet)
- For each YAML file in `/app/codeview-samples/screens` and `/components`,
  - Create a new **Screen** (or **Component** in a **component library**),
  - Open **Code View (Preview)**, **Paste** the YAML content, and save.
- Wire up Data sources to your Dataverse tables (see `/data-model`).

## 3) ALM
- Put the app in a **Solution**, commit via **Git Integration**, and use `/pipelines/azure-pipelines.yml` as a starting point for CI.
