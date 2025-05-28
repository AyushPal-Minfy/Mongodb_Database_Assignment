**Create ToDo List**<br>
<br>
use toDoList<br>
switched to db toDoList<br>
show dbs<br>
sample_mflix  185.68 MiB<br>
admin         344.00 KiB<br>
local          29.72 GiB<br>
<br>
**Creating Database**<br>
<br>
db.createCollection("Task")<br>
{ ok: 1 }<br>
<br>
**Adding Tasks**<br>
<br>
db.Task.insertMany([<br>
  { title: "Buy groceries", completed: true, dueDate: new Date("2025-06-01") },<br>
  { title: "Study", completed: false, dueDate: new Date("2025-06-02") },<br>
  { title: "Workout", completed: true, dueDate: new Date("2025-05-28") }<br>
])<br>
{<br>
  acknowledged: true,<br>
  insertedIds: {<br>
    '0': ObjectId('6836e2ae9873c45c382e4738'),<br>
    '1': ObjectId('6836e2ae9873c45c382e4739'),<br>
    '2': ObjectId('6836e2ae9873c45c382e473a')<br>
  }<br>
}<br>
<br>
**Print all Tasks**<br>
<br>
db.Task.find().pretty()<br>
{<br>
  _id: ObjectId('6836e2ae9873c45c382e4738'),<br>
  title: 'Buy groceries',<br>
  completed: true,<br>
  dueDate: 2025-06-01T00:00:00.000Z<br>
}<br>
{<br>
  _id: ObjectId('6836e2ae9873c45c382e4739'),<br>
  title: 'Study',<br>
  completed: false,<br>
  dueDate: 2025-06-02T00:00:00.000Z<br>
}<br>
{<br>
  _id: ObjectId('6836e2ae9873c45c382e473a'),<br>
  title: 'Workout',<br>
  completed: true,<br>
  dueDate: 2025-05-28T00:00:00.000Z<br>
}<br>
<br>
**Adding Tasks**<br>
<br>
db.Task.insertOne({title:"Walk",completed:"True",dueDate: new Date("2025-06-05")})<br>
{<br>
  acknowledged: true,<br>
  insertedId: ObjectId('6836e4fc9873c45c382e473b')<br>
}<br>
db.Task.insertOne({title:"Bike Ride",completed:"False",dueDate: new Date("2025-06-07")})<br>
{<br>
  acknowledged: true,<br>
  insertedId: ObjectId('6836e5949873c45c382e473c')<br>
}<br>
db.Task.insertOne({title:"Eat",completed:"True",dueDate: new Date("2025-05-28")})<br>
{<br>
  acknowledged: true,<br>
  insertedId: ObjectId('6836e66b9873c45c382e473d')<br>
}<br>
db.Task.insertMany([<br>
  { title: "Buy bike", completed: true, dueDate: new Date("2025-12-05") },<br>
  { title: "Sleep", completed: false, dueDate: new Date("2025-05-27") },<br>
  { title: "Trip", completed: false, dueDate: new Date("2025-06-28") }<br>
])<br>
{<br>
  acknowledged: true,<br>
  insertedIds: {<br>
    '0': ObjectId('6836e7459873c45c382e473e'),<br>
    '1': ObjectId('6836e7459873c45c382e473f'),<br>
    '2': ObjectId('6836e7459873c45c382e4740')<br>
  }<br>
}<br>
db.Task.updateOne(<br>
  { _id: ObjectId("6836e5949873c45c382e473c") },<br>
  { $set: { completed: true } }<br>
)<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 1,<br>
  modifiedCount: 1,<br>
  upsertedCount: 0<br>
}<br>
<br>
**Set all task as false<br>
<br>
db.Task.updateMany({}, { $set: { completed: false } })<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 9,<br>
  modifiedCount: 6,<br>
  upsertedCount: 0<br>
}<br>
<br>
**Updating task to TRUE using object id**<br>
<br>
db.Task.updateOne(<br>
  { _id: ObjectId("6836e5949873c45c382e473c") },<br>
  { $set: { completed: true } }<br>
)<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 1,<br>
  modifiedCount: 1,<br>
  upsertedCount: 0<br>
}<br>
<br>
**Adding updated Date**<br>
<br>
db.tasks.insertOne({<br>
  title: "Playing Cricket",<br>
  completed: false,<br>
  createdAt: new Date("28-05-28"),<br>
  updatedAt: new Date()<br>
})<br>
{<br>
  acknowledged: true,<br>
  insertedId: ObjectId('6836ea8a9873c45c382e4741')<br>
}<br>
db.tasks.updateOne(<br>
  { _id: ObjectId("6836ea8a9873c45c382e4741") },<br>
  {<br>
    $set: {<br>
      completed: true,<br>
      updatedAt: new Date(2025-05-29)<br>
    }<br>
  }<br>
)<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 1,<br>
  modifiedCount: 1,<br>
  upsertedCount: 0<br>
}<br>
db.task.updateMany({},{$set:{createdAt:new date()}})<br>
ReferenceError: date is not defined<br>
db.Task.updateMany({},{$set:{createdAt:new Date()}})<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 9,<br>
  modifiedCount: 9,<br>
  upsertedCount: 0<br>
}<br>
db.Task.find().forEach(task => {<br>
  db.Task.updateOne(<br>
    { _id: task._id },<br>
    {<br>
      $set: {<br>
        dueDate: task.createdAt,<br>
        updatedAt: new Date()<br>
      },<br>
      $unset: {<br>
        createdAt: ""<br>
      }<br>
    }<br>
  );<br>
});<br>
db.Task.find().forEach(task => {db.Task.updateOne({ _id: task._id },{ $set: { createdAt: task.dueDate } });});<br>
db.Task.updateMany({}, { $unset: { createdAt: "" } });<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 9,<br>
  modifiedCount: 9,<br>
  upsertedCount: 0<br>
}<br>
db.Task.updateMany({}, { $rename: { "dueDate": "createdDate" } });<br>
{<br>
  acknowledged: true,<br>
  insertedId: null,<br>
  matchedCount: 9,<br>
  modifiedCount: 9,<br>
  upsertedCount: 0<br>
}<br>
<br>
**Total Tasks**<br>
<br>
db.Task.countDocuments();<br>
9<br>
<br>
**Adding DueDate**<br>
<br>
const futureDate = new Date();<br>
futureDate.setDate(futureDate.getDate() + 7);<br>
<br>
db.tasks.updateMany({},{ $set: { dueDate: futureDate } });<br>
