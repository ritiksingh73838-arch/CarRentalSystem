# Features
- View available cars
- Rent a car (customer name, 10-digit phone and 12-digit Aadhar validation)
- Already-rented cars cannot be rented again
- Return a car
- Add a new car
- Delete a car (with confirmation)

## Tech Stack
- Java
- JDBC (MySQL Connector/J)
- MySQL
- IntelliJ IDEA

## Security
- All queries use PreparedStatement (protects against SQL injection)
- Database credentials are kept in config.properties, which is excluded from Git via .gitignore

## Database Setup
sql
CREATE DATABASE IF NOT EXISTS car_rental_db;
USE car_rental_db;

CREATE TABLE cars (
    car_id VARCHAR(10) PRIMARY KEY,
    brand VARCHAR(50) NOT NULL,
    model VARCHAR(50) NOT NULL,
    price_per_day DECIMAL(10,2) NOT NULL,
    is_available BOOLEAN DEFAULT TRUE
);

CREATE TABLE customers (
    customer_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    phone VARCHAR(15) NULL,
    aadhar VARCHAR(12) NULL
);

CREATE TABLE rentals (
    rental_id INT AUTO_INCREMENT PRIMARY KEY,
    car_id VARCHAR(10) NOT NULL,
    customer_id INT NOT NULL,
    days INT NOT NULL,
    rent_date DATE DEFAULT (CURRENT_DATE),
    return_date DATE NULL,
    FOREIGN KEY (car_id) REFERENCES cars(car_id),
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);


## How to Run
1. Install MySQL and create the database using the SQL above.
2. Add mysql-connector-j to the project libraries.
3. Create a config.properties file in the project root:
   
   db.url=jdbc:mysql://localhost:3306/car_rental_db
   db.username=root
   db.password=your_password_here
   
4. Run the Main class.

## Author
*Ritik Singh*
- GitHub: https://github.com/ritiksingh73838-arch
- Email: your_email@gmail.com
