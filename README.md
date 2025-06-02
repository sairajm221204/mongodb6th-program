# mongodb6th-program
Execute Aggregation Pipeline and its operations (pipeline must contain $match, $group, $sort, $project, $skip etc. students encourage to execute several queries to demonstrate various aggregation operators) 

{
  "_id": 1,
  "name": "Alice",
  "class": "10A",
  "subject": "Math",
  "marks": 85
}


db.students.insertMany([
  { name: "Alice", class: "10A", subject: "Math", marks: 85 },
  { name: "Bob", class: "10A", subject: "Math", marks: 78 },
  { name: "Charlie", class: "10A", subject: "Science", marks: 92 },
  { name: "David", class: "10B", subject: "Math", marks: 67 },
  { name: "Eve", class: "10B", subject: "Science", marks: 74 },
  { name: "Frank", class: "10B", subject: "Math", marks: 88 },
  { name: "Grace", class: "10A", subject: "Science", marks: 81 },
  { name: "Hannah", class: "10B", subject: "Science", marks: 90 }
])

$match filters the documents to include only "Science" subject.
$group groups by class, calculates:
•	averageMarks using $avg
•	totalStudents using $sum
$sort sorts the classes based on average marks in descending order.
$project reshapes the output, renaming _id to class.
$skip skips the top record (like skipping first page in pagination).

Count students scoring above 80 in Math:
db.students.aggregate([
  { $match: { subject: "Math", marks: { $gt: 80 } } },
  { $count: "highScorers" }
])

Top 3 students sorted by marks:
db.students.aggregate([
  { $sort: { marks: -1 } },
  { $limit: 3 }
])

$Project Include Specific Fields Only
db.students.aggregate([
  {
    $project: {
      _id: 0,
      name: 1,
      marks: 1
    }
  }
])

Purpose of $skip
•	Skips the first N documents in the aggregation result.
•	Commonly used for pagination (along with $limit).
db.students.aggregate([
  { $sort: { marks: -1 } }, 
  { $skip: 3 }              
])




