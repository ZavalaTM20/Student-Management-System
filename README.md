# Student-Management-System from Class

CREATE DATABASE StudentManagement;
USE StudentManagement;

CREATE TABLE Students (
    student_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE,
    gender ENUM('Male', 'Female', 'Other'),
    email VARCHAR(100) UNIQUE,
    phone_number VARCHAR(15),
    address VARCHAR(255)
);
CREATE TABLE Courses (
    course_id INT AUTO_INCREMENT PRIMARY KEY,
    course_name VARCHAR(100) NOT NULL,
    course_code VARCHAR(20) UNIQUE NOT NULL,
    course_description TEXT,
    credit_hours INT
);
CREATE TABLE Faculty (
    faculty_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(100) UNIQUE,
    department VARCHAR(50),
    phone_number VARCHAR(15)
);
CREATE TABLE Enrollments (
    enrollment_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    enrollment_date DATE,
    grade VARCHAR(5),
    FOREIGN KEY (student_id) REFERENCES Students(student_id),
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);
CREATE TABLE Faculty_Courses (
    faculty_course_id INT AUTO_INCREMENT PRIMARY KEY,
    faculty_id INT,
    course_id INT,
    semester VARCHAR(20),
    year INT,
    FOREIGN KEY (faculty_id) REFERENCES Faculty(faculty_id),
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);
INSERT INTO Students (first_name, last_name, date_of_birth, gender, email, phone_number, address) 
VALUES 
('Chris', 'Zavala', '2001-05-12', 'Male', 'chriszavala@example.com', '1234567890', '123 N Blvd St, City, Country'),
('Duarte', 'Zavela', '2000-07-22', 'Female', 'zaveala@example.com', '0987654321', '456 Oak St, City, Country');
INSERT INTO Courses (course_name, course_code, course_description, credit_hours) 
VALUES 
('Introduction to Programming', 'CS101', 'An introductory course to programming in C.', 3),
('Database Systems', 'CS202', 'A course on databases and SQL.', 4);
INSERT INTO Faculty (first_name, last_name, email, department, phone_number) 
VALUES 
('Dr. Chris', 'Turing', 'L556@example.com', 'Computer Science', '1122334455'),
('Dr. Zavala', 'Hopper', 'K123@example.com', 'Computer Science', '2233445566');
INSERT INTO Enrollments (student_id, course_id, enrollment_date, grade) 
VALUES 
(1, 1, '2025-02-01', 'A'),
(2, 2, '2025-02-01', 'B');
INSERT INTO Faculty_Courses (faculty_id, course_id, semester, year) 
VALUES 
(1, 1, 'Spring', 2025),
(2, 2, 'Spring', 2025);
SELECT * FROM Students;
SELECT * FROM Courses;
SELECT s.first_name, s.last_name, e.enrollment_date, e.grade
FROM Students s
JOIN Enrollments e ON s.student_id = e.student_id
JOIN Courses c ON e.course_id = c.course_id
WHERE c.course_code = 'CS101';
SELECT f.first_name, f.last_name, fc.semester, fc.year
FROM Faculty f
JOIN Faculty_Courses fc ON f.faculty_id = fc.faculty_id
JOIN Courses c ON fc.course_id = c.course_id
WHERE c.course_code = 'CS202';
