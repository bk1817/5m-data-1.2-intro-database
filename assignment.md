# Assignment

## Brief

Create an ERD for each of the following case study question.

## Instructions

Paste the answer as DBML in the answer code section below each question.

### Question 1

Construct an ERD for a social media company whose database includes information about users, their followers, and the posts that they make. Users can follow multiple users and create multiple posts.

Each entity has the following attributes:

- User: id, username, email, created_at
- Post: id, title, body, user_id, status, created_at
- Follows: following_user_id, followed_user_id, created_at

Answer:

```dbml
-- 👤 User Table
CREATE TABLE Users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL UNIQUE,
    email VARCHAR(100) NOT NULL UNIQUE,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP
);

-- 📝 Post Table
CREATE TABLE Posts (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(255),
    body TEXT,
    user_id INT NOT NULL,
    status VARCHAR(20), -- e.g., 'published', 'draft'
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id)
);

-- 🔗 Follows Table (Self-referential Many-to-Many)
CREATE TABLE Follows (
    following_user_id INT NOT NULL,
    followed_user_id INT NOT NULL,
    created_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (following_user_id, followed_user_id),
    FOREIGN KEY (following_user_id) REFERENCES Users(id),
    FOREIGN KEY (followed_user_id) REFERENCES Users(id)
);

```

### Question 2

Construct an ERD for a company that sells books online. The company has a website where customers can browse available books and add them to their shopping carts. Each cart can contain multiple books.

There are 4 entities, think of what attributes each entity should have.

- Customer
- Book
- Cart
- CartItem

Answer:

```dbml
// Docs: https://dbml.dbdiagram.io/docs

Table customers {
  id integer [primary key]
  name varchar
  email varchar
  password varchar
  created_at datetime
}

Table books {
  id integer [primary key]
  title varchar
  author varchar
  genre varchar
  price decimal
  stock integer
  published_at date
}

Table carts {
  id integer [primary key]
  customer_id integer
  status varchar // active, checked_out, abandoned
  created_at datetime
}

Table cart_items {
  cart_id integer
  book_id integer
  quantity integer
  added_at datetime
}

// Relationships
Ref: carts.customer_id > customers.id // many-to-one
Ref: cart_items.cart_id > carts.id // many-to-one
Ref: cart_items.book_id > books.id // many-to-one]
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
