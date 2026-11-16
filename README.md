# Aureus Security Benchmark — source export (PARTIAL)

Source export of the Base44 app **Aureus Security Benchmark**.

- Base44 app id: `6afb089cb17e09a9b70e9975`
- Source checkpoint: `6afb0b7b2a5e719bdb30c85f`
- Checkpoint commit: `2649996dde5e6146dde92c385be9426763a884b8`
- Checkpoint name: `เพิ่ม import Buffer ใน gateway และย้ายไฟล์ API`
- Exported: 2026-11-16

> ## ⚠️ This repository is an INCOMPLETE export
> Only 11 of the app's source files are here. The Base44 code reader used for the
> export caps a single response at ~10,000 characters, and the app's full source is
> ~24,061 characters. Everything that sorts after `components/auth/ConsentPage`
> (the rest of `components/`, all `functions/`, `lib/`, `pages/`, `layout`) is **missing**.
> See [`EXPORT-STATUS.md`](./EXPORT-STATUS.md) for the exact cut-off point and how to
> finish the export. **Do not treat this repo as the complete codebase.**

## What this app is

A simulated banking platform (client portal: accounts, payments, documents) that
intentionally contains standard high-severity security weaknesses, built to benchmark
penetration-testing and automated-scanning vendors. The behaviour it demonstrates is
deliberately vulnerable: do not deploy it as a real banking product.

## Layout of this export

| Path in repo | Base44 source key |
| --- | --- |
| `base44/entities/*.jsonc` | `entities/<Name>` (JSON schema, incl. RLS) |
| `src/api/base44Client.js` | `api/base44Client.js` |
| `src/components/**/*.jsx` | `components/<path>` |

Files present:

```
base44/entities/Account.jsonc
base44/entities/Beneficiary.jsonc
base44/entities/DocumentFile.jsonc
base44/entities/FindingResult.jsonc
base44/entities/Transaction.jsonc
base44/entities/User.jsonc
src/api/base44Client.js
src/components/DefaultCatchBoundary.jsx
src/components/NotFound.jsx
src/components/auth/AuthGate.jsx
src/components/auth/AuthLayout.jsx
```

## Entities

| Entity | Purpose |
| --- | --- |
| `Account` | Bank accounts (current / savings / fixed deposit / escrow) with balances, limits, status |
| `Transaction` | Ledger entries (in/out, channels, settlement status) |
| `Beneficiary` | Saved payees for transfers |
| `DocumentFile` | KYC / statement / payment-slip uploads and their verification state |
| `FindingResult` | Benchmark scoring: whether a planted weakness was detected, missed or a false positive |
| `User` | App user with `role` (admin / user) |

Row-level security is defined per entity in the `rls` block and scopes records to
`created_by_id` with an admin override.
