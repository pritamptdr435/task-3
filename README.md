const express = require("express");
const app = express();
const port = 3000;

// Middleware to parse JSON
app.use(express.json());

// In-memory book list
let books = [
  { id: 1, title: "Book One", author: "Author A" },
  { id: 2, title: "Book Two", author: "Author B" },
];

// GET all books
app.get("/books", (req, res) => {
  res.json(books);
});

// POST a new book
app.post("/books", (req, res) => {
  const newBook = req.body;
  books.push(newBook);
  res.status(201).json({ message: "Book added", book: newBook });
});

// PUT update book by ID
app.put("/books/:id", (req, res) => {
  const id = parseInt(req.params.id);
  const updatedBook = req.body;
  books = books.map((book) =>
    book.id === id ? { ...book, ...updatedBook } : book
  );
  res.json({ message: "Book updated", book: updatedBook });
});

// DELETE a book by ID
app.delete("/books/:id", (req, res) => {
  const id = parseInt(req.params.id);
  books = books.filter((book) => book.id !== id);
  res.json({ message: Book with id ${id} deleted });
});

// Start server
app.listen(port, () => {
  console.log(Server running on http://localhost:${port});
});
