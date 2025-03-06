### Backend Structure Document for Bac sỹ Thu Hà Clinic App MVP

---

#### Introduction  
The backend of the Bac sỹ Thu Hà Clinic App is designed to support a mobile and web-based platform for a small fertility clinic in Hai Phong, Vietnam, specializing in obstetrics, gynecology, reproductive support, and infertility treatment. The backend ensures secure user authentication, efficient data storage, and reliable management of appointments and patient information for the MVP (Minimum Viable Product). It provides the foundation for core functionalities like appointment scheduling, automated reminders, and basic patient data management, while prioritizing compliance with Vietnam’s data protection laws (Decree 13/2023/ND-CP). The backend is built to be simple, cost-effective, and scalable, allowing the clinic to expand features in future phases while maintaining performance and security for a local Vietnamese audience.

---

#### Backend Architecture  

The backend architecture leverages Supabase as the primary backend service, providing a modern, open-source solution for database management, authentication, and storage. Supabase is chosen for its ease of use, PostgreSQL-based database (which AI can easily understand and query), and built-in features like real-time updates and row-level security. This setup ensures the backend can handle the clinic’s needs efficiently while keeping development manageable for a small team.  

The architecture consists of a Node.js server with Express.js for handling custom API endpoints, integrated with Supabase for core backend services. Supabase manages user authentication, the PostgreSQL database for structured data storage, and file storage for any future needs (though not utilized in the MVP). The Node.js server acts as a middleware layer, facilitating secure communication between the frontend (patient app and staff dashboard) and Supabase, and enabling custom logic like notification triggers or basic AI-driven scheduling insights if data permits.  

This design ensures scalability for future enhancements (e.g., advanced analytics, secure messaging) and maintains compliance with local data residency requirements by hosting on Vietnamese cloud providers like VNG Cloud or CMC Corporation.

---

#### Database Management  

The Bac sỹ Thu Hà Clinic App uses Supabase’s PostgreSQL database for structured data storage, ensuring organized and efficient management of users, appointments, and notifications. PostgreSQL is chosen for its reliability, support for complex queries, and compatibility with Supabase’s real-time features. Row-level security (RLS) is enabled to restrict access to sensitive data, ensuring compliance with Decree 13/2023/ND-CP.

##### Database Tables  
Below are the key tables designed for the MVP, along with their schemas. Each table includes columns for essential data and relationships where applicable.  

1. **Users Table**  
   Stores information for both patients and staff. Patients and staff are differentiated by a `role` column.  
   ```sql
   CREATE TABLE users (
       id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
       email VARCHAR(255) UNIQUE,
       phone VARCHAR(20) UNIQUE,
       name VARCHAR(255) NOT NULL,
       password_hash TEXT, -- Hashed password (managed by Supabase Auth)
       role VARCHAR(20) NOT NULL CHECK (role IN ('patient', 'staff', 'admin')), -- Role-based access
       created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
       updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
   );
   ```
   - **Notes:** Supabase Auth manages user authentication, but this table stores additional profile data. `password_hash` is populated by Supabase Auth for security. RLS ensures patients can only access their own data, staff can access patient data, and admins have full access.  

2. **Appointments Table**  
   Stores appointment data, linking to the `users` table for patients and staff.  
   ```sql
   CREATE TABLE appointments (
       id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
       patient_id UUID REFERENCES users(id) ON DELETE CASCADE,
       staff_id UUID REFERENCES users(id) ON DELETE SET NULL,
       appointment_date TIMESTAMP WITH TIME ZONE NOT NULL,
       status VARCHAR(20) NOT NULL CHECK (status IN ('pending', 'confirmed', 'completed', 'missed', 'canceled')),
       purpose TEXT, -- Optional field for appointment purpose (e.g., "Consultation")
       created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
       updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
   );
   ```
   - **Notes:** `patient_id` links to the user making the appointment, while `staff_id` optionally links to the assigned staff member. `status` tracks the appointment lifecycle. RLS restricts patients to viewing their own appointments and staff to viewing assigned or all appointments (based on role).  

3. **Notifications Table**  
   Stores reminders and notifications sent to patients (e.g., appointment reminders).  
   ```sql
   CREATE TABLE notifications (
       id UUID PRIMARY KEY DEFAULT uuid_generate_v4(),
       user_id UUID REFERENCES users(id) ON DELETE CASCADE,
       appointment_id UUID REFERENCES appointments(id) ON DELETE CASCADE,
       message TEXT NOT NULL, -- e.g., "Reminder: Appointment on [Date] at [Time]"
       type VARCHAR(20) NOT NULL CHECK (type IN ('push', 'email')),
       status VARCHAR(20) NOT NULL CHECK (status IN ('pending', 'sent', 'failed')),
       scheduled_at TIMESTAMP WITH TIME ZONE NOT NULL,
       sent_at TIMESTAMP WITH TIME ZONE,
       created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP
   );
   ```
   - **Notes:** `user_id` links to the recipient (patient), and `appointment_id` links to the related appointment. `scheduled_at` defines when the notification should be sent (e.g., 24 hours before). RLS ensures users can only see their own notifications.

##### Row-Level Security (RLS) Policies  
Supabase’s RLS ensures data privacy:  
- **Users Table:** Patients can read/update their own record (`SELECT/UPDATE WHERE id = auth.uid()`). Staff can read all patient records but not modify them. Admins have full access.  
- **Appointments Table:** Patients can read/write their own appointments (`SELECT/INSERT/UPDATE WHERE patient_id = auth.uid()`). Staff can read/update appointments they’re assigned to or all appointments (for admins).  
- **Notifications Table:** Patients can read their own notifications (`SELECT WHERE user_id = auth.uid()`). Staff can read/write notifications for patients they manage.

---

#### API Design and Endpoints  

The backend uses a RESTful API design, implemented with Node.js and Express.js, to facilitate communication between the frontend and Supabase. Supabase’s built-in REST API is used for most CRUD operations, while custom endpoints in Node.js handle specific logic (e.g., triggering notifications, basic AI predictions).  

##### Supabase REST API  
Supabase auto-generates REST endpoints for database tables. Examples:  
- **Get User Profile:** `GET /rest/v1/users?id=eq.{user_id}&select=*`  
  - Headers: `Authorization: Bearer {token}`  
- **Create Appointment:** `POST /rest/v1/appointments`  
  - Body: `{ "patient_id": "uuid", "appointment_date": "2025-03-07T09:00:00+07:00", "status": "pending" }`  
  - Headers: `Authorization: Bearer {token}`  
- **Get Notifications:** `GET /rest/v1/notifications?user_id=eq.{user_id}&select=*`  
  - Headers: `Authorization: Bearer {token}`  

##### Custom Node.js Endpoints  
Custom endpoints are implemented for logic not covered by Supabase’s API:  
1. **Schedule Notification:** `POST /api/notifications/schedule`  
   - Body: `{ "appointment_id": "uuid", "user_id": "uuid", "scheduled_at": "2025-03-06T09:00:00+07:00" }`  
   - Logic: Inserts a notification into the `notifications` table and schedules it using a job queue (e.g., Node-cron). Sends via Firebase Cloud Messaging (FCM) when triggered.  
2. **Predict Appointment Demand (Optional):** `GET /api/predict-appointments`  
   - Query: `?date=2025-03-07`  
   - Logic: Calls a Python-based AI model (e.g., ARIMA) via a Flask API, returns predicted demand (e.g., “10 appointments expected”).  
3. **Update Appointment Status:** `PATCH /api/appointments/:id/status`  
   - Body: `{ "status": "completed" }`  
   - Logic: Updates the appointment status in Supabase and triggers a notification if needed.

---

#### Authentication  

Authentication is managed by Supabase Auth, which provides secure user management with email/phone login, password recovery, and token-based access.  

- **Setup:** Supabase Auth is configured to support email and phone login with SMS OTP for patients and email/password for staff.  
  - Enable in Supabase Dashboard: Settings > Authentication > Providers.  
- **Patient Flow:** Patients sign up with their phone number or email, verify via SMS OTP or email link, and receive a JWT token. The token is sent with API requests (`Authorization: Bearer {token}`).  
- **Staff Flow:** Staff use email/password login with optional multi-factor authentication (MFA) for added security. Admins can manage staff accounts via Supabase’s admin API.  
- **Security:** Supabase Auth hashes passwords and provides JWT tokens for session management. RLS policies ensure users only access their own data.

---

#### Storage  

For the MVP, file storage is not heavily utilized, as the focus is on appointment and user data. However, Supabase Storage is set up for potential future use (e.g., storing patient documents or staff reports).  

- **Setup:** Enable Supabase Storage in the dashboard and create a bucket named `clinic-files`.  
- **Access Control:** Use bucket-level permissions to restrict access (e.g., only admins can upload/view files).  
- **Example Use:** If needed, staff could upload a PDF report via the dashboard (`POST /storage/v1/object/clinic-files/{filename}`) and retrieve it (`GET /storage/v1/object/clinic-files/{filename}`).  

---

#### Hosting Solutions  

The backend is hosted on Vietnamese cloud providers to ensure compliance with local data residency laws (Decree 13/2023/ND-CP):  

- **Primary Hosting:** VNG Cloud or CMC Corporation hosts the Node.js server, Supabase instance (if self-hosted), and database.  
  - Setup: Use VNG Cloud VPS for Node.js and Supabase (or Supabase’s managed cloud if self-hosting isn’t required).  
  - Docs: [VNG Cloud Documentation](https://www.vngcloud.vn/en/docs), [CMC Corporation Cloud](https://cloud.cmc.vn/)  
- **Scalability:** VNG Cloud provides auto-scaling options for traffic spikes, though the MVP expects low to moderate usage.  
- **Security:** SSL certificates are enabled via Let’s Encrypt for HTTPS. Firewall rules restrict access to the database (only the Node.js server can connect).  
- **Backup:** Daily backups of the PostgreSQL database are configured via Supabase or VNG Cloud’s backup tools to prevent data loss.  

---

#### Additional Notes  

##### Job Scheduling  
For automated reminders, a job scheduler like Node-cron is used to check the `notifications` table periodically and send pending notifications via Firebase Cloud Messaging (FCM).  
- Install: `npm install node-cron`  
- Example: Check every minute for pending notifications (`cron.schedule('* * * * *', ...)`).  

##### Error Handling  
The backend includes middleware in Express.js to handle errors (e.g., `res.status(500).json({ error: "Internal server error" })`). Supabase API errors are logged for debugging.  

##### Logging  
Basic logging is implemented using Winston to track API requests, errors, and database operations.  
- Install: `npm install winston`  
- Docs: [Winston Documentation](https://github.com/winstonjs/winston)  

---

#### Conclusion  

The backend structure for the Bac sỹ Thu Hà Clinic App MVP provides a reliable, secure, and scalable foundation for managing appointments, user data, and notifications. Supabase simplifies database management, authentication, and storage, while a Node.js server adds flexibility for custom logic. The PostgreSQL database ensures structured data storage with robust security via RLS, and hosting on Vietnamese providers guarantees compliance with local laws. This setup supports the MVP’s core needs while allowing for future enhancements like advanced AI analytics or secure messaging, ensuring the clinic can grow its digital capabilities over time.

---

#### Key Citations  
- [Supabase Documentation](https://supabase.com/docs)  
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)  
- [Express Documentation](https://expressjs.com/en/starter/installing.html)  
- [Firebase Cloud Messaging Documentation](https://firebase.google.com/docs/cloud-messaging)  
- [VNG Cloud Documentation](https://www.vngcloud.vn/en/docs)  
- [Vietnam's Personal Data Protection Decree](https://securiti.ai/vietnam-personal-data-protection-decree/)  
- [Node-cron Documentation](https://github.com/node-cron/node-cron)  
- [Winston Documentation](https://github.com/winstonjs/winston)