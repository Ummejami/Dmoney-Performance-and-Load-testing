# 💰 Dmoney Performance Testing (JMeter)

## 📌 Project Overview
This project contains performance and functional testing of the Dmoney system using Apache JMeter.  
It simulates different financial transactions such as deposit, send money, and payment.

---

## 📂 Project Files
- **Dmoney.jmx** → Main JMeter test plan  
- **deposite.csv** → Data file for deposit transactions  
- **sendmoney.csv** → Data file for send money transactions  
- **payment.csv** → Data file for payment transactions  

---

## 🛠️ Tools & Concepts Used

- **Loop Controller**
  - Used to repeat API requests and simulate multiple user actions (Agent log in once and deposite money to one more customer through reuse token)
- **HTTP Header Manager**
  - Managed request headers such as Authorization token and Content-Type

- **Response Assertion**
  - Validated API responses (status code, message) to ensure correct behavior

- **Chaining Requests**
  - Maintained proper flow between APIs (e.g., Login → OTP → Transaction)
  - Passed dynamic data (token, userID) between requests

- **User Defined Variables**
  - Stored reusable values (e.g., base URL, credentials) for better maintainability

- **Random Variable**
  - Generated dynamic data for transaction amount

- **Listeners**
  - Used tools like View Results Tree and Summary Report to analyze test results
- **CSV Data Set Config**
  - Used to read test data from external CSV files
  - Supplied dynamic inputs such as user credentials (phone, password)
  - Enabled data-driven testing for multiple users
  - Helped simulate real-world scenarios with different datasets
- **JDBC Connection & JDBC Request**
  - Configured database connection in JMeter
  - Executed SQL queries directly (Extract OTP)
  - Used for test data setup and cleanup (e.g., activating users,delete last 10 transaction to avoid Daily transaction limit)
---

## ▶️ How to Run the Test

1. Open Apache JMeter  
2. Click on **File → Open**  
3. Select `Dmoney.jmx`  
4. Ensure all CSV files are properly linked  
5. Click on **Start (▶️)** to run the test  

---

## 📊 Test Scenarios
- ✅ Deposit Money  
- ✅ Send Money  
- ✅ Payment  

---
## 📸 Test Results

<p align="center">
  <strong>🔹 Request Summary</strong>
</p>

![Request Summary](https://github.com/Ummejami/Dmoney-Performance-and-Load-testing/blob/main/Images/request-summary.png)

---

<p align="center">
  <strong>🔹 Statistics</strong>
</p>

![Statistics](https://github.com/Ummejami/Dmoney-Performance-and-Load-testing/blob/main/Images/statistics.png)

---
## 📂 Structure Of Project
```
main/
│
├── Dmoney.jmx
├── README.md
│
├── Resources/
│   ├── deposite.csv
│   ├── sendmoney.csv
│   └── payment.csv
│
├── UserData/
│   ├── userlogin(Agent).csv
│   ├── userlogin(Customer_Payment).csv
│   └── userlogin(Customer_SendMoney).csv
│
└── Images/
    ├── request-summary.png
    └── statistics.png
```


---

## 📚 Issues Faced & Fixes

During JMeter performance testing, I encountered several practical issues and learned how to resolve them effectively.

---

### 🚨 Problem 1: Unauthorized Error Using Same CSV in Multiple Thread Groups

#### ❗ Issue
Using the same customer CSV file across multiple thread groups (Send Money & Payment) caused `401 Unauthorized` errors.

#### 🔍 Cause
- Same user logged in from multiple threads simultaneously  
- Backend invalidated previous tokens  

#### ✅ Solution
- Used separate CSV files for each thread group  
- Assigned unique users per thread  
  

---

### 🚨 Problem 2: Multiple Authorization Headers in One Request

#### ❗ Issue
Adding more than one `Authorization` header in a single request resulted in authentication failure.
I used Admin_token and User_token at once. 
#### 🔍 Cause
- HTTP does not support multiple Authorization headers reliably  
- Server may read incorrect token or reject request  

#### ✅ Solution
- Ensured only one `Authorization` header per request    
---
### 💡 Key Takeaway

> Proper data handling and variable management are critical for reliable performance testing in JMeter.
