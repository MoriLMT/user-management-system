# User Management System

A simple backend service for managing user profiles, built using Node.js, Express.js, and MongoDB.

Introduction

This project is a backend service for managing user profiles. It supports operations such as creating, reading, updating, and deleting users, as well as searching for users by username or email and filtering by role.

Prerequisites

Before you begin, ensure you have met the following requirements:
- A Windows operating system.
- Basic understanding of Node.js and MongoDB.
- Internet connection to download required software.

Installation

### Installing Node.js

1. Visit the [Node.js website](https://nodejs.org/).
2. Download the LTS (Long Term Support) version for Windows.
3. Run the installer and follow the prompts to complete the installation.
4. Verify the installation by opening a command prompt and typing:
   ```bash
   node -v
   ```

### Installing npm

npm (Node Package Manager) is installed automatically with Node.js.

1. Verify npm installation by typing in the command prompt:
   ```bash
   npm -v
   ```

### Installing MongoDB

1. Visit the [MongoDB download center](https://www.mongodb.com/try/download/community).
2. Download the MongoDB Community Server for Windows.
3. Run the installer and follow the setup wizard.
4. Choose "Complete" setup type.
5. Make sure to install MongoDB as a service when prompted.

### Setup MongoDB as a Service on Windows

1. During installation, ensure that the option to run MongoDB as a Windows service is selected.
2. Start the MongoDB service:
   - Open `services.msc` from the Run dialog (`Win + R`).
   - Locate `MongoDB` in the list of services, right-click, and select `Start`.

### Installing a Code Editor

1. Download and install [Visual Studio Code (VS Code)](https://code.visualstudio.com/).
2. Follow the installation instructions.
3. Launch VS Code and install the recommended extensions for Node.js and JavaScript.

## Project Setup

### Explaining the Code of the User-Management-System Project

1. **Clone the Repository**:
   - Use `git clone` to clone the project repository from GitHub:
     ```bash
     git clone https://github.com/MoriLMT/user-management-system.git
     ```

2. **Navigate to the Project Directory**:
     ```bash
     cd user-management-system
     ```

3. **Install Dependencies**:
   - Run `npm install` to install all the necessary packages:
     ```bash
     npm install
     ```

4. **Code Explanation**:

   - **app.js**: The main file that initializes the Express app and connects to MongoDB.
     ```javascript
     const express = require('express');
     const mongoose = require('mongoose');
     const userRoutes = require('./routes/userRoutes');

     const app = express();
     app.use(express.json());

     mongoose.connect('mongodb://localhost:27017/userdb', {
         useNewUrlParser: true,
         useUnifiedTopology: true,
     });

     app.use('/api/users', userRoutes);

     app.listen(5000, () => {
         console.log('Server is running on port 5000');
     });
     ```

   - **routes/userRoutes.js**: Defines the API endpoints for user operations.
     ```javascript
     const express = require('express');
     const router = express.Router();
     const userController = require('../controllers/userController');

     router.post('/', userController.createUser);
     router.get('/', userController.getAllUsers);
     router.get('/:id', userController.getUserById);
     router.put('/:id', userController.updateUser);
     router.delete('/:id', userController.deleteUser);

     module.exports = router;
     ```

   - **controllers/userController.js**: Contains the logic for handling user requests.
     ```javascript
     const User = require('../models/User');

     exports.createUser = async (req, res) => {
         // Implementation of user creation
     };

     exports.getAllUsers = async (req, res) => {
         // Implementation of fetching all users
     };

     exports.getUserById = async (req, res) => {
         // Implementation of fetching a user by ID
     };

     exports.updateUser = async (req, res) => {
         // Implementation of updating a user
     };

     exports.deleteUser = async (req, res) => {
         // Implementation of deleting a user
     };
     ```

   - **models/User.js**: Defines the user schema and model.
     ```javascript
     const mongoose = require('mongoose');

     const userSchema = new mongoose.Schema({
         username: { type: String, required: true },
         email: { type: String, required: true, unique: true },
         password: { type: String, required: true },
         role: { type: String, enum: ['user', 'admin'], default: 'user' },
     });

     module.exports = mongoose.model('User', userSchema);
     ```

## Running the Application

### Running the MongoDB Service

1. **Start MongoDB**:
   - Ensure MongoDB service is running. You can start it manually from `services.msc` if it’s not already running.

2. **Verify MongoDB**:
   - Open a command prompt and type:
     ```bash
     mongo
     ```
   - You should see the MongoDB shell prompt if it’s running correctly.

### Running the Project

1. **Start the Application**:
   - In your project directory, start the server by running:
     ```bash
     npx nodemon app.js
     ```
   - The server should start, and you’ll see `Server is running on port 5000` in the terminal.

2. **Open in Browser**:
   - Open a browser and go to `http://localhost:5000`. You can test if the server is up and running by making API requests using tools like Postman or directly through the browser.

## Testing the Endpoints

### Testing Endpoints with Postman

1. **Download and Install Postman**:
   - Visit the [Postman website](https://www.postman.com/downloads/) and download the app.

2. **Create a New Request**:
   - Open Postman and create a new request.
   - Set the request method and URL, for example, to create a new user:
     - Method: `POST`
     - URL: `http://localhost:5000/api/users`
     - Body: Select `raw` and `JSON`, then enter user data like:
       ```json
       {
         "username": "john",
         "email": "john@example.com",
         "password": "password123",
         "role": "user"
       }
       ```

3. **Send Requests**:
   - Click `Send` to test the endpoint. You should see the response from your server.

4. **Test Other Endpoints**:
   - Repeat similar steps for `GET`, `PUT`, and `DELETE` requests for other endpoints.


---

By following this README, users can set up, run, and test the User Management System project on their local machines.
