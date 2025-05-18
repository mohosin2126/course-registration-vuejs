# Course Registration & Management System (CRMS)

A full-featured platform enabling seamless course registration, schedule management, and administrative control across three user roles: Student, Instructor, and Admin.

## 🎯 Project Objectives

- Provide students with a seamless course registration and management experience
- Equip instructors with tools to manage their assigned courses and communicate with students
- Enable admins to manage courses, users, and the overall system efficiently

## 👥 User Roles & Core Features

### 🔹 Student Features
- Secure Register/Login with JWT authentication
- Browse all available courses with detailed view
- Register for courses (with a max credit limit of 18 per term)
- View and manage registered courses
- Drop registered courses
- View registration history and summary
- Profile management and updates

### 🔹 Instructor Features
- View a list of assigned courses
- Post course-specific announcements and resources
- View enrolled students for each course

### 🔹 Admin Features
- Interactive dashboard (statistics on students, courses, credit usage, etc.)
- Add, edit, and delete courses (with image, description, credit hours, and price)
- Assign instructors to courses
- Manage users (student and instructor roles)
- Control course registration periods (open/close)
- View and manage all course registrations

## 🏗️ Project Architecture

### 📦 Backend
**Technology Stack:**
- Express.js
- MySQL

**Security:**
- JWT (for authentication)
- Bcrypt (for password hashing)
- express-validator (for input validation)

**ORM:**
- Sequelize or Knex.js

### 📊 Database Tables
```sql
users: User details including role
courses: Course metadata (title, description, credit, image, price)
registrations: Mapping between users and registered courses
announcements: Instructor-posted course announcements
course_assignments: Course-instructor assignments
```
### 💻 Frontend
**Technology Stack:**
- Vue 3
- Pinia (state management)
- Vue Router
- Ant Design Vue or Tailwind UI

### 📄 Key Pages
- Home/Landing Page
- Register/Login Page
- Student Dashboard
- Instructor Dashboard
- Admin Dashboard
- Course Listings
- Course Details Page
- My Courses Page
- Registration Summary
- Course Management (Admin)
- Announcement Management (Instructor)

### 🧠 State Management (Pinia Stores)
```javascript
authStore: Manages user authentication and JWT
courseStore: Manages course data
registrationStore: Handles course selection, registration, and credit tracking
```
