---
{"dg-publish":true,"permalink":"/tomas-statnice/databaze-a-web/databaze/exercises/university-course-enrolment/conceptual/","tags":["excalidraw","databaze_a_web","databaze"],"noteIcon":""}
---

==⚠  Switch to EXCALIDRAW VIEW in the MORE OPTIONS menu of this document. ⚠== You can decompress Drawing data with the command palette: 'Decompress current Excalidraw file'. For more info check in plugin settings under 'Saving'


# Excalidraw Data
## Text Elements
Imagine you are tasked with designing a database system for managing courses, instructors, 
and students at a university. The system should track information about the courses offered, 
the instructors teaching them, the students enrolled in those courses, and their grades.
{ #QYlft5l7}


Entities: 
    - Instructors
    - Students
    - Courses
    - Enrolment
{ #YevmXvGl}


Relations:
    - instructor teaches course
    - student is enrolled into a course
{ #tMNqE7Td}


Course
{ #Eh7YWVwS}


Instructor
{ #Qo9SeXI4}


Enrolment
{ #Yozj7Gvc}


Person
{ #egwRSHsO}


Student
{ #fSsVAcxk}


+ email
+ phone number
+ name
+ DOB
{ #4b0SaZO9}


teaches
{ #rxfPlBle}


1...n
{ #MkQ25hGf}


1
{ #sd1mvdqU}


+ courseNumber
+ name
{ #px5aWzk8}


enroled
{ #A7laktns}


0...n
{ #7gvmjCJu}


0...*
{ #pSRdQVCS}


+ studentNumber
{ #REQLLXSU}


+ instructorNumber
{ #jZ0xDZST}


enroled
{ #qghI9F0Z}


1
{ #tmmM35nV}


+ grade
{ #8ciox0YM}


0...*
{ #wYk74Q3V}


Konceptuální úroveň
{ #fxbThYbN}


