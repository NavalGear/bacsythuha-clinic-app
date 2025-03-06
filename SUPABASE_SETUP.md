## Supabase Setup Guide

### Row-Level Security (RLS) Policies

This section details the Row-Level Security (RLS) policies configured for the Bac sy Thu Ha Clinic database tables. These policies ensure data privacy and access control based on user roles.

#### Enable RLS on Tables

First, enable RLS on all tables:

```sql
ALTER TABLE users ENABLE ROW LEVEL SECURITY;
ALTER TABLE appointments ENABLE ROW LEVEL SECURITY;
ALTER TABLE notifications ENABLE ROW LEVEL SECURITY;
```

#### Users Table Policies

```sql
-- Allow users to read their own data
CREATE POLICY "Users can view own data" ON users
FOR SELECT USING (auth.uid() = id);

-- Allow users to update their own data
CREATE POLICY "Users can update own data" ON users
FOR UPDATE USING (auth.uid() = id);

-- Allow staff to read all patient records
CREATE POLICY "Staff can view all patient records" ON users
FOR SELECT USING (
  (SELECT role FROM users WHERE id = auth.uid()) IN ('staff', 'admin')
);

-- Allow admins full access
CREATE POLICY "Admins have full access to users" ON users
FOR ALL USING (
  (SELECT role FROM users WHERE id = auth.uid()) = 'admin'
);
```

#### Appointments Table Policies

```sql
-- Allow patients to view their own appointments
CREATE POLICY "Patients can view own appointments" ON appointments
FOR SELECT USING (
  auth.uid() = patient_id
);

-- Allow patients to create their own appointments
CREATE POLICY "Patients can create appointments" ON appointments
FOR INSERT WITH CHECK (
  auth.uid() = patient_id
);

-- Allow patients to update their own appointments
CREATE POLICY "Patients can update own appointments" ON appointments
FOR UPDATE USING (
  auth.uid() = patient_id
);

-- Allow staff to read and update all appointments
CREATE POLICY "Staff can manage all appointments" ON appointments
FOR ALL USING (
  (SELECT role FROM users WHERE id = auth.uid()) IN ('staff', 'admin')
);
```

#### Notifications Table Policies

```sql
-- Allow patients to read their own notifications
CREATE POLICY "Patients can view own notifications" ON notifications
FOR SELECT USING (
  auth.uid() = user_id
);

-- Allow staff to read and write all notifications
CREATE POLICY "Staff can manage all notifications" ON notifications
FOR ALL USING (
  (SELECT role FROM users WHERE id = auth.uid()) IN ('staff', 'admin')
);
```

### Verification Steps

After applying these policies, verify them by:

1. Testing as a patient user:
   - Should only see their own profile
   - Should only see their own appointments
   - Should only see their own notifications

2. Testing as a staff user:
   - Should see all patient records
   - Should be able to manage all appointments
   - Should be able to manage all notifications

3. Testing as an admin:
   - Should have full access to all tables

### Important Notes

- These policies assume the existence of a `role` column in the `users` table with values: 'patient', 'staff', 'admin'
- All policies are enforced at the database level
- Default deny policy is in effect when no policy explicitly allows access
- Policies are additive - if any policy grants access, the operation is allowed 