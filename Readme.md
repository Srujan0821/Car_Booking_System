# Cab Booking System

## Agile Methodology

Agile methodology is a flexible and iterative approach to software development and project management. It emphasizes collaboration, customer feedback, and small, rapid releases to deliver high-quality software efficiently. Agile promotes adaptability to changing requirements and focuses on delivering value incrementally.

For more details, refer to this [Agile Methodology Excel Document](https://cognizantonline-my.sharepoint.com/:x:/g/personal/2407095_cognizant_com/EThTb_syc7VHqSHrXskZEwMBLyQqeR839zSEuAlkQIOw3g?e=4dETKk).

## 1. Introduction
The **Cab Booking System** is a backend application built using **Java (Spring Boot)** that enables users to:
- Book rides.
- Manage payments.
- Rate and provide feedback for drivers.

This system is designed to handle core functionalities such as user management, ride booking, payment processing, and driver ratings. It is built with a modular architecture to ensure scalability and maintainability.

---

## 2. Features
- **User Management**: Register,login and manage users.
- **Ride Booking**: Book rides with available drivers and can view past booking.
- **Payment Processing**: Process payments for rides.
- **Driver Ratings**: Submit and retrieve ratings for drivers.
- **Exception Handling**: Custom exceptions for better error management.
- **Security**: 
    - **JWT Authentication**: Secure endpoints using JSON Web Tokens.
    - **Password Encryption**: Encrypt user passwords using industry-standard hashing algorithms (e.g., Base64).

---

## 3. Folder Structure
The project follows the standard **Spring Boot** structure:
```
cabbookingsystem/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── cabbookingsystem/
│   │   │           ├── controller/       # REST controllers
│   │   │           ├── service/          # Business logic
│   │   │           ├── repository/       # Data access layer
│   │   │           ├── model/            # Entity classes
│   │   │           ├── exception/        # Custom exceptions
│   │   │           └── CabBookingSystemApplication.java  # Main application class
│   │   └── resources/
│   │       ├── application.properties    # Configuration properties
│   │       └── static/                   # Static resources (if any)
│   └── test/
│       └── java/
│           └── com/
│               └── cabbookingsystem/
│                   └── tests/            # Unit and integration tests
├── pom.xml                               # Maven configuration file
└── README.md                             # Project documentation
```

---

## 4. Technologies Used
- **Java**: Programming language.
- **Spring Boot**: Backend framework.
- **Spring Data JPA**: ORM for database interactions.
- **MySQL**: Relational database.
- **Hibernate Validator**: For input validation.
- **Maven**: Dependency management.
- **Postman**: API testing.

---
## 5. Entity Models

The following are the core entity models used in the system:

### 1. **User**
| Field        | Type         | Description                     | Key         |
|--------------|--------------|---------------------------------|-------------|
| userId       | Long         | Unique identifier               | Primary Key |
| name         | String       | Name of the user                |             |
| email        | String       | Email address                   |             |
| phone        | String       | Phone number of the user        |             |
| passwordHash | String       | Hashed password for security    |             |
| createdAt    | LocalDateTime| Account creation timestamp      |             |

---

### 2. **Driver**
| Field           | Type    | Description                     | Key         |
|------------------|---------|---------------------------------|-------------|
| driverId        | Long    | Unique identifier               | Primary Key |
| name            | String  | Name of the driver              |             |
| phone           | String  | Phone number of the driver      |             |
| licenseNumber   | String  | Driver's license number         |             |
| vehicleDetails  | String  | Details of the driver's vehicle |             |
| status          | String  | Driver's status (ACTIVE, INACTIVE) | |

---

### 3. **Ride**
| Field           | Type           | Description                     | Key         |
|------------------|----------------|---------------------------------|-------------|
| rideId          | Long           | Unique identifier               | Primary Key |
| userId          | Long           | ID of the customer              | Foreign Key (User.userId) |
| driverId        | Long           | ID of the driver                | Foreign Key (Driver.driverId) |
| pickupLocation  | String         | Pickup location of the ride     |             |
| dropoffLocation | String         | Drop-off location of the ride   |             |
| fare            | Double         | Fare for the ride               |             |
| status          | String         | Status of the ride (BOOKED, COMPLETED, CANCELLED) | |

---

### 4. **Payment**
| Field           | Type           | Description                     | Key         |
|------------------|----------------|---------------------------------|-------------|
| paymentId       | Long           | Unique identifier               | Primary Key |
| rideId          | Long           | ID of the associated ride       | Foreign Key (Ride.rideId) |
| userId          | Long           | ID of the user making payment   | Foreign Key (User.userId) |
| amount          | Double         | Payment amount                  |             |
| method          | String         | Method of payment (CARD, CASH, WALLET) | |
| status          | String         | Payment status (SUCCESS, FAILED) |             |
| timestamp       | LocalDateTime  | Payment timestamp               |             |

---

### 5. **Rating**
| Field           | Type    | Description                     | Key         |
|------------------|---------|---------------------------------|-------------|
| ratingId        | Long    | Unique identifier               | Primary Key |
| rideId          | Long    | ID of the associated ride       | Foreign Key (Ride.rideId) |
| fromUserId      | Long    | ID of the user giving the rating | Foreign Key (User.userId) |
| toUserId        | Long    | ID of the user being rated      | Foreign Key (User.userId) |
| score           | Integer | Rating given (1 to 5)           |             |
| comments        | String  | Comments provided by the user   |             |

These models are mapped to the database and form the foundation of the system's data layer.

## 6. Setup Instructions

### Prerequisites
- **Java 17** or higher installed.
- **Maven** installed.
- **MySQL** database running.

### Steps
1. Clone the repository:
    ```bash
    git clone https://github.com/Srujan0821/Car_Booking_System.git
    cd Car_Booking_System
    ```

2. Configure the database:
    - Open `src/main/resources/application.properties`.
    - Update the database connection details:
      ```properties
      spring.datasource.url=jdbc:mysql://localhost:3306/cab_booking_system
      spring.datasource.username=root
      spring.datasource.password=your_password
      spring.jpa.hibernate.ddl-auto=update
      ```

3. Build the project:
    ```bash
    mvn clean install
    ```

4. Run the application:
    ```bash
    mvn spring-boot:run
    ```

5. Access the application:
    - The application will run on `http://localhost:8080`.

---


## 6. License
This project is licensed under the MIT License.

---
