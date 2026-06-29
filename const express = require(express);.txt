const express = require("express");
const cors = require("cors");

const app = express();
const PORT = 3000;

app.use(cors());
app.use(express.json());

// Dummy database
let todos = [
  { id: 1, task: "Learn Node.js" },
  { id: 2, task: "Deploy on AWS EC2" }
];

// Home route
app.get("/", (req, res) => {
  res.json({
    message: "Welcome to Todo Backend API 🚀"
  });
});

// Get all todos
app.get("/api/todos", (req, res) => {
  res.json(todos);
});

// Add new todo
app.post("/api/todos", (req, res) => {
  const newTodo = {
    id: todos.length + 1,
    task: req.body.task
  };

  todos.push(newTodo);

  res.status(201).json({
    message: "Todo added successfully",
    data: newTodo
  });
});

// Delete todo
app.delete("/api/todos/:id", (req, res) => {
  const id = Number(req.params.id);

  todos = todos.filter(todo => todo.id !== id);

  res.json({
    message: "Todo deleted"
  });
});

app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});