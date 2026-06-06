
# Project Title:
Campus Incident Reporting and Alert System (CIRAS)

## 1.0 INTRODUCTION

The Campus Incident Reporting and Alert System (CIRAS) is a web-based system designed to digitize and streamline the reporting, tracking, and resolution of incidents within a campus environment. The system provides a centralized platform where students, staff, and administrative personnel can report incidents such as security threats, infrastructural faults, health emergencies, and general complaints.
In many traditional campus environments, incident reporting is informal, delayed, and lacks proper tracking mechanisms, leading to inefficiencies in response and resolution. CIRAS addresses this challenge by introducing a structured digital workflow that ensures transparency, accountability, and timely response.
The system is designed around a role-based architecture consisting of three primary user categories: Students/Staff (reporters), Administrators (incident managers), and Response Teams (field operators). Each role interacts with the system through defined permissions and workflows.

## 2.0 PROBLEM STATEMENT
Existing campus incident reporting methods are inefficient due to:
- Lack of centralized reporting system
- Delayed response to incidents
- Poor tracking of incident resolution
- Limited accountability in handling reports

This results in unresolved incidents, reduced safety awareness, and inefficient communication between stakeholders.

## 3.0 OBJECTIVES OF THE SYSTEM
The primary objectives of CIRAS are:
1. To provide a centralized platform for incident reporting
2. To enable real-time tracking of incident status
3. To improve response time to campus incidents
4. To ensure accountability through structured workflows
5. To support role-based access and secure data handling

## 4.0 SYSTEM REQUIREMENTS
### 4.1 Functional Requirements
- User registration and authentication
- Incident submission with metadata and optional evidence upload
- Incident categorization and severity classification
- Assignment of incidents to response teams
- Incident status tracking (Pending, In Progress, Resolved)
- Notification system for updates and alerts
- Administrative dashboard for incident monitoring

### 4.2 Non-Functional Requirements
- Security through role-based access control (RBAC)
- High availability and reliability
- Scalable architecture for multiple campuses
- Data integrity and consistency
- Responsive user interface

## 5.0 SYSTEM WORKFLOW
The system operates using a lifecycle-based workflow model where each incident progresses through defined states from creation to resolution.

### 5.1 Authentication Workflow
Users authenticate using credentials. The system validates identity and assigns session tokens based on user roles. Access to system features is determined by role permissions.

## 5.2 Incident Reporting Workflow
Authenticated users submit incident reports containing title, description, category, location, and optional evidence. The system validates and stores the data, assigning a default status of “Pending Review.”

### 5.3 Incident Review Workflow
Administrators access submitted incidents, review details, and classify them based on severity and category.

### 5.4 Incident Assignment Workflow
Reviewed incidents are assigned to response teams. The system updates assignment records and changes status to “In Progress.”

### 5.5 Incident Resolution Workflow
Response teams investigate and resolve incidents. Upon completion, the incident status is updated to “Resolved,” and relevant stakeholders are notified.

### 5.6 Notification Workflow
System events trigger notifications for incident submission, assignment, updates, and resolution. Notifications are stored and displayed to relevant users.

### 5.7 Access Control Workflow
Access to system features is enforced through role-based authorization rules applied at both frontend and backend layers.

## 6.0 SYSTEM ARCHITECTURE
CIRAS will be designed using a 3-tier architecture model consisting of:

### 6.1 Presentation Layer (Frontend)
This layer handles user interaction and interface rendering. It provides dashboards for students, administrators, and response teams.

### 6.2 Application Layer (Backend)
This layer processes business logic including authentication, incident management, assignment processing, and notification handling. It exposes RESTful APIs for communication with the frontend.

### 6.3 Data Layer (Database)
This layer stores all persistent system data including user records, incidents, assignments, and notifications.

## 7.0 DATABASE DESIGN
### 7.1 Users Table
user_id (Primary Key)
full_name
email
password_hash
role (student, admin, response_team)
created_at

### 7.2 Incidents Table
incident_id (Primary Key)
title
description
category
severity
status
location
created_by (Foreign Key → Users)
created_at

### 7.3 Evidence Table
evidence_id (Primary Key)
incident_id (Foreign Key)
file_url
uploaded_at

### 7.4 Assignments Table
assignment_id (Primary Key)
incident_id (Foreign Key)
assigned_to (Foreign Key → Users)
assigned_at
status_update

### 7.5 Notifications Table
notification_id (Primary Key)
user_id (Foreign Key)
message
is_read
created_at

### 8.0 API DESIGN
Authentication
POST /api/auth/register
POST /api/auth/login
Incidents
POST /api/incidents (create incident)
GET /api/incidents (fetch incidents)
GET /api/incidents/{id} (incident details)
PATCH /api/incidents/{id} (update status)
Assignment
POST /api/incidents/assign
Notifications
GET /api/notifications

### 9.0 DATA FLOW OVERVIEW
- User submits incident via frontend
- Request is sent to backend API
- Backend validates and stores data in database
- Notification service triggers alerts
- Admin reviews and assigns incident
- Response team updates status
- System persists updates and notifies stakeholders

## 10.0 SECURITY DESIGN
The system implements the following security mechanisms:
- Role-Based Access Control (RBAC)
- Password hashing for credential storage
- Token-based authentication (session/JWT)
- Input validation and sanitization
- Restricted API endpoints based on roles

## 11.0 ASSUMPTIONS AND CONSTRAINTS
Assumptions:
- Users have access to internet-enabled devices
- Campus administration manages response teams
- Notifications are delivered via in-app system
Constraints:
- No real-time GPS tracking in initial version
- No external emergency service integration
- No AI-based classification in initial deployment

## 12.0 CONCLUSION
The Campus Incident Reporting and Alert System provides a structured and scalable approach to managing campus-related incidents. By combining role-based access control, centralized reporting, and lifecycle-based incident tracking, the system improves transparency, accountability, and response efficiency within campus environments.