### Frontend Guidelines Document for Bac sỹ Thu Hà Clinic App MVP

---

#### Introduction  
The Bac sỹ Thu Hà Clinic App is a mobile and web-based platform designed for a small fertility clinic in Hai Phong, Vietnam, specializing in obstetrics, gynecology, reproductive support, and infertility treatment. The frontend of the app plays a critical role in delivering a seamless and trustworthy user experience for both patients and clinic staff. For patients, the mobile app provides an intuitive interface for booking appointments and receiving reminders, while the staff dashboard offers a professional web-based tool for managing schedules and patient data. The design prioritizes simplicity, cultural sensitivity, and accessibility to cater to a local Vietnamese audience with varying levels of technological literacy. This document outlines the UI, styling, and design principles, along with specific guidelines for color palettes, fonts, and icons, to ensure consistency and build trust with users.

---

#### Frontend Architecture  

The frontend is divided into two interfaces: a mobile app for patients built with React Native and a web-based dashboard for staff built with React.js. Both are designed for ease of use, performance, and scalability.  

For the patient app, React Native enables cross-platform development, allowing a single codebase to support both Android and iOS devices. NativeBase provides pre-built UI components to ensure consistency across screens while maintaining a lightweight footprint. React Navigation handles screen transitions, ensuring smooth navigation between pages like the dashboard, booking, and profile screens.  

For the staff dashboard, React.js offers a responsive and modular framework for building a professional interface. Material-UI provides robust UI components tailored for a web environment, and React Router manages navigation between pages such as appointments and patient information. Tailwind CSS is used alongside Material-UI to enable rapid styling adjustments and responsive layouts.  

This architecture ensures maintainability and scalability, allowing the app to grow in future phases while keeping development manageable for a small team.  

---

#### Design Principles  

The design of the Bac sỹ Thu Hà Clinic App adheres to the following principles to ensure a consistent and trust-building user experience:  

1. **Simplicity:** The interface prioritizes minimalism to avoid overwhelming users, especially those with limited tech literacy. Clear labels, large buttons, and intuitive layouts guide users effortlessly through tasks like booking appointments or viewing schedules.  
2. **Cultural Sensitivity:** The app reflects the cultural context of Hai Phong, Vietnam, using Vietnamese as the primary language, calming colors associated with healthcare, and imagery that resonates with local patients (e.g., clinic branding).  
3. **Accessibility:** The design follows basic accessibility standards (e.g., WCAG 2.1) to ensure usability for all users, including those with visual or motor impairments. High-contrast text, tappable areas with sufficient padding, and voice-over compatibility are prioritized.  
4. **Responsiveness:** The patient app adjusts seamlessly to various screen sizes on mobile devices, while the staff dashboard is responsive across desktop and tablet browsers, ensuring usability in different contexts.  
5. **Trust and Professionalism:** The UI builds trust by maintaining a clean, professional look with consistent branding (e.g., clinic logo), error-free interactions, and secure handling of sensitive data, visually reinforced through lock icons and privacy notices.  

---

#### Styling and Theming  

Styling is managed to ensure consistency across both the patient app and staff dashboard, creating a unified visual identity that reinforces the clinic’s professionalism.  

For the patient app, React Native’s StyleSheet is used alongside NativeBase components to style elements inline and maintain a lightweight footprint. NativeBase’s theming capabilities allow customization of colors and typography to align with the clinic’s brand. For the staff dashboard, Tailwind CSS provides a utility-first approach for rapid styling, supplemented by Material-UI’s theme system for consistent component design.  

Theming is anchored by a defined color palette, typography, and icon set (detailed below), ensuring a cohesive look across all interfaces. CSS variables (for the web dashboard) and React Native’s StyleSheet constants (for the mobile app) centralize theme values, making updates straightforward.  

---

#### Component Structure  

The frontend follows a component-based architecture for reusability and scalability:  

- **Patient App (React Native):** Components are organized into a modular structure. Core components include `Button`, `Calendar`, `NotificationCard`, and `AppointmentCard`, each styled with NativeBase and custom StyleSheet properties. A `ThemeProvider` wrapper applies the global theme (colors, fonts) to all components. Screens like `DashboardScreen`, `BookingScreen`, and `ProfileScreen` compose these components into full pages.  
- **Staff Dashboard (React.js):** Components are structured hierarchically, with reusable elements like `Sidebar`, `CalendarView`, `PatientCard`, and `SearchBar`. Material-UI components (e.g., `Table`, `Button`) are customized with Tailwind CSS classes for flexibility. A global `ThemeProvider` from Material-UI applies the theme across the app, ensuring consistency. Pages like `AppointmentsPage` and `PatientInfoPage` assemble these components into functional views.  

This structure ensures that updates to styles or functionality can be applied globally without breaking individual pages, supporting maintainability for a small development team.  

---

#### Color Palettes  

The color palette is designed to evoke trust, calmness, and professionalism, aligning with healthcare aesthetics while being approachable for Vietnamese users.  

- **Primary Color (Soft Blue):** Used for buttons, headers, and interactive elements to signify trust and reliability.  
  - Hex: `#4A90E2`  
  - RGB: `74, 144, 226`  
- **Secondary Color (Light Green):** Used for success messages, confirmations (e.g., appointment booked), and accents to convey positivity and health.  
  - Hex: `#50C878`  
  - RGB: `80, 200, 120`  
- **Background Color (White):** Provides a clean backdrop for all screens to enhance readability.  
  - Hex: `#FFFFFF`  
  - RGB: `255, 255, 255`  
- **Neutral Gray (Light Gray):** Used for borders, dividers, and secondary text to maintain a clean hierarchy without distraction.  
  - Hex: `#E0E0E0`  
  - RGB: `224, 224, 224`  
- **Error Color (Soft Red):** Used for error messages and alerts to grab attention without being alarming.  
  - Hex: `#FF6B6B`  
  - RGB: `255, 107, 107`  
- **Text Color (Dark Gray):** Ensures high contrast for readability on light backgrounds.  
  - Hex: `#333333`  
  - RGB: `51, 51, 51`  

For accessibility, all color combinations meet WCAG 2.1 contrast ratios (e.g., text-to-background ratio of at least 4.5:1). These colors are defined as variables in the app’s theme configuration (e.g., `const COLORS = { primary: '#4A90E2', ... }` in React Native, or CSS variables like `--primary: #4A90E2` in the web dashboard).  

---

#### Fonts  

Typography is chosen for clarity and cultural familiarity, ensuring text is readable and approachable for Vietnamese users.  

- **Primary Font (Patient App):** Roboto is used for its clean, modern look and excellent support for Vietnamese diacritics. It’s widely available and optimized for mobile screens.  
  - Weights: Regular (400), Medium (500), Bold (700)  
  - Usage: Body text (Regular), headings (Medium/Bold), buttons (Medium)  
  - Install: Available by default in React Native or via `@fontsource/roboto` for web (`npm install @fontsource/roboto`)  
  - Docs: [Roboto on Google Fonts](https://fonts.google.com/specimen/Roboto)  

- **Primary Font (Staff Dashboard):** Open Sans complements Roboto for the web dashboard, offering a professional yet friendly appearance with good Vietnamese support.  
  - Weights: Regular (400), SemiBold (600), Bold (700)  
  - Usage: Body text (Regular), headings (SemiBold/Bold), table headers (SemiBold)  
  - Install: `npm install @fontsource/open-sans`  
  - Docs: [Open Sans on Google Fonts](https://fonts.google.com/specimen/Open+Sans)  

- **Font Sizes:**  
  - Headings: 20px (mobile), 24px (web)  
  - Body Text: 16px (mobile), 14px (web)  
  - Small Text (e.g., captions): 12px (mobile), 12px (web)  
  - Line Height: 1.5 for body text, 1.2 for headings  
  - These sizes ensure readability on small screens while maintaining a professional look on larger displays.  

Vietnamese diacritics are fully supported by both fonts, ensuring proper rendering of text like “Hải Phòng” or “Bác sỹ Thu Hà.” Font sizes and weights are applied consistently via the app’s theme configuration to maintain typographic hierarchy.  

---

#### Icons  

Icons enhance usability by providing visual cues for actions, making navigation intuitive. A single icon set ensures consistency across the app.  

- **Icon Set:** Material Icons (from Google’s Material Design) are used for their simplicity, recognizability, and extensive library. They’re optimized for both mobile and web environments.  
  - Install (React Native): `npm install @expo/vector-icons` (if using Expo) or `npm install react-native-vector-icons`  
  - Install (React.js): `npm install @mui/icons-material`  
  - Docs: [Material Icons Documentation](https://mui.com/material-ui/material-icons/), [Expo Vector Icons](https://icons.expo.fyi/)  
- **Usage Examples:**  
  - Calendar icon (`calendar_today`) for booking screens  
  - Bell icon (`notifications`) for reminders  
  - Person icon (`person`) for profile screens  
  - Search icon (`search`) for staff dashboard search bar  
  - Checkmark icon (`check_circle`) for confirmations  
- **Icon Sizes:**  
  - Default: 24px (mobile), 20px (web)  
  - Larger (e.g., for buttons): 32px (mobile), 24px (web)  
- **Icon Colors:** Icons use the primary color (`#4A90E2`) for active states, neutral gray (`#E0E0E0`) for inactive states, and error red (`#FF6B6B`) for alerts.  

Icons are applied consistently across all components (e.g., `IconButton` in NativeBase or Material-UI) to ensure a cohesive visual language.  

---

#### Additional UI Guidelines  

- **Buttons:** Primary buttons (e.g., “Đặt lịch”) use the primary color (`#4A90E2`) with white text, rounded corners (8px radius), and a minimum touch area of 48x48px for accessibility. Secondary buttons (e.g., “Hủy”) use a light gray background (`#E0E0E0`) with dark gray text (`#333333`).  
- **Forms:** Input fields have a light gray border (`#E0E0E0`), rounded corners (4px radius), and placeholder text in a slightly lighter gray (`#666666`). Labels are positioned above fields for clarity.  
- **Spacing:** Consistent padding and margins (8px for small elements, 16px for sections) create breathing room and prevent a cluttered look.  
- **Error States:** Errors (e.g., “Invalid time slot”) are displayed in red (`#FF6B6B`) below the relevant field with a small warning icon (`error_outline`).  
- **Loading States:** A simple spinner (using the primary color) appears during loading actions like booking an appointment, centered on the screen with a semi-transparent overlay.  
- **Branding:** The clinic’s logo appears in the top-left corner of all screens (patient app) and the sidebar (staff dashboard). The logo is scaled to 40px height on mobile and 48px on web for visibility without overpowering the layout.  

---

#### Conclusion  

The frontend guidelines for the Bac sỹ Thu Hà Clinic App ensure a consistent, user-friendly, and trust-building experience for both patients and staff. By adhering to principles of simplicity, cultural sensitivity, and accessibility, the app meets the needs of its Vietnamese audience while maintaining a professional healthcare aesthetic. The defined color palette, typography, and icon set create a cohesive visual identity, while the component structure and styling approach enable scalability and maintainability. These guidelines provide a clear blueprint for developers to build an interface that fosters trust and encourages adoption among users.

---

#### Key Citations  
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/standards-guidelines/wcag/)  
- [Roboto on Google Fonts](https://fonts.google.com/specimen/Roboto)  
- [Open Sans on Google Fonts](https://fonts.google.com/specimen/Open+Sans)  
- [Material Icons Documentation](https://mui.com/material-ui/material-icons/)  
- [NativeBase Documentation](https://docs.nativebase.io/)  
- [Material-UI Documentation](https://mui.com/material-ui/getting-started/)  
- [Tailwind CSS Documentation](https://tailwindcss.com/docs/installation)