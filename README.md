 **Deutschline - Dynamic Fare Calculation**

This project is a Flask-based web application called **Deutschline - Dynamic Fare Calculation**, which provides real-time train fare calculation, booking, and demand prediction services. It integrates with Neo4j for station connections, MongoDB for storing bookings, and uses a dynamic approach to calculate train fares based on demand and seat availability.

## Table of Contents
1. [Introduction](#introduction)
2. [Installation](#installation)
3. [API Endpoints](#api-endpoints)
4. [Dependencies](#dependencies)
5. [Usage](#usage)
6. [Folder Structure](#folder-structure)

## Introduction

**Deutschline - Dynamic Fare Calculation** provides the following features:
- Search for available train routes between two stations.
- View dynamic fare calculations based on real-time seat availability and demand.
- Book train tickets and store the booking data in a MongoDB database.
- Calculate train fare increases based on seat demand and available capacity.

The system is designed to integrate with **Neo4j** for graph-based station connections and **MongoDB** for storing the booking information.

## Installation

### Prerequisites
Make sure you have the following installed on your machine:
- Python 3.7 or later
- Neo4j instance running (for station data)
- MongoDB instance running (for storing bookings)

### Step 1: Clone the repository
```bash
git clone https://github.com/yourusername/deutschline-dynamic-fare-calculation.git
cd deutschline-dynamic-fare-calculation
```

### Step 2: Install dependencies
Create a virtual environment and install the required Python packages:
```bash
python3 -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt
```

### Step 3: Configure Neo4j and MongoDB
Ensure your **Neo4j** and **MongoDB** configurations are correctly set up in the `db.py` file. You may need to configure your local or remote database details (e.g., default ports for Neo4j: `7687` and MongoDB: `27017`).

### Step 4: Run the application
```bash
python app.py
```

By default, the application will be available at `http://127.0.0.1:5000/`.

## API Endpoints

### 1. `/deutschline` - Get Train Route Details and Fare Calculation

**Method**: GET  
**Parameters**:
- `current_location`: The starting station name (e.g., "Berlin").
- `destination`: The destination station name (e.g., "Munich").
- `date`: The date of travel in `dd-mm-yyyy` format.
- `time`: The time of travel in `HH:mm` format.
- `class`: The class of the ticket (`First` or `Second`).

**Response**:  
Returns the available train routes between the stations, along with total fare, seat availability, and demand.

**Example**:
```bash
GET /deutschline?current_location=Berlin&destination=Munich&date=08-11-2024&time=14:30&class=First
```

### 2. `/create_booking` - Create a Booking

**Method**: POST  
**Body**: JSON payload containing:
- `source`: The station name where the journey starts.
- `destination`: The station name where the journey ends.
- `train_date`: The date of the train (`dd-mm-yyyy`).
- `departureTime`: The time of departure (`HH:mm`).
- `price`: The price of the ticket.
- `email`: The user's email address.
- `number_of_tickets`: Number of tickets to be booked.
- `train_number`: The train number.
- `train_demand`: The demand percentage for the train.
- `class`: The class of the ticket (`First` or `Second`).

**Response**:  
Returns a success message with the booking ID if the booking is created successfully.

**Example**:
```bash
POST /create_booking
{
  "source": "Berlin",
  "destination": "Munich",
  "train_date": "08-11-2024",
  "departureTime": "14:30",
  "price": 120,
  "email": "user@example.com",
  "number_of_tickets": 2,
  "train_number": "ICE123",
  "train_demand": 15,
  "class": "First"
}
```

## Dependencies

The following Python libraries are required to run the application:

- **Flask**: A lightweight web framework for building web applications.
- **Flask-CORS**: Handles Cross-Origin Resource Sharing in Flask applications.
- **Py2neo**: Python client for interacting with Neo4j.
- **Pymongo**: Python client for interacting with MongoDB.
- **Datetime**: Library for handling date and time operations.

To install all dependencies, run:

```bash
pip install -r requirements.txt
```

## Usage

- Start the Flask application:
  ```bash
  python app.py
  ```
- The API will be accessible at `http://127.0.0.1:5000/`.
- You can use Postman, Curl, or any HTTP client to interact with the API endpoints.

## Folder Structure

```
deutschline-dynamic-fare-calculation/
│
├── app.py                # Main Flask app with routes
├── db.py                 # Database connections (Neo4j and MongoDB)
├── mongo.py              # MongoDB operations (insertion and querying)
├── utils.py              # Helper functions for fare calculation, date/time conversions
└── frontend/             # (Optional) Frontend assets (HTML, JS, CSS)
```
