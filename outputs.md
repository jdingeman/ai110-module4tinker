# Part 1

Run DocuBot in Naive LLM Mode (Mode 1). Ask a few questions drawn from the docs folder:

- "Where is the auth token generated?"

```
Running naive LLM mode on custom query...

============================================================
Question: Where is the auth token generated?

Answer:
The generation of an authentication token (auth token) depends heavily on the specific authentication mechanism and system architecture you're referring to. However, here are the most common scenarios:

1.  **During User Login (Your Backend Server):**
    *   **Where:** Typically, your backend application server.
    *   **How:** When a user successfully authenticates by providing a username and password (or other credentials) to your application, your backend server validates these credentials against your user database. If valid, the server then *generates* a new token (e.g., a JSON Web Token - JWT, or a session token) and sends it back to the client (web browser, mobile app). This token represents the authenticated user's session.
    *   **Example:** A user logs into your website. Your Node.js, Python, Java, or Ruby backend validates credentials and issues a JWT signed with your server's secret key.

2.  **By an OAuth 2.0 / OpenID Connect Authorization Server (Identity Provider):**
    *   **Where:** An dedicated Authorization Server, often provided by a third-party identity provider (IdP) or an OAuth server you've implemented.
    *   **How:** This is common when you use services like Auth0, Okta, Google Sign-In, Facebook Login, Azure AD, etc.
        1.  Your application redirects the user to the Authorization Server to log in.
        2.  The user authenticates directly with the Authorization Server and grants your application permission.
        3.  The Authorization Server then issues an `authorization code` (or directly an `access token` in some flows) back to your application.
        4.  Your application exchanges this `authorization code` (along with its client ID and secret) for an `access token` (and often a `refresh token` and `ID token`) directly with the Authorization Server's token endpoint.
    *   **Example:** You integrate "Login with Google." When a user clicks this, they're redirected to Google to log in and approve. Google then issues an access token which your application can use to access Google APIs on behalf of the user, or your own backend can validate to establish a session.

3.  **From a Developer/Admin Dashboard (for API Keys):**
    *   **Where:** The administration panel or developer dashboard of a service you want to integrate with.
    *   **How:** For static API keys (which are also a form of auth token), you typically *manually generate* them through a user interface provided by the service you're using. These are usually long-lived and represent your application, not a specific user.
    *   **Example:** You generate an API key on the Stripe dashboard to make payments programmatically from your backend, or a Google Maps API key to embed maps on your website.

4.  **For Server-to-Server Communication:**
    *   **Where:**
        *   The **calling service** might generate a JWT signed with a shared secret to authenticate with another internal service.
        *   An **internal OAuth server** might issue a token based on client credentials (client ID/secret) when one service needs to call another, bypassing a human user.
        *   An **internal OAuth server** might issue a token based on client credentials (client ID/secret) when one service needs to call another, bypassing a human user.
    *   **How:** These tokens are programmatically generated and used within your backend infrastructure for microservice communication.
        *   An **internal OAuth server** might issue a token based on client credentials (client ID/secret) when one service needs to call another, bypassing a human user.
        *   An **internal OAuth server** might issue a token based on client credentials (client ID/secret) when one service needs to call another, bypassing a human user.
        *   An **internal OAuth server** might issue a token based on client credentials (client ID/secret) when one service needs to call another, bypassing a human user.
        *   An **internal OAuth server** might issue a token based on client credentials (client ID/secret) when one service needs to call another, bypassing a human user.
    *   **How:** These tokens are programmatically generated and used within your backend infrastructure for microservice communication.

**To give you a more precise answer, please tell me:**

*   **What kind of application are you working with?** (e.g., web frontend, mobile app, backend service, a script?)
*   **What is the authentication flow you're using or trying to understand?** (e.g., "users log into my website," "I'm calling a third-party API," "I'm using OAuth with Auth0")
*   **What is the overall goal you're trying to achieve with the token?**
```

- "Which endpoint returns all users?"

````
Running naive LLM mode on custom query...

============================================================
Question: Which endpoint returns all users?

Answer:
The most common and RESTful endpoint for returning all users is:

**`GET /users`**

However, many APIs include prefixes, versioning, or other conventions. Here are some common variations you might encounter:

*   **`GET /api/users`**
*   **`GET /v1/users`** (for API versioning)
*   **`GET /api/v1/users`**
*   **`GET /users/list`** (less common for "all," but possible)

---

**Key Considerations:**

1.  **HTTP Method:** It should always be `GET` for retrieving a collection of resources.
2.  **Authentication:** This endpoint typically requires authentication (e.g., an API key, OAuth token, session cookie) to prevent unauthorized access to user data.
3.  **Pagination:** For APIs with many users, this endpoint will often support pagination parameters to limit the number of results returned per request and allow you to fetch results in batches.
    *   Example: `GET /users?page=1&limit=20` or `GET /users?offset=0&count=20`
4.  **Filtering & Sorting:** You might also find parameters for filtering (e.g., by status, role) or sorting the results.
    *   Example: `GET /users?status=active&sort_by=email&order=asc`
5.  **Response Format:** The response will typically be a JSON array of user objects.
    ```json
    [
      {
        "id": "user_abc123",
        "username": "alice_smith",
        "email": "alice@example.com",
        "first_name": "Alice",
        "last_name": "Smith",
        "role": "admin",
        "created_at": "2023-01-01T10:00:00Z"
      },
      {
        "id": "user_xyz456",
        "username": "bob_jones",
        "email": "bob@example.com",
        "first_name": "Bob",
        "last_name": "Jones",
        "role": "user",
        "created_at": "2023-01-05T14:30:00Z"
      }
    ]
    ```
    Or, if pagination is used, it might be wrapped in an object:
    ```json
    {
      "data": [
        // ... array of user objects ...
      ],
      "total": 100,
      "page": 1,
      "limit": 20
    }
    ```

---

**How to find the definitive answer:**

Always refer to the API's official documentation. Look for sections titled "Users," "User Management," "Endpoints," or "API Reference" to find the exact path, required authentication, and supported parameters.

**Example `curl` request (assuming `GET /api/users` and a Bearer token):**

```bash
curl -X GET \
  'https://api.yourdomain.com/api/users' \
  -H 'Authorization: Bearer YOUR_AUTH_TOKEN' \
  -H 'Accept: application/json'
````

- "How do I connect to the database?"

````
Running naive LLM mode on custom query...

============================================================
Question: How do I connect to the database?

Answer:
Connecting to a database depends on several key factors:

1.  **What kind of database are you connecting to?** (e.g., PostgreSQL, MySQL, SQL Server, MongoDB, Redis, Cassandra, Oracle, SQLite, etc.)
2.  **What programming language are you using?** (e.g., Python, Node.js, Java, C#, PHP, Go, Ruby, etc.)
3.  **Where is the database hosted?** (e.g., local machine, cloud service like AWS RDS/Azure SQL/GCP Cloud SQL, on-premise server, Docker container)
4.  **Are you using an Object-Relational Mapper (ORM) or Object-Document Mapper (ODM)?** (e.g., SQLAlchemy, TypeORM, Hibernate, Mongoose)

Below is a general guide and examples for common scenarios.

---

### **Essential Information You'll Need (Connection Details)**

Before you write any code, you'll need these details from your database administrator or your hosting provider:

- **Database Type:** (e.g., PostgreSQL)
- **Host/Server Address:** (e.g., `localhost`, `my-database.abcdef.us-east-1.rds.amazonaws.com`, `192.168.1.100`)
- **Port:** (e.g., `5432` for PostgreSQL, `3306` for MySQL, `27017` for MongoDB)
- **Database Name:** The specific database you want to connect to on the server (e.g., `my_app_db`)
- **Username:** The user account for the database (e.g., `admin`, `app_user`)
- **Password:** The password for the user account
- **SSL/TLS Requirements:** (Does it require a secure connection? Do you need certificates?)

---

### **General Steps for Connecting to a Database**

Regardless of the technology stack, the process generally involves these steps:

1.  **Install the Database Driver/Library:** Your programming language needs a specific library or driver to communicate with your chosen database type.
2.  **Import the Library:** Bring the installed library into your code.
3.  **Construct Connection Parameters:** Provide the host, port, username, password, and database name.
    - **Best Practice:** **NEVER hardcode credentials** directly in your code. Use environment variables, a configuration management system, or a secure vault.
4.  **Establish the Connection:** Use the library's function to open a connection to the database.
5.  **Handle Errors:** Be prepared for connection failures (e.g., incorrect credentials, database offline, network issues).
6.  **Execute Operations:** Once connected, you can send queries (SQL statements, NoSQL commands) to the database.
7.  **Close the Connection:** Release the database connection when you're done, especially for short-lived scripts. For long-running applications (like web servers), connection pooling is often used.

---

### **Examples by Language and Database Type**

Here are common examples for popular languages and databases:

---

#### 1. Python + PostgreSQL (using `psycopg2`)

**Prerequisites:**

```bash
pip install psycopg2-binary
```

**Code Example:**

```python
import os
import psycopg2
from psycopg2 import Error

try:
    # Construct connection string from environment variables for security
    DB_HOST = os.environ.get('DB_HOST', 'localhost')
    DB_NAME = os.environ.get('DB_NAME', 'mydatabase')
    DB_USER = os.environ.get('DB_USER', 'myuser')
    DB_PASSWORD = os.environ.get('DB_PASSWORD', 'mypassword')
    DB_PORT = os.environ.get('DB_PORT', '5432')

    connection = psycopg2.connect(
        host=DB_HOST,
        database=DB_NAME,
        user=DB_USER,
        password=DB_PASSWORD,
        port=DB_PORT
    )

    cursor = connection.cursor()

    # Execute a query
    cursor.execute("SELECT version();")
    record = cursor.fetchone()
    print(f"You are connected to - {record}")

    # Example: Insert data
    # cursor.execute("INSERT INTO users (name, email) VALUES (%s, %s);", ('Alice', 'alice@example.com'))
    # connection.commit() # Commit the transaction for changes

except (Exception, Error) as error:
    print(f"Error while connecting to PostgreSQL or executing query: {error}")

finally:
    # Closing database connection
    if connection:
        cursor.close()
        connection.close()
        print("PostgreSQL connection is closed")

```

---

#### 2. Node.js + MongoDB (using `mongodb` driver)

**Prerequisites:**

```bash
npm install mongodb
```

**Code Example:**

```javascript
const { MongoClient } = require("mongodb");
require("dotenv").config(); // For loading .env files

async function connectToMongoDB() {
  // Construct connection URI from environment variables for security
  const uri = process.env.MONGO_URI || "mongodb://localhost:27017";
  const client = new MongoClient(uri, {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  });

  try {
    await client.connect();
    console.log("Connected successfully to MongoDB server");

    const database = client.db(process.env.MONGO_DB_NAME || "mydatabase");
    const collection = database.collection("mycollection");

    // Example: Insert a document
    const doc = { name: "John Doe", email: "john@example.com" };
    const result = await collection.insertOne(doc);
    console.log(`A document was inserted with the _id: ${result.insertedId}`);

    // Example: Find documents
    const docs = await collection.find({}).toArray();
    console.log("Found documents:", docs);
  } catch (error) {
    console.error("Error connecting to MongoDB:", error);
  } finally {
    await client.close();
    console.log("MongoDB connection closed");
  }
}

connectToMongoDB();
```

`.env` file example:

```
MONGO_URI="mongodb://username:password@host:port"
MONGO_DB_NAME="mydatabase"
```

---

#### 3. Java + MySQL (using JDBC)

**Prerequisites:**

1.  **Download the JDBC driver:** Get the MySQL Connector/J JAR file from the official MySQL website.
2.  **Add to your project's classpath:** If using Maven/Gradle, add the dependency.
    - **Maven:**
      ```xml
      <dependency>
          <groupId>mysql</groupId>
          <artifactId>mysql-connector-java</artifactId>
          <version>8.0.33</version> <!-- Use your desired version -->
      </dependency>
      ```

**Code Example:**

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

public class MySQLConnectionExample {

    public static void main(String[] args) {
        Connection connection = null;
        Statement statement = null;
        ResultSet resultSet = null;

        // Use environment variables or a configuration file for security
        String DB_HOST = System.getenv("DB_HOST") != null ? System.getenv("DB_HOST") : "localhost";
        String DB_PORT = System.getenv("DB_PORT") != null ? System.getenv("DB_PORT") : "3306";
        String DB_NAME = System.getenv("DB_NAME") != null ? System.getenv("DB_NAME") : "mydatabase";
        String DB_USER = System.getenv("DB_USER") != null ? System.getenv("DB_USER") : "myuser";
        String DB_PASSWORD = System.getenv("DB_PASSWORD") != null ? System.getenv("DB_PASSWORD") : "mypassword";

        String url = "jdbc:mysql://" + DB_HOST + ":" + DB_PORT + "/" + DB_NAME + "?useSSL=false";

        try {
            // Load the JDBC driver (optional for modern JDBC, but good practice)
            // Class.forName("com.mysql.cj.jdbc.Driver");

            connection = DriverManager.getConnection(url, DB_USER, DB_PASSWORD);
            System.out.println("Connected to MySQL database!");

            statement = connection.createStatement();

            // Example: Execute a query
            resultSet = statement.executeQuery("SELECT VERSION()");
            if (resultSet.next()) {
                System.out.println("MySQL Version: " + resultSet.getString(1));
            }

            // Example: Insert data
            // int rowsAffected = statement.executeUpdate("INSERT INTO users (name, email) VALUES ('Bob', 'bob@example.com');");
            // System.out.println(rowsAffected + " row(s) inserted.");

        } catch (SQLException e) {
            System.err.println("Database connection error: " + e.getMessage());
        } finally {
            // Close resources in reverse order of creation
            try {
                if (resultSet != null) resultSet.close();
                if (statement != null) statement.close();
                if (connection != null) connection.close();
                System.out.println("MySQL connection closed.");
            } catch (SQLException e) {
                System.err.println("Error closing resources: " + e.getMessage());
            }
        }
    }
}
```

---

### **Important Considerations**

- **Security:**

  - **Never hardcode credentials.** Use environment variables (`process.env`, `os.environ`), secrets management tools (AWS Secrets Manager, Azure Key Vault, HashiCorp Vault), or a secure configuration file.
  - **Use SSL/TLS:** Always encrypt your database connections, especially over public networks. Most drivers support SSL/TLS configuration.
  - **Least Privilege:** Grant database users only the minimum necessary permissions.

- **Connection Pooling:** For web applications or services with frequent database access, establishing a new connection for every request is inefficient. Use a connection pool (e.g., `pg-pool` for Node.js, HikariCP for Java, SQLAlchemy's built-in pool for Python) to manage a pool of reusable connections.

- **Error Handling:** Implement robust `try-catch`/`try-except` blocks to handle connection errors, network issues, and database specific errors gracefully.

- **Object-Relational Mappers (ORMs) / Object-Document Mappers (ODMs):**

  - For relational databases, ORMs like **SQLAlchemy (Python)**, **Hibernate (Java)**, **TypeORM/Sequelize (Node.js)**, **Entity Framework (C#)** abstract away raw SQL and provide an object-oriented way to interact with your database.
  - For NoSQL databases like MongoDB, ODMs like **Mongoose (Node.js)** offer similar benefits.
  - These tools often include their own connection management and pooling.

- **Configuration Management:** For complex applications, consider using libraries like `dotenv` (Node.js/Python) or spring-cloud-config (Java) to manage environment-specific configurations.

---

### **Troubleshooting Common Issues**

- **"Connection refused" / "No route to host":**
  - Database server is not running or is not accessible at the specified host/port.
  - Firewall blocking the connection (on your machine or the database server).
  - Incorrect host or port.
- **"Authentication failed" / "Invalid credentials":**
  - Incorrect username or password.
  - User doesn't exist.
- **"Database 'X' does not exist":**
  - Incorrect database name.
  - Database hasn't been created yet.
- **Missing Driver/Library:**
  - Ensure you've installed the correct package via `pip`, `npm`, `maven`, etc.
- **Network Latency:**
  - If connecting to a cloud database, ensure your local network or server has internet access and can reach the cloud provider's region.

---

**To give you a more precise answer, please tell me:**

- **What database system are you trying to connect to?** (e.g., PostgreSQL, MySQL, MongoDB, Redis, etc.)
- **What programming language are you using?** (e.g., Python, Node.js, Java, C#, PHP, Go, Ruby)
- **Are you trying to connect directly or use an ORM/ODM?**

````

# Part 2

Try asking questions that appear in the docs, such as:

- "Where is the auth token generated?"

`````
Running retrieval only mode on custom query...

============================================================
Question: Where is the auth token generated?

Retrieved snippets:
[API_REFERENCE.md]
# API Reference

This document lists the main API endpoints available in the sample application. It describes each route's purpose, required parameters, and expected responses. All protected endpoints require a valid access token.

## Base URL

    ```plaintext
    /api
    ````

## Authentication Endpoints

### POST /api/login

Authenticates a user and returns a short lived access token.

Request Body:

    ```json
    {
    "username": "example",
    "password": "secret"
    }
    ````

Successful Response:

    ```json
    {
    "access_token": "<token>"
    }
    ```

Notes:

* Returns 401 if credentials are invalid.
* The token must be included in the Authorization header for protected endpoints.

### POST /api/refresh

Exchanges an existing valid token for a new one with an updated expiration time.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response:

    ```json
    {
    "access_token": "<new_token>"
    }
    ```

## User Data Endpoints

### GET /api/users/<user_id>

Fetches profile data for a specific user.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    {
    "user_id": 42,
    "email": "user@example.com",
    "joined_at": "2024-01-15T10:22:00Z"
    }
    ```

Failure Cases:

* 401 if the token is missing or expired
* 403 if the user lacks permission to view this profile
* 404 if no user exists with the given ID

### GET /api/users

Returns a list of all users. Only accessible to admins.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Successful Response:

    ```json
    [
    {
        "user_id": 1,
        "email": "admin@example.com"
    },
    {
        "user_id": 2,
        "email": "guest@example.com"
    }
    ]
    ```

Notes:

* Returns 403 for non admin accounts.

## Project Data Endpoints

### GET /api/projects

Returns all projects visible to the calling user.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    [
    {
        "project_id": "alpha",
        "name": "Alpha Project",
        "status": "active"
    }
    ]
    ```

### GET /api/projects/<project_id>

Fetches detailed information for a single project.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    {
    "project_id": "alpha",
    "name": "Alpha Project",
    "description": "Internal research initiative.",
    "status": "active",
    "owner": 1
    }
    ```

Failure Cases:

* 401 for missing token
* 403 if caller cannot access the project
* 404 if the project does not exist

## Error Formats

All error responses follow this structure:

    ```json
    {
    "error": "Description of the problem"
    }
    ```

Common error messages include:

* "Unauthorized"
* "Forbidden"
* "Not Found"
* "Invalid Request"


---
[AUTH.md]
# Authentication Guide

This document explains how authentication works in the sample application. It covers token generation, required environment variables, and the expected client workflow.

## Overview

The application uses a simple token based system. Every request to a protected endpoint must include a valid access token in the Authorization header. Tokens are short lived and tied to a single user.

## Token Generation

Tokens are created by the `generate_access_token` function in the `auth_utils.py` module. The function takes a user ID and returns a signed JSON Web Token string.

Internally, the token is signed using the secret stored in the `AUTH_SECRET_KEY` environment variable. If the key is missing or empty, token creation will fail.

The token payload includes:

- `user_id`
- `issued_at`
- `expires_at`
- `permissions` (optional)

## Validating Requests

Requests are validated by the `require_auth` decorator. This decorator ensures that:

1. A token is present in the Authorization header
2. The token signature is valid
3. The token has not expired
4. The user has permission to access the requested resource

If validation fails, the client receives a 401 Unauthorized response.

## Environment Variables

The authentication system depends on two variables:

- `AUTH_SECRET_KEY`
  A secret string used to sign all access tokens. Must be long and unpredictable.

- `TOKEN_LIFETIME_SECONDS`
  Controls how long a generated token remains valid. Defaults to 3600 seconds if not set.

Both variables must be configured before starting the server.

## Client Workflow

A typical client follows this sequence:

1. Send credentials to `/api/login`
2. Receive an access token in the response
3. Include the token in the Authorization header for all subsequent requests:

    ```plaintext
    Authorization: Bearer <token>
    ```

4. Refresh the token when it expires by calling `/api/refresh`

Clients should never store tokens in URL query parameters.

## Common Failure Cases

- Token signed with a stale or rotated key
- Clock skew causing premature expiration
- Missing Authorization header
- Incorrect token format (extra whitespace or missing Bearer prefix)

If unexpected authentication failures occur, rotate the secret key and instruct users to log in again.


---
[DATABASE.md]
# Database Guide

This document describes the database layer used in the sample application. It covers connection details, table structures, and common query patterns that appear throughout the codebase.

## Overview

The application uses a lightweight SQLite database for local development. In production environments, it can be configured to use PostgreSQL by providing the correct connection string.

All database interactions are handled through the `db.py` module, which provides helper functions for connecting, executing queries, and mapping results into Python objects.

## Connection Configuration

The database connection is determined by the `DATABASE_URL` environment variable.

Examples:

- SQLite (default):

    ```plaintext
    sqlite:///app.db
    ```

- PostgreSQL:

    ```plaintext
    postgres://user:password@localhost:5432/appdb
    ```

If `DATABASE_URL` is not provided, the application creates a local SQLite database file named `app.db`.

## Tables

### users

Stores basic account information.

| Column       | Type      | Description                         |
|--------------|-----------|-------------------------------------|
| user_id      | INTEGER   | Primary key                         |
| email        | TEXT      | Unique email address                |
| password_hash| TEXT      | Hashed password                     |
| joined_at    | TEXT      | ISO 8601 timestamp                  |

### projects

Represents projects owned or shared with users.

| Column       | Type      | Description                         |
|--------------|-----------|-------------------------------------|
| project_id   | TEXT      | Primary key (string identifier)     |
| name         | TEXT      | Human readable name                 |
| description  | TEXT      | Optional longer description         |
| status       | TEXT      | active, archived, or pending        |
| owner_id     | INTEGER   | Foreign key referencing users       |

### permissions

Maps users to projects and defines what actions they can take.

| Column     | Type    | Description                             |
|------------|---------|-----------------------------------------|
| user_id    | INTEGER | Foreign key                             |
| project_id | TEXT    | Foreign key                             |
| role       | TEXT    | admin, editor, or viewer                |

A user listed as admin automatically has full access to the project.

## Query Helpers

The `db.py` module exposes several helpful functions:

- `get_user_by_id(user_id)`
Returns a dictionary with user details or None if not found.

- `get_all_users()`
Returns a list of all user records.

- `get_projects_for_user(user_id)`
Returns all projects where the user has at least viewer access.

- `get_project_details(project_id)`
Returns a single project record, including its metadata.

These functions are thin wrappers over SQL queries and intentionally simple to make debugging easier.

## Common Failure Cases

- Missing or invalid `DATABASE_URL`
- Incorrect table schema after manual edits
- Queries returning empty results due to missing foreign key references
- SQLite locking errors when multiple writes happen quickly

If schema inconsistencies appear, run database migrations again or recreate the local SQLite file.

## Notes for Development

Developers often encounter confusion between SQLite and PostgreSQL behavior. In particular:

- SQLite allows many implicit type conversions
- SQLite ignores certain constraint violations that PostgreSQL enforces
- Timestamps may appear in different formats across engines

Always test schema related changes using both database backends when possible.
`````

- "Which endpoint returns all users?"

`````
Running retrieval only mode on custom query...

============================================================
Question: Which endpoint returns all users?

Retrieved snippets:
[AUTH.md]
# Authentication Guide

This document explains how authentication works in the sample application. It covers token generation, required environment variables, and the expected client workflow.

## Overview

The application uses a simple token based system. Every request to a protected endpoint must include a valid access token in the Authorization header. Tokens are short lived and tied to a single user.

## Token Generation

Tokens are created by the `generate_access_token` function in the `auth_utils.py` module. The function takes a user ID and returns a signed JSON Web Token string.

Internally, the token is signed using the secret stored in the `AUTH_SECRET_KEY` environment variable. If the key is missing or empty, token creation will fail.

The token payload includes:

- `user_id`
- `issued_at`
- `expires_at`
- `permissions` (optional)

## Validating Requests

Requests are validated by the `require_auth` decorator. This decorator ensures that:

1. A token is present in the Authorization header
2. The token signature is valid
3. The token has not expired
4. The user has permission to access the requested resource

If validation fails, the client receives a 401 Unauthorized response.

## Environment Variables

The authentication system depends on two variables:

- `AUTH_SECRET_KEY`
  A secret string used to sign all access tokens. Must be long and unpredictable.

- `TOKEN_LIFETIME_SECONDS`
  Controls how long a generated token remains valid. Defaults to 3600 seconds if not set.

Both variables must be configured before starting the server.

## Client Workflow

A typical client follows this sequence:

1. Send credentials to `/api/login`
2. Receive an access token in the response
3. Include the token in the Authorization header for all subsequent requests:

    ```plaintext
    Authorization: Bearer <token>
    ```

4. Refresh the token when it expires by calling `/api/refresh`

Clients should never store tokens in URL query parameters.

## Common Failure Cases

- Token signed with a stale or rotated key
- Clock skew causing premature expiration
- Missing Authorization header
- Incorrect token format (extra whitespace or missing Bearer prefix)

If unexpected authentication failures occur, rotate the secret key and instruct users to log in again.


---
[DATABASE.md]
# Database Guide

This document describes the database layer used in the sample application. It covers connection details, table structures, and common query patterns that appear throughout the codebase.

## Overview

The application uses a lightweight SQLite database for local development. In production environments, it can be configured to use PostgreSQL by providing the correct connection string.

All database interactions are handled through the `db.py` module, which provides helper functions for connecting, executing queries, and mapping results into Python objects.

## Connection Configuration

The database connection is determined by the `DATABASE_URL` environment variable.

Examples:

- SQLite (default):

    ```plaintext
    sqlite:///app.db
    ```

- PostgreSQL:

    ```plaintext
    postgres://user:password@localhost:5432/appdb
    ```

If `DATABASE_URL` is not provided, the application creates a local SQLite database file named `app.db`.

## Tables

### users

Stores basic account information.

| Column       | Type      | Description                         |
|--------------|-----------|-------------------------------------|
| user_id      | INTEGER   | Primary key                         |
| email        | TEXT      | Unique email address                |
| password_hash| TEXT      | Hashed password                     |
| joined_at    | TEXT      | ISO 8601 timestamp                  |

### projects

Represents projects owned or shared with users.

| Column       | Type      | Description                         |
|--------------|-----------|-------------------------------------|
| project_id   | TEXT      | Primary key (string identifier)     |
| name         | TEXT      | Human readable name                 |
| description  | TEXT      | Optional longer description         |
| status       | TEXT      | active, archived, or pending        |
| owner_id     | INTEGER   | Foreign key referencing users       |

### permissions

Maps users to projects and defines what actions they can take.

| Column     | Type    | Description                             |
|------------|---------|-----------------------------------------|
| user_id    | INTEGER | Foreign key                             |
| project_id | TEXT    | Foreign key                             |
| role       | TEXT    | admin, editor, or viewer                |

A user listed as admin automatically has full access to the project.

## Query Helpers

The `db.py` module exposes several helpful functions:

- `get_user_by_id(user_id)`
Returns a dictionary with user details or None if not found.

- `get_all_users()`
Returns a list of all user records.

- `get_projects_for_user(user_id)`
Returns all projects where the user has at least viewer access.

- `get_project_details(project_id)`
Returns a single project record, including its metadata.

These functions are thin wrappers over SQL queries and intentionally simple to make debugging easier.

## Common Failure Cases

- Missing or invalid `DATABASE_URL`
- Incorrect table schema after manual edits
- Queries returning empty results due to missing foreign key references
- SQLite locking errors when multiple writes happen quickly

If schema inconsistencies appear, run database migrations again or recreate the local SQLite file.

## Notes for Development

Developers often encounter confusion between SQLite and PostgreSQL behavior. In particular:

- SQLite allows many implicit type conversions
- SQLite ignores certain constraint violations that PostgreSQL enforces
- Timestamps may appear in different formats across engines

Always test schema related changes using both database backends when possible.


---
[API_REFERENCE.md]
# API Reference

This document lists the main API endpoints available in the sample application. It describes each route's purpose, required parameters, and expected responses. All protected endpoints require a valid access token.

## Base URL

    ```plaintext
    /api
    ````

## Authentication Endpoints

### POST /api/login

Authenticates a user and returns a short lived access token.

Request Body:

    ```json
    {
    "username": "example",
    "password": "secret"
    }
    ````

Successful Response:

    ```json
    {
    "access_token": "<token>"
    }
    ```

Notes:

* Returns 401 if credentials are invalid.
* The token must be included in the Authorization header for protected endpoints.

### POST /api/refresh

Exchanges an existing valid token for a new one with an updated expiration time.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response:

    ```json
    {
    "access_token": "<new_token>"
    }
    ```

## User Data Endpoints

### GET /api/users/<user_id>

Fetches profile data for a specific user.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    {
    "user_id": 42,
    "email": "user@example.com",
    "joined_at": "2024-01-15T10:22:00Z"
    }
    ```

Failure Cases:

* 401 if the token is missing or expired
* 403 if the user lacks permission to view this profile
* 404 if no user exists with the given ID

### GET /api/users

Returns a list of all users. Only accessible to admins.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Successful Response:

    ```json
    [
    {
        "user_id": 1,
        "email": "admin@example.com"
    },
    {
        "user_id": 2,
        "email": "guest@example.com"
    }
    ]
    ```

Notes:

* Returns 403 for non admin accounts.

## Project Data Endpoints

### GET /api/projects

Returns all projects visible to the calling user.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    [
    {
        "project_id": "alpha",
        "name": "Alpha Project",
        "status": "active"
    }
    ]
    ```

### GET /api/projects/<project_id>

Fetches detailed information for a single project.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    {
    "project_id": "alpha",
    "name": "Alpha Project",
    "description": "Internal research initiative.",
    "status": "active",
    "owner": 1
    }
    ```

Failure Cases:

* 401 for missing token
* 403 if caller cannot access the project
* 404 if the project does not exist

## Error Formats

All error responses follow this structure:

    ```json
    {
    "error": "Description of the problem"
    }
    ```

Common error messages include:

* "Unauthorized"
* "Forbidden"
* "Not Found"
* "Invalid Request"
`````

# Part 3

Run DocuBot again in Retrieval Only mode and test a question clearly answered by the docs and a vague or unrelated question. Verify that relevant answers are more focused, and irrelevant questions trigger your guardrail.

- "Where is the auth token generated?"

````
Running retrieval only mode on custom query...

============================================================
Question: Where is the auth token generated?

Retrieved snippets:
[API_REFERENCE.md]
### GET /api/users/<user_id>

Fetches profile data for a specific user.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    {
    "user_id": 42,
    "email": "user@example.com",
    "joined_at": "2024-01-15T10:22:00Z"
    }
    ```

Failure Cases:

* 401 if the token is missing or expired
* 403 if the user lacks permission to view this profile
* 404 if no user exists with the given ID

---
[AUTH.md]
## Token Generation

Tokens are created by the `generate_access_token` function in the `auth_utils.py` module. The function takes a user ID and returns a signed JSON Web Token string.

Internally, the token is signed using the secret stored in the `AUTH_SECRET_KEY` environment variable. If the key is missing or empty, token creation will fail.

The token payload includes:

- `user_id`
- `issued_at`
- `expires_at`
- `permissions` (optional)

---
[AUTH.md]
## Validating Requests

Requests are validated by the `require_auth` decorator. This decorator ensures that:

1. A token is present in the Authorization header
2. The token signature is valid
3. The token has not expired
4. The user has permission to access the requested resource

If validation fails, the client receives a 401 Unauthorized response.
````

- "Which endpoint returns all users?"

````
Running retrieval only mode on custom query...

============================================================
Question: Which endpoint returns all users?

Retrieved snippets:
[API_REFERENCE.md]
### GET /api/users

Returns a list of all users. Only accessible to admins.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Successful Response:

    ```json
    [
    {
        "user_id": 1,
        "email": "admin@example.com"
    },
    {
        "user_id": 2,
        "email": "guest@example.com"
    }
    ]
    ```

Notes:

* Returns 403 for non admin accounts.

---
[API_REFERENCE.md]
### GET /api/projects

Returns all projects visible to the calling user.

Headers:

    ```plaintext
    Authorization: Bearer <token>
    ```

Response Example:

    ```json
    [
    {
        "project_id": "alpha",
        "name": "Alpha Project",
        "status": "active"
    }
    ]
    ```

---
[DATABASE.md]
## Overview

The application uses a lightweight SQLite database for local development. In production environments, it can be configured to use PostgreSQL by providing the correct connection string.

All database interactions are handled through the `db.py` module, which provides helper functions for connecting, executing queries, and mapping results into Python objects.
````

- "How do I connect to the database?"

```
Running retrieval only mode on custom query...

============================================================
Question: How do I connect to the database?

Retrieved snippets:
[AUTH.md]
## Environment Variables

The authentication system depends on two variables:

- `AUTH_SECRET_KEY`
  A secret string used to sign all access tokens. Must be long and unpredictable.

- `TOKEN_LIFETIME_SECONDS`
  Controls how long a generated token remains valid. Defaults to 3600 seconds if not set.

Both variables must be configured before starting the server.

---
[SETUP.md]
# Setup Guide

This document explains how to install, configure, and run the sample application. Follow these steps to prepare your environment, set required variables, and verify that everything is working correctly.

---
[SETUP.md]
### Optional Variables

- `TOKEN_LIFETIME_SECONDS`
Controls how long access tokens remain valid.

- `GEMINI_API_KEY`
Enables LLM powered features such as enhanced documentation answers. Without this key, the application falls back to rule based behavior.
```

- "Why is my session expiring?"

```
Running retrieval only mode on custom query...

============================================================
Question: Why is my session expiring?

Retrieved snippets:
I do not know based on these docs.
```

- "What are frogs?"

```
Running retrieval only mode on custom query...

============================================================
Question: What are frogs?

Retrieved snippets:
I do not know based on these docs.
```

# Part 4

Run DocuBot and test the same questions across all three modes. Keep the wording identical so your comparisons are meaningful. As you test, pay attention to what evidence each mode uses, what assumptions it makes, and when it should refuse to answer.

_Mode 3 Only_:

- "Where is the auth token generated?"

```
Running RAG mode on custom query...

============================================================
Question: Where is the auth token generated?

Answer:
The authentication token is generated by the `generate_access_token` function, which is located in the `auth_utils.py` module. This function takes a user ID as input and returns a signed JSON Web Token string. The token is signed using the `AUTH_SECRET_KEY` environment variable.

(Information from `AUTH.md`)
```

- "Which endpoint returns all users?"

```
Running RAG mode on custom query...

============================================================
Question: Which endpoint returns all users?

Answer:
The `GET /api/users` endpoint returns all users.

*   File relied on: `API_REFERENCE.md`
```

- "How do I connect to the database?"

```
Running RAG mode on custom query...

============================================================
Question: How do I connect to the database?

Answer:
I do not know based on the docs I have.
```

- "Why is my session expiring?"

```
Running RAG mode on custom query...

============================================================
Question: Why is my session expiring?

Answer:
I do not know based on these docs.
```

- "What are frogs?"

```
Running RAG mode on custom query...

============================================================
Question: What are frogs?

Answer:
I do not know based on these docs.
```
