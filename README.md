# Student Attendance Management System

A production-style, full-stack **Student Attendance Management System** built with **Java (Spring Boot 3)**, **MySQL / H2 Database**, **Spring Security & JWT**, and **HTML5, CSS3, JavaScript, Chart.js & Axios**.

Features include student biodata management, parent/guardian records, class management, backend network-verified attendance marking, automatic daily parent SMS/WhatsApp notifications, timetable, notes, classwork, announcements, PDF & Excel export, audit logs, and a role-aware AI Assistant.

---

## 🚀 Key Features & Modules

1. **Role-Based Access Control (RBAC)**
   - **ADMIN**: Complete system control, student biodata, class management, parent details, audit logs, report generation, network settings.
   - **TEACHER**: Assigned class management, student view, manual attendance entry, post notes/study material/classwork.
   - **STUDENT**: Profile view, self-mark attendance with network check, attendance history & calendar, timetable, notes, AI assistant.

2. **Complete Student Biodata & Parent Database**
   - Detailed personal, academic, address & linked parent/guardian records.
   - Multiple emergency contacts & strict role-based access privacy.

3. **Backend Network-Verified Attendance Marking**
   - Inspects client request IP / headers against configured college subnets (e.g. `192.168.1.0/24`, `10.0.0.0/16`, `127.0.0.1`).
   - Prevents duplicate attendance for the same (Student + Subject + Session + Date).

4. **Automatic Daily Parent Attendance Notifications**
   - Pluggable `NotificationService` interface (`MockNotificationService`, `TwilioNotificationService`, `WebhookNotificationService`).
   - Dispatches status-specific template messages to registered parent phone numbers:
     - **PRESENT**: `"Dear Parent/Guardian, your ward Rahul Kumar was marked PRESENT for 2026-09-27."`
     - **ABSENT**: `"Dear Parent/Guardian, your ward Rahul Kumar was marked ABSENT on 2026-09-27. Please contact the institution if necessary."`
     - **LATE**: `"Dear Parent/Guardian, your ward Rahul Kumar was marked LATE on 2026-09-27."`
     - **LOW ATTENDANCE**: `"Dear Parent/Guardian, your ward Rahul Kumar's attendance is 68.5%, below the required 75% threshold."`

5. **PDF & Excel Report Generation**
   - **PDF**: Generated via OpenPDF with college header, student summary, attendance logs, and statistics.
   - **Excel**: Generated via Apache POI (`.xlsx`) with auto-sized columns and formatted status cells.

6. **Role-Aware AI Assistant**
   - Embedded floating AI assistant widget handling natural language queries tailored for Student, Teacher, and Admin roles.

---

## 🛠️ Technology Stack

- **Frontend**: HTML5, CSS3 (Vanilla CSS with Dark/Light Glassmorphism), JavaScript (ES6+), Chart.js, Axios.
- **Backend**: Java 17, Spring Boot 3.2.3, Spring Security, JWT (jjwt), JPA / Hibernate, OpenPDF, Apache POI.
- **Database**: H2 (In-Memory for instant out-of-the-box run) & MySQL 8.x ready (`application-mysql.yml`).

---

## 🔑 Quick Demo Credentials

| Role | Username | Password |
|---|---|---|
| **Admin** | `admin` | `admin123` |
| **Teacher** | `teacher1` | `teacher123` |
| **Student** | `student1` | `student123` |

---

## 🖥️ How to Run the Project

### Step 1: Run Spring Boot Backend

Using Maven or the provided launcher:
```bash
cd backend
mvn spring-boot:run
```
*(Or use `java -jar target/attendance-system-1.0.0.jar` if built).*

The backend starts on `http://localhost:8080`.
H2 Console is accessible at `http://localhost:8080/h2-console` (JDBC URL: `jdbc:h2:mem:attendancedb`, User: `sa`, Password: `password`).

### Step 2: Open Frontend Application

Open `frontend/index.html` directly in any web browser, or serve it using any HTTP server:
```bash
npx serve frontend
```

---

## 🗄️ MySQL Production Deployment

To connect to a real MySQL instance instead of H2:
1. Create a MySQL database: `CREATE DATABASE attendance_db;`
2. Run backend with the MySQL profile:
   ```bash
   mvn spring-boot:run -Dspring-boot.run.profiles=mysql
   ```
   Or set `SPRING_PROFILES_ACTIVE=mysql`.

---

## 📁 Project Structure

```
IP Studentt Attendance management System/
├── backend/
│   ├── pom.xml
│   └── src/
│       ├── main/
│       │   ├── java/com/college/attendance/
│       │   │   ├── config/ (SecurityConfig, JwtUtils, JwtAuthFilter)
│       │   │   ├── controller/ (Auth, Student, Attendance, Class, Notif, Report, Audit, AI)
│       │   │   ├── entity/ (User, Student, ParentGuardian, ClassEntity, Attendance, etc.)
│       │   │   ├── repository/ (*Repository)
│       │   │   ├── service/ (AttendanceService, NotificationService, AiAssistantService, AuditService)
│       │   │   ├── util/ (NetworkUtils, PdfReportGenerator, ExcelReportGenerator)
│       │   │   └── seed/ (DataInitializer)
│       │   └── resources/
│       │       ├── application.yml
│       │       └── application-mysql.yml
├── frontend/
│   ├── index.html
│   ├── css/
│   │   └── style.css
│   └── js/
│       ├── config.js
│       ├── api.js
│       ├── auth.js
│       ├── dashboards.js
│       ├── ai-assistant.js
│       └── app.js
└── README.md
```
