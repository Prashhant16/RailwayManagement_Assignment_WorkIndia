# RailwayManagement_Assignment_WorkIndia

This project is a **Railway Management System** that simulates the core functionalities of the IRCTC system. The system enables/allows users/admins to:

- Register (User role)
- Login (User/Admin role)
- Add new train (Admin role)
- Check train/seat availability (User role)
- Book seats and train tickets (User role)
- Get booking details (User role)
- Update train details (Admin role)
- Implement role-based access for both users and administrators

The backend is developed using **Node.js**, **Express.js**, and **MySQL** as database to ensure efficient and scalable performance.

---

## Project Setup

### Prerequisites

To run this project, ensure you have the following installed:

- Node.js
- MySQL
- Postman


### Environment Variables

You need to create a `.env` file in the root of your project with the following environment variables:

```bash
PORT=4000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=root
DB_NAME=workindia
JWT_SECRET=0878066ea00590424c461a06d026046ce1f64995285de5e43b261dd443244276
API_KEY=admin_Prashant
```

### Installation

1. Clone the repository to your local machine:
   ```bash

      git clone https://github.com/Prashhant16/RailwayManagement_Assignment_WorkIndia
      cd RailwayManagement_Assignment_WorkIndia
   ```
2. Install all necessary dependencies using npm:

   ```bash
    npm install
   ```

3. Set up your MySQL database:

- Create a MySQL database named workindia.
- Run the SQL scripts in database/schema.sql to create necessary tables (users, trains, bookings).

Example:

```bash

CREATE DATABASE workindia;
USE workindia;

CREATE TABLE users (
   id INT AUTO_INCREMENT PRIMARY KEY,
   name VARCHAR(255) NOT NULL,
   email VARCHAR(255) UNIQUE NOT NULL,
   password VARCHAR(255) NOT NULL,
   role ENUM('user', 'admin') DEFAULT 'user',
   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE trains (
   id INT AUTO_INCREMENT PRIMARY KEY,
   train_number VARCHAR(50) NOT NULL,
   source VARCHAR(255) NOT NULL,
   destination VARCHAR(255) NOT NULL,
   total_seats INT NOT NULL,
   available_seats INT NOT NULL,
   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE bookings (
   id INT AUTO_INCREMENT PRIMARY KEY,
   user_id INT,
   train_id INT,
   seats INT NOT NULL,
   FOREIGN KEY (user_id) REFERENCES users(id),
   FOREIGN KEY (train_id) REFERENCES trains(id)
);

```

### Starting the Server

Once the setup is complete, start the server using npm:

```bash

  node server.js

```





#### Note :- By default, the server will run on port 4000. You can access the API at http://localhost:4000.

### API Endpoints

#### User Routes

    1. Register a new user
       * HTTP Method :- POST
       * Endpoint :- http://localhost:4000/user/register
       * Body:

```bash
{
  "name": "Prashant Sharma",
  "email": "prashhant16@gmail.com",
  "password": "1234"
}

```

2. Login
   - HTTP Method :- POST
   - Endpoint :- http://localhost:4000/user/login
   - Body:

```bash
{
  "email": "prashhant16@gmail.com",
  "password": "1234"
}
```

3. Check train availability

   - HTTP Method :- GET
   - Endpoint :- http://localhost:4000/user/availability?source=Mumbai&destination=Pune
   - Query Parameters
     - source: Source station (e.g., "Mumbai")
     - destination: Destination station (e.g., "Pune")
   - Response:

```bash
{
    "available": true,
    "availableTrainCount": 1,
    "trains": [
        {
            "trainNumber": "101010",
            "availableSeats": 200
        }
    ]
}

```

4.  Book Seats
    - HTTP Method :- POST
    - Endpoint :- http://localhost:4000/user/book
    - Request Body:

```bash
{
  "trainId": 1,
  "seatsToBook": 2
}

```

- Response:

```bash
{
  "message": "Seats booked successfully"
}
```

Note :- Requires JWT authentication.

5.  Booking Details

    - HTTP Method :- GET
    - Endpoint :- http://localhost:4000/user/getAllbookings

    - Response:

```bash
[
    {
        "booking_id": 17,
        "number_of_seats": 100,
        "train_number": "101010",
        "source": "Mumbai",
        "destination": "Pune"
    }
]


```

#### Admin Routes

1.  Add a new train

    - HTTP Method :- POST
    - Endpoint :- http://localhost:4000/admin/addTrain

    - Request Body:

```bash
{
    "message": "Trains added successfully",
    "trainIds": [
        {
            "trainNumber": "101010",
            "trainId": 1
        }
    ]
}
```

         * Headers :
             * x-api-key: Your admin API key which is stored in .env (in my case its `admin_Prashant`)

2. Update seat availability

   - HTTP Method :- PUT
   - Endpoint :- http://localhost:4000/admin/update-seats/10
   - Request Body:

```bash
 {
  "totalSeats": 200,
  "availableSeats": 150
 }
```

       * Response:

```bash
{
  "message": "Seats updated successfully"
}
```

        * Headers:
            * x-api-key:  Your admin API key which is stored in .env

### Running Tests

You can test all the available APIs using Postman. The endpoints are well-structured and follow RESTful conventions.

```bash
[
  {
    "trainNumber": "101010",
    "source": "Mumbai",
    "destination": "Pune",
    "totalSeats": 200
  },
  {
    "trainNumber": "102020",
    "source": "Chennai",
    "destination": "Bangalore",
    "totalSeats": 250
  },
  {
    "trainNumber": "103030",
    "source": "Kolkata",
    "destination": "Patna",
    "totalSeats": 300
  },
  {
    "trainNumber": "104040",
    "source": "Jaipur",
    "destination": "Agra",
    "totalSeats": 150
  },
  {
    "trainNumber": "105050",
    "source": "Hyderabad",
    "destination": "Visakhapatnam",
    "totalSeats": 350
  }
]

```

### Technologies Utilized

- **MySQL**: Relational database used for storing user information, train schedules, and booking data.
- **Node.js**: Backend runtime environment enabling the server-side logic and API management.
- **Express.js**: A lightweight framework that facilitates the creation of the RESTful API.
- **JWT (JSON Web Token)**: For secure user authentication and authorization processes.
- **bcrypt**: Encryption library used for securely hashing user passwords.
- **dotenv**: Manages environment variables for secure configuration and deployment.


# photos of the project

### Screenshots of the Project

#### 1. Database Creation

![Database Creation Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/creatingDatabase.png)

Description: This screenshot showcases the creation of the database schema for the Railway Management system.

---

#### 2. User Table

![User Database Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/usersTable.png)

Description: The structure and data stored in the `users` table of the `workindia` database.

---

#### 3. Workbench SQL View

![Workbench SQL Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/database_tables.png)

Description: An overview of the SQL queries and table structures in MySQL Workbench.

---

#### 4. Server Running Locally

![Localhost Running Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/serverRunning.png)

Description: The server running locally on `http://localhost:4000` as part of the project setup.

---

#### 5. User Registration via Postman

![Postman Registration Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/RegisterNewUser.png)

Description: A Postman request to register a new user, demonstrating the registration functionality.

---

#### 6. User Login via Postman

![Postman Login Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/loginUser.png)

Description: A Postman request to log in a user, showcasing how the login API works.

---

#### 7. Checking Train Availability

![Train Availability Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/checkAvailability.png)

Description: This screenshot demonstrates how the `GET /user/availability` API is used to check train availability.

---

#### 8.  Add a New Train

![Train Availability Screenshot](./RailwayManagement_Assignment_WorkIndia/Photo/addTrainAdmin.png)

Description: This screenshot demonstrates how the `POST /admin/addTrain` API is used to add new train by admin.
