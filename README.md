# 🍔 QuickBite — Campus Food Ordering System

A JavaFX + JDBC + MySQL desktop project for VS Code. Includes a modern food-app-inspired interface, **54 seeded Indian/campus dishes**, signup/login, search, categories, cart, stock-validated checkout, order status, downloadable text receipt, admin order management and inventory CRUD.

## Requirements
- JDK 21 (check `java -version`)
- Maven 3.9+ (`mvn -version`)
- MySQL Server 8+ running locally
- VS Code with **Extension Pack for Java**

## Run in VS Code
1. Extract the ZIP, then open the **QuickBite** folder in VS Code (`File > Open Folder`).
2. Start MySQL server. Create a MySQL user or use your existing root user. **No manual SQL import is needed**: the app creates the database/tables and sample menu on first run (the user must have CREATE DATABASE privileges).
3. Set the database credentials in your VS Code terminal:
   - **Windows PowerShell**: `$env:QB_DB_USER="root"; $env:QB_DB_PASS="YOUR_MYSQL_PASSWORD"`
   - **Windows CMD**: `set QB_DB_USER=root` and `set QB_DB_PASS=YOUR_MYSQL_PASSWORD`
   - **macOS/Linux**: `export QB_DB_USER=root QB_DB_PASS=YOUR_MYSQL_PASSWORD`
4. In the **same terminal**, run `mvn clean javafx:run`.
5. JavaFX window opens. Click **Create account** to sign up as a student.

Optional connection override: `QB_DB_URL=jdbc:mysql://localhost:3306/quickbite?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true`.

## Demo admin login
- Email: `admin@quickbite.local`
- Password: `Admin@123`

**Change the default admin password before any deployment.** The password is seeded only if there is no admin account. Authentication uses SHA-256 for this local classroom demonstration; a production system should use salted Argon2id or bcrypt hashes, authorization checks, and a proper secrets manager.

## Student features
- Register, log in, browse food by category, search by dish name (press **Enter**), add/remove/change quantities in cart.
- Checkout with **Cash on Pickup**, **UPI (Demo)** or **Card (Demo)**.
- View current status by refreshing **My Orders**; view and save receipt to your home folder.

## Admin features
- Log in with demo admin credentials, open **Admin Orders** to set PLACED → PREPARING → READY → COMPLETED (or CANCELLED).
- Open **Inventory** to add dishes, edit prices and stock, or hide dishes.
- Order placement is a MySQL transaction that locks rows and decrements stock safely.

## Important limitations
- UPI and Card are **simulated**: no real money is collected. For real payments, integrate a certified gateway with server-side payment verification and webhooks.
- Status is refreshed manually, not WebSocket push. Admin cancellation does not restock automatically.
- This is a desktop application with a local MySQL database, not a cloud/mobile app. For multi-device production, add a backend API and role-secured server.
- Menu uses emoji illustrations, not copyrighted brand images.

## Structure
- `src/main/java/com/quickbite/App.java`: all JavaFX screens and event handlers
- `src/main/java/com/quickbite/DB.java`: MySQL schema, demo data, transactional ordering
- `src/main/resources/com/quickbite/style.css`: app theme
- `pom.xml`: Maven dependencies and JavaFX run plugin
