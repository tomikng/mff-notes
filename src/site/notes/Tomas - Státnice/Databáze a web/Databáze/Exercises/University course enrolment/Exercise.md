---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/databaze/exercises/university-course-enrolment/exercise/","tags":["databaze","databaze_a_web"],"noteIcon":""}
---

Imagine you are tasked with designing a database system for managing courses, instructors, 
and students at a university. The system should track information about the courses offered, 
the instructors teaching them, the students enrolled in those courses, and their grades.

# Solution

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">




==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'


# Excalidraw Data
## Text Elements
Imagine you are tasked with designing a database system for managing courses, instructors, 
and students at a university. The system should track information about the courses offered, 
the instructors teaching them, the students enrolled in those courses, and their grades. 
Entities: 
    - Instructors
    - Students
    - Courses
    - Enrolment 
Relations:
    - instructor teaches course
    - student is enrolled into a course 
Course 
Instructor 
Enrolment 
Person 
Student 
+ email
+ phone number
+ name
+ DOB 
teaches 
1...n 
1 
+ courseNumber
+ name 
enroled 
0...n 
0...* 
+ studentNumber 
+ instructorNumber 
enroled 
1 
+ grade 
0...* 
Konceptuální úroveň 


</div></div>


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/tomas-statnice/databaze-a-web/databaze/exercises/university-course-enrolment/logical-layer/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">




Person(***personId,*** email, phoneNumber, name, DOB)
Instructor(***instructorNumber***) instructorNumber $\subseteq$  Person.personId
Student(***studentNumber***) studentNumber $\subseteq$  Person.personId

Course(***courseNumber***, name)

Enrolment(***enrolmentId***, ***studentNumber***, ***courseNumber***, grade) studentNumber $\subseteq$  Student.studentNumber, courseNumber $\subseteq$ Course.courseNumber

Teaches(***instructorNumber***, ***courseNumber***) instructorNumber $\subseteq$ Instructor.instructorNumber, courseNumber $\subseteq$ Course.courseNumber

</div></div>
