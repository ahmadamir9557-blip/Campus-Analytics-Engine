# Campus Analytics Engine

A multi-file, menu-driven C++ console application for managing student
records, course enrollments, attendance, grades, and fee transactions.
Built only with C++.
## File Structure

```
CampusAnalyticsEngine/
├── main.cpp            # M0 - entry point, 3-level nested menu
├── filehandler.h/.cpp   # M1 - all txt file read/write
├── student_ops.h/.cpp    # M2 - add/search/update/soft-delete students
├── course_ops.h/.cpp     # M3 - enroll/drop, prerequisites, credit load
├── attendance.h/.cpp     # M4 - mark attendance, %, shortage, undo
├── grades.h/.cpp         # M5 - marks, weighted total, GPA, class stats
├── fee_tracker.h/.cpp    # M6 - payments, late fines, receipts
├── reports.h/.cpp        # M7 - merit list, defaulters, summaries
└── data/
    ├── students.txt
    ├── courses.txt
    ├── enrollments.txt
    ├── attendance_log.txt
    ├── fees.txt
    └── grades.txt        # created/maintained by the grades module
```

## How to Compile

IN THE TERMINAL, TYPE
```bash
g++ -o campus_engine main.cpp filehandler.cpp student_ops.cpp course_ops.cpp attendance.cpp grades.cpp fee_tracker.cpp reports.cpp
.\campus_engine.exe
```

## How to Run

```bash
./campus_engine
```

You must run it from the folder that contains the `data/` subfolder,
since all file paths in the code are relative (e.g. `data/students.txt`).
On Windows (after compiling with g++/MinGW or in Visual Studio), just run
`campus_engine.exe` from the same folder structure.

## Menu Overview

```
MAIN MENU
1. Student Management   -> Add / Search by Roll / Search by Name (live, bonus) / Update / Soft-delete / List
2. Course Management     -> Enroll / Drop / Credit load / List enrolled
3. Attendance             -> Mark / % / Shortage list / Undo / Daily sheet
4. Grades                  -> Enter marks / Compute GPA
5. Fee Tracker              -> Record payment / Receipt / Late fine
6. Reports                   -> Merit list / Defaulters / Summary / Export
0. Exit
```

## Sample Run

```
      CAMPUS ANALYTICS ENGIN
            MAIN MENU
1. Student Management
2. Course Management
3. Attendance
4. Grades
5. Fee Tracker
6. Reports
0. Exit
Choice: 6

----- REPORTS -----
1. Merit List
...
Choice: 1

================= MERIT LIST =================
Rank  Roll No       Name                  CGPA
------------------------------------------------
1     BSAI-23-006   Sana Pervez           3.90
2     BSAI-23-012   Maham Javed           3.80
...
```

