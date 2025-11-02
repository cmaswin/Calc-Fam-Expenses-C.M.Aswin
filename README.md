# Calc-Fam-Expenses-C.M.Aswin
# 💰 Calculating Family Expenses using ServiceNow

## 🧾 Overview
The **Family Expense Management System** is a ServiceNow-based application designed to help families efficiently **record, categorize, and analyze their daily and monthly expenses**. The system provides automation for recurring transactions, dashboards for insights, and role-based access for multiple users.  

This project aims to make family budgeting simple, automated, and data-driven.

---

## 👥 Team Information
**Team ID:** NM2025TMID02060  
**Team Leader:** Aswin C M  
**Team Members:**  
- Adhithya R  
- Anistan A  
- Arulraj R  

---

## 🚀 Project Phases

### 1️⃣ Ideation Phase
- Identified the problem: families lack an efficient system to manage expenses.
- Proposed an automated expense tracking system using **ServiceNow**.
- Core idea: Create a **Family Expense Management System** to record, analyze, and visualize expenses.
- Focus areas: financial visibility, prevention of overspending, real-time tracking, and automation of recurring payments.

---

### 2️⃣ Project Planning Phase
**Tools Used:**  
- ServiceNow App Engine Studio  
- Flow Designer  
- Reporting  

**Milestones:**
1. Set up the ServiceNow instance.  
2. Created update sets for version tracking.  
3. Designed tables for **Family Expenses** and **Daily Expenses**.  
4. Defined relationships and automation using business rules.  
5. Configured reports and dashboards.

**Team Responsibilities:**  
Each member contributed to table creation, UI design, script development, and testing to ensure a smooth implementation.

---

### 3️⃣ Project Design Phase
- Designed database schema with two main tables:
  - `Family Expenses` — stores overall summaries.
  - `Daily Expenses` — stores individual entries.
- Linked tables for dynamic updates.
- Created user-friendly forms with fields:
  - Date, Amount, Expense Details, Family Member Name.
- Implemented business rules for automatic total updates.

---

### 4️⃣ Requirement Analysis
**Functional Requirements:**
- Add and view daily and total expenses.
- Auto-update totals in real-time.
- Support multiple family members (multi-user roles).
- Generate analytical dashboards and reports.

**Technical Requirements:**
- ServiceNow Developer Instance  
- App Engine Studio  
- Flow Designer  
- Business Rules for scripting  
- Reporting and Dashboard modules  

---

### 5️⃣ Performance Testing
**Testing Parameters:**
- Speed of data entry and update  
- Accuracy of total calculations  
- System responsiveness under concurrent usage  
- Validation of business rules and automation  
- Dashboard data refresh rates  

**Results:**  
✔️ Fast data updates  
✔️ Accurate calculations  
✔️ Real-time dashboard performance  
✔️ Smooth automation with minimal latency  

---

## 🧩 Problem Statement
There is no efficient, automated platform for families to manage expenses in real time. Manual methods cause poor financial tracking, overspending, and missed payments.

---

## 🎯 Objective
To design and develop a ServiceNow-based system that enables users to:
- Input and categorize expenses easily.  
- Automate recurring expenses (e.g., rent, subscriptions).  
- Track and visualize monthly/weekly spending.  
- Set budget limits and receive alerts.  
- Share visibility with family members.

---

## 🛠️ Skills and Tools Used
- **ServiceNow App Development (App Engine Studio)**
- **Custom Tables & Data Modeling**
- **Form Design & UI Customization**
- **Flow Designer (for automation)**
- **Business Rules & Scripting**
- **Reporting & Dashboards**
- **User Roles & Access Control (ACLs)**

---

## 🧱 Project Milestones

| Milestone | Description |
|------------|-------------|
| 1️⃣ Instance Setup | Created personal developer instance on ServiceNow |
| 2️⃣ Update Set | Created “Family Expenses” update set for version tracking |
| 3️⃣ Family Expenses Table | Defined structure and columns (Number, Date, Amount, Expense Details) |
| 4️⃣ Daily Expenses Table | Added daily entry table with fields and auto-numbering |
| 5️⃣ Relationship | Linked `Daily Expenses` to `Family Expenses` |
| 6️⃣ Related List | Added `Daily Expenses` related list to `Family Expenses` form |
| 7️⃣ Business Rule | Automated total updates using GlideRecord scripting |
| 8️⃣ Query Relationship | Filtered data by matching dates for relational accuracy |

---

## 🧠 Business Rule Script Example

```javascript
(function executeRule(current, previous /*null when async*/) {

  var FamilyExpenses = new GlideRecord('u_family_expenses');
  FamilyExpenses.addQuery('u_date', current.u_date);
  FamilyExpenses.query();

  if (FamilyExpenses.next()) {
      FamilyExpenses.u_amount += current.u_expense;
      FamilyExpenses.u_expense_details += " > " + current.u_comments + ": Rs." + current.u_expense + "/-";
      FamilyExpenses.update();
  } else {
      var NewFamilyExpenses = new GlideRecord('u_family_expenses');
      NewFamilyExpenses.u_date = current.u_date;
      NewFamilyExpenses.u_amount = current.u_expense;
      NewFamilyExpenses.u_expense_details = " > " + current.u_comments + ": Rs." + current.u_expense + "/-";
      NewFamilyExpenses.insert();
  }

})(current, previous);

