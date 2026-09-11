# 🏋️‍♂️ Flex Gym Management System
### **ITS1114 - Advanced Application Development (AAD) | 2nd Semester Final Project**

[![Java](https://img.shields.io/badge/Java-21-orange.svg?logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x%2F4.x-brightgreen.svg?logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![Spring Security](https://img.shields.io/badge/Spring%20Security-JWT-blue.svg?logo=springsecurity&logoColor=white)](https://spring.io/projects/spring-security)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-4479A1.svg?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26.svg?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-Modern%20Glassmorphism-1572B6.svg?logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E.svg?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![jQuery](https://img.shields.io/badge/jQuery-3.7.1-0769AD.svg?logo=jquery&logoColor=white)](https://jquery.com/)
[![SweetAlert2](https://img.shields.io/badge/SweetAlert2-Notifications-purple.svg)](https://sweetalert2.github.io/)

---

## 📑 Final Project Report

> [!IMPORTANT]
> ### 📖 Official Project Documentation & Report
> The complete academic project report covering system requirements, architectural designs, entity-relationship diagrams (ERD), API specifications, UI mockups, and implementation details is accessible via the link below:
> 
> 🔗 **Google Docs Final Project Report:**  
> **[https://docs.google.com/document/d/1D7bh78hsTH1o-hcSJ2iw-BM9-7cNruUXdbo-qxLYTXw/edit?usp=sharing](https://docs.google.com/document/d/1D7bh78hsTH1o-hcSJ2iw-BM9-7cNruUXdbo-qxLYTXw/edit?usp=sharing)**

---

## 📌 Executive Summary

**Flex Gym Management System** is an enterprise-level, full-stack gym and fitness club automation software designed and implemented for the **ITS1114 - Advanced Application Development (AAD)** course (2nd Semester Final Project).

The platform addresses all critical day-to-day operational requirements of fitness centers, bridging administrative management, front-desk operations, trainer routines, and member digital self-service. Built on a decoupled client-server architecture, it pairs a **Spring Boot REST API** backend with a dynamic, responsive **HTML5/CSS3/JavaScript (jQuery)** frontend powered by **JWT (JSON Web Token)** stateless security.

```
+---------------------------------------------------------------------------------------+
|                                    CLIENT BROWSER                                     |
|  +---------------------+ +----------------------+ +------------------+ +-----------+  |
|  |   Admin Dashboard   | | Receptionist Portal  | |  Trainer Portal  | |  Member    |  |
|  | (admin-dashboard)   | |(receptionist-dash..) | |(trainer-dash...) | |  Dashboard |  |
|  +---------------------+ +----------------------+ +------------------+ +-----------+  |
|  +---------------------------------------------------------------------------------+  |
|  |     Public Pages: Home (index.html), Shop, Membership, Trainers, Workouts       |  |
|  +---------------------------------------------------------------------------------+  |
+-------------------------------------------+-------------------------------------------+
                                            |
                                REST API    | AJAX Requests (JSON)
                             (JWT Bearer)   | [http://localhost:8080/api]
                                            v
+---------------------------------------------------------------------------------------+
|                                SPRING BOOT BACKEND API                                 |
|  +---------------------------------------------------------------------------------+  |
|  |                     Spring Security & JwtAuthenticationFilter                   |  |
|  +---------------------------------------------------------------------------------+  |
|  +---------------------------------------------------------------------------------+  |
|  | Controllers: Auth, Member, Membership, Attendance, Product, Order, Payment, ... |  |
|  +---------------------------------------------------------------------------------+  |
|  +---------------------------------------------------------------------------------+  |
|  | Service Layer & Business Logic | ModelMapper DTO-Entity Conversion             |  |
|  +---------------------------------------------------------------------------------+  |
|  +---------------------------------------------------------------------------------+  |
|  | Spring Data JPA Repositories  | Automated Expiry Schedulers (Daily Cron)        |  |
|  +---------------------------------------------------------------------------------+  |
+-----------------------------------+-----------------------------------+---------------+
                                    |                                   |
                                    v                                   v
                   +---------------------------------+  +-------------------------------+
                   |          MySQL DATABASE         |  |       SMTP EMAIL SERVER       |
                   |   (flex_gym_management_system)  |  |  (Gmail TLS - HTML Templates) |
                   +---------------------------------+  +-------------------------------+
```

---

## 📦 Project Packages & Repository Structure

This repository provides the complete source deliverables:

| Package Archive | Layer | Primary Technologies | Description |
|---|---|---|---|
| 🗄️ `Flex-Gym-Management-System-Backend.zip` | Backend Service | Java 21, Spring Boot, Spring Security, JPA, MySQL, JavaMail | RESTful API, database persistence, automated background tasks, email service |
| 💻 `Flex-Gym-Management-System-Frontend.zip` | Web Client | HTML5, Modern CSS3, JavaScript (ES6+), jQuery, SweetAlert2 | Responsive multi-role dashboards, landing site, e-commerce store, virtual assistant |

---

## 👥 Role-Based Access Control (RBAC)

The system enforces strict multi-role separation to ensure privacy, security, and tailored workflows:

| Role | Access Level | Target Portal | Key Capabilities |
|---|---|---|---|
| 👑 **Admin** (`ROLE_ADMIN`) | System Master | `admin-dashboard.html` | Full system control, Member/Staff management, Package configurations, Store inventory & restock alerts, Locker master, Revenue & Payment auditing, System analytics |
| 🛎️ **Receptionist** (`ROLE_RECEPTIONIST`) | Front Desk Operations | `receptionist-dashboard.html` | Member check-ins & attendance scanning, Walk-in member onboarding, Membership approvals, Locker key assignment, POS counter sales |
| 🏋️ **Trainer** (`ROLE_TRAINER`) | Fitness Management | `trainer-dashboard.html` | Client management, Custom workout program builder, Assigning routines to members, Trainee fitness metric & progress monitoring |
| 🏃 **Member** (`ROLE_MEMBER`) | Self-Service Portal | `member-dashboard.html` | Personal profile & BMI tracking, Active subscription & renewal alerts, Assigned workout plans viewer, Locker status, POS store purchase history |

---

## ✨ Core System Modules & Features

### 1. 🔐 Security & Identity Management
- **Stateless JWT Authentication:** Generates cryptographically signed Bearer tokens upon valid login.
- **BCrypt Password Encryption:** Sensitive credentials hashed using BCrypt.
- **Role-Based Authorization:** Secure route guards and backend endpoint method restrictions.
- **Smart Frontend Redirection:** Automatic routing of logged-in users to their authorized dashboard based on token claims.

### 2. 📋 Member & Subscription Lifecycle Management
- **Full Member Profiles:** Detailed personal, contact, and health metrics recording.
- **Membership Request Workflow:** Members can select packages and submit online requests, reviewed and approved/rejected by staff.
- **Multi-Tier Packages:** Custom plans with configurable duration, pricing, and facility privileges.
- **Automated Expiry Scheduler (`MembershipScheduler.java`):**
  - Daily background cron execution at midnight (`0 0 0 * * ?`).
  - Automatically identifies subscriptions expiring in **3 days** and dispatches automated reminder emails.
  - Automatically marks overdue memberships as `EXPIRED` and sends expiration notices.

### 3. ⏱️ Attendance & Check-In System
- **Quick Attendance Verification:** Front desk QR / ID scanner endpoint for instant check-in verification.
- **Attendance History Logs:** Real-time timestamps for check-in records.
- **Monthly Attendance Summaries:** Aggregated attendance statistics for members and trainers.

### 4. 🛒 Store, Inventory & POS E-Commerce
- **Product Catalog & Categorization:** Supplements, workout gear, apparel, and gym accessories.
- **Low Stock Alerts:** Automatic threshold detection (`minStock`) with front-end visual warning badges.
- **Shopping Cart & Checkout:** Multi-item cart management with localStorage state preservation.
- **Automated HTML Email Invoices:** Generates and emails itemized purchase receipts (`order-receipt.html`) directly to the member upon order placement.

### 5. 🏋️ Workout Plan Builder & Tracking
- **Workout Plan Templates:** Reusable training plans classified by difficulty levels (Beginner, Intermediate, Advanced).
- **Personalized Assignments:** Trainers assign and tailor custom routines with specific reps, sets, and rest intervals to individual members.
- **Progress Visibility:** Members can access their active daily routines directly on their portal.

### 6. 🏢 Facility Operations (Lockers & Equipment)
- **Locker Allocation System:** Real-time tracking of available, reserved, and occupied lockers with automated assignment to active memberships.
- **Gym Equipment Inventory:** Machinery tracking, maintenance schedules, and equipment condition logs.

### 7. 🤖 Interactive Public Web & Virtual Assistant
- **Modern Landing Portal (`index.html`):** Glassmorphism aesthetic, dark mode UI, smooth transitions, testimonials, and interactive pricing tables.
- **AI Chatbot (`chatbot.js`):** Embedded floating assistant answering common gym queries, membership information, and operating hours.

---

## 🛠️ Technology Stack Breakdown

### Backend Architecture
- **Language:** Java 21 (LTS)
- **Framework:** Spring Boot 4.1.0 / 3.x
- **Security:** Spring Security 6, JJWT (io.jsonwebtoken:jjwt-api:0.12.6)
- **ORM / Persistence:** Spring Data JPA, Hibernate Core
- **Database:** MySQL 8.0+
- **Object Mapping:** ModelMapper 3.2.2
- **Utilities & Boilerplate:** Project Lombok
- **Email Service:** Spring Boot Starter Mail (JavaMailSender, SMTP with TLS)
- **Task Scheduling:** Spring `@Scheduled` & `@EnableScheduling`

### Frontend Architecture
- **Markup:** HTML5 (Semantic Structure)
- **Styling:** Custom Vanilla CSS3 (Custom Properties, Dark/Neon Theme, Glassmorphism, CSS Grid & Flexbox)
- **Scripting:** JavaScript ES6+ & jQuery 3.7.1
- **Alerts & Modals:** SweetAlert2
- **Typography:** Google Fonts (`Inter`, `Poppins`)
- **Icons:** FontAwesome 6 / SVG Iconography

---

## 📡 REST API Specifications

All backend endpoints communicate via JSON and adhere to a unified response wrapper:

```json
{
  "code": 200,
  "message": "Operation Successful",
  "data": { ... }
}
```

### Key API Endpoint Routes:

| Module | Base Path | Methods | Description |
|---|---|---|---|
| **Authentication** | `/api/users` | `POST` | `/login`, `/saveUser` (Public) |
| **User Management** | `/api/users` | `GET`, `PUT`, `DELETE` | `/getAllUsers`, `/getUser/{id}`, `/updateUser`, `/deleteUser/{id}` |
| **Members** | `/api/members` | `GET`, `POST`, `PUT`, `DELETE` | `/saveMember`, `/getAllMembers`, `/getMember/{id}`, `/updateMember/{id}`, `/deleteMember/{id}` |
| **Memberships** | `/api/memberships` | `GET`, `POST`, `PUT`, `DELETE` | `/requestMembership`, `/approveMembership/{id}`, `/rejectMembership/{id}`, `/getAllPendingMemberships`, `/getAllMemberships`, `/run-expiry-check` |
| **Attendance** | `/api/attendance` | `POST`, `GET` | `/scan`, `/getAllLogs`, `/getMemberAttendance/{memberId}`, `/getMonthlySummary/{memberId}/{year}/{month}` |
| **Packages** | `/api/packages` | `GET`, `POST`, `PUT`, `DELETE` | `/savePackage`, `/getAllPackages`, `/updatePackage`, `/deletePackage/{id}` |
| **Trainers** | `/api/trainers` | `GET`, `POST`, `PUT`, `DELETE` | `/saveTrainer`, `/getAllTrainers`, `/getTrainer/{id}`, `/updateTrainer/{id}`, `/deleteTrainer/{id}` |
| **Products** | `/api/products` | `GET`, `POST`, `PUT`, `DELETE` | `/saveProduct`, `/getAllProducts`, `/getProductsByCategory/{id}`, `/getLowStockAlerts`, `/updateProduct`, `/deleteProduct/{id}` |
| **Categories** | `/api/categories` | `GET`, `POST`, `DELETE` | `/saveCategory`, `/getAllCategories`, `/deleteCategory/{id}` |
| **Orders & POS** | `/api/orders` | `POST`, `GET`, `PUT` | `/placeOrder`, `/getAllOrders`, `/getOrder/{id}`, `/getMemberOrders/{memberId}`, `/updateOrderStatus/{id}` |
| **Payments** | `/api/payments` | `POST`, `GET`, `PUT`, `DELETE` | `/savePayment`, `/getAllPayments`, `/getPayment/{id}`, `/getPaymentsByMember/{memberId}`, `/updatePaymentStatus/{id}` |
| **Workout Plans** | `/api/workout-plans` | `POST`, `GET`, `PUT`, `DELETE` | `/saveWorkoutPlan`, `/getAllWorkoutPlans`, `/getWorkoutPlan/{id}` |
| **Member Workouts** | `/api/member-workout-plans` | `POST`, `GET`, `PUT`, `DELETE` | `/assignPlan`, `/getAllPlans`, `/getPlansByMember/{memberId}`, `/updatePlan`, `/deletePlan/{id}` |
| **Lockers** | `/api/lockers` | `POST`, `GET`, `PUT`, `DELETE` | `/saveLocker`, `/getAllLockers`, `/getAvailableLockers`, `/updateLocker`, `/deleteLocker/{id}` |
| **Equipments** | `/api/equipments` | `POST`, `GET`, `PUT`, `DELETE` | `/saveEquipment`, `/getAllEquipments`, `/updateEquipment`, `/deleteEquipment/{id}` |

---

## 📁 Detailed Source Structure

```plaintext
ITS1114-AAD-2nd-Sem-Final-Project-Report/
│
├── 📄 README.md                                    # Comprehensive Master Documentation
├── 🗄️ Flex-Gym-Management-System-Backend.zip       # Spring Boot Backend Source
│   └── Flex-Gym-Management-System-Backend/
│       ├── pom.xml                                 # Maven dependencies & build configuration
│       ├── src/main/java/lk/ijse/Flex_Gym_Management_System_Backend/
│       │   ├── FlexGymManagementSystemBackendApp.java
│       │   ├── config/                             # ModelMapper, WebMvc, & App configs
│       │   ├── constant/                           # Response codes & standard messages
│       │   ├── controller/                         # 14 REST Controllers
│       │   ├── dto/                                # Data Transfer Objects
│       │   ├── entity/                             # 15 JPA Entity Models
│       │   ├── enumeration/                        # Roles & Status enums
│       │   ├── exception/                          # Global AppExceptionHandler
│       │   ├── repository/                         # Spring Data JPA Repositories
│       │   ├── scheduler/                          # MembershipScheduler (Cron tasks)
│       │   ├── security/                           # JWT Filter, Token Provider, SecurityConfig
│       │   └── service/                            # Service Interfaces & Implementations
│       └── src/main/resources/
│           ├── application.properties              # Database, JWT, & Mail configurations
│           └── html/                               # HTML Email templates (Receipt, Reminders)
│
└── 💻 Flex-Gym-Management-System-Frontend.zip      # Frontend Client Source
    └── Flex-Gym-Management-System-Frontend/
        ├── CSS/
        │   └── style.css                           # Unified glassmorphism stylesheet
        ├── JS/
        │   ├── api.js                              # Centralized AJAX API wrapper & JWT handler
        │   ├── auth.js                             # Auth utilities & role route guards
        │   ├── admin-dashboard.js                  # Admin management & metrics logic
        │   ├── receptionist-dashboard.js           # Reception desk & check-in logic
        │   ├── trainer-dashboard.js                # Trainer client & routine manager
        │   ├── member-dashboard.js                 # Member portal & progress tracking
        │   ├── cart.js, order.js, payment.js       # Store, POS, & checkout handlers
        │   ├── attendance.js, locker.js, user.js   # Service helpers
        │   ├── chatbot.js                          # Virtual assistant script
        │   └── alerts.js                           # SweetAlert2 toast & dialog wrappers
        ├── index.html                              # Public landing page
        ├── about.html, trainer.html, shop.html     # Public pages & catalog
        ├── membership.html, workout-plans.html     # Plans & guides
        ├── login.html, signup.html                 # Authentication & Registration
        ├── admin-dashboard.html                    # Admin Control Portal
        ├── receptionist-dashboard.html             # Reception Desk Portal
        ├── trainer-dashboard.html                  # Trainer Management Portal
        ├── member-dashboard.html                   # Member Self-Service Portal
        └── cart.html                               # Checkout & Cart View
```

---

## 🚀 Setup & Execution Guide

### 1. Prerequisites
- **Java Development Kit (JDK):** Version 21 or higher
- **Relational Database:** MySQL Server 8.0+
- **Build Tool:** Apache Maven 3.9+ (or included `mvnw`)
- **Web Browser:** Google Chrome, Microsoft Edge, or Mozilla Firefox
- **Web Server Tool (Recommended):** VS Code with **Live Server** extension

---

### 2. Backend Installation & Startup

1. **Extract Backend ZIP:**
   Extract `Flex-Gym-Management-System-Backend.zip` to your desired workspace directory.

2. **Configure Database Connection:**
   Open `src/main/resources/application.properties` and verify your MySQL credentials:
   ```properties
   spring.application.name=Flex-Gym-Management-System-Backend
   spring.datasource.url=jdbc:mysql://localhost:3306/flex_gym_management_system?createDatabaseIfNotExist=true
   spring.datasource.username=root
   spring.datasource.password=your_mysql_password
   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   ```

3. **Configure Mail & JWT Parameters:**
   ```properties
   spring.mail.host=smtp.gmail.com
   spring.mail.port=587
   spring.mail.username=your_email@gmail.com
   spring.mail.password=your_smtp_app_password
   spring.mail.properties.mail.smtp.auth=true
   spring.mail.properties.mail.smtp.starttls.enable=true

   jwt.secret=1affa4451895bcb7166cd38c515c67671bbfa9345a66a93f290cd6b1c22927ef650900f6604ba2aeaf40a4b146e9caff9a142876fb669143e143ef3b00bce5cbcc9368424d233406b82d723a858cacc8841c38bcfb6730de8612c74917e90327afd67ff791bea2957e05b1678553c24d87bdb13d3023515e40acdd649c531b53d9130f5460be12a8dad98c31724cb85b1793575701021090abae41460f826b35c8759088c8e2ae8e4e667821baba2a16e2886392ce7a1ce30cb0c35626abd4eb56f2657738742e769d704ebab311bde1fd2177b9f250f6bd92f4f993b745ff82b340dd5a9b833152e53f28ccd3193cc7c1bdf151471a4d122fb331713d2c05db
   jwt.expiration=86400000
   ```

4. **Build and Run Backend:**
   ```bash
   cd Flex-Gym-Management-System-Backend
   ./mvnw clean install
   ./mvnw spring-boot:run
   ```
   *The backend REST API server will boot and listen on `http://localhost:8080`.*

---

### 3. Frontend Setup & Launch

1. **Extract Frontend ZIP:**
   Extract `Flex-Gym-Management-System-Frontend.zip` to your workspace.

2. **Verify API Base URL:**
   Open `JS/api.js` to ensure the API URL points to your running backend:
   ```javascript
   const API_BASE_URL = "http://localhost:8080/api";
   ```

3. **Run using Live Server:**
   - Open the extracted folder in **Visual Studio Code**.
   - Right-click `index.html` and select **"Open with Live Server"** (or launch on `http://127.0.0.1:5500`).
   - Navigate through the landing page, register a new account (`signup.html`), or log in (`login.html`) to test role-based portals.

---

## 🧪 Quick Test Credentials & Verification

| Portal | Role | Sample Action |
|---|---|---|
| **Admin Dashboard** | `ROLE_ADMIN` | Add trainers, create membership packages, check stock restock alerts |
| **Receptionist Portal** | `ROLE_RECEPTIONIST` | Search member ID, perform check-in, assign available lockers |
| **Trainer Portal** | `ROLE_TRAINER` | View assigned members, build and assign custom workout plans |
| **Member Portal** | `ROLE_MEMBER` | Review active membership status, view workout schedule, browse shop |

---

## 📄 Academic Project Details & Submissions

- **Module:** ITS1114 - Advanced Application Development (AAD)
- **Developer:** [Chathunga Bimsara](https://github.com/chathunga2007)
- **Institution:** IJSE (Institute of Software Engineering)
- **Project Report Link:** [Google Docs Final Report](https://docs.google.com/document/d/1D7bh78hsTH1o-hcSJ2iw-BM9-7cNruUXdbo-qxLYTXw/edit?usp=sharing)

---

<p align="center">
  <b>Flex Gym Management System</b> &bull; Built with dedication for modern fitness club administration.
</p>
