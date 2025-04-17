
# Calculator Microservice

This is a simple Node.js microservice that performs arithmetic operations using REST API endpoints. It includes error handling and logging using Winston.

---

## Step-by-Step Instructions

### 1. Install Dependencies

Install required packages:

```bash
npm install
```

This will install:
- `express` – for the web server
- `winston` – for logging

### 2. Run the Microservice

```bash
node index.js
```

### 4. Use API Endpoints

You can test the following endpoints in your browser or Postman:

```
GET http://localhost:3000/add?num1=5&num2=2
GET http://localhost:3000/subtract?num1=10&num2=4
GET http://localhost:3000/multiply?num1=3&num2=6
GET http://localhost:3000/divide?num1=20&num2=5
```

---

## Logging with Winston

### Instructions

1. To add logging to your Node.js microservice, you can use a logging library by installing the Winston library using NPM:

```bash
npm install winston
```

2. In your Node.js application code, require the Winston library and create a new logger object:

```javascript
const winston = require('winston');
const logger = winston.createLogger({
  level: 'info',
  format: winston.format.json(),
  defaultMeta: { service: 'calculator-microservice' },
  transports: [
    new winston.transports.Console({
      format: winston.format.simple(),
    }),
    new winston.transports.File({ filename: 'logs/error.log', level: 'error' }),
    new winston.transports.File({ filename: 'logs/combined.log' }),
  ],
});
```

Here, we're creating a new logger object that will log messages at the "info" level or higher, in JSON format, and with a default service name of "calculator-microservice". We're also specifying three different transports: one for logging to the console (useful during development), one for logging errors to a file, and one for logging all messages (except errors) to a different file.

3. Wherever you want to log a message in your application code, use the `logger.log()` method:

```javascript
logger.log({
  level: 'info',
  message: `New ${operation} operation requested: ${num1} ${operation} ${num2}`,
});
```

Here, we're logging an "info" level message that contains the requested operation and operands.

4. Run your application and check the log files in the `logs` directory to see the logged messages.

```bash
tail -f logs/combined.log
```

This will show you the latest messages logged to the `combined.log` file in real-time.

> Note that this is just a basic example of how to add logging to your microservice. There are many additional features and options available in Winston and other logging libraries that you can explore to customize your logging output and behavior.

---

## Error Handling

- If inputs are not numbers, it returns a 400 error with a message.
- Division by zero is caught and handled.
- All errors are also logged to `error.log`.

---

## Notes

> This project is built for learning how to create and log basic microservices in Node.js.

