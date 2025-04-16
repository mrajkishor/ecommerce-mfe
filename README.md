

# 🧩 E-Commerce Frontend – Micro Frontends Architecture (MFE)

This project is the **frontend counterpart** to the [ecommerce-application](https://github.com/mrajkishor/ecommerce-application) backend, designed using **Micro Frontends (MFE)** with **Nx monorepo**, **React**, **Webpack Module Federation**, and **Tailwind CSS**. Each domain feature (User, Product, Order, etc.) is its own independent MFE, enabling modular development and deployment.

---

## 📦 Tech Stack

| Layer             | Technology                                 |
|------------------|--------------------------------------------|
| Monorepo         | Nx                                          |
| UI Framework     | React (MFE shell + remotes)                |
| Styling          | Tailwind CSS                               |
| Micro Frontend   | Webpack 5 Module Federation                |
| State Management | Redux Toolkit + RTK Query                  |
| Dev Tools        | Storybook, ESLint, Prettier                |
| CI/CD            | GitHub Actions / Jenkins (optional)        |
| Deployment       | Docker + NGINX or CDN (e.g., S3 + CloudFront) |

---

## 📁 Project Structure

```
apps/
├── container-shell/       # Host application (root shell)
├── mfe-user/              # User domain frontend
├── mfe-product/           # Product catalog UI
├── mfe-order/             # Order placement and history
├── mfe-review/            # Reviews and ratings
├── mfe-payment/           # Payment interface
libs/
├── common/                # Shared UI components (buttons, layout, etc.)
├── framework/             # Store, API service, config, logging
├── plugins/               # Mock server, CLI utilities
```

---

## 🧠 Features

- 🧱 **Independent MFEs** with separate routes, builds, and teams
- 🧩 **Host shell** loads MFEs dynamically at runtime
- 🔐 **Auth-aware routing** using JWT
- ⚡ **Tailwind-based design system** in `libs/common`
- 🧪 **Storybook + RTL tests** for each component
- 🧬 **RTK Query** replaces Axios for data fetching
- 🔄 **Real-time updates** using WebSockets/Kafka-bridge (optional)

---

## 🧭 MFE Mapping to Backend Services

| Frontend App      | Backend Microservice      |
|-------------------|---------------------------|
| `mfe-user`        | `user-service` (Java)     |
| `mfe-auth`        | `auth-service` (Node.js)  |
| `mfe-product`     | `product-service` (Java)  |
| `mfe-order`       | `order-service` (Java)    |
| `mfe-payment`     | `payment-service` (Java)  |
| `mfe-review`      | `review-service` (Node.js)|
| `mfe-notification`| For SSE/WebSocket bridge  |
| `mfe-analytics`   | `analytics-service` (Python)|

---

## 🚀 Getting Started

```bash
git clone https://github.com/mrajkishor/ecommerce-mfe.git
cd ecommerce-mfe
npm install

# Start all MFEs + Shell
npm run dev
```

Or run a specific app:

```bash
nx serve mfe-user
```

---

## 🛠️ Commands

| Command                     | Description                                |
|----------------------------|--------------------------------------------|
| `nx serve <app>`           | Serve any MFE app                          |
| `nx build <app>`           | Build a single MFE                         |
| `nx run-many --target=build --all` | Build all apps/libraries              |
| `nx lint <app>`            | Lint using ESLint + Prettier               |
| `nx test <app>`            | Run unit tests                             |
| `nx graph`                 | Visualize project dependency graph         |
| `nx storybook <lib>`       | Launch Storybook for shared UI             |

---

## 📦 Deployment Strategy

1. Each MFE builds a static bundle (e.g., `remoteEntry.js`, `bundle.js`)
2. Upload to CDN (S3, CloudFront, EdgeCast, etc.)
3. Shell loads MFEs dynamically via `remoteEntryUrl` config
4. Use NGINX or gateway to host the shell

---

## 🔐 Security & Auth

- 🔐 JWT stored in memory or HttpOnly cookie
- 🔒 Auth guard wrapper around protected routes
- 🧩 Token passed to RTK Query for secure API calls

---

## 🔬 Monitoring & Observability

- Custom `logger.ts` in `libs/framework` sends logs to ELK
- App lifecycle metrics collected using Web Vitals
- UI error boundaries for fault isolation

---

## 📈 CI/CD Setup

- ✅ Lint, test, and build each app/lib
- ✅ Upload bundles to S3/CDN
- ✅ Trigger cache invalidation
- ✅ GitHub Actions + Docker support

---

## 📚 Documentation

- `docs/architecture.md`: System architecture
- `docs/usage.md`: Developer onboarding
- `docs/api.md`: REST contracts and mock data
- `docs/deploy.md`: Hosting + CDN integration

---

## 🤝 Contributing

PRs welcome! Focus on:
- Adding new MFEs (e.g., Cart)
- Improving shared libraries
- Integrating backend event flows (Kafka, etc.)

---

## 📬 Contact

Maintainer: [@mrajkishor](https://github.com/mrajkishor)  
Backend Repo: [ecommerce-application](https://github.com/mrajkishor/ecommerce-application)

