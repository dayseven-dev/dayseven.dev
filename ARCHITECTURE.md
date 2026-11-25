# Architecture

This file records which technology each platform is built with and which environments the product
runs in, so anyone joining the project sees the whole system in one place. It describes how the
system is built, not how to work on it; for that, see CONTRIBUTING.md. Update it only when a
platform or an environment changes.

## Tech Stack

| #  | Target            | Stack                              | Status  |
|----|-------------------|------------------------------------|---------|
| 1  | Android           | Compose Multiplatform + KMP        | Planned |
| 2  | iOS               | SwiftUI + KMP                      | Planned |
| 3  | Desktop           | Compose Multiplatform + KMP        | Planned |
| 4  | Web app           | SvelteKit + KMP (Kotlin/JS)        | Planned |
| 5  | Marketing site    | SvelteKit (prerendered)            | Planned |
| 6  | Browser extension | TBD                                | Planned |
| 7  | Backend           | Ktor + KMP models                  | Planned |

## Environments

One name per environment, used the same way on every platform.

| Branch | Environment | Android flavor | Web                     |
|--------|-------------|----------------|-------------------------|
| `dev`  | DEV         | `dev`          | `devapp.dayseven.dev`   |
| `main` | PROD        | `prod`         | `app.dayseven.dev`      |

- DEV is where a sprint's work is tested before it ships. PROD is the live product.
- How work moves from `dev` to `main` is in
  [CONTRIBUTING.md](CONTRIBUTING.md#branching-strategy).
- On Android, environments are product flavors. Build types stay `debug` and `release`, so a
  `devRelease` build can be tested on DEV.
