# System Architecture

---

## Tech Stack Overview

The Job Portal App uses the **MERN (MongoDB, Express, React, Node)** stack

## System Architecture Diagram

```mermaid
graph LR
    %% Frontend
    subgraph "Frontend"
        A[React App]
        S3FE[Amazon S3 + CloudFront - Static Website Hosting]
    end

    %% Backend
    subgraph "Backend"
        B[Node.js + Express API]
        EB[Amazon Elastic Beanstalk - EC2]
        J[JWT Authentication]
    end

    %% Database
    subgraph "Database"
        C[MongoDB Atlas]
    end

    %% File Storage
    subgraph "Storage"
        S3[AWS S3 - File Uploads]
    end

    %% Relationships
    A -->|HTTPS Requests| B
    A -->|Served via| S3FE
    B -->|Deployed on| EB
    B -->|Uses JWT for Auth| J
    B -->|Reads/Writes Data| C
    B -->|Uploads/Downloads Files| S3
```

### Frontend
- **React + Vite:** Provides fast UI rendering and hot module replacement for rapid development.
- **Redux:** Manages global state across different components.
- **Tailwind CSS:** Used for responsive and modern design.
- **Shadcn/ui:** customizable component library used for accessible UI components (like modals, dropdowns, buttons, and inputs).

### Backend
- **Express.js:** Handles API routes and middleware logic.
- **Node.js:** Provides a runtime environment for server-side logic.
- **JWT Authentication:** Ensures secure login and role-based route protection.

### Database
- **MongoDB:** Stores users, jobs, and applications. Each recruiter’s jobs and corresponding applications are linked via object references.

### File Storage
- **AWS S3:** Stores Resume file and photos like company logo, user profile photo.

---

## Deployment Structure

- **Frontend Deployment:** Deployed on **Vercel** for fast builds and global CDN delivery.  
- **Backend Deployment:** Hosted on **Render** for dynamic APIs.  
- **Database:** Managed on **MongoDB Atlas**, ensuring scalability and cloud reliability.



