# DriveBridge

DriveBridge is a microservices-based ride-sharing platform built with Node.js, MongoDB, RabbitMQ, and Express.js. It provides a scalable, event-driven architecture for managing users, captains (drivers), and rides, with secure authentication and robust inter-service communication.

## Tech Stack

- **Node.js**: JavaScript runtime for the backend.
- **Express.js**: Web framework for building RESTful APIs and HTTP services.
- **MongoDB**: NoSQL database for storing user, captain, and ride information.
- **Mongoose**: ODM for MongoDB, used for schema modeling.
- **RabbitMQ**: Message broker for asynchronous event-driven communication between services.
- **JWT (jsonwebtoken)**: Used for secure authentication.
- **bcrypt**: Password hashing for user and captain accounts.
- **dotenv**: Loads environment variables from `.env` files.
- **cookie-parser**: Parses cookies attached to client requests.
- **axios**: HTTP client for internal service communication.
- **express-http-proxy**: API gateway/proxy for routing requests to microservices.

## Microservices Architecture

- **Gateway**: Handles incoming requests and routes them to appropriate microservices.
- **User Service**: Manages user registration, login, profile, and authentication.
- **Captain Service**: Manages captain registration, login, availability, and authentication.
- **Ride Service**: Handles ride creation, acceptance, and status updates.

Each service runs independently and communicates via REST APIs and RabbitMQ events.

## Environment Variables

Each microservice and the gateway require their own `.env` file in their respective directories.

### Common Variables

- `MONGO_URL`: MongoDB connection URI
- `JWT_SECRET`: Secret key for JWT authentication
- `RABBIT_URL`: RabbitMQ connection URI
- `BASE_URL`: Base URL for internal API communication (used in ride service)
- (Optionally) `PORT`: Port number for the service (or set in code)

### Example `.env` file

```env
MONGO_URL=mongodb://localhost:27017/drivebridge
JWT_SECRET=your_jwt_secret
RABBIT_URL=amqp://localhost
BASE_URL=http://localhost:3000
PORT=3001
```

## Running the Project

### Prerequisites

- Node.js (v14 or above)
- MongoDB instance running locally or remotely
- RabbitMQ instance running locally or remotely

### Installation

Clone the repo:
```bash
git clone https://github.com/kushagragupta04/DriveBridge.git
cd DriveBridge
```

Install dependencies for each microservice and gateway:

```bash
cd user && npm install
cd ../captain && npm install
cd ../ride && npm install
cd ../gateway && npm install
```

Create `.env` files for each service as described above.

### Running Services

Start **MongoDB** and **RabbitMQ** locally (or ensure remote instances are accessible).

Run each microservice in a separate terminal:

**User Service**
```bash
cd user
npm start   # or node server.js
```

**Captain Service**
```bash
cd captain
npm start   # or node server.js
```

**Ride Service**
```bash
cd ride
npm start   # or node server.js
```

**Gateway**
```bash
cd gateway
npm start   # or node app.js
```

### Default Ports

- Gateway: `3000`
- User Service: `3001`
- Captain Service: `3002`
- Ride Service: `3003`

You can change ports in `.env` or server files.

## API Endpoints

- **Gateway**: `/user`, `/captain`, `/ride` routes to their respective services
- **User Service**: Registration, login, profile, accepted rides
- **Captain Service**: Registration, login, manage availability
- **Ride Service**: Create ride, accept ride, ride status

## How It Works

- Users can register, login, and request rides.
- Captains can register, login, and accept rides.
- Ride requests and acceptances are communicated via RabbitMQ queues.
- Authentication is handled via JWT tokens and cookies.
- Gateway proxies requests to appropriate services.

