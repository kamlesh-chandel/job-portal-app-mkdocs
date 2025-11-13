# TC 1: Authentication and Authorization Module

---

## TC 1.A: Register Test Cases

| Test Case No. | Module Name    | Test Case Description                              | Acceptance Criteria                                                   |
|---------------|----------------|-----------------------------------------------------|-----------------------------------------------------------------------|
| **T.C.1.1**   | Registration   | Register with valid name, email, password           | User created, password hashed, verification email sent               |
| **T.C.1.2**   | Registration   | Register with existing email                        | API returns 400 “Email already exists”                                |
| **T.C.1.3**   | Registration   | Register with invalid email format                  | API returns 400 “Invalid email format”                                |
| **T.C.1.4**   | Registration   | Register with password less than 8 characters       | API returns 400 “Password must be at least 8 characters”              |
| **T.C.1.5**   | Registration   | Register missing required fields                    | API returns 400 “All fields are required”                             |
| **T.C.1.6**   | Registration   | Register with name containing surrounding spaces    | Name is trimmed and saved correctly                                   |
| **T.C.1.7**   | Registration   | Email verification token generation                 | Verification email must include a valid JWT token                     |
| **T.C.1.8**   | Registration   | Ensure password hashing on registration             | Stored password must not match plain password                         |
| **T.C.1.9**   | Registration   | Register after soft deletion                        | New user allowed only if deleted_at is not null                       |
| **T.C.1.10**  | Registration   | Verify timestamps created_at and updated_at         | Both timestamps should be auto-populated                              |

---

## TC 1.B: Login Test Cases

| Test Case No. | Module Name | Test Case Description                           | Acceptance Criteria                                           |
|---------------|-------------|--------------------------------------------------|---------------------------------------------------------------|
| **T.C.2.1**   | Login       | Login with correct email and password            | Return success and JWT token                                  |
| **T.C.2.2**   | Login       | Login with wrong password                        | Return 401 “Invalid credentials”                               |
| **T.C.2.3**   | Login       | Login with unregistered email                    | Return 404 “User not found”                                   |
| **T.C.2.4**   | Login       | Login before email verification                  | Return 403 “Email not verified”                               |
| **T.C.2.5**   | Login       | Login of soft-deleted user                       | Return 403 “Account deleted”                                  |
| **T.C.2.6**   | Login       | Login with missing email or password             | Return 400 “All fields are required”                          |
| **T.C.2.7**   | Login       | Ensure password select:false is enforced         | Password must not be returned in any response                 |
| **T.C.2.8**   | Login       | Login with uppercase email                       | Email should auto-lowercase and login successfully            |
| **T.C.2.9**   | Login       | Validate token returned for FE localStorage      | Token must be present in login response                       |
| **T.C.2.10**  | Login       | Ensure timestamps on login                       | updated_at should be updated after login                      |

---

## TC 1.C: Email Verification Test Cases

| Test Case No. | Module Name        | Test Case Description                     | Acceptance Criteria                            |
|---------------|---------------------|--------------------------------------------|------------------------------------------------|
| **T.C.3.1**   | Email Verification  | Verify user with correct token             | User isVerified = true                          |
| **T.C.3.2**   | Email Verification  | Verify with expired token                  | Return 400 “Verification link expired”          |
| **T.C.3.3**   | Email Verification  | Verify with invalid token                  | Return 401 “Invalid verification token”         |
| **T.C.3.4**   | Email Verification  | Verify already verified user               | Return 400 “Email already verified”             |
| **T.C.3.5**   | Email Verification  | Verify with tampered token                 | Return 401 “Invalid signature”                  |

---

## TC 1.D: Role-Based Authorization Test Cases

| Test Case No. | Module Name     | Test Case Description                                   | Acceptance Criteria                      |
|---------------|------------------|----------------------------------------------------------|------------------------------------------|
| **T.C.4.1**   | Authorization    | Recruiter accessing student-only route                   | Return 403 “Access denied”               |
| **T.C.4.2**   | Authorization    | Student accessing recruiter-only route                   | Return 403 “Not allowed for this role”   |
| **T.C.4.3**   | Authorization    | Valid JWT and correct role access                        | Request allowed                           |
| **T.C.4.4**   | Authorization    | Valid JWT but incorrect role                             | Return 403                                |
| **T.C.4.5**   | Authorization    | Access without JWT                                       | Return 401 “Authorization token missing” |
| **T.C.4.6**   | Authorization    | Access with expired JWT                                  | Return 401 “Token expired”               |
| **T.C.4.7**   | Authorization    | Access with tampered JWT                                 | Return 401 “Invalid token”               |
| **T.C.4.8**   | Authorization    | Access with deleted or blocked user                      | Return 403 “Account disabled”            |

---

## TC 1.E: Protected Route Access Test Cases

| Test Case No. | Module Name       | Test Case Description                                | Acceptance Criteria                                   |
|---------------|-------------------|-------------------------------------------------------|---------------------------------------------------------|
| **T.C.5.1**   | Protected Routes  | Fetch user profile with valid JWT                     | Profile returned successfully                           |
| **T.C.5.2**   | Protected Routes  | Fetch profile without token                           | Return 401                                              |
| **T.C.5.3**   | Protected Routes  | Fetch profile with expired token                      | Return 401                                              |
| **T.C.5.4**   | Protected Routes  | Access route after token removal                      | Return 401                                              |
| **T.C.5.5**   | Protected Routes  | Ensure user returned matches token user               | Returned user must match token                          |
| **T.C.5.6**   | Protected Routes  | Access with old token after password change (future)  | Return 401 invalid token                                |
| **T.C.5.7**   | Protected Routes  | Ensure sensitive fields (password) not returned       | Password must never appear in API response              |
