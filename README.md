# Digitizing the Data for Lawn Squad
### Transforming a Small Business's Operations with a Structured SQL Database

## Overview
Lawn Squad, a Calgary-based lawn care business offering aeration, power raking,
window cleaning, and fertilization, relied on manual, paper-based scheduling with
no centralized customer database and no way to track employee assignments. This
project designs and implements a structured relational database in Azure SQL to
replace manual logs with an automated, scalable system — turning raw transaction
data into actionable business insight.

## Mission
To design and implement a digital data system for Lawn Squad that replaces manual
logs with automated, scalable workflows.

## Key Objectives
- **Digitize Operations** — replace manual logs with an automated system
- **Automate Business Insights** — transform raw data into actionable reports
- **Optimize Resource Allocation** — use historical data to predict demand and schedule staff/materials
- **Reduce Costs & Errors** — eliminate double bookings and payment errors

## Entity Relationship Design
A star-schema database with **Sales** as the central fact table, linking five core entities:

| Entity | Purpose |
|---|---|
| Customers | Tracks client details and service history |
| Employees | Holds staff details involved in service delivery |
| Services | Lists lawn care offerings and pricing |
| Payment Methods | Records payment options used in transactions |
| Reviews | Captures customer feedback and ratings |

**Relationships:**
- Employees → Sales (One-to-Many)
- Customers → Sales (One-to-Many)
- Sales → Services (Many-to-One)
- Sales → Payment Methods (Many-to-One)
- Customers → Reviews (One-to-Many)

The `Sales` table acts as the fact table, with foreign keys to `customer_id`,
`employee_id`, `service_id`, and `payment_method_id`, plus `total_amount` and
`service_date` for financial tracking.

## Implementation
Implemented as a full relational schema in **Azure SQL**, including:
- Table creation with primary/foreign key constraints across all five entities
- Sample data population for employees, services, customers, payment methods, and sales

## SQL Views
Three views were built to turn raw transactional data into business-ready insight:

1. **`View_Windowcleaning_Employees`** — lists employees who performed Window Cleaning services, via a subquery joining employees, sales, and services
2. **`View_ServiceAssignments`** — a general employee-to-service mapping using inner joins across sales, employees, and services, for tracking which staff performed which services
3. **`View_CustomerServiceHistory`** — a full customer summary (total services booked, total spent, last service date, services used) using `LEFT JOIN`, `COUNT`, `SUM`, `MAX`, and `GROUP_CONCAT`, so customers with no purchase history are still included

## Conclusion
The project replaces Lawn Squad's manual scheduling and tracking with a structured
SQL system that eliminates double bookings and payment errors, while the automated
views surface actionable insight — from employee performance to customer
preferences — to support scheduling, service quality, and sustainable growth. It
also lays the groundwork for future enhancements such as demand forecasting and
dynamic pricing.

## Author
Ramya Ramesh — Data Science Student, SAIT
