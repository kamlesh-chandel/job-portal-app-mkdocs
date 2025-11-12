# Data Flow Diagrams

This section shows how data moves through the **Job Portal App** at different levels of detail — from a high-level system view to a detailed breakdown of key processes.

---

### Level 0 DFD
The Level 0 diagram represents the overall system as a single process interacting with — **Students**, **Recruiters**, **AWS S3**, **MongoDB Atlas**.  

--- 
```mermaid
---
config:
  theme: neutral
---

flowchart TD
    %% External Users
    Student[Student]
    Recruiter[Recruiter]

    %% System
    System[Job Portal Application]

    %% Data Stores (shown as external connections)
    DB[(MongoDB Atlas)]
    S3[(AWS S3)]

    %% Flows
    Student -->|Register / Login / Browse / Apply / Upload Resume / Save Jobs| System
    Recruiter -->|Register / Login / register company / Post Jobs / View Applicants / change application status | System

    System -->|Return Data, Status, Responses| Student
    System -->|Return Applicant Data, Job Status| Recruiter

    System -->|Store & Fetch Data| DB
    System -->|Upload & Retrieve Files| S3

    %% Styling
    classDef user fill:#e3f2fd,stroke:#1976d2,stroke-width:3px,color:#000;
    classDef system fill:#fff3e0,stroke:#ef6c00,stroke-width:3px,color:#000;
    classDef storage fill:#e8f5e9,stroke:#388e3c,stroke-width:3px,color:#000;

    class Student,Recruiter user
    class System system
    class DB,S3 storage

```

---

### Level 1 DFD
This diagram breaks the system into key functional modules like Authentication, Company & Jobs, Student Actions, and Storage.
```mermaid
flowchart TD
    %% Users
    A[Student]
    B[Recruiter]

    %% Main Processes
    subgraph "Authentication"
        Login[Login / Register]
    end

    subgraph "Company & Jobs"
        Company[Create / Manage Company]
        Jobs[Post / Edit / Delete Jobs]
    end

    subgraph "Student Actions"
        Browse[Browse Jobs]
        Apply[Apply for Jobs]
        Upload[Upload Resume / Photo]
        Save[Save Jobs]
    end

    subgraph "Storage"
        DB[(MongoDB Atlas<br>Users, Roles, Companies, Jobs, Submissions, Bookmarks )]
        S3[(AWS S3<br>Resumes & Photos)]
    end

    %% Flows
    A --> Login
    B --> Login
    Login --> DB

    B --> Company --> DB
    B --> Jobs --> DB

    A --> Browse --> DB
    A --> Apply --> DB
    A --> Upload --> S3 --> DB
    A --> Save --> DB

    B --> ViewApps[View Applicants] --> DB

    DB --> Jobs --> A
    DB --> Jobs --> B
    DB --> ViewApps --> B

    %% Styles
    classDef user fill:#e3f2fd,stroke:#1976d2,stroke-width:3px,color:#000;
    classDef process fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px;
    classDef storage fill:#e8f5e9,stroke:#388e3c,stroke-width:3px;

    class A,B user
    class Login,Company,Jobs,Browse,Apply,Upload,Save,ViewApps process
    class DB,S3 storage
```

### Level 2 DFD
This level provides a detailed view of the internal operations inside each module.

---

```mermaid
flowchart TD
    %% Users
    Student[Student]
    Recruiter[Recruiter]

    %% Auth Process Breakdown
    subgraph "Authentication Module"
        Register[Register New User]
        Login[Login User]
        Validate[Validate Credentials]
        StoreUser[Store User Info in DB]
    end

    %% Company & Job Process Breakdown
    subgraph "Company & Job Module"
        CreateCompany[Register Company]
        FetchCompanies[Fetch Companies]
        FetchJobs[Fetch Jobs]
        PostJob[Post Job]
        EditJob[Edit Job]
        DeleteJob[Delete Job]
        FetchJobApplicants[Fetch Job Applicants]
        UpdateApplicationStatus[Update Application Status]
    end

    %% Student Application Module
    subgraph "Application Module"
        BrowseJobs[Browse All Jobs]
        ApplyJob[Apply for Job]
        UploadFile[Upload Resume to S3]
        SaveJob[Save Job for Later]
        TrackStatus[View Application Status]
    end

    %% Data Stores
    DB[(MongoDB Atlas)]
    S3[(AWS S3)]

    %% Flows
    Student --> Register --> StoreUser
    Student --> Login --> Validate --> DB
    Recruiter --> Login --> Validate --> DB

    Recruiter --> CreateCompany --> DB
    Recruiter --> PostJob --> DB
    Recruiter --> EditJob --> DB
    Recruiter --> DeleteJob --> DB
    Recruiter --> FetchJobs --> DB --> FetchJobs
    Recruiter --> FetchJobApplicants --> DB --> FetchJobApplicants
    Recruiter --> FetchCompanies --> DB --> FetchCompanies
    Recruiter --> UpdateApplicationStatus --> DB

    Student --> BrowseJobs --> DB
    Student --> ApplyJob --> DB
    Student --> UploadFile --> S3 --> DB
    Student --> SaveJob --> DB
    Student --> TrackStatus --> DB

    DB --> TrackStatus --> Student
    DB --> PostJob --> Recruiter
    DB --> ApplyJob --> Recruiter

    %% Styles
    classDef user fill:#e3f2fd,stroke:#1976d2,stroke-width:3px,color:#000;
    classDef process fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px;
    classDef storage fill:#e8f5e9,stroke:#388e3c,stroke-width:3px;

    class Student,Recruiter user
    class Register,Login,Validate,StoreUser,CreateCompany,PostJob,EditJob,DeleteJob,BrowseJobs,ApplyJob,UploadFile,SaveJob,TrackStatus,FetchCompanies,FetchJobs,FetchJobApplicants,UpdateApplicationStatus process
    class DB,S3 storage
```

