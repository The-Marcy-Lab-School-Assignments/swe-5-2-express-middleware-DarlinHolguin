# Short Response Questions

Answer each question below in your own words. Aim for 3–5 sentences per answer. Be specific — use the exact terms and concepts from the lesson.

Your responses will each be evaluated out of 6 points. You can earn 3 points for writing quality and 3 points for the accuracy and precision of the technical content per question.

---

## Question 1: Express vs `node:http`

Express is described as a framework that "wraps" `node:http`. What does that mean? Compare how you would handle a `GET /api/users` request in `node:http` versus in Express. What does Express do for you automatically that you had to write manually with `node:http`?

**Your answer here**:
`node:http` is `node.js`'s built in module for handling requests and building servers, it differs from **express** in terms of automation vs manually doing. Using `node:http` you have to manually construct and send an HTTP response for a single route.

Express is a **framework**, it wraps `node:http` which means, it builds on top of it and handles all the manual repetitive labor for you. For example instead of manually checking for every method like `if (method === 'GET' && url === '/api/users')` and manually calling `res.writeHead` and `JSON.stringify()` every single time,Express allows you to just write `app.get('/api/users', handler)` and use `res.json()` which handles the status code, header, and JSON serialization all in one.

---

## Question 2: Endpoints, Controllers, and Middleware

What are **controllers** and **middleware** in Express? What are each responsible for and how do they work together to handle incoming requests?

**Your answer here**:
In Express controllers are callback functions that are responsible for looking at a request and sending a response back to the client. Controllers are connected to a specific endpoint using `app.get`, meaning that they only begin to run when that exact route is hit.

In Express middleware is a function that is responsible for running on every incoming request before it reaches the controller. Its registered utilizing `app.use()` and unlike controllers it doesn't lock to one specific endpoint, and needs to call `next()` in order to pass the request along.

They work together when handling an incoming request. When the request hits the server the middleware runs first and handles logging the request as well as parsing the body, next it gets passed down to the corresponding controller which sends a response back.

---

## Question 3: Query Strings and Route Parameters

How are **query strings** and **route parameters** similar? How are they different? In your answer, provide an example of when you would use each.

**Your answer here**:
**Query strings** are the parts of an **URL** that come after the `?` and is used for filtering or searching. For example if you wanted to filter only by a specific topic that you want back then you would do-

### Query String Example

`/api/quotes?topic=science`

**Route parameters** are the parts of an **URL path** that are defined with `:`. Route parameters are used for when you need to fetch a specific resource by its unique identifier. For example when someone searches for a specific data-

### Route Parameters Example

`/api/quotes/1`

Both query strings and route parameters allow the client to send or request extra information to the server through the URL.

## Question 4: Same-Origin Requests

For API fetch calls from a client-side application, explain the difference between fetching from endpoints with relative paths like `/api/quotes` and fetching from endpoints with a full **URL** like `https://dog.ceo/api/breeds/image/random`. Why do we not send a fetch using a url like `http://localhost:8080/api/quotes`?

**Your answer here**:

For API fetch calls from a client-side application, the difference between fetching from **endpoints** with relative paths like `/api/quotes` and fetching from endpoints with a full URL like `http://dog.ceo/api/breeds/image/random` is that a relative path automatically sends the request to which ever app is being hosted. Meaning that if your application is running on `localhost:8080`, then it just resolves to `http://localhost:8080/api/quotes`.

The reasons why we do not send a fetch using a **URL** like `http://localhost:8080/api/quotes` is because **localhost** is only on your own machine. It cannot exist on any other devices except yours, thats why we deploy websites, so that it can be made public for anyone from any other device.
