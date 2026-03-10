# TEST PLAN

## Booking Homestay System – BookNow

**Subject:** SWT391 – Software Development Project  
**Group:** 02 – SE1910  
**Mentor:** Lam Le Huan  
**Version:** 1.0  
**Date:** March 10, 2026  

---

## VERSION HISTORY

| Version | Date       | Author            | Description          |
|---------|------------|-------------------|----------------------|
| 1.0     | 10/03/2026 | Nguyen Hoang Han  | Initial Test Plan    |

---

## TABLE OF CONTENTS

- I. Introduction
- II. Test Objective
- III. Scope of Testing
- IV. Test Strategy
- V. Risks
- VI. Test Criteria
- VII. Resource Planning
- VIII. Test Environment
- IX. Schedule & Estimation
- X. Test Deliverables

---

## I. INTRODUCTION

### 1. Team Members

| No | Full Name             | Student ID | Role                    |
|----|-----------------------|------------|-------------------------|
| 1  | Nguyen Hoang Han      | CE192048   | Leader – Test Plan      |
| 2  | Le Tan Loc            | CE191560   | Unit Test               |
| 3  | Nguyen Hung Phat Dat  | CE191354   | System Test – Decision Table Testing & Feedback |
| 4  | Vo Thanh Dat          | CE191280   | System Test – Use Case Testing / Booking Flow   |
| 5  | Vo Anh Hao            | CE191463   | System Test – Use Case Testing / Booking Flow   |
| 6  | Phung Dinh Khang      | CE191105   | Testing Tools           |

### 2. Project Description

The **Booking Homestay System (BookNow)** is a web-based application designed to facilitate room booking, check-in/check-out management, payment processing, and feedback handling for a homestay business. The system serves three user roles: **Customer**, **Staff**, and **Admin**.

- **Customers** can register, log in, browse available rooms, make bookings, pay online, check in using a booking code, view booking history, and submit feedback.
- **Staff** can log in to the management portal, manage rooms (add, update, view), manage bookings (view, update status), handle check-in/check-out processes, and view feedback.
- **Admin** has full access including staff account management, user management, revenue reporting, and all staff capabilities.

**Technology Stack:**
- **Backend:** Java, Spring Boot, Spring Security, JPA/Hibernate
- **Database:** Microsoft SQL Server
- **Architecture:** MVC (Controller → Service → Repository)
- **Packages:** `booknow` root package with `controllers`, `services`, `repositories`, `security`, `utils`, `model` (entities, dto, map)

---

## II. TEST OBJECTIVE

The objective of this test plan is to verify and validate the **Booking Homestay System (BookNow)** against the requirements specified in the SDS document. Testing aims to:

1. Verify that all functional requirements (17 use cases) are correctly implemented and behave as expected.
2. Validate the user interface for usability, responsiveness, and consistency across supported browsers.
3. Ensure the system handles invalid inputs, boundary conditions, and error scenarios gracefully.
4. Confirm that authentication, authorization, and session management (Spring Security, JWT/Refresh Token) work correctly for all three roles (Customer, Staff, Admin).
5. Validate data integrity across all 14 database tables (Customer, StaffAccounts, RefreshToken, RoomType, Room, Amenity, RoomAmenity, Image, Booking, Payment, Invoice, Feedback, Timetable, Scheduler).
6. Assess system performance under expected load conditions.
7. Identify, document, and track all defects to resolution.

---

## III. SCOPE OF TESTING

### a. In Scope

#### Functional Testing

| No | Feature / Module                  | Description                                                                 |
|----|-----------------------------------|-----------------------------------------------------------------------------|
| 1  | Authenticate User (UC-01)         | Customer login, reset password (email OTP verification)                     |
| 2  | Register Account (UC-02)          | Customer registration with email OTP and profile setup                      |
| 3  | Logout (UC-03)                    | Session termination and token revocation for all roles                      |
| 4  | Manage Profile (UC-04)            | View profile, update profile information, change password                   |
| 5  | Looking For Room (UC-05)          | View homepage & timetable, filter/search rooms, view room detail page       |
| 6  | Booking (UC-06)                   | Room booking creation with date selection, ID card upload, and validation   |
| 7  | Make Payment (UC-07)              | Payment processing (MoMo QR, bank transfer) and payment confirmation       |
| 8  | View Booking History (UC-08)      | Customer views list of past and current bookings with status                |
| 9  | Check-in Room (UC-09)             | Booking code verification, camera/manual check-in process                   |
| 10 | Check-out Room (UC-10)            | Check-out process with feedback prompt                                      |
| 11 | Login to System – Staff/Admin (UC-11) | Staff and Admin authentication to management portal                     |
| 12 | Manage Room (UC-12)               | View room list, search, view detail, add room, update room (Staff/Admin)    |
| 13 | Manage Booking (UC-13)            | View booking list, view booking detail, update booking status (Staff/Admin) |
| 14 | Manage Feedback (UC-14)           | View feedback detail, hide/show feedback, reply feedback (Admin)            |
| 15 | View Revenue Report (UC-15)       | Weekly, monthly, and quarterly revenue reports (Admin)                      |
| 16 | Manage Staff Account (UC-16)      | Create staff account, update staff role (Admin)                             |
| 17 | Manage User (UC-17)               | View user list, view user detail, inactive user account (Admin)             |

#### Non-Functional Testing

| No | Type                | Description                                                        |
|----|---------------------|--------------------------------------------------------------------|
| 1  | UI / Usability      | Verify UI layout, navigation, responsiveness on desktop browsers   |
| 2  | Performance          | Basic load testing on critical APIs (login, booking, search room)  |
| 3  | Security            | Role-based access control, input validation, SQL injection prevention |
| 4  | Compatibility       | Cross-browser testing (Chrome, Firefox, Edge)                      |

### b. Out of Scope

| No | Item                                  | Reason                                              |
|----|---------------------------------------|-----------------------------------------------------|
| 1  | Mobile native application testing     | System is web-based only                             |
| 2  | Third-party payment gateway internals | External service (MoMo, bank) not controlled by team |
| 3  | Infrastructure / deployment testing   | Not part of SWP391 course scope                      |
| 4  | Stress testing / disaster recovery    | Limited testing environment and timeline              |
| 5  | Automated regression test suite       | Not required for this project phase                   |

---

## IV. TEST STRATEGY

### a. Test Types

#### 1. UI Testing

| Item              | Detail                                                                                      |
|-------------------|---------------------------------------------------------------------------------------------|
| **Objective**     | Verify that all web pages render correctly, navigation works, and UI elements function as designed. |
| **Technique**     | Manual exploratory testing against UI mockups in the SDS.                                    |
| **Scope**         | All customer-facing pages (index, login, register, room search, room detail, booking, payment, booking history, profile, feedback) and admin/staff pages (dashboard, room management, booking management, feedback management, user management, staff account management, revenue report). |
| **Completion Criteria** | All pages load without errors; all buttons, links, forms, and modals function correctly; layout is consistent. |

#### 2. Function Testing

| Item              | Detail                                                                                      |
|-------------------|---------------------------------------------------------------------------------------------|
| **Objective**     | Verify all 17 use cases (UC-01 to UC-17) produce correct outputs for valid and invalid inputs. |
| **Technique**     | Decision Table Testing (for input-heavy features like Feedback, Registration), Use Case Testing (for flow-based features like Booking, Check-in/Check-out), Boundary Value Analysis, Equivalence Partitioning. |
| **Scope**         | All functional requirements per SDS use case specifications.                                 |
| **Completion Criteria** | All planned test cases executed; all critical and high-severity defects resolved.         |

#### 3. Load Testing

| Item              | Detail                                                                                      |
|-------------------|---------------------------------------------------------------------------------------------|
| **Objective**     | Verify system stability under concurrent user load for key operations.                       |
| **Technique**     | Simulate multiple concurrent users using JMeter on critical endpoints (Login, Search Room, Create Booking). |
| **Scope**         | API endpoints: POST /auth/login, GET /rooms/search, POST /bookings                          |
| **Completion Criteria** | Response time < 6 seconds under 50 concurrent users; no server errors (5xx).             |

### b. Test Levels

| Test Level       | Description                                              | Performed By         | Technique                          |
|------------------|----------------------------------------------------------|----------------------|------------------------------------|
| Unit Test        | Test individual methods in Service and Repository layers | Le Tan Loc           | JUnit 5, Mockito                   |
| Integration Test | Test Controller ↔ Service ↔ Repository interaction       | Le Tan Loc           | Spring Boot Test          |
| System Test      | End-to-end testing of complete use case flows            | Phat Dat, Thanh Dat, Anh Hao | Decision Table, Use Case Testing |
| Acceptance Test  | Validate system meets business requirements              | Nguyen Hoang Han     | Manual walkthrough with mentor     |

### c. Supporting Tools

| No | Tool Name                | Purpose                                    | License    |
|----|--------------------------|--------------------------------------------|------------|
| 1  | JUnit 5                  | Unit testing framework for Java            | Open Source |
| 2  | Mockito                  | Mocking framework for unit tests           | Open Source |
| 3  | Spring Boot Test         | Integration testing with Spring context    | Open Source |
| 4  | Google Chrome DevTools   | UI testing and debugging                   | Free        |
| 5  | Microsoft SQL Server Management Studio | Database verification and queries | Free        |
| 6  | Google Sheets            | Test case management and defect tracking   | Free        |
| 7  | Git / GitHub             | Version control and issue tracking         | Free        |

---

## V. RISKS

| No | Risk Description                                              | Probability | Impact | Mitigation Strategy                                                           |
|----|---------------------------------------------------------------|-------------|--------|-------------------------------------------------------------------------------|
| 1  | Requirements changes during testing phase                      | Medium      | High   | Freeze requirements before testing; document change requests formally          |
| 2  | Team members unavailable due to other coursework               | High        | Medium | Plan buffer time in schedule; cross-train members on multiple modules          |
| 3  | Test environment instability (SQL Server, Spring Boot server)  | Medium      | High   | Maintain local dev environments as backup; document setup steps                |
| 4  | Insufficient test data for complex booking/payment scenarios   | Medium      | Medium | Prepare test data scripts in advance; create seed data for all booking states  |
| 5  | Late delivery of features blocks system testing                | High        | High   | Prioritize critical path features (Login, Booking, Payment) for early delivery |
| 6  | Third-party payment (MoMo) sandbox unavailability              | Low         | Medium | Use mock payment responses for testing; test payment flow with stubs           |
| 7  | Defect backlog grows faster than fix rate                      | Medium      | Medium | Daily defect triage; prioritize Critical/High bugs; block release on Critical  |
| 8  | Inexperience with testing tools (JUnit)               | Medium      | Low    | Conduct tool training session (assigned to Phung Dinh Khang)                   |

---

## VI. TEST CRITERIA

### a. Entry Criteria

| No | Criteria                                                                                  |
|----|-------------------------------------------------------------------------------------------|
| 1  | SDS document (SWP392_SE1910_G02_SDS) is reviewed and approved by the team.                |
| 2  | Test Plan document is reviewed and approved.                                               |
| 3  | Development of the feature/module under test is complete (code committed to repository).   |
| 4  | Test environment is set up and accessible (Spring Boot server running, SQL Server database provisioned with schema). |
| 5  | Test data is prepared and loaded into the database.                                        |
| 6  | All critical build/compilation errors are resolved.                                        |

### b. Suspension Criteria

| No | Criteria                                                                                  |
|----|-------------------------------------------------------------------------------------------|
| 1  | More than 3 Critical (Blocker) defects are found in a single test cycle.                   |
| 2  | Test environment is unavailable for more than 1 working day.                               |
| 3  | A major requirement change invalidates more than 30% of existing test cases.               |
| 4  | The application build fails and cannot be deployed to the test environment.                 |

### c. Exit Criteria

| No | Criteria                                                                                  |
|----|-------------------------------------------------------------------------------------------|
| 1  | 100% of planned test cases have been executed.                                             |
| 2  | All Critical and High severity defects are resolved and verified.                          |
| 3  | Pass rate is ≥ 90% for all functional test cases.                                          |
| 4  | All Medium severity defects are either resolved or have an approved deferral.              |
| 5  | Test Summary Report is completed and reviewed.                                             |
| 6  | Load test results meet the defined performance criteria (< 6s response, 0% error rate under 50 users). |

---

## VII. RESOURCE PLANNING

### a. System Resources

| No | Resource                          | Specification                                           | Quantity |
|----|-----------------------------------|---------------------------------------------------------|----------|
| 1  | Development/Test PC               | Windows 10/11, Intel i5+, 8GB+ RAM, SSD                | 6        |
| 2  | Java Development Kit (JDK)        | JDK 21                                        | 6        |
| 3  | Spring Boot Application Server    | Embedded Tomcat (Spring Boot)                           | 1        |
| 4  | Microsoft SQL Server              | SQL Server 2022 (Developer Edition)                    | 1        |
| 5  | Web Browsers                      | Google Chrome (latest), Mozilla Firefox, Microsoft Edge  | 6        |
| 6  | IDE                               | IntelliJ IDEA / VS Code                                 | 6        |
| 7  | Apache JMeter                     | Version 5.6+                                            | 1        |
| 8  | Postman                           | Latest version                                          | 6        |

### b. Human Resources

| No | Name                  | Role in Testing                                    | Responsibilities                                                         |
|----|-----------------------|----------------------------------------------------|--------------------------------------------------------------------------|
| 1  | Nguyen Hoang Han      | Test Lead / Test Plan Author                       | Create Test Plan, coordinate testing, review test results, acceptance test |
| 2  | Le Tan Loc            | Unit Tester                                        | Write and execute unit tests (JUnit 5, Mockito) for Service/Repository layers |
| 3  | Nguyen Hung Phat Dat  | System Tester (Decision Table)                     | Design and execute Decision Table test cases for Feedback, Registration, Profile modules |
| 4  | Vo Thanh Dat          | System Tester (Use Case Testing)                   | Design and execute Use Case test cases for Booking flow, Check-in/Check-out |
| 5  | Vo Anh Hao            | System Tester (Use Case Testing)                   | Design and execute Use Case test cases for Booking flow, Payment, Room search |
| 6  | Phung Dinh Khang      | Testing Tools Specialist                           | Set up and demonstrate testing tools (JMeter, Postman); execute load tests |

---

## VIII. TEST ENVIRONMENT

| Component        | Specification                                                        |
|------------------|----------------------------------------------------------------------|
| **Device**       | Laptop (Windows 10/11)                                  |
| **OS**           | Windows 10 / Windows 11                                              |
| **Browser**      | Google Chrome (latest), Mozilla Firefox (latest), Microsoft Edge (latest) |
| **Network**      | Local network / Wi-Fi (university LAN)                               |
| **Database**     | Microsoft SQL Server 2022 (Developer Edition), 14 tables as per SDS |
| **Backend**      | Java 21, Spring Boot (embedded Tomcat), Spring Security, JPA/Hibernate |
| **Version Control** | Git / GitHub repository                                           |

---

## IX. SCHEDULE & ESTIMATION

| No | Task                                | Assigned To                          | Start Date  | End Date    | Effort (man-hours) |
|----|-------------------------------------|--------------------------------------|-------------|-------------|---------------------|
| 1  | Test Plan creation & review         | Nguyen Hoang Han                     | 15/02/2026  | 20/02/2026  | 16                  |
| 2  | Test case design – Unit Test        | Le Tan Loc                           | 18/02/2026  | 28/02/2026  | 30                  |
| 3  | Test case design – Decision Table   | Nguyen Hung Phat Dat                 | 18/02/2026  | 28/02/2026  | 24                  |
| 4  | Test case design – Use Case Testing | Vo Thanh Dat, Vo Anh Hao            | 18/02/2026  | 28/02/2026  | 32                  |
| 5  | Testing tools setup & training      | Phung Dinh Khang                     | 20/02/2026  | 25/02/2026  | 12                  |
| 6  | Test environment setup              | Phung Dinh Khang, Le Tan Loc         | 20/02/2026  | 22/02/2026  | 8                   |
| 7  | Unit test execution                 | Le Tan Loc                           | 01/03/2026  | 08/03/2026  | 24                  |
| 8  | System test execution – Decision Table | Nguyen Hung Phat Dat              | 01/03/2026  | 10/03/2026  | 20                  |
| 9  | System test execution – Use Case    | Vo Thanh Dat, Vo Anh Hao            | 01/03/2026  | 10/03/2026  | 28                  |
| 10 | Load test execution                 | Phung Dinh Khang                     | 08/03/2026  | 12/03/2026  | 10                  |
| 11 | Defect tracking & retesting         | All members                          | 01/03/2026  | 13/03/2026  | 16                  |
| 12 | Test Summary Report                 | Nguyen Hoang Han                     | 12/03/2026  | 15/03/2026  | 8                   |
|    | **TOTAL**                           |                                      | **15/02/2026** | **15/03/2026** | **228**          |

---

## X. TEST DELIVERABLES

### a. Before Testing Phase

| No | Deliverable                        | Description                                                  |
|----|------------------------------------|--------------------------------------------------------------|
| 1  | Test Plan                          | This document – defines scope, strategy, schedule, resources |
| 2  | Test Case Specifications           | Detailed test cases for Unit, System (Decision Table, Use Case), and Load tests |
| 3  | Test Data                          | Prepared datasets and SQL seed scripts for all test scenarios |
| 4  | Test Environment Setup Checklist   | Verified setup of Spring Boot, SQL Server, browsers, tools   |

### b. During Testing Phase

| No | Deliverable                        | Description                                                  |
|----|------------------------------------|--------------------------------------------------------------|
| 1  | Test Execution Logs                | Records of each test case execution with pass/fail status    |
| 2  | Defect Reports                     | Documented bugs with severity, steps to reproduce, screenshots |
| 3  | Daily/Weekly Test Status Reports   | Progress updates on test execution and defect metrics         |

### c. After Testing Phase

| No | Deliverable                        | Description                                                  |
|----|------------------------------------|--------------------------------------------------------------|
| 1  | Test Summary Report                | Final report with pass/fail statistics, defect summary, coverage metrics |
| 2  | Defect Summary & Trend Analysis    | Analysis of defects by module, severity, and resolution status |
| 3  | Lessons Learned                    | Documentation of challenges faced and improvements for future projects |
| 4  | Test Closure Sign-off              | Formal approval that testing phase is complete                |

---

*End of Test Plan Document*
