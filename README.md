# Customer Appointment Booking API Calendar Query Service

## Project Overview

This project provides an API service to query available calendar slots for sales managers based on specified input criteria such as language, customer rating, and products. It utilizes a PostgreSQL database with Dockerized services for easy setup and deployment.

The API is developed using **.NET 8 , C# and Dapper** to ensure high performance, scalability, and maintainability. The project leverages modern features and best practices of .NET 8 to provide a clean, structured architecture for handling API requests and database interactions.

Newly created **DB Indexes and Function** are placed in **db/init.sql** file.

### Features

- **Retrieve Available Slots**: Query available slots for sales managers' appointments based on specific input filters (language, rating, and products).
- **Conflict-Free Slot Management**: Excludes overlapping booked slots for accurate availability results.
- **Optimized Database Queries**: Used GIN indexing for array columns in PostgreSQL to improve the performance of complex queries.
- **Custom PostgreSQL Function**: Implements a user-defined function in PostgreSQL (`get_available_slots`) to encapsulate logic for retrieving available slots based on input criteria. This function centralizes complex business logic, optimizes performance, reduces data transfer, and simplifies application code by handling data operations directly within the database.
- **Unit Testing**: Comprehensive unit tests are implemented to ensure robust and reliable API behavior, covering critical functionalities, database interactions, and business logic scenarios.
- **FluentValidation**: Utilizes FluentValidation to ensure input data is validated in a clean, extensible, and maintainable way, reducing boilerplate code and improving overall input validation logic consistency.

---

## Prerequisites

Before running this project, make sure you have the following installed:

- [Docker](https://www.docker.com/products/docker-desktop)
- [Docker Compose](https://docs.docker.com/compose/install/)

---

## Getting Started

### 1. Build and Run with Docker Compose

1. Unzip the **CustomerAppointmentBookingProject** folder and navigate to the **CustomerAppointmentBookingProject** project directory.
2. Build and run the services using Docker Compose:

   ```bash
   docker-compose up --build

## Services

The following services will be started:

- **Database**: PostgreSQL running on port 5432.
- **API**: Running on port 3000.

## API Endpoints

### Query Available Slots

- **Endpoint**: `POST /calendar/query`
- **URL**: [http://localhost:3000/calendar/query](http://localhost:3000/calendar/query)

## Running Unit Tests

### Unit Test Prerequisites

- Ensure that the .NET 8 SDK is installed on your machine.
- Used mocking for the database context to isolate and test individual components effectively.

### Steps to Run the Unit Tests

1. Navigate to the unit test project directory:

   ```bash
   cd "CustomerAppointmentBookingProject"
  
   docker build -t bookifyapi-unittest -f BookifyAPI.UnitTest/Dockerfile .
   docker run --rm -it bookifyapi-unittest /bin/bash
   dotnet test

from the container root need to run dotnet test to see result. 
### Steps to Run the Tests

1. Make sure API is running on [http://localhost:3000/calendar/query](http://localhost:3000/calendar/query).
2. Navigate to the directory containing the test application.
3. Install the required dependencies by running:
   ```bash
   npm install
   npm run test
This will execute the predefined test scenarios and compare the actual API responses with the expected results.

## Project Structure Explanation


### Controllers
**Purpose**: Defines the API endpoints for the application. Controllers manage incoming HTTP requests, interact with services, and handle responses to clients.

**Benefits**: Clear separation of API endpoint logic from the rest of the application. Improves readability, isolates request handling, and separates user-facing logic from underlying business logic.

---

### Models
**Purpose**: Represents data structures used throughout the application, including request/response bodies and database entities.

**Benefits**: Centralized location for all data structures promotes consistency, simplifies maintenance, and enhances reusability across different parts of the application.

---

### Repositories
**Purpose**: Contains classes that handle data access logic, such as database operations and queries.

**Benefits**: Abstracts data access logic from other components, promoting separation of concerns and improving maintainability and testability of database interactions.

---

### Services
**Purpose**: Contains the business logic of the application. Services perform data operations or implement business-specific rules and are called by controllers.

**Benefits**: Encapsulates business logic, providing a clean architecture by separating business concerns from presentation logic. This approach makes the code more maintainable, testable, and flexible for future changes.

---
### Validators - QueryRequestValidator.cs
**Purpose**: Defines validation rules for incoming data related to queries, ensuring data integrity and consistency. `QueryRequestValidator.cs` enforces business and data validation logic before requests are processed.

**Benefits**: Centralizing validation logic in `QueryRequestValidator.cs` improves code maintainability, reduces duplication, and ensures consistent enforcement of rules, leading to more robust and predictable application behavior.

---

### BookifyAPI.csproj
**Purpose**: The .NET project file containing configuration, build settings, and dependency management for the application.

**Benefits**: Manages and configures dependencies, build processes, and metadata for consistent behavior across different environments.

---

### Dockerfile
**Purpose**: Specifies how to build and containerize the application, ensuring consistent behavior across environments.

**Benefits**: Containerization with Docker ensures consistent deployment, easy creation of reproducible builds, and simplifies setup for different development, testing, and production environments.

---

### Overall Benefits of the Project Structure
- **Separation of Concerns**: By dividing logic across controllers, models, repositories, and services, the structure promotes isolation of different application layers, enhancing maintainability and scalability.
- **Readability and Organization**: Easier navigation and understanding of the purpose of each component, which improves productivity for developers.
- **Reusability and Testability**: Isolating data access, business logic, and API handling allows for reusable code and easier testing, both unit and integration tests.
- **Scalability**: The modular approach makes it simpler to add new features or modify existing functionality without disrupting other components.
