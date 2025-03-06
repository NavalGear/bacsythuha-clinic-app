### App Flow Document for Bac sỹ Thu Hà Clinic App MVP

---

#### Introduction  
The Bac sỹ Thu Hà Clinic App is a mobile and web-based platform designed to streamline operations and improve patient engagement for a small fertility clinic in Hai Phong, Vietnam. The app focuses on providing core functionalities for appointment scheduling, automated reminders, and basic patient information management, catering to a local patient base with varying levels of technological literacy. For patients, the app offers a simple and accessible way to book appointments and receive reminders, while staff can manage schedules and access basic patient data securely through a web dashboard. The MVP ensures compliance with Vietnam’s data protection laws (Decree 13/2023/ND-CP) and prioritizes a user-friendly experience tailored to the cultural and linguistic needs of the Hai Phong community. This document serves as a clear map for developers, detailing how users move through the app from the landing page to every other page.

---

#### Onboarding and Sign-In/Sign-Up  

Patients first encounter the app through the Google Play Store or Apple App Store, where they download it onto their mobile devices. Upon opening the app for the first time, they land on the welcome screen, which displays the clinic’s logo, a brief tagline (“Chăm sóc sức khỏe sinh sản dễ dàng”), and two buttons: “Đăng ký” (Register) and “Đăng nhập” (Sign In).  

For new users, pressing “Đăng ký” takes them to the registration page. Here, they enter their full name, phone number, and email address into simple text fields. A checkbox requires them to agree to the app’s terms of use and data privacy policy, ensuring compliance with Decree 13/2023/ND-CP. After filling in the details, they press “Tiếp tục” (Continue), and a verification code is sent to their phone number or email (via Firebase Authentication). They enter this code on the next screen to verify their identity, then set a password. Once completed, they are redirected to the main dashboard with a welcome message (“Chào mừng đến với ứng dụng Bac sỹ Thu Hà!”).  

For returning users, pressing “Đăng nhập” on the welcome screen takes them to the login page. They enter their phone number or email and password into two text fields and press “Đăng nhập.” If they forget their password, a “Quên mật khẩu?” (Forgot Password?) link below the fields leads to a password recovery page, where they enter their phone number or email to receive a reset code. After entering the code and setting a new password, they return to the login page to sign in. Upon successful login, they are taken to the main dashboard.  

For staff, access is through a web-based dashboard. They open a browser and navigate to a secure URL (e.g., `dashboard.bacsythuha.vn`). The landing page shows a login form with fields for username and password. After entering their credentials and pressing “Đăng nhập,” they are directed to the staff dashboard. If they forget their password, a “Quên mật khẩu?” link allows them to reset it via email, following a similar verification process as patients.

---

#### Main Dashboard or Home Page  

For patients, the main dashboard appears after login. The screen is clean and minimalistic, with a white background, the clinic’s logo at the top, and a greeting (“Xin chào, [Tên bệnh nhân]”). Below the greeting, there are three main buttons in a vertical layout: “Đặt lịch hẹn” (Book Appointment), “Lịch hẹn sắp tới” (Upcoming Appointments), and “Hồ sơ” (Profile). A small notification bell icon in the top-right corner shows the number of unread reminders (e.g., “2” if there are two pending reminders). The dashboard uses simple Vietnamese text and a calming color scheme (soft blues and greens) to make navigation intuitive for users with limited tech literacy.  

For staff, the web-based dashboard opens after login. The layout features a sidebar on the left with three options: “Lịch hẹn” (Appointments), “Thông tin bệnh nhân” (Patient Information), and “Đăng xuất” (Logout). The main area displays a calendar view of all appointments for the current day by default, with options to switch to weekly or monthly views using a dropdown at the top. A search bar in the top-right corner allows staff to look up patients by name or phone number. The design uses a professional color palette (white background with blue accents) and clear fonts for easy readability.

---

#### Detailed Feature Flows and Page Transitions  

##### Patient Flows  
From the patient dashboard, pressing “Đặt lịch hẹn” leads to the booking page. This page shows a calendar (using a library like React Native Calendars) displaying the current month. Available dates are highlighted in green, and unavailable dates are grayed out. After selecting a date, a list of available time slots (e.g., “9:00 AM,” “10:00 AM”) appears below the calendar. The patient selects a time slot, then presses “Xác nhận” (Confirm). A confirmation pop-up appears, asking them to verify the date and time (“Bạn muốn đặt lịch vào [Ngày] lúc [Giờ]?”) with “Đồng ý” (Agree) and “Hủy” (Cancel) buttons. Pressing “Đồng ý” books the appointment, and they are redirected to the dashboard with a success message (“Đặt lịch thành công!”). Pressing “Hủy” returns them to the booking page.  

Pressing “Lịch hẹn sắp tới” on the dashboard takes the patient to the upcoming appointments page. This page lists all scheduled appointments in a scrollable list, each entry showing the date, time, and a status (e.g., “Đã xác nhận”). Each entry has two buttons: “Thay đổi lịch” (Reschedule) and “Hủy lịch” (Cancel). Pressing “Thay đổi lịch” takes them back to the booking page, where the previously selected slot is marked as “Đã chọn” (Selected), and they can pick a new slot. Pressing “Hủy lịch” shows a confirmation pop-up (“Bạn có chắc muốn hủy lịch không?”) with “Đồng ý” and “Không” buttons. Selecting “Đồng ý” cancels the appointment, updates the list, and shows a success message (“Đã hủy lịch!”). Selecting “Không” returns them to the list.  

Pressing the notification bell icon on the dashboard opens the reminders page. This page lists all reminders in a scrollable list, each showing the message (e.g., “Nhắc nhở: Lịch hẹn ngày [Ngày] lúc [Giờ]”), date, and time. Tapping a reminder marks it as read (the unread count decreases). Each reminder has a “Thay đổi lịch” or “Hủy lịch” button, leading to the same flows as on the upcoming appointments page.  

Pressing “Hồ sơ” on the dashboard opens the profile page. This page displays the patient’s name, phone number, and email in read-only fields. A “Chỉnh sửa” (Edit) button allows them to update their details (except phone number, which requires re-verification). After editing, they press “Lưu” (Save) to update their profile or “Hủy” to discard changes. A “Đăng xuất” (Logout) button at the bottom logs them out and returns them to the welcome screen.  

##### Staff Flows  
From the staff dashboard, selecting “Lịch hẹn” in the sidebar refreshes the main area to show the calendar view. Each appointment on the calendar is clickable, revealing details like patient name, time, and purpose. A dropdown next to each entry allows staff to mark the status as “Hoàn thành” (Completed), “Không đến” (Missed), or “Đã hủy” (Canceled). After selecting a status, they press “Cập nhật” (Update) to save changes, and the calendar updates accordingly. A “Thêm lịch hẹn” (Add Appointment) button above the calendar opens a form where staff can manually add an appointment by entering the patient’s name, phone number (to link to an existing record), date, and time. After submitting, the appointment appears on the calendar.  

Selecting “Thông tin bệnh nhân” in the sidebar loads the patient information page. This page shows a searchable list of patients, with each entry displaying the name and phone number. Using the search bar at the top, staff can enter a name or phone number to filter the list. Clicking an entry opens a detailed view, showing the patient’s name, phone number, email, and appointment history in a timeline format (e.g., “Lịch hẹn ngày [Ngày]: [Trạng thái]”). Staff can press “Quay lại” (Back) to return to the list.  

If AI-driven scheduling insights are available (based on historical data), a small “Gợi ý lịch” (Scheduling Suggestions) section appears below the calendar on the “Lịch hẹn” page. It displays basic predictions (e.g., “Thứ Hai dự kiến đông: 10 lịch hẹn”), but staff can dismiss it by pressing “Ẩn” (Hide). This section is static unless updated by the backend AI model.  

Selecting “Đăng xuất” in the sidebar logs the staff member out and returns them to the web login page.  

---

#### Conclusion  
This app flow document provides a clear and detailed map for the Bac sỹ Thu Hà Clinic App MVP, covering every page and interaction for both patients and staff. The patient app focuses on simplicity and accessibility, ensuring ease of use for a local audience, while the staff dashboard prioritizes functionality and efficiency. By avoiding complex transitions and keeping the design intuitive, the app ensures a smooth experience while laying the groundwork for future enhancements like personalized recommendations and secure messaging. Developers can use this flow to build a cohesive and user-friendly application tailored to the clinic’s needs.