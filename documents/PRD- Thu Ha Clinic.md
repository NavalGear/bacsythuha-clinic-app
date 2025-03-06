### Project Requirements Document (PRD) for Bac sỹ Thu Hà Clinic App MVP

---

#### App Overview

The Bac sỹ Thu Hà Clinic App is a mobile and web-based platform designed for a small fertility clinic in Hai Phong, Vietnam, specializing in obstetrics, gynecology, reproductive support, and infertility treatment. The app aims to streamline clinic operations, improve patient engagement, and enhance service quality by leveraging technology and simple AI integration. The MVP (Minimum Viable Product) focuses on core functionalities such as appointment scheduling, automated reminders, and basic patient information management, tailored to the needs of a local patient base with varying levels of technological literacy.

The primary objective of the MVP is to provide a user-friendly solution that addresses key pain points for both patients and clinic staff: scheduling inefficiencies and missed appointments. Patients will be able to book, reschedule, or cancel appointments and receive reminders, while staff can manage schedules and store basic patient data securely. Simple AI will be integrated to optimize scheduling (if data is available) and automate reminders, improving operational efficiency. The app will prioritize compliance with Vietnam’s data protection laws (Decree 13/2023/ND-CP), ensuring patient data security while maintaining a culturally sensitive and accessible design for the Hai Phong community.

The success of this MVP will be measured by its ability to reduce missed appointments, increase patient satisfaction, and improve staff efficiency in managing schedules. Future phases will build on this foundation to include advanced features like personalized health recommendations and secure messaging, but the MVP will focus on establishing a reliable and scalable base.

---

#### User Flow

##### Patient User Flow
1. **Download and Installation:**  
   - Patient downloads the app from Google Play Store or Apple App Store (or accesses via a mobile browser).  
   - Installs the app and opens it.  

2. **Registration/Login:**  
   - Patient selects “Register” and provides basic details (name, phone number, email).  
   - Agrees to data usage terms (required by Decree 13/2023/ND-CP).  
   - Receives a verification code via SMS/email to confirm identity.  
   - Logs in using phone number/email and password.  

3. **Dashboard:**  
   - Upon login, patient sees a simple dashboard with options: “Book Appointment,” “View Upcoming Appointments,” and “Profile.”  

4. **Booking an Appointment:**  
   - Selects “Book Appointment.”  
   - Views available time slots (displayed via a calendar).  
   - Chooses a slot, confirms details (e.g., purpose of visit), and submits.  
   - Receives a confirmation notification within the app.  

5. **Receiving Reminders:**  
   - Receives automated reminders (push notifications or email) 24 hours and 1 hour before the appointment.  
   - Can reschedule or cancel directly from the reminder notification.  

6. **Managing Appointments:**  
   - Goes to “View Upcoming Appointments” to see scheduled visits.  
   - Can reschedule or cancel an appointment if needed.  

##### Staff User Flow
1. **Access Dashboard:**  
   - Staff logs into a web-based dashboard using a secure URL, username, and password (with multi-factor authentication if possible).  

2. **View and Manage Appointments:**  
   - Sees a calendar view of all appointments for the day/week.  
   - Can mark appointments as “Completed,” “Missed,” or “Canceled.”  

3. **Access Patient Information:**  
   - Searches for a patient by name or phone number.  
   - Views basic details (contact info, appointment history) to facilitate communication.  

4. **Review AI Suggestions (if available):**  
   - If historical data exists, sees basic AI-driven suggestions for scheduling optimization (e.g., “High demand expected on Monday mornings”).  
   - Adjusts schedules manually based on suggestions.  

---

#### Tech Stack & APIs

##### Tech Stack
- **Frontend (Patient App):**  
  - Framework: React Native (for cross-platform mobile development, supporting both Android and iOS).  
  - UI Components: NativeBase or Material-UI for a consistent and user-friendly design.  
- **Frontend (Staff Dashboard):**  
  - Framework: React.js (for a responsive web-based dashboard).  
  - Hosting: Netlify or Vercel for easy deployment and scaling.  
- **Backend:**  
  - Language: Node.js with Express.js (for a lightweight and scalable backend).  
  - Database: MongoDB (for flexible storage of patient data and appointments).  
- **Cloud Hosting:**  
  - Provider: VNG Cloud or CMC Corporation (Vietnamese providers to comply with local data residency laws).  
  - Storage: Cloud storage for encrypted patient data.  
- **Authentication:**  
  - Firebase Authentication (for secure user login with SMS/email verification).  
- **Notifications:**  
  - Firebase Cloud Messaging (FCM) for push notifications and automated reminders.  

##### APIs
- **Calendar API:**  
  - Custom-built API to manage appointment slots and calendar synchronization (via Node.js backend).  
- **Notification API:**  
  - Firebase Cloud Messaging API for sending push notifications and email reminders.  
- **Data Encryption:**  
  - Use libraries like `crypto` (Node.js) for AES-256 encryption of sensitive data.  
- **AI Integration (if applicable):**  
  - Scikit-learn (Python) for basic time-series forecasting of appointment demand (e.g., ARIMA model).  
  - Flask API to integrate Python-based AI models with the Node.js backend.  

---

#### Core Features

##### For Patients
1. **User Registration/Login:**  
   - Register with name, phone number, email, and consent for data usage.  
   - Login with phone number/email and password, verified via SMS/email code.  

2. **Appointment Scheduling:**  
   - View available time slots on a calendar.  
   - Book, reschedule, or cancel appointments.  
   - Receive in-app confirmation after booking.  

3. **Automated Reminders:**  
   - Receive push notifications or email reminders 24 hours and 1 hour before appointments.  
   - Option to reschedule/cancel directly from reminders.  

4. **Dashboard:**  
   - Simple dashboard showing upcoming appointments and options to book or manage them.  

##### For Staff
1. **Appointment Management:**  
   - Web-based dashboard to view and manage all appointments (calendar view).  
   - Mark appointments as completed, missed, or canceled.  

2. **Basic Patient Information Storage:**  
   - Store and access basic patient details (name, phone number, email, appointment history).  
   - Searchable by name or phone number.  

3. **AI-Driven Scheduling Insights (Optional):**  
   - If historical data is available, display basic AI-driven insights (e.g., predicted busy times).  

##### General
1. **Data Security:**  
   - End-to-end encryption for data transmission and storage (AES-256).  
   - Compliance with Decree 13/2023/ND-CP for data protection.  

2. **Localization:**  
   - Interface in Vietnamese, with English as an optional language.  
   - Culturally sensitive design for Hai Phong patients.  

---

#### In-Scope vs. Out-of-Scope

##### In-Scope
- User authentication for patients and staff using Firebase Authentication (SMS/email verification).  
- Appointment scheduling with calendar view for patients and staff.  
- Automated reminders via push notifications and email using Firebase Cloud Messaging.  
- Basic patient information storage (name, contact details, appointment history) with encryption.  
- Web-based dashboard for staff to manage appointments and view patient data.  
- Simple AI integration for scheduling optimization (if historical data is available) using time-series forecasting.  
- Compliance with Vietnam’s data protection laws (Decree 13/2023/ND-CP), including data encryption and patient consent.  
- Hosting on Vietnamese cloud providers (e.g., VNG Cloud) to ensure data residency compliance.  
- Vietnamese language interface with optional English support.  

##### Out-of-Scope
- Advanced AI features like personalized health recommendations or predictive analytics for treatment outcomes (planned for later phases).  
- Secure messaging between patients and staff (to be added in the “Complete” phase).  
- Integration with third-party payment systems for online payments (not needed for MVP).  
- Mobile app analytics or advanced reporting dashboards for staff.  
- Support for multiple languages beyond Vietnamese and English.  
- Integration with external healthcare systems or EHR (Electronic Health Record) platforms.  
- Development of a full desktop application (web dashboard suffices for staff).  

---

#### Additional Notes

##### Timeline and Milestones
1. **Requirement Gathering and Planning:** 2 weeks  
   - Finalize features, tech stack, and compliance requirements.  
2. **Design and Prototyping:** 2 weeks  
   - Create wireframes and UI mockups for patient app and staff dashboard.  
3. **Development:** 6–8 weeks  
   - Build backend, frontend, and integrate APIs for scheduling and notifications.  
   - Implement basic AI if data is available.  
4. **Testing and QA:** 2 weeks  
   - Test app functionality, security, and compliance with data protection laws.  
5. **Deployment and Initial Rollout:** 1 week  
   - Deploy to app stores and web hosting, roll out to a small group of patients for feedback.  
   - Total: Approximately 13–15 weeks  

##### Success Metrics
- **Patient Adoption:** At least 50% of regular patients using the app within 3 months of launch.  
- **Missed Appointment Rate:** Reduce missed appointments by 20% within 3 months.  
- **Staff Efficiency:** Staff report reduced time spent on scheduling (e.g., via feedback surveys).  
- **Compliance:** No data breaches or violations of Decree 13/2023/ND-CP within the first 6 months.  

##### Risks and Mitigation
- **Risk:** Limited patient adoption due to low tech literacy.  
  - **Mitigation:** Provide in-clinic tutorials and a simple UI with clear instructions.  
- **Risk:** Insufficient historical data for AI scheduling optimization.  
  - **Mitigation:** Start with rule-based scheduling and collect data over time to train models.  
- **Risk:** High development costs exceeding budget.  
  - **Mitigation:** Use open-source tools and local cloud providers to minimize expenses; partner with local developers for cost-effective implementation.  
