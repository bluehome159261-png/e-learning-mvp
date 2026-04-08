# Projet RIS — Technical Specification Document

## 1. Project Overview
**Projet RIS** (Renforcement des Capacités et Réinsertion Socio-Professionnelle des Sportifs) is a digital learning platform designed for **Fondation BEF** in Yaoundé, Cameroon. The platform aims to empower young athletes by providing them with practical digital and entrepreneurial skills, facilitating their professional transition beyond sports.

---

## 2. System Actors
| Actor | Description |
| :--- | :--- |
| **Guest / Free User** | Unauthenticated user who can browse the landing page and access limited "Free Plan" content. |
| **Student** | Authenticated athlete who enrolls in courses, completes modules, and interacts with mentors. |
| **Mentor** | Authenticated expert who creates content, hosts live sessions, and manages student progress. |
| **Admin** | System administrator who manages users, verifies mentors, and oversees platform health. |

---

## 3. Functional Requirements

### 3.1 Authentication & Authorization
- **Registration**: Students and Mentors can register. Mentors require a specific verification code (`1234567890`) for the prototype.
- **Login**: Role-based redirection to specific dashboards.
- **Access Control**: Protection of dashboard routes based on user role.

### 3.2 Student Features
- **Home Feed**: Social-style feed with updates from mentors and the platform.
- **Playbook (Learning)**: Access to enrolled course modules with progress tracking.
- **Locker Room**: Live video streaming and chat interface for real-time interaction.
- **Performance**: Visualization of learning stats and achievements.
- **Messaging**: Direct messaging with mentors.

### 3.3 Mentor Features
- **Course Management**: Create and update course modules.
- **Student Tracking**: Monitor enrollment and completion rates.
- **Live Sessions**: Initiate and manage live streams in the Locker Room.
- **Feed Management**: Post updates and announcements to the student feed.

### 3.4 Admin Features
- **User Management**: View and manage all registered users.
- **Mentor Verification**: Review and approve mentor applications.
- **Platform Analytics**: High-level overview of revenue, user growth, and engagement.

---

## 4. Data Models (Class Diagram Reference)

### 4.1 User Entity
- `id`: Unique Identifier
- `name`: Full Name
- `email`: Unique Email Address
- `password`: Hashed Password
- `role`: [Student, Mentor, Admin]
- `specialty`: (For Mentors) Area of expertise
- `created_at`: Timestamp

### 4.2 Course Entity
- `id`: Unique Identifier
- `title`: Course Title
- `description`: Detailed Description
- `mentor_id`: Foreign Key (User)
- `category`: [Tech, Business, Agriculture, etc.]
- `thumbnail`: Image URL

### 4.3 Module Entity
- `id`: Unique Identifier
- `course_id`: Foreign Key (Course)
- `title`: Module Title
- `content`: Text/Video URL
- `order`: Sequence number

### 4.4 Enrollment Entity
- `id`: Unique Identifier
- `student_id`: Foreign Key (User)
- `course_id`: Foreign Key (Course)
- `progress`: Percentage (0-100)
- `status`: [Active, Completed]

---

## 5. System Architecture
- **Frontend**: HTML5, CSS3 (Custom Properties, Flexbox/Grid), Vanilla JavaScript.
- **Backend**: PHP 8+ (PDO for database interactions).
- **Database**: MySQL.
- **Hosting**: Vercel (Frontend), InfinityFree (Backend).

---

## 6. Key Workflows (Sequence Diagram Reference)

### 6.1 Authentication Flow
1. User enters credentials on `auth.html`.
2. Frontend validates input and sends to `login.php`.
3. Backend verifies credentials against MySQL.
4. If valid, session is started and user is redirected based on `role`.

### 6.2 Mentor Verification Flow
1. User selects "Mentor" role during registration.
2. User enters the prototype passkey (`1234567890`).
3. System validates the key and creates a "Pending" mentor account.
4. Admin reviews the application in the Admin Dashboard and updates status to "Verified".

---

## 7. Design Standards
- **Mobile-First**: Optimized for 360px width (Cameroon mobile market).
- **Colors**: 
  - Primary: `#008751` (Green)
  - Secondary: `#FCD116` (Yellow)
  - Accent: `#EF3340` (Red)
- **Typography**: Montserrat (Headings), Inter (Body).
