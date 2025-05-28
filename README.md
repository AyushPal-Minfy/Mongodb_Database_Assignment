'''**Create ToDo List**

use toDoList
switched to db toDoList
show dbs
sample_mflix  185.68 MiB
admin         344.00 KiB
local          29.72 GiB

**Creating Database**

db.createCollection("Task")
{ ok: 1 }

**Adding Tasks**

db.Task.insertMany([
  { title: "Buy groceries", completed: true, dueDate: new Date("2025-06-01") },
  { title: "Study", completed: false, dueDate: new Date("2025-06-02") },
  { title: "Workout", completed: true, dueDate: new Date("2025-05-28") }
])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6836e2ae9873c45c382e4738'),
    '1': ObjectId('6836e2ae9873c45c382e4739'),
    '2': ObjectId('6836e2ae9873c45c382e473a')
  }
}

**Print all Tasks**

db.Task.find().pretty()
{
  _id: ObjectId('6836e2ae9873c45c382e4738'),
  title: 'Buy groceries',
  completed: true,
  dueDate: 2025-06-01T00:00:00.000Z
}
{
  _id: ObjectId('6836e2ae9873c45c382e4739'),
  title: 'Study',
  completed: false,
  dueDate: 2025-06-02T00:00:00.000Z
}
{
  _id: ObjectId('6836e2ae9873c45c382e473a'),
  title: 'Workout',
  completed: true,
  dueDate: 2025-05-28T00:00:00.000Z
}

**Adding Tasks**

db.Task.insertOne({title:"Walk",completed:"True",dueDate: new Date("2025-06-05")})
{
  acknowledged: true,
  insertedId: ObjectId('6836e4fc9873c45c382e473b')
}
db.Task.insertOne({title:"Bike Ride",completed:"False",dueDate: new Date("2025-06-07")})
{
  acknowledged: true,
  insertedId: ObjectId('6836e5949873c45c382e473c')
}
db.Task.insertOne({title:"Eat",completed:"True",dueDate: new Date("2025-05-28")})
{
  acknowledged: true,
  insertedId: ObjectId('6836e66b9873c45c382e473d')
}
db.Task.insertMany([
  { title: "Buy bike", completed: true, dueDate: new Date("2025-12-05") },
  { title: "Sleep", completed: false, dueDate: new Date("2025-05-27") },
  { title: "Trip", completed: false, dueDate: new Date("2025-06-28") }
])
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6836e7459873c45c382e473e'),
    '1': ObjectId('6836e7459873c45c382e473f'),
    '2': ObjectId('6836e7459873c45c382e4740')
  }
}
db.Task.updateOne(
  { _id: ObjectId("6836e5949873c45c382e473c") },
  { $set: { completed: true } }
)
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

**Set all task as false

db.Task.updateMany({}, { $set: { completed: false } })
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 9,
  modifiedCount: 6,
  upsertedCount: 0
}

**Updating task to TRUE using object id**

db.Task.updateOne(
  { _id: ObjectId("6836e5949873c45c382e473c") },
  { $set: { completed: true } }
)
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

**Adding updated Date**

db.tasks.insertOne({
  title: "Playing Cricket",
  completed: false,
  createdAt: new Date("28-05-28"),
  updatedAt: new Date()
})
{
  acknowledged: true,
  insertedId: ObjectId('6836ea8a9873c45c382e4741')
}
db.tasks.updateOne(
  { _id: ObjectId("6836ea8a9873c45c382e4741") },
  {
    $set: {
      completed: true,
      updatedAt: new Date(2025-05-29)
    }
  }
)
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
db.task.updateMany({},{$set:{createdAt:new date()}})
ReferenceError: date is not defined
db.Task.updateMany({},{$set:{createdAt:new Date()}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 9,
  modifiedCount: 9,
  upsertedCount: 0
}
db.Task.find().forEach(task => {
  db.Task.updateOne(
    { _id: task._id },
    {
      $set: {
        dueDate: task.createdAt,
        updatedAt: new Date()
      },
      $unset: {
        createdAt: ""
      }
    }
  );
});
db.Task.find().forEach(task => {db.Task.updateOne({ _id: task._id },{ $set: { createdAt: task.dueDate } });});
db.Task.updateMany({}, { $unset: { createdAt: "" } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 9,
  modifiedCount: 9,
  upsertedCount: 0
}
db.Task.updateMany({}, { $rename: { "dueDate": "createdDate" } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 9,
  modifiedCount: 9,
  upsertedCount: 0
}

**Total Tasks**

db.Task.countDocuments();
9

**Adding DueDate**

const futureDate = new Date();
futureDate.setDate(futureDate.getDate() + 7);

db.tasks.updateMany({},{ $set: { dueDate: futureDate } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 0,
  modifiedCount: 0,
  upsertedCount: 0
}
const futureDate = new Date();
futureDate.setDate(futureDate.getDate() + 7);

db.Task.updateMany({},{ $set: { dueDate: futureDate } });
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 9,
  modifiedCount: 9,
  upsertedCount: 0
}
db.Task.countDocuments({
  dueDate: new Date("2025-06-02")
});
0
