# simple-php-rest-api

This API allows for managing part numbers in a manufacturer database. It provides CRUD (Create, Read, Update, Delete) functionality for part numbers, enabling users to retrieve, add, update, and delete part records.

## Table of Contents
- [Technologies Used](#technologies-used)
- [Installation](#installation)
- [Database Setup](#database-setup)
- [API Endpoints](#api-endpoints)
- [Request & Response Examples](#request--response-examples)
- [Error Handling](#error-handling)
- [License](#license)

## Technologies Used
- **PHP** (backend language)
- **MySQL** (database)
- **WAMP/XAMPP/MAMP** (for local development)
- **JSON** (for request and response payloads)

## Installation

### Requirements
- PHP 7.x or higher
- MySQL database (or MariaDB)
- A web server like Apache (e.g., using WAMP, XAMPP, or MAMP)

### Steps
1. **Clone the Repository**: Clone the project into your local machine.
   ```bash
   git clone https://github.com/yourusername/part-number-api.git
Configure Database Connection:

Open the config/db.php file and update your MySQL connection details:
php
Copy code
$host = 'localhost';
$username = 'root';
$password = '';
$database = 'manufacturer_db';
Start Your Web Server: Ensure your Apache server (e.g., WAMP, XAMPP, or MAMP) is running.

Access the API: You can now start making requests to the API using tools like Postman, cURL, or directly from your front-end app.

Database Setup
Create a Database: Create a new database in your MySQL server.

sql
Copy code
CREATE DATABASE manufacturer_db;
Create the part_numbers Table: Run the following SQL to create the part_numbers table.

sql
Copy code
CREATE TABLE `part_numbers` (
  `id` INT NOT NULL AUTO_INCREMENT,
  `part_number` VARCHAR(255) NOT NULL,
  `name` VARCHAR(255) NOT NULL,
  `description` TEXT,
  `price` DECIMAL(10, 2) NOT NULL,
  PRIMARY KEY (`id`)
);
(Optional) Insert Sample Data: You can insert some sample part numbers into the table.

sql
Copy code
INSERT INTO `part_numbers` (`part_number`, `name`, `description`, `price`) VALUES
('PN-001', 'Part A', 'Description of Part A', 100.00),
('PN-002', 'Part B', 'Description of Part B', 150.00),
('PN-003', 'Part C', 'Description of Part C', 200.00);
API Endpoints
1. GET /api/part-numbers
Description: Retrieve all part numbers or a specific part number by ID.
Query Parameters:
id (optional) — Retrieve a specific part number by its ID.
Response:
200 OK — Returns a list of part numbers or the specific part number if an ID is provided.
2. POST /api/part-numbers
Description: Create a new part number record.
Request Body (JSON):
json
Copy code
{
  "part_number": "ABC123",
  "name": "Widget Part",
  "description": "This is a widget part.",
  "price": 49.99
}
Response:
201 Created — Returns the ID of the newly created part.
3. PUT /api/part-numbers?id={id}
Description: Update an existing part number.

Query Parameters:

id — The ID of the part to be updated.
Request Body (JSON):

json
Copy code
{
  "part_number": "ABC123",
  "name": "Updated Widget Part",
  "description": "This is the updated widget part.",
  "price": 59.99
}
Response:

200 OK — Returns a success message when the part is updated.
4. DELETE /api/part-numbers?id={id}
Description: Delete a part number by ID.

Query Parameters:

id — The ID of the part to be deleted.
Response:

200 OK — Returns a success message if the part is deleted.
Request & Response Examples
1. GET All Part Numbers
Request:
bash
Copy code
curl -X GET http://localhost/api/part-numbers
Response:
json
Copy code
[
  {
    "id": 1,
    "part_number": "ABC123",
    "name": "Widget Part",
    "description": "This is a widget part.",
    "price": 49.99
  },
  {
    "id": 2,
    "part_number": "XYZ456",
    "name": "Gadget Part",
    "description": "This is a gadget part.",
    "price": 29.99
  }
]
2. POST a New Part Number
Request:
bash
Copy code
curl -X POST http://localhost/api/part-numbers \
  -H "Content-Type: application/json" \
  -d '{"part_number": "DEF789", "name": "New Widget", "description": "A new widget part", "price": 69.99}'
Response:
json
Copy code
{
  "message": "Part added successfully",
  "id": 3
}
3. PUT Update an Existing Part
Request:
bash
Copy code
curl -X PUT http://localhost/api/part-numbers?id=3 \
  -H "Content-Type: application/json" \
  -d '{"part_number": "DEF789", "name": "Updated Widget", "description": "Updated description", "price": 79.99}'
Response:
json
Copy code
{
  "message": "Part updated successfully"
}
4. DELETE a Part
Request:
bash
Copy code
curl -X DELETE http://localhost/api/part-numbers?id=3
Response:
json
Copy code
{
  "message": "Part deleted successfully"
}
Error Handling
For any unsupported HTTP methods or invalid requests, the API returns a message like:

json
Copy code
{
  "message": "Unsupported method"
}
Database connection errors or query execution errors are also handled and returned as JSON with an appropriate message.

License
This project is licensed under the MIT License.
