# Homework 5.3

There are documents for each student (student_id) across a variety of classes (class_id). Note that not all students in the same class have the same exact number of assessments. Some students have three homework assignments, etc. 

Your task is to calculate the class with the best average student performance. This involves calculating an average for each student in each class of all non-quiz assessments and then averaging those numbers to get a class average. To be clear, each student's average includes only exams and homework grades. Don't include their quiz scores in the calculation. 

What is the class_id which has the highest average student performance? 

## Answer

Steps are:
* Unwind scores
* Exclude quiz results
* Group average for each student in class
* Group average for class
* Select top class

```
db.grades.aggregate([
    {
        $unwind: "$scores"
    },
    {
        $match: { "scores.type": { $ne: "quiz" } }
    },
    {
        $group: { _id: { student: "$student_id", class: "$class_id" }, score: { $avg: "$scores.score" } }
    },
    {
        $group: { _id: "$_id.class", avg: { $avg: "$score" } }
    },
    {
        $sort: { avg: -1 }
    }
])
```
