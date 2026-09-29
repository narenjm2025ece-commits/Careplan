# CarePlan - Elderly Medicine Reminder Tracker

## 1. Requirements

Install:
- JDK 17
- Maven
- MySQL
- VS Code with Extension Pack for Java

## 2. MySQL

Make sure MySQL Server is running.

You do NOT need to manually create the database.

The application uses:
`createDatabaseIfNotExist=true`

So the `careplan` database will be created automatically if your MySQL user has permission.

## 3. Enter your MySQL password

Open:

`src/main/resources/application.properties`

Set the `DB_PASSWORD` environment variable in the terminal before running the application.

PowerShell:

`$env:DB_PASSWORD="your_mysql_password"`

Command Prompt:

`set DB_PASSWORD=your_mysql_password`

Do not commit your database password.

## 4. Run

Open the terminal in the folder containing `pom.xml`.

Run:

`mvn spring-boot:run`

When successful, you should see:

`Started CarePlanApplication`

The API runs at:

`http://localhost:8080`

## 5. Main API endpoints

Create patient:
POST /api/patients

Create medicine:
POST /api/patients/{patientId}/medicines

Create schedule:
POST /api/medicines/{medicineId}/schedules

Generate today's doses:
GET /api/patients/{patientId}/doses/today

Mark taken:
PUT /api/doses/{doseLogId}/taken

Mark missed:
PUT /api/doses/{doseLogId}/missed

Missed history:
GET /api/patients/{patientId}/doses/missed?from=2026-09-01&to=2026-09-30

Overdue doses:
GET /api/patients/{patientId}/doses/overdue

## 6. Important business rules

- A dose belongs to a specific schedule, date and scheduled time.
- The same scheduled dose cannot be created twice.
- A TAKEN dose cannot be marked TAKEN again.
- A TAKEN dose cannot be changed to MISSED.
- A MISSED dose cannot be changed to TAKEN.
- Invalid input returns HTTP 400.
- Missing resources return HTTP 404.
- A dose is considered overdue when it is still PENDING and its scheduled time was more than one hour ago.
