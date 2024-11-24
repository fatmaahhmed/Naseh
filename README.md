# Naseh

# Restaurant Chain Analytics System 🍽️

A modern JavaScript-based application for managing and analyzing restaurant chain data with AI-powered insights, multilingual support, and secure access control.

## 🌟 Features

- **🔐 Secure Authentication**
  - JWT-based user authentication
  - Role-based access control
  - Branch-level data permissions

- **📊 Analytics**
  - AI-powered insights using ChatGPT
  - Real-time sales analysis
  - Performance tracking
  - Custom report generation

- **🌐 Multilingual Support**
  - Arabic and English interfaces
  - Multilingual reporting
  - Localized data formatting

- **📈 Reporting**
  - Excel report generation
  - Custom data views
  - Automated insights

## 📋 Prerequisites

```bash
Node.js >= 18
PostgreSQL >= 14
OpenAI API key
```

## 🚀 Quick Start

1. **Clone the repository**
```bash
git clone https://github.com/your-username/restaurant-analytics.git
cd restaurant-analytics
```

2. **Install dependencies**
```bash
npm install
```

3. **Set up environment variables**
Create a `.env` file in the root directory:
```env
DATABASE_URL=postgresql://user:password@localhost:5432/restaurant_db
JWT_SECRET=your-secret-key
OPENAI_API_KEY=your-openai-key
PORT=3000
```

4. **Initialize database**
```bash
npm run init-db
```

5. **Start the application**
```bash
npm start
```

## 🏗️ Project Structure

```
src/
├── config/          # Configuration files
│   ├── database.js
│   └── openai.js
├── models/          # Database models
│   ├── user.js
│   ├── branch.js
│   └── sales.js
├── middleware/      # Custom middleware
│   ├── auth.js
│   └── accessControl.js
├── services/        # Business logic
│   ├── chatService.js
│   ├── reportService.js
│   └── analyticsService.js
└── routes/          # API routes
    ├── auth.js
    ├── analytics.js
    └── reports.js
```

## 🔧 Configuration

### Database Setup

1. **Create database tables**
```sql
-- Users table
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  username VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  allowed_branches INTEGER[]
);

-- Branches table
CREATE TABLE branches (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  location VARCHAR(255) NOT NULL
);

-- Sales table
CREATE TABLE sales (
  id SERIAL PRIMARY KEY,
  branch_id INTEGER REFERENCES branches(id),
  item_name VARCHAR(255) NOT NULL,
  quantity INTEGER NOT NULL,
  price DECIMAL(10,2) NOT NULL,
  sale_date TIMESTAMP NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

2. **Create optimization views**
```sql
CREATE OR REPLACE VIEW branch_sales_summary AS
SELECT 
  b.id as branch_id,
  b.name as branch_name,
  DATE_TRUNC('month', s.sale_date) as month,
  SUM(s.quantity * s.price) as total_sales,
  COUNT(DISTINCT s.id) as transaction_count
FROM branches b
JOIN sales s ON b.id = s.branch_id
GROUP BY b.id, b.name, DATE_TRUNC('month', s.sale_date);
```

## 📡 API Endpoints

### Authentication

```http
POST /api/auth/login
Content-Type: application/json

{
  "username": "user@example.com",
  "password": "secure_password"
}
```

### Analytics

```http
# Get branch sales
GET /api/analytics/branch-sales/{branchId}
Authorization: Bearer <token>

# Chat analysis
POST /api/analytics/chat-analysis
Authorization: Bearer <token>
Content-Type: application/json

{
  "query": "Show me sales trends for last month",
  "language": "en"
}

# Generate report
GET /api/analytics/export-report
Authorization: Bearer <token>
Query Parameters: startDate, endDate, language
```

## 🔒 Security

- JWT-based authentication
- Password hashing with bcrypt
- Branch-level access control
- Request validation
- SQL injection protection

## 📊 Usage Examples

### User Authentication
```javascript
// Login
const response = await fetch('/api/auth/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    username: 'user@example.com',
    password: 'password123'
  })
});

const { token } = await response.json();
```

### Getting Sales Data
```javascript
// Fetch branch sales
const sales = await fetch('/api/analytics/branch-sales/1', {
  headers: {
    'Authorization': `Bearer ${token}`
  }
});

const data = await sales.json();
```

### Generating Reports
```javascript
// Get Excel report
const report = await fetch('/api/analytics/export-report?startDate=2024-01-01&endDate=2024-01-31&language=en', {
  headers: {
    'Authorization': `Bearer ${token}`
  }
});

const blob = await report.blob();
```

## 🚀 Development

### Running Tests
```bash
npm test
```

### Code Linting
```bash
npm run lint
```

### Building for Production
```bash
npm run build
```

## 📈 Performance Optimization

- Database connection pooling
- Query optimization with views
- Caching strategies
- Efficient data pagination

## 🔄 Error Handling

The application includes comprehensive error handling:
- Validation errors
- Authentication errors
- Database errors
- API errors

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## 👥 Support

For support, email support@example.com or join our Slack channel.

## 🙏 Acknowledgments

- OpenAI for ChatGPT API
- Express.js team
- PostgreSQL community

---

