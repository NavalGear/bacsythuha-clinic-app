### Tech Stack Document for Bac sỹ Thu Hà Clinic App MVP

---

#### Introduction  
The Bac sỹ Thu Hà Clinic App is a mobile and web-based platform designed for a small fertility clinic in Hai Phong, Vietnam, specializing in obstetrics, gynecology, reproductive support, and infertility treatment. The app’s MVP (Minimum Viable Product) focuses on core functionalities such as appointment scheduling, automated reminders, and basic patient information management, tailored to a local patient base with varying technological literacy. The technical architecture prioritizes simplicity, cost-effectiveness, and compliance with Vietnam’s data protection laws (Decree 13/2023/ND-CP). This document outlines the technologies, packages, dependencies, and APIs used to build the app, ensuring a secure, scalable, and user-friendly solution for both patients and clinic staff. The chosen tech stack balances ease of development with the ability to scale in future phases.

---

#### Frontend Technologies  

The frontend is split into two components: a mobile app for patients and a web-based dashboard for staff. Both prioritize simplicity, responsiveness, and accessibility for a Vietnamese-speaking audience.  

##### Patient Mobile App  
The patient-facing app is built using React Native, a cross-platform framework that allows development for both Android and iOS with a single codebase, reducing costs and development time.  
- **Framework:** React Native (version 0.74 or latest stable)  
  - Install: `npm install react-native`  
  - Docs: [React Native Documentation](https://reactnative.dev/docs/getting-started)  
- **UI Components and Styling:** NativeBase is used for pre-built, customizable UI components to ensure a consistent and user-friendly design. Styling is managed inline with React Native’s StyleSheet for simplicity.  
  - Install: `npm install native-base`  
  - Docs: [NativeBase Documentation](https://docs.nativebase.io/)  
- **Navigation:** React Navigation handles screen transitions (e.g., from dashboard to booking page). It’s lightweight and integrates seamlessly with React Native.  
  - Install: `npm install @react-navigation/native @react-navigation/stack`  
  - Additional dependencies: `npm install react-native-screens react-native-safe-area-context`  
  - Docs: [React Navigation Documentation](https://reactnavigation.org/docs/getting-started)  
- **Calendar:** React Native Calendars provides a customizable calendar for the appointment booking feature.  
  - Install: `npm install react-native-calendars`  
  - Docs: [React Native Calendars Documentation](https://github.com/wix/react-native-calendars)  

##### Staff Web Dashboard  
The staff dashboard is a web application built with React.js, offering a responsive and professional interface for managing appointments and patient data.  
- **Framework:** React.js (version 18 or latest stable)  
  - Install: `npx create-react-app staff-dashboard`  
  - Docs: [React Documentation](https://reactjs.org/docs/getting-started.html)  
- **UI Components and Styling:** Material-UI provides pre-built components for a clean and professional look, suitable for a staff-facing dashboard. Tailwind CSS is used for rapid styling and responsiveness.  
  - Install Material-UI: `npm install @mui/material @emotion/react @emotion/styled`  
  - Install Tailwind CSS: `npm install tailwindcss postcss autoprefixer`  
  - Docs: [Material-UI Documentation](https://mui.com/material-ui/getting-started/), [Tailwind CSS Documentation](https://tailwindcss.com/docs/installation)  
- **Routing:** React Router manages navigation between pages (e.g., appointments to patient information).  
  - Install: `npm install react-router-dom`  
  - Docs: [React Router Documentation](https://reactrouter.com/en/main/start/tutorial)  

---

#### Backend Technologies  

The backend is designed to be lightweight and scalable, handling data storage, user authentication, and appointment management while ensuring compliance with local data protection laws.  

- **Runtime Environment:** Node.js with Express.js provides a fast and minimal framework for building RESTful APIs to handle requests between the frontend and database.  
  - Install: `npm install express`  
  - Docs: [Express Documentation](https://expressjs.com/en/starter/installing.html)  
- **Database:** MongoDB is used for flexible, schema-less storage of patient data, appointment records, and logs. It integrates well with Node.js and supports scaling as data grows.  
  - Install MongoDB driver: `npm install mongodb`  
  - Docs: [MongoDB Node.js Driver Documentation](https://mongodb.github.io/node-mongodb-native/)  
- **Authentication:** Firebase Authentication manages user login for both patients and staff, offering secure SMS/email verification and password recovery.  
  - Install: `npm install firebase`  
  - Docs: [Firebase Authentication Documentation](https://firebase.google.com/docs/auth)  
- **API Development:** Custom REST APIs are built with Express.js to handle operations like booking appointments, retrieving patient data, and sending notifications.  
  - Example endpoint: `POST /api/appointments/book`  
- **Data Encryption:** The `crypto` module in Node.js handles AES-256 encryption for sensitive data (e.g., patient contact info).  
  - Included in Node.js core, no installation required.  
  - Docs: [Node.js Crypto Documentation %

](https://nodejs.org/api/crypto.html)  

---

#### AI and Automation Technologies  

For the MVP, AI is minimal and focuses on basic scheduling optimization (if historical data is available) and automated notifications.  

- **Notification Automation:** Firebase Cloud Messaging (FCM) sends push notifications and email reminders to patients.  
  - Included with Firebase SDK (`npm install firebase`).  
  - Docs: [Firebase Cloud Messaging Documentation](https://firebase.google.com/docs/cloud-messaging)  
- **Basic AI for Scheduling (Optional):** If historical appointment data exists, a simple time-series forecasting model (e.g., ARIMA) is implemented using Python and Scikit-learn. The model runs on a separate server and exposes predictions via a Flask API, which the Node.js backend consumes.  
  - Install Scikit-learn: `pip install scikit-learn`  
  - Install Flask: `pip install flask`  
  - Docs: [Scikit-learn Documentation](https://scikit-learn.org/stable/), [Flask Documentation](https://flask.palletsprojects.com/en/3.0.x/)  
  - Example endpoint: `GET /predict-appointments?date=YYYY-MM-DD`  

---

#### Infrastructure and Deployment  

The app is deployed on infrastructure that ensures compliance with Vietnam’s data residency laws while keeping costs low for a small clinic.  

- **Cloud Hosting:** VNG Cloud or CMC Corporation (Vietnamese cloud providers) hosts the backend, database, and static assets, ensuring data stays within Vietnam to comply with Decree 13/2023/ND-CP.  
  - Setup: Use VNG Cloud VPS or cloud storage services.  
  - Docs: [VNG Cloud Documentation](https://www.vngcloud.vn/en/docs), [CMC Corporation Cloud](https://cloud.cmc.vn/)  
- **Mobile App Deployment:** The patient app is published to Google Play Store and Apple App Store.  
  - Tools: Use Expo for React Native to simplify the build and deployment process (`npm install -g expo-cli`).  
  - Docs: [Expo Documentation](https://docs.expo.dev/)  
- **Web Dashboard Deployment:** The staff dashboard is deployed on Netlify or Vercel for simplicity and cost-effectiveness.  
  - Setup: `npm run build` and deploy via Netlify CLI (`npm install -g netlify-cli`).  
  - Docs: [Netlify Documentation](https://docs.netlify.com/), [Vercel Documentation](https://vercel.com/docs)  
- **Version Control:** Git with GitHub for collaborative development and version tracking.  
  - Setup: Initialize a Git repository (`git init`) and push to GitHub.  
  - Docs: [GitHub Documentation](https://docs.github.com/en)  
- **CI/CD Pipeline (Optional):** If budget allows, set up a basic CI/CD pipeline using GitHub Actions to automate testing and deployment.  
  - Example workflow: Run tests (`npm test`) on push, deploy to Netlify on merge to main.  
  - Docs: [GitHub Actions Documentation](https://docs.github.com/en/actions)  

---

#### Security and Compliance  

Security is critical due to the sensitive nature of patient data and Vietnam’s strict data protection laws.  

- **Data Encryption:** Use AES-256 for data at rest (via Node.js `crypto`) and HTTPS for data in transit.  
  - Ensure SSL certificates are enabled on VNG Cloud or via Let’s Encrypt.  
  - Docs: [Let’s Encrypt Documentation](https://letsencrypt.org/docs/)  
- **Access Control:** Role-based access for staff (admin vs. regular staff) is implemented in the backend using middleware in Express.js.  
  - Example: `if (user.role !== 'admin') return res.status(403).send('Access denied')`  
- **Compliance:** Patient consent for data usage is collected during registration. Data residency is ensured by using Vietnamese cloud providers. Audit logs track access to patient data.  
  - Docs: [Vietnam's Personal Data Protection Decree](https://securiti.ai/vietnam-personal-data-protection-decree/)  

---

#### Dependencies and Packages  

Below is a consolidated list of key packages and dependencies to install for the project.  

##### Frontend (Patient App)  
- `react-native`: Core framework (`npm install react-native`)  
- `native-base`: UI components (`npm install native-base`)  
- `@react-navigation/native`, `@react-navigation/stack`: Navigation (`npm install @react-navigation/native @react-navigation/stack`)  
- `react-native-screens`, `react-native-safe-area-context`: Navigation dependencies (`npm install react-native-screens react-native-safe-area-context`)  
- `react-native-calendars`: Calendar for booking (`npm install react-native-calendars`)  
- `firebase`: Authentication and notifications (`npm install firebase`)  

##### Frontend (Staff Dashboard)  
- `react`: Core framework (`npx create-react-app staff-dashboard`)  
- `@mui/material`, `@emotion/react`, `@emotion/styled`: Material-UI components (`npm install @mui/material @emotion/react @emotion/styled`)  
- `tailwindcss`, `postcss`, `autoprefixer`: Styling (`npm install tailwindcss postcss autoprefixer`)  
- `react-router-dom`: Routing (`npm install react-router-dom`)  

##### Backend  
- `express`: API framework (`npm install express`)  
- `mongodb`: Database driver (`npm install mongodb`)  
- `firebase`: Authentication (`npm install firebase`)  
- `crypto`: Encryption (built into Node.js)  

##### AI (Optional)  
- `scikit-learn`: Time-series forecasting (`pip install scikit-learn`)  
- `flask`: API for AI predictions (`pip install flask`)  

---

#### Conclusion  

The tech stack for the Bac sỹ Thu Hà Clinic App MVP is designed to balance simplicity, cost-effectiveness, and scalability while ensuring compliance with local regulations. React Native and React.js provide flexible frontends for patients and staff, respectively, while Node.js with MongoDB offers a lightweight and scalable backend. Firebase handles authentication and notifications, and Vietnamese cloud providers ensure data residency compliance. The minimal use of AI (via Python and Scikit-learn) allows for future enhancements without overcomplicating the MVP. This stack ensures the app can deliver core functionalities efficiently, with clear paths for scaling as the clinic grows.

---

#### Key Citations  
- [React Native Documentation](https://reactnative.dev/docs/getting-started)  
- [React Documentation](https://reactjs.org/docs/getting-started.html)  
- [Express Documentation](https://expressjs.com/en/starter/installing.html)  
- [MongoDB Node.js Driver Documentation](https://mongodb.github.io/node-mongodb-native/)  
- [Firebase Authentication Documentation](https://firebase.google.com/docs/auth)  
- [Firebase Cloud Messaging Documentation](https://firebase.google.com/docs/cloud-messaging)  
- [Scikit-learn Documentation](https://scikit-learn.org/stable/)  
- [VNG Cloud Documentation](https://www.vngcloud.vn/en/docs)  
- [Vietnam's Personal Data Protection Decree](https://securiti.ai/vietnam-personal-data-protection-decree/)