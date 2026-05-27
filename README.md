# 💰 Velto
**Velto** — *Velocity of Money*

Velto is a full-stack personal finance dashboard that gives you complete control over your income and expenses. It goes beyond simple record-keeping by providing rich visual analytics, exportable reports, and a polished, animated interface—all secured behind OTP-verified authentication.

Add your earnings and expenses with emoji-tagged categories, watch your financial story unfold through interactive charts, and download everything as a clean Excel spreadsheet whenever you need it.

## 🚀 Live Application
Velto is fully deployed and accessible online.

🔗 [Access Velto Here](https://velto-finc-tracker.vercel.app/)

## ✨ Key Features

🏠 **Financial Command Center**: A comprehensive dashboard that displays your total balance, income, and expenses at a glance. Three summary cards with real-time figures give you instant clarity, while recent transactions and trend data scroll below—everything you need on a single screen.

💵 **Smart Income Tracking**: Log every source of income with a custom emoji icon, source label, and date. All entries are sorted chronologically and can be viewed, managed, or bulk-downloaded as an `.xlsx` spreadsheet with a single click.

💸 **Expense Management**: Categorise your spending with emoji-tagged categories and precise date tracking. Like income, expenses support full CRUD operations and one-click Excel export, making tax time and budgeting painless.

📈 **Visual Analytics & Charts**: Powered by Recharts, the dashboard renders interactive line charts and bar visualisations covering the last 30 days of expenses and 60 days of income. Watch your financial trends emerge instead of staring at numbers.

📥 **Excel Export**: Both income and expense data can be downloaded as professionally formatted `.xlsx` files using the SheetJS library. Export your records for accountants, personal archives, or further analysis—no copy-pasting required.

🔐 **OTP-Verified Authentication**: Signup requires a 6-digit OTP sent to your email via Nodemailer. No unverified accounts exist in the system. Login uses JWT tokens with 1-hour expiry for stateless, secure sessions.

🔑 **Forgot Password Flow**: A complete password recovery pipeline: request a reset OTP, verify it, and set a new password—all backed by rate-limited OTP resending (1-minute cooldown) and automatic expiry.

👤 **Profile Management**: Upload a profile avatar (auto-compressed with Sharp if over 1MB), edit your name and email, and view your account details. The profile image is processed server-side and stored as an optimized base64 string.

📱 **Responsive & Animated UI**: Built with Tailwind CSS and Framer Motion, the interface adapts seamlessly from mobile to desktop. Smooth page transitions and micro-animations make every interaction feel polished.

## 🏗️ Technical Architecture
An overview of the core architecture of the Velto workspace:

```
Velto/
├── client/                     # Frontend React Application
│   ├── public/                 # Static assets
│   └── src/
│       ├── components/
│       │   ├── Cards/          # Summary info cards
│       │   ├── Charts/         # Recharts visualisations
│       │   ├── Dashboard/      # Dashboard widgets (RecentTransactions, FinanceOverview, etc.)
│       │   ├── Expense/        # Expense list & form components
│       │   ├── Income/         # Income list & form components
│       │   ├── Inputs/         # Reusable form inputs
│       │   ├── Landing/        # Landing page sections (Navbar, Hero, Features, Testimonials, Footer)
│       │   ├── Layouts/        # Dashboard sidebar layout
│       │   └── Modal/          # Modal dialogs
│       ├── context/            # React Context providers (UserContext)
│       ├── hooks/              # Custom hooks & AuthGuard
│       ├── pages/
│       │   ├── Auth/           # Login, SignUp, ForgotPassword
│       │   └── Dashboard/      # Home, Income, Expense, Profile, LandingPage
│       ├── utils/              # Axios instance, API paths, helper functions
│       └── index.css           # Global styles & Tailwind config
│
├── server/                     # Backend Node.js / Express API
│   ├── config/
│   │   └── db.js               # MongoDB connection
│   ├── controllers/
│   │   ├── authController.js   # OTP generation, verification, login, password reset
│   │   ├── dashboardController.js  # Aggregation pipelines for summary data
│   │   ├── expenseController.js    # Expense CRUD + Excel export
│   │   ├── incomeController.js     # Income CRUD + Excel export
│   │   └── profileController.js    # Profile read, update, avatar upload
│   ├── middleware/
│   │   ├── authMiddleware.js       # JWT token verification
│   │   ├── profileMiddleware.js    # Profile-specific validation
│   │   └── uploadMiddleware.js     # Multer file upload configuration
│   ├── models/
│   │   ├── Expense.js          # Expense schema (category, amount, date, icon)
│   │   ├── Income.js           # Income schema (source, amount, date, icon)
│   │   ├── OtpGetter.js        # OTP storage with expiry & type (verify/reset)
│   │   └── User.js             # User schema with bcrypt password hashing
│   ├── routes/                 # RESTful API endpoint definitions
│   ├── uploads/                # Server-side file storage
│   └── utils/
│       ├── emailTemplates.js   # Styled HTML email templates for OTPs
│       └── sendEmail.js        # Nodemailer transport wrapper
```

## 🛠️ Technology Stack

### Frontend
- **React 19** with Vite 7 for blazing-fast HMR and builds
- **React Router v7** for seamless client-side navigation
- **Recharts** for interactive financial charts and visualisations
- **Tailwind CSS** for utility-first responsive styling
- **Framer Motion** for smooth page transitions and micro-animations
- **Axios** for HTTP requests with a centralised instance
- **emoji-picker-react** for emoji-tagged categories
- **Moment.js** for date formatting
- **react-hot-toast** for toast notifications
- **Lucide React & React Icons** for iconography

### Backend
- **Node.js & Express 5** for a lightweight, modular REST API
- **MongoDB & Mongoose** for schema-driven data modelling and aggregation pipelines
- **JSON Web Tokens (JWT)** for secure, stateless authentication
- **bcryptjs** for password hashing with salt rounds
- **Nodemailer** for transactional email delivery (OTP codes)
- **Multer & Sharp** for file upload handling and image compression
- **SheetJS (xlsx)** for server-side Excel file generation

## 🚀 Getting Started

### Prerequisites

- **Node.js** ≥ 18
- **MongoDB** (local instance or [MongoDB Atlas](https://www.mongodb.com/atlas))
- **npm** (comes with Node.js)

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/Velto.git
cd Velto
```

### 2. Setup the Server

```bash
cd server
npm install
```

Create a `.env` file in `server/`:

```env
PORT=8000
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/velto
JWT_SECRET=your_jwt_secret_key
CLIENT_URL=http://localhost:5173

# Email (for OTP)
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
```

Start the server:

```bash
npm run dev
```

The server will run on `http://localhost:8000`.

### 3. Setup the Client

```bash
cd client
npm install
```

Create a `.env` file in `client/`:

```env
VITE_BASE_URL=http://localhost:8000
```

Start the client:

```bash
npm run dev
```

The app will be available at `http://localhost:5173`.

## 📡 API Reference

All endpoints are prefixed with `/api/v1`. Routes marked with 🔒 require a valid JWT token in the `Authorization` header.

### Authentication
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/auth/request-otp` | Send OTP for email verification |
| `POST` | `/auth/verify-otp` | Verify OTP & create account |
| `POST` | `/auth/login` | Login with email & password |
| `GET` | `/auth/getUser` 🔒 | Get current user info |
| `POST` | `/auth/forgot-password` | Send password reset OTP |
| `POST` | `/auth/reset-password` | Reset password with OTP |
| `POST` | `/auth/resend-otp` | Resend OTP (verify or reset) |
| `POST` | `/auth/upload-image` | Upload profile image (base64) |

### Income 🔒
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/income/add` | Add new income entry |
| `GET` | `/income/get` | Get all income entries |
| `GET` | `/income/downloadexcel` | Download income as Excel |
| `DELETE` | `/income/:id` | Delete an income entry |

### Expense 🔒
| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/expense/add` | Add new expense entry |
| `GET` | `/expense/get` | Get all expense entries |
| `GET` | `/expense/downloadexcel` | Download expenses as Excel |
| `DELETE` | `/expense/:id` | Delete an expense entry |

### Dashboard 🔒
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/dashboard` | Get aggregated financial summary |

### Profile 🔒
| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/profile` | Get user profile |
| `PUT` | `/profile` | Update profile (name, email) |
| `POST` | `/profile/upload-avatar` | Upload profile avatar |

## 📜 License
This project is for educational and portfolio purposes. All rights reserved.
