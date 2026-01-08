# Store

A modern product management application built with Rails 8 and Bootstrap 5.

## Quick Start

```bash
# Install dependencies
bundle install

# Setup database
bin/rails db:setup

# Start server
bin/rails server
```

Visit `http://localhost:3000`

## Test Login

**Email:** test@gmail.com
**Password:** test

## Features

- Modern Bootstrap 5 UI with responsive design
- Product CRUD operations (Create, Read, Update, Delete)
- User authentication with session management
- Password reset functionality
- Public product browsing, authenticated product management

## Screenshots

### Home Page (Unauthenticated)
![Home Page - Unauthenticated](doc/screenshots/store_home_unauthenticated.png)

---

### Login Page
![Login Page](doc/screenshots/store_login.png)

---

### Home Page (Authenticated)
![Home Page - Authenticated](doc/screenshots/store_home_authenticated.png)

---

### Product Details
![Product Details](doc/screenshots/store_product_details_unauthenticated.png)

---

### New Product
![New Product](doc/screenshots/store_product_new.png)

---

### Edit Product
![Edit Product](doc/screenshots/store_product_edit.png)

## Tech Stack

- **Ruby:** 4.0.0
- **Rails:** 8.1.1
- **Database:** SQLite3
- **Frontend:** Bootstrap 5, Hotwire (Turbo + Stimulus)
- **Authentication:** Rails 8 built-in authentication

## Development

```bash
# Run tests
bin/rails test

# Run code quality checks
bin/rubocop
bin/brakeman

# Database operations
bin/rails db:migrate
bin/rails db:reset
```
