# ct-custom-app

A CommerceTools Merchant Center Custom Application built with the official `create-mc-app` starter template and deployed via CommerceTools Connect.

---

## Overview

This project extends the CommerceTools Merchant Center UI with a custom application that runs inside the MC shell. It is deployed to CommerceTools Connect (Australia GCP) and accessible directly from the MC sidebar.

---

## Tech Stack

- **Framework**: React (CommerceTools Application Kit)
- **Scaffolding**: `@commercetools-frontend/create-mc-app`
- **Deployment**: CommerceTools Connect (Sandbox, Australia GCP)
- **Cloud Region**: `gcp-au` (australia-southeast1)
- **CT Project**: `timepass`

---

## Project Structure

```
ct-connect-repo/
├── connect.yaml                        # CT Connect deployment config
└── ct-custom-app/                      # Custom Application source
    ├── custom-application-config.mjs   # App config (ID, cloud, scopes)
    ├── src/
    │   ├── components/
    │   │   ├── channel-details/        # Channel detail view
    │   │   ├── channels/               # Channels list view
    │   │   ├── entry-point/            # App entry point & routing
    │   │   └── welcome/                # Welcome/home page
    │   ├── hooks/
    │   │   └── use-channels-connector/ # GraphQL hooks for CT Channels API
    │   └── routes.jsx                  # App routes
    ├── i18n/data/                      # Translations (en, de)
    ├── package.json
    └── yarn.lock
```

---

## Configuration

### `custom-application-config.mjs`

| Field | Value |
|-------|-------|
| `entryPointUriPath` | `ct-custom-app` |
| `cloudIdentifier` | `gcp-au` |
| `initialProjectKey` | `timepass` |
| `applicationId` | `cmp56r6c0000101yl8lqnpi3x` |

### `connect.yaml`

```yaml
deployAs:
  - name: ct-custom-app
    applicationType: merchant-center-custom-application
    configuration:
      standardConfiguration:
        - key: CUSTOM_APPLICATION_ID
          description: The Custom Application ID
          required: true
        - key: CLOUD_IDENTIFIER
          description: The cloud identifier
          default: 'gcp-au'
        - key: ENTRY_POINT_URI_PATH
          description: The Application entry point URI path
          required: true
```

---

## Local Development

### Prerequisites
- Node.js v22
- yarn

### Setup

```bash
cd ct-custom-app
yarn install
yarn start
```

The app starts at `http://localhost:3001` and redirects to the MC login. After login it loads the app in the MC context.

---

## Deployment

The app is deployed via **CommerceTools Connect** using the `ct-connect-repo` GitHub repository.

### Steps to redeploy

1. Make changes to the app
2. Push to GitHub:
```bash
git add .
git commit -m "your message"
git push origin main
```
3. Create a new GitHub release tag (e.g. `v1.0.x`)
4. In MC → Organization → Connect → Manage connectors → `ct-custom-app` → update the tag → Save → **Publish for private use**
5. Once published, click **Deploy** and install on the `timepass` project

### Deployed URL

```
https://mc-app-m5v79uqdni3xcun0379ws15u.australia-southeast1.gcp.3.sandbox.commercetools.app
```

### MC App URL

```
https://mc.australia-southeast1.gcp.commercetools.com/timepass/ct-custom-app
```

---

## Key Learnings

- CT Connect requires a `yarn.lock` file to build successfully (not just `package-lock.json`)
- The repo must follow the monorepo structure: `connect.yaml` at root, app in a subfolder matching the `name` in `connect.yaml`
- `merchant-center-custom-application` type does not require `endpoint` or `scripts` in `connect.yaml`
- The `production.url` in `custom-application-config.mjs` must match the Connect deployed URL

---

## Resources

- [CT Custom Applications Docs](https://docs.commercetools.com/merchant-center-customizations/custom-applications)
- [Deploy to Connect](https://docs.commercetools.com/merchant-center-customizations/deployment/commercetools-connect)
- [CT Connect Application Kit](https://github.com/commercetools/connect-application-kit)
