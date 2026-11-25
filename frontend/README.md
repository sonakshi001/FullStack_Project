# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

# 🍽️ Restaurant Reservation System (MERN Stack)

A full-stack restaurant table reservation web application built with **MongoDB, Express.js, React, and Node.js**. Customers can browse the restaurant, book a table online, and receive confirmation, while admins can manage reservations from a dashboard.

![MERN](https://img.shields.io/badge/Stack-MERN-green)
![License](https://img.shields.io/badge/License-MIT-blue)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## 📌 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Screenshots](#-screenshots)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [API Endpoints](#-api-endpoints)
- [Database Schema](#-database-schema)
- [Deployment](#-deployment)
- [Future Improvements](#-future-improvements)
- [Contributing](#-contributing)
- [License](#-license)
- [Author](#-author)

---

## ✨ Features

### Customer
- Responsive home page with menu, about, and contact sections
- Book a table by selecting date, time, and number of guests
- Form validation with instant feedback
- Email confirmation after successful reservation
- User registration and login (JWT authentication)
- View, update, and cancel own reservations

### Admin
- Secure admin login
- Dashboard to view all reservations
- Approve, reject, edit, or delete reservations
- Manage tables and time slots
- Filter and search reservations by date or customer

---

## 🛠️ Tech Stack

| Layer      | Technology                                   |
|------------|----------------------------------------------|
| Frontend   | React.js, React Router, Axios, CSS / Tailwind |
| Backend    | Node.js, Express.js                          |
| Database   | MongoDB with Mongoose                        |
| Auth       | JSON Web Tokens (JWT), bcrypt                |
| Email      | Nodemailer                                   |
| Tools      | Git, Postman, VS Code                        |

---

## 📁 Project Structure

```
restaurant-reservation/
├── client/                  # React frontend
│   ├── public/
│   └── src/
│       ├── components/
│       ├── pages/
│       ├── context/
│       ├── services/
│       ├── App.js
│       └── index.js
│
├── server/                  # Node + Express backend
│   ├── config/
│   │   └── db.js
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   ├── routes/
│   ├── utils/
│   └── server.js
│
├── screenshots/
├── .gitignore
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (v18 or later)
- [MongoDB](https://www.mongodb.com/) (local or MongoDB Atlas)
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/your-username/restaurant-reservation.git
   cd restaurant-reservation
   ```

2. **Install backend dependencies**
   ```bash
   cd server
   npm install
   ```

3. **Install frontend dependencies**
   ```bash
   cd ../client
   npm install
   ```

4. **Set up environment variables** (see below)

5. **Run the app**

   Backend:
   ```bash
   cd server
   npm run dev
   ```

   Frontend (in a new terminal):
   ```bash
   cd client
   npm start
   ```

6. Open **http://localhost:3000** in your browser.

---

## 🔐 Environment Variables

Create a `.env` file inside the `server/` folder:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret
JWT_EXPIRE=7d

# Email (Nodemailer)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
```

Create a `.env` file inside the `client/` folder:

```env
REACT_APP_API_URL=http://localhost:5000/api
```

> ⚠️ Never commit your `.env` files. Make sure they are listed in `.gitignore`.

---

## 🔌 API Endpoints

### Auth
| Method | Endpoint             | Description          | Access |
|--------|----------------------|----------------------|--------|
| POST   | `/api/auth/register` | Register new user    | Public |
| POST   | `/api/auth/login`    | Login user           | Public |
| GET    | `/api/auth/me`       | Get logged-in user   | Private |

### Reservations
| Method | Endpoint                   | Description                  | Access  |
|--------|----------------------------|------------------------------|---------|
| POST   | `/api/reservations`        | Create a reservation         | Private |
| GET    | `/api/reservations/my`     | Get user's reservations      | Private |
| GET    | `/api/reservations`        | Get all reservations         | Admin   |
| PUT    | `/api/reservations/:id`    | Update a reservation         | Private |
| DELETE | `/api/reservations/:id`    | Cancel / delete reservation  | Private |

### Tables
| Method | Endpoint            | Description        | Access |
|--------|---------------------|--------------------|--------|
| GET    | `/api/tables`       | List all tables    | Public |
| POST   | `/api/tables`       | Add a table        | Admin  |
| PUT    | `/api/tables/:id`   | Update a table     | Admin  |
| DELETE | `/api/tables/:id`   | Remove a table     | Admin  |

---

## 🗄️ Database Schema

### User
```js
{
  name: String,
  email: String,       // unique
  password: String,    // hashed
  role: String,        // "user" | "admin"
  createdAt: Date
}
```

### Reservation
```js
{
  user: ObjectId,      // ref: User
  name: String,
  email: String,
  phone: String,
  date: Date,
  time: String,
  guests: Number,
  table: ObjectId,     // ref: Table
  status: String,      // "pending" | "confirmed" | "cancelled"
  specialRequest: String,
  createdAt: Date
}
```

### Table
```js
{
  tableNumber: Number,
  capacity: Number,
  isAvailable: Boolean
}
```

---

## ☁️ Deployment

- **Frontend:** Vercel / Netlify
- **Backend:** Render / Railway / Heroku
- **Database:** MongoDB Atlas

Set the same environment variables on your hosting platform and update `REACT_APP_API_URL` to point to your deployed backend.

---

## 🔮 Future Improvements

- [ ] Online payment / deposit integration (Stripe or Razorpay)
- [ ] SMS reminders for upcoming reservations
- [ ] Real-time table availability with Socket.io
- [ ] Reviews and ratings
- [ ] Multi-restaurant support
- [ ] Dark mode

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👩‍💻 Author

**Sonakshi Kumari**
B.Tech CSE (AI & ML)

- GitHub: [@sonakshi001](https://github.com/your-sonakshi001)
- LinkedIn: [your-linkedin](https://linkedin.com/in/sonakshi001)

⭐ If you like this project, give it a star!
