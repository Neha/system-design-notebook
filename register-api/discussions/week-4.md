# Week 4: Login API 

In this session, we focused on extending our existing register API to include login functionality.
We discussed both functional and non-functional system requirements, along with a basic system design for the login API.

The goal was to understand what changes or considerations are needed when adding login capabilities to the current register API design.

[Diagram week 4](./diagrams/week-4.png)

---

## Validation for Input fields

- Added necessary validations for email and password fields.
- Identified that input validations for email and password were missing in the original register API design.
- Implemented basic password rules: minimum 8 characters, including at least one number and one special character.

---

## Login by Password vs OTP

- Discussed the trade-offs between **password-based** and **OTP-based** authentication.
- Chose to implement **password-based** login for now to keep the system simple.
- Agreed to revisit this decision in future sessions, along with evaluating support for **social logins**.

---

## Security

- Added the following **security** considerations for Login API:
    - Implemented **input sanitization** on the frontend to protect against vulnerabilities like **SQL injection** and **script injection**.
    - Addressed **login error handling** to prevent malicious users from determining whether an account exists by submitting incorrect passwords.
    - Defined a **session timeout policy (TTL)** to ensure users are automatically logged out after a period of inactivity.
    - **rate limiting** on the Login API to mitigate brute-force attacks.
    - Planned to explore adding **MFA** in upcoming sessions.

---

## Functional and Non-functional Requirements

- Discussed the definitions for Functional and Non-functional Requirements

- **Functional Requirements**
    - UI for Email, Password, Submit Button
    - Helpful Error Messages
    - Geo Fencing
    - Role based authentication and authorization
    - Forgot Password
    - Reset Password
    - Delete Profile/Account
 
- **Non Functional Requirements**
    - Consistency
    - Availability
    - Performance
    - Concurrency

---

## Role based authentication and authorization

- 3 roles in the system - **Super Admin**, **Admin** & **User**
- Decided to onboard everyone as basic **User** role
- Basic users can be upgraded to **Admin** or **Super Admin** role when needed

---

## Next Session

- Relook at Functional and Non-functional requirements
- Database Design for Login API - Design for Scale
- Adding support for **Social Logins** and **MFA**
- Discuss what prior decisions needs to be reconsidered/changed to add Login functionality

