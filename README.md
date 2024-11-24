# Naseh
Here is the README format based on your project requirements:

Restaurant Chain Data Management Application

Overview

This application is designed to manage and analyze customer and sales data for a restaurant chain using the ChatGPT API. It features user authentication, access control based on permissions, real-time data analysis, chat functionality for generating insights, and report generation in multiple languages (Arabic and English).

Features

	1.	User Authentication and Access Control:
	•	Users log in using their credentials (email and password).
	•	Upon successful login, the system verifies the user’s access rights.
	•	Each user is granted access to specific rows of data based on permissions (e.g., Fatma can access branches 1 and 2, while Yomna can access branches 3 and 4).
	2.	Data Query and Analysis:
	•	Users can query the database for specific sales data based on their access permissions.
	•	The system uses database views to optimize queries and improve performance, especially for frequently requested data like sales summaries and top-selling products.
	3.	ChatGPT Integration:
	•	Users who are authorized to access the chat feature can interact with ChatGPT to get insights based on specific data queries.
	•	Example queries include:
	•	“Give me a sales summary for the last month.”
	•	“What are the top-selling items in branches 1 and 2?”
	4.	Excel Report Generation:
	•	The application can generate Excel reports based on data analysis results, allowing users to download and review their insights.
	•	Reports are generated in both Arabic and English.
	5.	Admin Panel:
	•	Admin users can manage the application’s users, control access rights, and monitor the overall performance of the system.

Workflow

	1.	User Login:
	•	Users enter their credentials to log in.
	•	The system authenticates the user and retrieves their user ID and permissions.
	2.	Access Control:
	•	Each user is granted access to specific data rows in the database.
	•	Permissions are checked before allowing users to query or view data.
	3.	Data Analysis:
	•	The user queries data (e.g., sales data) based on their access rights.
	•	The system uses database views to ensure fast and optimized data retrieval.
	4.	Chat Feature:
	•	Authorized users can interact with ChatGPT to receive tailored insights based on their queries.
	5.	Excel Report Generation:
	•	Once analysis is complete, users can generate reports in Excel format for further review.

Database Design

	•	Schema Overview:
	•	Users: Stores user details and access permissions.
	•	Sales Data: Stores data for each restaurant branch, including sales, products, and customer information.
	•	Reports: Stores generated reports linked to specific users.
	•	Example Schema:

{
  "Users": {
    "userID": "12345",
    "username": "Fatma",
    "email": "fatma@example.com",
    "permissions": ["branch1", "branch2"]
  },
  "SalesData": {
    "branchID": "branch1",
    "salesSummary": {"totalSales": 1000, "topSelling": "item1"},
    "products": ["item1", "item2"]
  },
  "Reports": {
    "reportID": "67890",
    "userID": "12345",
    "reportType": "salesSummary",
    "generatedDate": "2024-11-25",
    "language": "Arabic"
  }
}

Technologies Used

	•	Frontend: React.js or another framework (optional)
	•	Backend: Node.js, Express.js
	•	Database: MongoDB (with views for optimization)
	•	Authentication: JWT (JSON Web Token)
	•	API Integration: OpenAI ChatGPT API
	•	Excel Generation: ExcelJS or similar library
	•	Multilingual Support: i18n for language handling (Arabic & English)

Setup Instructions

1. Clone the Repository:

git clone <repository_url>

2. Install Dependencies:

cd <project_folder>
npm install

3. Configure Environment Variables:

	•	JWT_SECRET: Secret key for JWT authentication.
	•	CHATGPT_API_KEY: Your OpenAI API Key for ChatGPT integration.

4. Run the Application:

npm start

API Endpoints

	•	POST /login:
	•	Logs the user in and returns a JWT token.
	•	GET /sales-summary:
	•	Retrieves sales data for authorized branches.
	•	POST /generate-report:
	•	Generates an Excel report based on the user’s requested data analysis.

Usage Example

1. User Login

POST /login
Body: {
  "email": "fatma@example.com",
  "password": "password123"
}

2. Request Sales Summary

GET /sales-summary?branch=branch1

3. Generate Report

POST /generate-report
Body: {
  "type": "salesSummary",
  "branch": "branch1",
  "language": "English"
}

Future Enhancements

	•	Improve ChatGPT prompt engineering for better data-specific analysis.
	•	Admin Dashboard to manage users and monitor the system in real-time.
	•	More advanced report generation with customizable options.

License

This project is licensed under the MIT License - see the LICENSE file for details.

Let me know if you need any more details or adjustments!
