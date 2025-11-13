# Test Plan – Job Portal App

Below is the comprehensive test plan for the Job Portal Application, structured in a tabular format as per the required template.

---

## 1. Introduction

| Section | Description |
|--------|-------------|
| Purpose | Define the strategy and approach for testing the Job Portal Application (Frontend + Backend). |
| Scope | Covers authentication, role-based access, companies, jobs, submissions, bookmarks, UI flows, and API validations. |
| Audience | Developers, QA engineers, mentors, and stakeholders. |

---

## 2. Objective

| Objective | Description |
|-----------|-------------|
| Ensure Quality | Validate that all modules function as expected in various scenarios (happy, negative, boundary). |
| Ensure Security | Verify JWT authentication, password hashing, and role-based authorization. |
| Ensure Stability | Verify API reliability, error handling, and correct data flows across modules. |
| Ensure Usability | Confirm that UI is consistent, user-friendly, and behaves correctly on all flows. |

---

## 3. In Scope

| In Scope Modules |
|------------------|
| User Registration & Login |
| Email Verification |
| JWT Authentication |
| Role-Based Authorization |
| Company Management |
| Job Management |
| Job Applications / Submissions |
| Bookmarking Feature |
| Frontend UI Testing |
| API Testing |
| Validation Testing |

---

## 4. Out of Scope

| Out of Scope |
|--------------|
| Performance testing (load, stress) |
| Penetration testing / security red teaming |
| Third-party service internal logic (AWS S3, email service) |
| Localization (multi-language support) |
| Mobile app-specific behavior |

---

## 5. Test Items

| Module | Items to Test |
|--------|----------------|
| Authentication | Register, Login, Email Verify, JWT validation |
| Authorization | Role-based access (student/recruiter) |
| Company Module | Create, update, fetch companies |
| Job Module | Post job, edit job, delete job, view jobs |
| Submission Module | Apply job, view applicants, update status |
| Bookmark Module | Save jobs, remove saved jobs |
| Frontend UI | Forms, routing, rendering, error states |

---

## 6. Testing Approach

| Area | Description |
|------|-------------|
| Framework | **Vitest** for unit & integration (Frontend + Backend), **Supertest** for API testing |
| Tools | React Testing Library, Postman, MongoDB Compass |
| Test Levels | Unit testing, Component testing, API testing, Integration testing |
| Strategy | Data-driven, modular, feature-wise testing |
| File Structure | <br>**client/tests/** → frontend unit & component tests <br>**server/tests/** → backend api & unit tests |

---

## 7. Data-Driven Testing

| Test Data Type | Examples |
|----------------|----------|
| Valid User Data | Correct name, valid email, strong password |
| Invalid User Data | Wrong email format, weak password |
| Role Data | `student`, `recruiter` |
| Company Data | Valid company name, website, address |
| Job Data | Titles, descriptions, salary ranges |
| Application Data | Status values: pending, under review, hired, rejected |

---

## 8. Test Cases

| Module | Reference |
|--------|-----------|
| Authentication | Refer to **Authentication Test Cases (TC 1)** |
| Authorization | TC 2 |
| Company Module | TC 3 |
| Job Module | TC 4 |
| Submissions | TC 5 |
| Bookmarks | TC 6 |

---

## 9. Exit Criteria

| Criteria | Description |
|----------|-------------|
| All test cases executed | 100% planned tests executed |
| 95% test cases pass | Critical flows must have 100% pass rate |
| No major/blocker bugs | All P0/P1 bugs resolved |
| Test coverage target met | Target: 80%+ for backend, 70%+ for frontend |

---

## 10. Risk & Mitigation

| Risk | Impact | Mitigation |
|------|--------|------------|
| Incomplete test coverage | High | Prioritize critical flows (auth, jobs, submissions) |
| API integration failures | Medium | Use Postman + Supertest for early validation |
| Incorrect role mapping | High | Add strict validation + DB seeding |
| Environment issues | Medium | Use `.env.example` and consistent setup docs |

---

## 11. Deliverables

| Deliverable | Description |
|-------------|-------------|
| Test Plan Document | This file |
| Test Case Documents | Separate `.md` files for each module |
| Test Execution Report | Summary of passed/failed test cases |
| Defect Report | List of bugs with severity and status |
| Coverage Report | Vitest coverage summary |

---
