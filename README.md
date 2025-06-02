# CyberMACS Alumni System

The **CyberMACS Alumni System** is a comprehensive relational database project developed as part of a university course at SRH Berlin. It is designed to manage alumni data, facilitate networking, support career development, and enhance institutional engagement through job postings, events, and mentorship programs.

---

## 📌 Features

- **Alumni Management**: Profiles with contact info, graduation year, job history, specializations, and privacy settings.
- **Job Portal**: Employers post job openings; alumni can apply and track application statuses.
- **Event System**: Admins create and manage events; alumni can attend, rate, and give feedback.
- **Mentorship Program**: Alumni can register as mentors/mentees and be matched accordingly.
- **Analytics & Reports**: Powerful SQL queries to generate insights on alumni engagement, employment trends, and event participation.

---

## 🧰 Technologies Used

- **MySQL 8.0** – Relational database management system.
- **MySQL Workbench** – ERD/EER diagram design and schema planning.
- **Mockaroo** – Data generation for realistic testing.
- **SQL** – Querying, data population, reporting.
- **ChatGPT**

---

## 🗂️ Project Structure

```
CyberMACS-Alumni-System/
├── README.md                          # Project overview (this file)
├── documentation/
│   └── CyberMACS_Alumni_Report.docx   # Full project report
├── database/
│   ├── alumni.sql
│   ├── DATA_Template.xlsx
│   ├── alumni_db/                     # Raw InnoDB .ibd files
│   └── csv/                           # Mockaroo-generated CSVs
├── diagrams/
│   ├── Conceptual ERD.jpg
│   └── Logical Design EER.png
├── queries/                           # Analytical and operational SQL
│   └── *.sql
└── .gitignore
```

---

## 📊 Sample SQL Queries

```sql
-- 1. Count Alumni by Graduation Year
SELECT graduation_year, COUNT(*) AS total_alumni
FROM Alumni
GROUP BY graduation_year
ORDER BY total_alumni DESC;

-- 2. Top Employers Hiring Alumni
SELECT e.company_name, COUNT(eh.alumni_id) AS total_hires
FROM employer e
JOIN employment_history eh ON e.employer_id = eh.employer_id
GROUP BY e.company_name
ORDER BY total_hires DESC
LIMIT 10;

-- 3. Alumni Who Applied and Got Hired
SELECT a.full_name, jp.job_title, e.company_name
FROM job_application ja
JOIN job_posting jp ON ja.job_posting_id = jp.job_posting_id
JOIN employer e ON jp.employer_id = e.employer_id
JOIN employment_history eh ON ja.alumni_id = eh.alumni_id AND eh.employer_id = e.employer_id
JOIN alumni a ON a.alumni_id = ja.alumni_id
WHERE eh.start_date > ja.submission_date;
```

---

## 🧾 Business Rules Overview

- Alumni can apply to many jobs, attend multiple events, and act as mentors.
- Job applications link alumni to specific postings and track their status.
- Events are managed by administrators and support feedback/rating.
- Mentorships are many-to-many between mentors and mentees.
- Employers can post jobs and track alumni hires.

📄 See `documentation/CyberMACS_Alumni_Report.docx` for the full report and SQL query explanations.

---

## 👥 Authors

- **Amin Niaziardekani** ([@amin4554](https://github.com/amin4554))
- **Swapnaneel Sarkhel**
- **Ajdin Buljko**

---

## 🏛️ University

**SRH University of Applied Sciences Berlin**  
**Course:** Databases 
**Supervisor:** Prof. Dilan Ebru  
**Date:** February 11, 2025

---

## 🔒 License

This project is intended for academic and educational use only. All data is mock data generated for demonstration purposes.

---

![Logical Design EER](https://github.com/user-attachments/assets/1775d68f-69f2-4aa5-ba88-9a8c9f57abfe)
