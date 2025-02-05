# Project Proposal for Personal Finance Management App

## Executive Summary
The Personal Finance Management App is designed to provide users with an easy-to-use tool for tracking their financial transactions, managing budgets, and gaining insights into their spending habits. Unlike existing online services that connect to banks and often come with subscription fees, our app offers a simpler, free solution for personal use, accessible both via web and mobile platforms.

## Project Background
Many existing financial tracking services can connect directly to banks to gather transaction data. However, these services are not without flaws: some banks deny access requests, and the services typically come with a cost. Our app aims to offer a simpler, cost-free alternative for users who want to manually track their finances without the complexities and fees of current solutions.

## Project Vision & Success Criteria
The goal of this project is to empower users to manage their finances more effectively by providing a clear view of their income, expenses, and budgets. Success will be measured by user engagement and feedback, the number of active users, and the app's ability to help users make informed financial decisions.

## Potential Risks and Mitigation Strategies
While using AWS, a trusted and secure cloud service, minimizes many potential risks, we will also implement strong encryption and follow best practices for data security to protect user information.

## Project Scope & Deliverables
**Initial Phase (2 weeks):**
- **API Engineering:** Develop and test the backend API using C# and deploy it on AWS ECS Fargate with a MySQL database on AWS RDS.
- **Frontend Development:** Create a basic web interface using React and a mobile app using React Native Expo.
- **Dashboard:** Implement a simple dashboard for users to view their financial summary, including total income, expenses, and recent transactions.
- **Accounts & Transactions:** Enable users to add accounts and transactions, and view account balances.

**Future Iterations:**
- **Mobile Deployment:** Extend the mobile app to support both Android and iOS platforms.
- **Enhanced Features:** Introduce budget management, notifications, and detailed reporting functionalities.

## Expected Benefits
The app will provide users with a straightforward tool to track their finances, helping them make better financial decisions and manage their budgets effectively. Over time, additional features will enhance the user experience and provide deeper financial insights.

## Project Resource Requirements
- **Technologies:** React, C#, React Native Expo, AWS ECS Fargate, AWS RDS, Swagger, GitHub
- **Tools:** Visual Studio Code, Postman, Expo Go, AWS Console

## Project Timeline
**Day 1 - Day 3:**
- API Engineering: Develop and test backend API using C#.
- Set up AWS ECS Fargate and RDS.

**Day 4 - Day 7:**
- Frontend Development: Create web interface using React.
- Implement basic dashboard and account management.

**Day 8 - Day 10:**
- Mobile Development: Start with React Native Expo for the mobile app.
- Ensure account and transaction management work on mobile.

**Day 11 - Day 14:**
- Testing: Perform thorough testing across web and mobile platforms.
- Deployment: Deploy backend to AWS and finalize local deployment for frontend.

# Requirement Definition for Personal Finance Management App

## Functionality

### User Management
- **User Registration and Login:**
  - Allow users to create an account using email and password.

### Dashboard
- **Overview:**
  - Provide a summary view of the user's financial status, including total income, total expenses, and balance.
  - Display recent transactions.

### Accounts Management
- **Account Types:**
  - Allow users to add multiple account types (e.g., bank accounts, credit cards, cash).
  - Enable users to name and categorize their accounts.
- **Account Overview:**
  - Display balance for each account.

### Transaction Management
- **Add Transactions:**
  - Allow users to manually add transactions (income or expense).
  - Enable categorization of transactions (e.g., food, rent, entertainment).
  - Provide fields for amount, date, account, category, and description.
- **Edit/Delete Transactions:**
  - Allow users to edit or delete existing transactions.

### Budget Management
- **Set Budgets:**
  - Enable users to set monthly budgets for different categories (e.g., groceries, utilities).
- **Track Budgets:**
  - Display budget utilization (amount spent vs. budget limit) for each category.

### Reporting
- **Basic Reports:**
  - Provide a summary report of income and expenses by category.
  - Allow users to view reports for different time periods (e.g., weekly, monthly, yearly).

### Notifications
- **Alerts and Reminders:**
  - Notify users of budget limits reached.

### Settings
- **Profile Management:**
  - Allow users to update personal information and change passwords.
- **App Preferences:**
  - Enable users to customize app settings, such as notification preferences.


## Entity Definitions

### USER
- **userId**: Unique identifier for the user (Primary Key).
- **email**: Email address of the user.
- **password**: Password for user authentication.
- **name**: Name of the user.

### ACCOUNT
- **accountId**: Unique identifier for the account (Primary Key).
- **name**: Name of the account.
- **type**: Type of the account (e.g., bank account, credit card, cash).
- **balance**: Current balance of the account.
- **userId**: Identifier of the user who owns the account (Foreign Key).

### TRANSACTION
- **transactionId**: Unique identifier for the transaction (Primary Key).
- **amount**: Amount of the transaction.
- **date**: Date of the transaction.
- **type**: Type of transaction (income or expense).
- **category**: Category of the transaction (e.g., food, rent, entertainment).
- **description**: Description of the transaction.
- **accountId**: Identifier of the account associated with the transaction (Foreign Key).

### BUDGET
- **budgetId**: Unique identifier for the budget (Primary Key).
- **category**: Category for which the budget is set.
- **amount**: Amount allocated for the budget.
- **userId**: Identifier of the user who sets the budget (Foreign Key).

### REPORT
- **reportId**: Unique identifier for the report (Primary Key).
- **startDate**: Start date of the report period.
- **endDate**: End date of the report period.
- **userId**: Identifier of the user who generates the report (Foreign Key).

### NOTIFICATION
- **notificationId**: Unique identifier for the notification (Primary Key).
- **message**: Notification message.
- **date**: Date of the notification.
- **type**: Type of notification (e.g., alert, reminder).
- **userId**: Identifier of the user who receives the notification (Foreign Key).

### SETTINGS
- **settingsId**: Unique identifier for the settings (Primary Key).
- **emailNotifications**: Preference for email notifications.
- **userId**: Identifier of the user who configures the settings (Foreign Key).

```mermaid
erDiagram
    USER {
        int userId PK
        string email
        string password
        string name
    }
    
    ACCOUNT {
        int accountId PK
        string name
        string type
        float balance
        int userId FK
    }

    TRANSACTION {
        int transactionId PK
        float amount
        date date
        string type
        string category
        string description
        int accountId FK
    }
    
    BUDGET {
        int budgetId PK
        string category
        float amount
        int userId FK
    }
    
    REPORT {
        int reportId PK
        date startDate
        date endDate
        int userId FK
    }
    
    NOTIFICATION {
        int notificationId PK
        string message
        date date
        string type
        int userId FK
    }
    
    SETTINGS {
        int settingsId PK
        boolean emailNotifications
        int userId FK
    }
    
    USER ||--o{ ACCOUNT: owns
    USER ||--o{ BUDGET: sets
    USER ||--o{ REPORT: generates
    USER ||--o{ NOTIFICATION: receives
    USER ||--o{ SETTINGS: configures
    ACCOUNT ||--o{ TRANSACTION: records
```

## API Endpoints

### User Management

#### ✅ Register a new user
- **Endpoint:** `POST /api/users/register`
- **Request Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "password123",
    "name": "User Name"
  }
  ```
- **Expected Response:**
  ```json
  {
    "userId": 1,
    "email": "user@example.com",
    "name": "User Name"
  }
  ```

#### ✅ Login a user
- **Endpoint:** `POST /api/users/login`
- **Request Body:**
  ```json
  {
    "email": "user@example.com",
    "password": "password123"
  }
  ```
- **Expected Response:**
  ```json
  {
    "userId": 1,
    "email": "user@example.com",
    "name": "User Name"
  }
  ```

### Dashboard

#### ✅ Get dashboard overview
- **Endpoint:** `GET /api/dashboard`
- **Query Parameters:**
  - `userId` (required): The ID of the user for whom the dashboard summary is to be retrieved.
- **Response:**
  ```json
  {
    "totalIncome": 1000.00,
    "totalExpenses": 500.00,
    "balance": 1500.00,
    "recentTransactions": [
      {
        "transactionId": 1,
        "amount": 100.00,
        "type": "income",
        "category": "salary",
        "description": "Monthly salary",
        "date": "2023-01-01T00:00:00"
      },
      {
        "transactionId": 2,
        "amount": 50.00,
        "type": "expense",
        "category": "groceries",
        "description": "Grocery shopping",
        "date": "2023-01-02T00:00:00"
      },
      ...
    ]
  }
  ```

### Accounts Management

#### ✅ Add a new account
- **Endpoint:** `POST /api/accounts/{userId}`
- **Query Parameters:**
  - `userId` (required): The ID of the user to whom the new account will be associated.
- **Request Body:**
  ```json
  {
    "name": "Savings Account",
    "type": "bank account",
    "balance": 1000.00
  }
  ```
- **Expected Response:**
  ```json
  {
    "accountId": 1,
    "name": "Savings Account",
    "type": "bank account",
    "balance": 1000.00,
    "userId": 1
  }
  ```

#### ✅ Get all accounts
- **Endpoint:** `GET /api/accounts/{userId}`
- **Query Parameters:**
  - `userId` (required): The ID of the user whose accounts are to be retrieved.
- **Expected Response:**
  ```json
  [
    {
      "accountId": 1,
      "name": "Savings Account",
      "type": "bank account",
      "balance": 1000.00,
      "userId": 1
    },
    {
      "accountId": 2,
      "name": "Credit Card",
      "type": "credit card",
      "balance": -500.00,
      "userId": 1
    }
  ]
  ```

#### ✅ Update an account
- **Endpoint:** `PUT /api/accounts/{account_id}`
- **Path Parameters:**
  - `account_id` (required): The ID of the account to be updated.
- **Request Body:**
  ```json
  {
    "name": "Updated Account Name",
    "type": "credit card",
    "balance": 1500.00
  }
  ```
- **Expected Response:**
  ```json
  {
    "accountId": 1,
    "name": "Updated Account Name",
    "type": "credit card",
    "balance": 1500.00,
    "userId": 1
  }
  ```

#### ✅ Delete an account
- **Endpoint:** `DELETE /api/accounts/{account_id}`
- **Path Parameters:**
  - `account_id` (required): The ID of the account to be deleted.
- **Expected Response:**
  - Status: `204 No Content`

### Transaction Management

#### ✅ Add a transaction
- **Endpoint:** `POST /api/transactions`
- **Request Body:**
  ```json
  {
    "amount": 100,
    "date": "2023-01-01",
    "type": "expense",
    "category": "food",
    "description": "Grocery shopping",
    "account_id": 1
  }
  ```

#### ✅ Get transactions
- **Endpoint:** `GET /api/transactions`
- **Response:**
  ```json
  [
    {
      "transaction_id": 1,
      "amount": 100,
      "date": "2023-01-01",
      "type": "expense",
      "category": "food",
      "description": "Grocery shopping",
      "account_id": 1
    },
    ...
  ]
  ```

#### ✅ Update a transaction
- **Endpoint:** `PUT /api/transactions/{transaction_id}`
- **Request Body:**
  ```json
  {
    "amount": 150,
    "date": "2023-01-01",
    "type": "expense",
    "category": "food",
    "description": "Grocery shopping updated",
    "account_id": 1
  }
  ```

#### ✅ Delete a transaction
- **Endpoint:** `DELETE /api/transactions/{transaction_id}`

### Budget Management

#### Set a budget
- **Endpoint:** `POST /api/budgets`
- **Request Body:**
  ```json
  {
    "category": "groceries",
    "amount": 300
  }
  ```

#### Get budgets
- **Endpoint:** `GET /api/budgets`
- **Response:**
  ```json
  [
    {
      "budget_id": 1,
      "category": "groceries",
      "amount": 300
    },
    ...
  ]
  ```

#### Update a budget
- **Endpoint:** `PUT /api/budgets/{budget_id}`
- **Request Body:**
  ```json
  {
    "category": "groceries",
    "amount": 350
  }
  ```

#### Delete a budget
- **Endpoint:** `DELETE /api/budgets/{budget_id}`

### Reporting

#### Generate a report
- **Endpoint:** `POST /api/reports`
- **Request Body:**
  ```json
  {
    "start_date": "2023-01-01",
    "end_date": "2023-01-31"
  }
  ```
- **Response:**
  ```json
  {
    "report_id": 1,
    "start_date": "2023-01-01",
    "end_date": "2023-01-31",
    "data": {
      "income": [...],
      "expenses": [...]
    }
  }
  ```

#### Get reports
- **Endpoint:** `GET /api/reports`
- **Response:**
  ```json
  [
    {
      "report_id": 1,
      "start_date": "2023-01-01",
      "end_date": "2023-01-31"
    },
    ...
  ]
  ```

### Notifications

#### Get notifications
- **Endpoint:** `GET /api/notifications`
- **Response:**
  ```json
  [
    {
      "notification_id": 1,
      "message": "Budget limit reached for groceries",
      "date": "2023-01-15",
      "type": "alert"
    },
    ...
  ]
  ```

#### Delete a notification
- **Endpoint:** `DELETE /api/notifications/{notification_id}`

### Settings

#### Get user settings
- **Endpoint:** `GET /api/settings`
- **Response:**
  ```json
  {
    "settings_id": 1,
    "email_notifications": true
  }
  ```

#### Update user settings
- **Endpoint:** `PUT /api/settings`
- **Request Body:**
  ```json
  {
    "email_notifications": true
  }
  ```

## App Architecture

```mermaid

graph LR
    subgraph Client Side
        RN[React Native App]
    end

    subgraph AWS
        ECS[Amazon ECS]
        RDS[(Amazon RDS)]
    end

    RN -->|API Requests| ECS
    ECS -->|Database Queries| RDS

```
