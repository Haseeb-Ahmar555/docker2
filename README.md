# docker2
Calculator Web App with Docker Compose
This project is a simple calculator web application built using HTML, CSS, and JavaScript. The app is containerized using Docker Compose, and it is served using an Nginx web server.

Project Structure
Copy code
calculator/
│
├── app/
│   ├── index.html
│   ├── script.js
│   └── style.css
├── docker-compose.yml
└── Dockerfile
Files Description:
app/index.html: The main HTML file for the calculator app interface.
app/script.js: Contains JavaScript code to handle the logic of the calculator.
app/style.css: Contains the CSS styles for the calculator layout.
docker-compose.yml: Docker Compose file to define the services and network.
Dockerfile: Defines the container setup using Nginx to serve the app.
Getting Started
To get started with the Calculator Web App, follow these steps:

1. Clone the Repository
Clone the repository to your local machine:

bash
Copy code
git clone <repository-url>
cd calculator
2. Set up Docker Environment
Ensure that you have Docker and Docker Compose installed on your system.

3. Build and Run the Docker Container
In the project directory, run the following command to build and start the application using Docker Compose:

bash
Copy code
docker-compose up --build
This command will build the Docker image defined in the Dockerfile and start the containerized application.

4. Access the Application
Once the containers are up and running, open a browser and go to:

arduino
Copy code
http://localhost
You should see the working calculator app interface.

5. Stopping the Application
To stop the application, run:

bash
Copy code
docker-compose down
This will stop and remove the containers.

Code
1. docker-compose.yml
yaml
Copy code
version: '3'
services:
  app:
    build: .
    ports:
      - "80:80"
    volumes:
      - ./app:/app
    networks:
      - app_network

networks:
  app_network:
    driver: bridge
2. Dockerfile
dockerfile
Copy code
# Use a basic web server image
FROM nginx:alpine

# Copy app files into the container
COPY ./app /usr/share/nginx/html

# Expose the container's port 80
EXPOSE 80
3. index.html
html
Copy code
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" disabled>
        <button onclick="clearDisplay()">C</button>
        <button onclick="appendToDisplay('1')">1</button>
        <button onclick="appendToDisplay('2')">2</button>
        <button onclick="appendToDisplay('3')">3</button>
        <button onclick="appendToDisplay('+')">+</button>
        <button onclick="appendToDisplay('4')">4</button>
        <button onclick="appendToDisplay('5')">5</button>
        <button onclick="appendToDisplay('6')">6</button>
        <button onclick="appendToDisplay('-')">-</button>
        <button onclick="appendToDisplay('7')">7</button>
        <button onclick="appendToDisplay('8')">8</button>
        <button onclick="appendToDisplay('9')">9</button>
        <button onclick="appendToDisplay('*')">*</button>
        <button onclick="appendToDisplay('0')">0</button>
        <button onclick="appendToDisplay('.')">.</button>
        <button onclick="calculateResult()">=</button>
        <button onclick="appendToDisplay('/')">/</button>
    </div>
    <script src="script.js"></script>
</body>
</html>
4. script.js
javascript
Copy code
let display = document.getElementById('display');

function appendToDisplay(value) {
    display.value += value;
}

function clearDisplay() {
    display.value = '';
}

function calculateResult() {
    try {
        display.value = eval(display.value);
    } catch (e) {
        display.value = 'Error';
    }
}
5. style.css
css
Copy code
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background-color: #f4f4f4;
}

.calculator {
    width: 220px;
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 10px;
}

button {
    padding: 20px;
    font-size: 18px;
    border: none;
    background-color: #f1f1f1;
    cursor: pointer;
    border-radius: 5px;
}

button:hover {
    background-color: #ddd;
}

#display {
    grid-column: span 4;
    padding: 20px;
    font-size: 24px;
    text-align: right;
    border: 1px solid #ccc;
    border-radius: 5px;
    background-color: #fff;
}
Project Details
Frontend: Built with HTML, CSS, and JavaScript to provide a basic calculator UI and functionality.
Backend: Served using the Nginx web server inside a Docker container.
Docker: The app is containerized with Docker for portability and easy deployment.
License
This project is open-source and available under the MIT License.
