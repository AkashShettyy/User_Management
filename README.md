# UserManagementNodeAPI

REST API for user management built with Node.js, Express, and MySQL.

## Prerequisites

- Node.js 14+
- MySQL 5.7+
- npm

## Setup

```bash
npm install
```

Create `.env` file:

```env
PORT=3000
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=root123
DB_NAME=usermanagement
```

## Database

Create DB and tables:

```bash
mysql -u root -p -e "CREATE DATABASE IF NOT EXISTS usermanagement;"
mysql -u root -p usermanagement < database/init.sql
```

Note: This project does not auto-seed users. The `users` table will be empty until you create records via API or SQL insert.

## Run

Development:

```bash
npm run dev
```

Production:

```bash
npm start
```

## Health Check

- `GET /health`

Example:

```bash
curl http://localhost:3000/health
```

## API Endpoints

Base path: `/api/users`

- `GET /api/users` - Get all users
- `GET /api/users/:id` - Get user by ID
- `GET /api/users/username/:username` - Get user by username
- `GET /api/users/email/:email` - Get user by email
- `POST /api/users` - Create user
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user

## Create User Example

```bash
curl -X POST http://localhost:3000/api/users \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Leanne Graham",
    "username": "Bret",
    "email": "sincere@april.biz",
    "phone": "1-770-736-8031 x56442",
    "website": "hildegard.org",
    "address": {
      "street": "Kulas Light",
      "suite": "Apt. 556",
      "city": "Gwenborough",
      "zipcode": "92998-3874",
      "geo": {
        "lat": "-37.3159",
        "lng": "81.1496"
      }
    },
    "company": {
      "name": "Romaguera-Crona",
      "catchPhrase": "Multi-layered client-server neural-net",
      "bs": "harness real-time e-markets"
    }
  }'
```

## Verify Data in MySQL

```bash
mysql -u root -p -D usermanagement -e "SELECT * FROM users;"
```

If your MySQL client shows socket connection errors, try TCP explicitly:

```bash
mysql -h 127.0.0.1 -P 3306 -u root -p -D usermanagement -e "SELECT * FROM users;"
```
