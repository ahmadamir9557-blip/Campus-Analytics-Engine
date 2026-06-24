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

From inside the project folder (the one containing `main.cpp` and the
`data/` folder):

```bash
g++ -o campus_engine main.cpp filehandler.cpp student_ops.cpp course_ops.cpp attendance.cpp grades.cpp fee_tracker.cpp reports.cpp
.\campus_engine.exe
```

This has been tested and compiles with **zero errors and zero warnings**
under `-std=c++98 -Wall`.

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

## Notes on Design Choices

- **No STL algorithms / no `<map>` / no `class`:** all sorting (selection
  sort, bubble sort) and lookups (linear search, nested loops over
  parallel arrays) are written manually as required.
- **No `<ctime>`:** `daysBetween()` in `fee_tracker.cpp` parses
  `DD-MM-YYYY` strings manually and uses a hand-written month-length
  array (with leap year handling) to compute the day difference.
- **grades.txt** is not one of the 5 source data files you provided, but
  it is generated and maintained by the grades module (`enterMarks`) so
  that GPA, prerequisite checks, and result reports have somewhere to
  store computed marks. It starts out as just a header row.
- All file I/O goes through `filehandler.cpp` — no other module opens a
  file directly, satisfying the cross-file dependency requirement.

## Bonus Feature (Implemented)

"Search as you type" is not one isolated menu option — it's built into
**every place in the whole project where the user is asked to enter a
roll number or a course code**: Search by Roll, Update Student, Soft
Delete, Search by Name, Enroll/Drop Course, Get Credit Load, List
Enrolled Students, Mark Attendance, Get Attendance %, Print Daily Sheet,
Enter Marks, Compute GPA, Record Payment, Generate Receipt, Late Fine,
and Semester Result.

You type one character at a time (no Enter needed per keystroke), and
the matching student or course list re-filters and reprints after every
keystroke — implemented purely with `substr`/`length` comparisons
(case-insensitive, via a small hand-written `toUpperChar`), no STL
find/search. Backspace deletes the last character and re-filters. Enter
finishes/confirms, Esc cancels back to the menu.

**Add Student** uses the same live-typing screen for the roll number,
but with one extra rule: if the roll being typed already belongs to an
existing student, it shows an error immediately after Enter and asks you
to type a different roll — so the same roll can never be added twice.

Note: reading a single keystroke without waiting for Enter isn't
standard C++ — it needs OS-specific code. The implementation uses
`<conio.h>`'s `_getch()` on Windows, and a `<termios.h>`-based raw-mode
reader on Linux/Mac, guarded by `#ifdef _WIN32`. This only works in a
real terminal (TTY) — not if input is piped or redirected.-entered "current date" prompt in the menu to make this more accurate.
