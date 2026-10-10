# 🚀 Document 6: Deployment & DevOps Playbook
> **Project:** Task Management System (Kanban Style)  
> **Version:** 1.0.0  
> **Author:** Ashish Thombare  
> **Date:** 10-Oct-2026  
> **Status:** APPROVED Production Deployment Architecture  

---

## 1. Cloud Architecture Overview (Microsoft Azure)
To deploy our decoupled architecture globally, we utilize Microsoft Azure App Services. The systems are split into two independent production environments to enforce **Separation of Concerns (SoC)** at the infrastructure level:

1. **Backend Web API Environment:** Hosted on **Azure App Service (Linux / .NET 8.0/9.0 runtime)**.
2. **Frontend Client Environment:** Hosted on **Azure Static Web Apps** or Static Website Hosting via Azure Storage for optimized edge delivery.

---

## 2. Step-by-Step Deployment Protocol

### Phase 2.1: Backend Production Release (ASP.NET Core API)
Before pushing the backend live, the application must be compiled into a release-ready package.

1. **Local Compilation Check:** Run the release build command to ensure no compilation warnings exist:
   ```bash
   dotnet publish -c Release -o ./publish
   ```
2. **Azure Configuration:**
   * Create a new **Web App** instance via the Azure Portal.
   * Select the appropriate **.NET Runtime Stack** and Linux Operating System.
   * Configure Environment Variables under `Settings -> Configuration` for production application configurations.
3. **CORS Security Setup:** Update Azure CORS settings to explicitly allow traffic *only* from the authenticated frontend production URL, blocking external malicious access vectors.

### Phase 2.2: Frontend Production Release (React + Tailwind)
1. **Production Assets Generation:** Build the React application into optimized static assets (HTML, CSS, JS chunks) using Vite:
   ```bash
   npm run build
   ```
   *This command isolates code execution and outputs a highly minified `/dist` folder ready for production edge deployment.*
2. **Deployment Execution:**
   * Initialize an **Azure Static Web App** instance linked directly to your GitHub repository.
   * Setup GitHub Actions for automated CI/CD deployments. The build engine will automatically capture updates on the `main` branch, build the static files, and push them live to the Azure content delivery network (CDN).

---

## 3. Production Environment Validation Matrix (Sanity Checklist)
Post-deployment, the production runtime environments must pass the following structural validation criteria:
* [ ] **API Vitality:** Navigating to `https://azurewebsites.net` displays the functional Swagger UI engine.
* [ ] **Data Integrity Gateway:** Triggering a `GET /api/tasks` from the production cloud endpoint returns a valid `200 OK` array payload.
* [ ] **Cross-Origin Security:** The frontend successfully communicates with the backend without encountering console CORS policy blockades.
---
