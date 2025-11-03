# JVBE__BT_SQL
CODE SESSION 3:

```
-- Bảng Khoa (Department)
CREATE TABLE Departments (
    department_id SERIAL PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL,
    location VARCHAR(100)
);

-- Bảng Bác sĩ (Doctor)
CREATE TABLE Doctors (
    doctor_id SERIAL PRIMARY KEY,
    doctor_name VARCHAR(100) NOT NULL,
    specialization VARCHAR(100),
    phone VARCHAR(20),
    department_id INT REFERENCES Departments(department_id)
        ON DELETE SET NULL
);

-- Bảng Bệnh nhân (Patient)
CREATE TABLE Patients (
    patient_id SERIAL PRIMARY KEY,
    patient_name VARCHAR(100) NOT NULL,
    gender VARCHAR(10),
    birth_date DATE,
    phone VARCHAR(20),
    address VARCHAR(150)
);

-- Bảng Hồ sơ khám bệnh (Medical Record)
CREATE TABLE MedicalRecords (
    record_id SERIAL PRIMARY KEY,
    patient_id INT NOT NULL REFERENCES Patients(patient_id)
        ON DELETE CASCADE,
    doctor_id INT NOT NULL REFERENCES Doctors(doctor_id)
        ON DELETE SET NULL,
    diagnosis TEXT NOT NULL,
    treatment TEXT,
    record_date DATE DEFAULT CURRENT_DATE
);

```
