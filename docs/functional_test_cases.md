# Unit Test Cases — Job Portal App

This document outlines the **initial set of unit test cases** for the **Job Portal Application**.  
These tests focus on validating the core functionalities like **Authentication**, **Company Registration**, **Job Management**, **Applications**, and **Profile Management**.

---

| **Test Case No.** | **Module Name**                    | **Test Case Description**                                                                                           | **Acceptance Criteria**                                                                                     |
|-------------------|------------------------------------|----------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| **T.C. 1**        | **User Authentication - Signup**   | Verify that a new user (student/recruiter) can register successfully using valid name, email, password, and role.    | The system should create a new user record in the database, return **201 Created**, and a success message.  |
| **T.C. 2**        | **User Authentication - Signup (Duplicate Email)** | Attempt to register a user with an existing email. | The API should return **400 Bad Request** with an error message like *“Email already exists”*. |
| **T.C. 3**        | **User Authentication - Login**    | Verify that a registered user can log in using correct credentials.                                                  | The system should authenticate successfully, return **200 OK**, and provide a valid **JWT token**.          |
| **T.C. 4**        | **User Authentication - Login (Invalid Password)** | Attempt to log in with an incorrect password. | The API should return **401 Unauthorized** with a message *“Invalid credentials”*. |
| **T.C. 5**        | **Company Registration**           | Verify that a recruiter can register a new company by providing valid company name, website, and logo.               | A new company record should be created in the database, return **201 Created**, and link to recruiter ID.   |
| **T.C. 6**        | **Company Update**                 | Verify that a recruiter can update company details such as name, logo, or website.                                   | Updated company details should reflect in the database and return **200 OK** with success message.          |
| **T.C. 7**        | **Post Job**                       | Verify that a recruiter can create a job post with all required details (title, description, location, etc.).        | A job should be saved successfully in the database and return **201 Created** with a job ID in response.    |
| **T.C. 8**        | **Get All Jobs**                   | Verify that the system retrieves all available job listings for students.                                            | The API should return **200 OK** and a list of job objects in JSON format.                                 |
| **T.C. 9**        | **Get Job Details by ID**          | Verify that a student can fetch full job details using job ID.                                                       | The API should return **200 OK** with job details like title, description, and company info.                |
| **T.C. 10**       | **Apply for Job**                  | Verify that a student can apply for a job by submitting resume and job ID.                                           | The system should save the application in DB, return **201 Created**, and link it to the correct job & user.|
| **T.C. 11**       | **Get Applied Jobs (Student)**     | Verify that a student can view all applied jobs.                                                                     | The API should return **200 OK** and list of applications linked to the logged-in user.                     |
| **T.C. 12**       | **Update Application Status**      | Verify that a recruiter can update an applicant’s job status (Pending → Hired/Rejected).                             | The API should update the application status in DB and return **200 OK** with confirmation message.         |
| **T.C. 13**       | **Save Job (Bookmark)**            | Verify that a student can save a job to bookmarks for later viewing.                                                 | The job should be saved in the user’s bookmark list and return **200 OK** with success message.             |
| **T.C. 14**       | **Unsave Job**                     | Verify that a student can remove a previously saved job.                                                             | The job should be removed from bookmarks and return **200 OK** with confirmation message.                   |
| **T.C. 15**       | **Update Profile Information**     | Verify that a student can update their profile (skills, resume, profile photo).                                      | The updated data should reflect in the database, return **200 OK**, and success message displayed.          |

---

## Notes

- These are **initial test cases** for the early development phase of the project.  
- They will be expanded as new features like **Job Search**, **Pagination** etc. are implemented.  
- Test cases will be written using the following frameworks:
  - **Frontend:** Jest 
  - **Backend:** Jest  

---