# Qveto-Java-Team-Project-02

[![Java Version](https://img.shields.io/badge/Java-17%20%2F%2021-orange.svg)](https://adoptium.net/)
[![Build Tool](https://img.shields.io/badge/Build-Maven%20%2F%20Batch-blue.svg)](https://maven.apache.org/)
[![Database](https://img.shields.io/badge/Database-MySQL%208.x-lightgrey.svg)](https://www.mysql.com/)
[![UI Framework](https://img.shields.io/badge/UI-Java%20Swing%20(CardLayout)-green.svg)](https://docs.oracle.com/en/java/javase/21/docs/api/java.desktop/javax/swing/package-summary.html)

A desktop-based **Online Examination System** built with **Java Swing** and **MySQL** that enables administrators to configure exams and manage reusable question banks, while students take timed multiple-choice assessments with visible countdown timers, answer persistence during navigation, confirmed manual submission, and automatic timeout submission.

---

## 📌 Project Overview

Developed as part of the **Qveto Java Development Internship (Project 3: Online Examination System)** following the 4-week implementation lifecycle:
- **Week 1:** Requirements, Database Design & Application Foundation (Schema, CardLayout shell, SHA-256 Authentication, Validation)
- **Week 2:** Exam Creation, Question Bank & Student Dashboard
- **Week 3:** Timed Examination, Navigation, javax.swing.Timer Countdown & Submission Engine
- **Week 4:** Results Calculation, Exam History, Admin Reporting, Security & Packaging

---

## 🏗️ Architecture & Packages

```
src/main/java/com/qveto/exam/
├── Main.java               # Application bootstrap (Swing EventQueue EDT)
├── model/                  # POJOs and domain models
│   ├── User.java           # User entity (Admin / Student)
│   ├── Role.java           # Role enum (ADMIN, STUDENT)
│   ├── Exam.java           # Examination entity
│   ├── Question.java       # MCQ entity with 4 options and answer
│   ├── ExamAttempt.java    # Student assessment attempt
│   ├── AttemptStatus.java  # IN_PROGRESS, SUBMITTED, TIMED_OUT, ABANDONED
│   ├── SubmissionType.java # MANUAL, AUTO_TIMEOUT
│   ├── AttemptAnswer.java  # Selected option per question
│   └── ExamResult.java     # Computed score, percentage, and pass/fail
├── dao/                    # JDBC persistence layer (PreparedStatements)
│   ├── UserDAO.java        # User database operations & authentication
│   ├── ExamDAO.java        # Exam listings & paper management
│   ├── QuestionDAO.java    # Reusable question bank management
│   ├── AttemptDAO.java     # Real-time answer persistence & session updates
│   └── ResultDAO.java      # Score persistence and student history
├── service/                # Business logic & timing rules
│   ├── AuthService.java    # Authentication, registration & offline fallback
│   └── ExamService.java    # Exam catalog, grading rules & attempt initialization
├── validation/             # Validation logic
│   ├── InputValidator.java # Email format, password length, exam boundaries
│   └── ValidationResult.java # Error collection
├── util/                   # Infrastructure helpers
│   ├── DBConnection.java   # Externalized JDBC loader with diagnostic polling
│   ├── PasswordUtil.java   # SHA-256 password hashing & verification
│   ├── SessionManager.java # Thread-safe current user session store
│   └── AppConstants.java   # Theme colors, fonts, CardLayout IDs
└── ui/                     # Presentation layer (Java Swing)
    ├── MainFrame.java      # JFrame window managing CardLayout navigation
    ├── LoginPanel.java     # Sign in screen with quick demo fill buttons
    ├── RegisterPanel.java  # Student self-registration screen
    ├── AdminDashboardPanel.java   # Admin portal, question bank & candidate results reporting
    ├── StudentDashboardPanel.java # Candidate portal, catalog & assessment history
    ├── CreateExamDialog.java      # Admin modal to create & configure exams
    ├── AddQuestionDialog.java     # Admin modal to author reusable MCQs
    ├── UserProfileDialog.java     # Student & Admin profile / password management
    ├── ExamDetailsDialog.java     # Pre-exam syllabus overview & instructions modal
    ├── TimedExamPanel.java        # Active assessment with timer, navigation & palette
    ├── ExamResultPanel.java       # Graded results, pass/fail status & question review
    └── AttemptReviewDialog.java   # Modal breakdown dialog for past assessment submissions
```

---

## 🔑 Default Synthetic Credentials

| Role | Email | Password | Notes |
| :--- | :--- | :--- | :--- |
| **System Admin** | `admin@qveto.com` | `Admin@123` | Full access to exam creation & question bank |
| **Student 1** | `student1@qveto.com` | `Student@123` | Registered candidate (Aarav Patel) |
| **Student 2** | `student2@qveto.com` | `Student@123` | Registered candidate (Diya Sharma) |

*(Quick-fill buttons are provided on the login screen for instant one-click testing.)*

---

## 🗄️ Database Setup (MySQL)

1. Make sure MySQL server is running (e.g. on port `3306`).
2. Run the schema creation script:
   ```bash
   mysql -u root -p < database/schema.sql
   ```
3. Load the synthetic demo seed data:
   ```bash
   mysql -u root -p < database/seed.sql
   ```
4. Verify or customize database credentials in `src/main/resources/db.properties`:
   ```properties
   db.url=jdbc:mysql://localhost:3306/online_exam_db?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
   db.user=root
   db.password=root
   ```

> **Note:** If MySQL is not locally running, the application automatically enters **Standalone / Demo Mode**, allowing full UI testing and demonstration with synthetic in-memory accounts without throwing JDBC exceptions!

---

## 🚀 How to Run the Application

### Option A: Using the Windows Batch Script (Recommended for Quick Launch)
Simply double-click or run from PowerShell/CMD:
```cmd
run.bat
```

### Option B: Using Maven
```bash
mvn clean compile exec:java
```

---

## 🧪 Running Automated Unit Tests

### Option A: Using the Test Batch Script
```cmd
test.bat
```

### Option B: Using Maven
```bash
mvn test
```

---

## 👥 Contributors
- **Chetanreddysai** & Team
- Qveto Java Development Internship — Project 3
