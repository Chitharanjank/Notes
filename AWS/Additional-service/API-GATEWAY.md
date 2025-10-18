---

## What is an API?

**API = Application Programming Interface**
It’s a way for two applications (or systems) to talk to each other.

---

### Layman Example:

Imagine you go to a **restaurant**:

* You (the customer) want food.
* The **kitchen** makes food.
* But you don’t go inside the kitchen — you talk to the **waiter**.

You give your *order* (request) to the waiter.
The waiter gives it to the kitchen and brings back your *food* (response).

 **The waiter = API**
He’s the **middleman** who helps two systems communicate — *you* (the user) and *the kitchen* (the system).

---

###  In the digital world:

Let’s say your phone’s **Weather App** needs today’s temperature.

* The app sends a request to a weather company’s **API**.
* The API fetches data from their database.
* The API sends the weather info back to your app.

So your app doesn’t need to know **how** the weather data is stored — it just **asks** the API.

---

##  What are API Methods?

APIs work mostly using the **HTTP protocol** (the same thing web browsers use).

Different actions are done using **HTTP methods** — you can think of them like verbs in a sentence.

| Method     | What it does         | Everyday Analogy                         |
| ---------- | -------------------- | ---------------------------------------- |
| **GET**    | Fetch data           | “Show me the menu.”                      |
| **POST**   | Create new data      | “I’d like to order a pizza.”             |
| **PUT**    | Update existing data | “Change my pizza order to extra cheese.” |
| **DELETE** | Remove data          | “Cancel my pizza order.”                 |

---

### Real Example:

Imagine an app for managing users.

| Action         | API Endpoint | Method | What happens            |
| -------------- | ------------ | ------ | ----------------------- |
| View all users | `/users`     | GET    | Get list of users       |
| Add a new user | `/users`     | POST   | Add a user              |
| Update a user  | `/users/123` | PUT    | Update user with ID 123 |
| Delete a user  | `/users/123` | DELETE | Remove user 123         |

---

##  What is an API Gateway?

Now that you know APIs are like waiters… imagine a **big restaurant with many kitchens**:

* One kitchen for pizza 
* One for pasta 
* One for desserts 

If every kitchen had its own waiter, things would get confusing!
So the restaurant hires **one main waiter** — he takes all orders, decides which kitchen should cook it, and brings back the food.

That **main waiter** is the **API Gateway**.

---

### ⚙️ Technical version:

An **API Gateway** is a **single entry point** that receives all client requests and forwards them to the correct backend service.

It handles:

*  **Routing:** Sends each request to the right API/microservice
*  **Security:** Checks login/authentication before allowing access
*  **Monitoring:** Tracks how many requests are made
*  **Rate Limiting:** Prevents overuse (like spam requests)
*  **Caching:** Speeds up responses for repeated requests

---

### Without API Gateway:

```
Client → user-service
Client → order-service
Client → payment-service
```

The client must know every backend address — messy, hard to manage!

---

###  With API Gateway:

```
Client → API Gateway → (routes to correct service)
```

| Request  | API Gateway sends to |
| -------- | -------------------- |
| `/login` | user-service         |
| `/order` | order-service        |
| `/pay`   | payment-service      |

Only **one public URL** (like `https://api.myapp.com`) is exposed.

---

### 🏦 Analogy Recap

| Real Life             | Tech Equivalent  |
| --------------------- | ---------------- |
| Customer              | App user         |
| Waiter                | API              |
| Head Waiter / Manager | API Gateway      |
| Kitchen               | Backend services |

---

## Real-World API Gateway Tools

| Tool                | Type          | Description                            |
| ------------------- | ------------- | -------------------------------------- |
| **AWS API Gateway** | Cloud         | Part of AWS services for managing APIs |
| **Kong**            | Open-source   | Popular, easy to use API gateway       |
| **NGINX**           | Reverse Proxy | Can work as a gateway                  |
| **Apigee**          | Enterprise    | Google’s API management tool           |
| **Traefik**         | Open-source   | Lightweight gateway for microservices  |

---

## 🧾 Summary

| Concept         | Simple Meaning                                 | Example                                                 |
| --------------- | ---------------------------------------------- | ------------------------------------------------------- |
| **API**         | Middleman between two apps                     | Waiter between you & kitchen                            |
| **API Methods** | Actions you can perform                        | GET (see), POST (create), PUT (update), DELETE (remove) |
| **API Gateway** | One gate that manages and routes all API calls | Head waiter directing orders to the right kitchen       |

---

