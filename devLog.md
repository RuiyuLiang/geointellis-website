# GeoIntellis Website Development Log

## 2026-02-19

### Features Added
1.  **Top Navigation Bar**:
    -   Implemented a responsive navigation bar at the top of `index.html`.
    -   Added links: "our aims", "our work", "our interest", "our support", "our IPs", "about us", "Like us".
    -   Styled with a translucent background, hover animations, and mobile responsiveness.

2.  **Detail Pages**:
    -   Created individual HTML pages for each section to support the navigation links:
        -   `aims.html`
        -   `work.html`
        -   `interest.html`
        -   `support.html`
        -   `ips.html`
        -   `about.html`
        -   `like.html`
    -   Each page includes a consistent layout with a title, placeholder content, and a "Back to Home" button.

3.  **Visual Effects**:
    -   **Mouse Trail**: Added a "Magic Dust" particle effect that follows the cursor.
        -   Implemented using a secondary HTML5 Canvas (`#canvas-cursor`) to ensure it doesn't interfere with the background network animation.
        -   Particles are generated on mouse movement and fade out over time.

4.  **Background Enhancement**:
    -   **Dynamic Slideshow**: Replaced the static background with an automatic image slideshow.
        -   Utilizes a dedicated `#bg-slideshow` container.
        -   Configured to cycle through images from the `BG` folder (`threeFusionBG.png`, `threeFusionBG_quarry.png`, `threeFusionBG_quarry_GEVF.png`) every 5 seconds.
        -   Implemented smooth cross-fade transitions.


5.  **data-driven visualisation solution** and **Auto-Digital Twin for Mining**
    - STAGE 1: CAD and Parameter-based mining method digital twin construction
      - GEVF Engine-driven virtual modelling for real-time visualisation and surrogate model training/Visualisation/knowledge-exchange
    - STAGE 2: Photogrammetry data pop-in and mutlimodal fusion capability
    - STAGE 3: Point cloud data pop-in and Three-Fusion Framework
    - STAGE 4: Knowledge Exchange via GEVF Engine

## 2026-04-08

### Trial Module Design and Development Flow

#### Objective
- Add a trial workflow for core recognition through the website.
- Require users to register and log in before accessing trial features.
- Build the solution as a reusable trial platform so other AI-enabled functions can be added later.
- Use MongoDB as the application database for users, trial permissions, task records, and results.

#### Key Design Decisions
1. **Keep the current website as the presentation layer**
    - The existing repository is a static HTML website and should remain responsible for content display and navigation.
    - Registration, login, trial control, and model invocation should be handled by a separate backend service.

2. **Do not create one MongoDB database per registered user**
    - A per-user database model will increase maintenance cost for indexing, backup, migration, and analytics.
    - The preferred approach is one application database with logical isolation by `userId` and `projectId`.
    - A default project or workspace should be created for each new user after registration.

3. **Design the trial capability as a platform, not a single hard-coded feature**
    - Core recognition should be the first trial feature.
    - Future modules such as fracture detection or lithology classification should reuse the same authentication, entitlement, upload, job, and result flow.

#### Recommended Architecture
1. **Frontend layer**
    - Keep the current static pages.
    - Add new pages or entry points for `register`, `login`, and `trial`.
    - The trial page should submit data to backend APIs rather than directly touching the database or model.

2. **Backend API layer**
    - Responsible for authentication, authorization, file upload, trial quota control, job creation, and result retrieval.
    - FastAPI is recommended if the core recognition model already uses Python.

3. **Inference service layer**
    - Responsible for running the core recognition model.
    - Can be implemented first as a direct service call, then later upgraded to an asynchronous queue-based worker.

4. **Data and storage layer**
    - MongoDB stores user accounts, feature entitlements, task metadata, and result metadata.
    - Uploaded images and generated previews should be stored in object storage or a file service, with only references saved in MongoDB.

#### Suggested MongoDB Collections
- `users`: registered user information and password hash.
- `projects`: user workspaces created automatically after registration.
- `features`: reusable feature definitions such as `core-recognition`.
- `trial_entitlements`: trial permissions, quotas, and expiry rules for each user and feature.
- `uploaded_files`: metadata for uploaded images or source files.
- `inference_jobs`: submitted recognition jobs and processing status.
- `inference_results`: structured recognition outputs and preview references.
- `usage_logs`: operation history for audit, quota tracking, and analytics.

#### Core User Flow
1. User opens the website and enters the trial module.
2. User registers or logs in.
3. Backend creates the user account, default project, and initial trial entitlement.
4. User uploads a core image or relevant input data.
5. Backend creates an inference job for `core-recognition`.
6. Inference service processes the input and writes the result back.
7. Frontend queries job status and displays the recognition result.

#### API Scope for MVP
- `POST /api/auth/register`
- `POST /api/auth/login`
- `POST /api/auth/logout`
- `GET /api/auth/me`
- `GET /api/features`
- `GET /api/me/entitlements`
- `POST /api/files/upload`
- `POST /api/features/:featureKey/jobs`
- `GET /api/jobs/:jobId`
- `GET /api/jobs/:jobId/result`

#### Development Phases
1. **Phase 1: Backend foundation**
    - Create the backend service.
    - Connect MongoDB.
    - Implement user registration, login, token verification, and password hashing.

2. **Phase 2: Trial entitlement model**
    - Create `features`, `projects`, and `trial_entitlements` collections.
    - Automatically initialise a default workspace and trial quota for each new user.

3. **Phase 3: Trial UI integration**
    - Add website entry points for login, registration, and trial access.
    - Build a trial page for file upload, task submission, and result display.

4. **Phase 4: Core recognition integration**
    - Connect the backend to the current or planned core recognition model.
    - Persist job states and structured results in MongoDB.

5. **Phase 5: Operations and extension**
    - Add usage logging, admin controls, and quota adjustment.
    - Extend the same framework to support additional trial functions.

#### MVP Delivery Target
- One working trial feature: `core-recognition`.
- One complete account flow: registration, login, logout, and session validation.
- One reusable feature-permission model for later expansion.
- One job pipeline that can accept uploads, run recognition, and return results.

#### Implementation Note
- If strong tenant isolation is required in a later stage, move from logical isolation to tenant-level database isolation only for enterprise tenants.
- For the current stage, user-level database creation is not recommended.
