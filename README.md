# MehmetHairDesigner Backend API

This is the backend system of **MehmetHairDesigner**, a modern barbershop management platform that supports:

- Role-based admin control  
- Appointment booking (for both guests and registered users)  
- Barber and schedule management  
- Expense tracking and profit analytics  
- Dashboard-level statistics and insights  
- Google and classic login options via JWT  

---

## 🚀 Tech Stack

- **.NET 7 / ASP.NET Core Web API**  
- **Entity Framework Core**  
- **SQL Server**  
- **JWT Authentication**  
- **Google OAuth2 Integration**  
- **Clean Architecture + Service & Repository Layers**

---

## 📦 Key Features

### 🔐 Authentication (`/api/auth`)
- `POST /register` — Register new users with roles  
- `POST /login` — Login and receive JWT token  
- `POST /google-login` — Sign in with Google OAuth2  
- `GET /userinfo` — Get authenticated user info  
- `POST /add-phone` — Add phone to user profile  

### 💈 Barbers (`/api/barber`)
- `GET /get-barber` — List all barbers  
- `POST /post-barber` — Add a new barber  
- `PUT /update-barber/{id}` — Update barber info  
- `DELETE /delete-barber/{id}` — Delete a barber  

### 📅 Appointments (`/api/appointment`)
- `POST /registered` — Create appointment for registered users  
- `POST /guest` — Create appointment for guests  
- `GET /availability` — Get available times by date/barber  
- `GET /available-slots` — Get weekly slot availability  
- `POST /notify-when-available` — Email notification when a time opens  
- `DELETE /{appointmentId}` — Cancel appointment (auth required)  
- `GET /my-appointment` — Fetch user's upcoming appointment  

### 🧑‍💼 Admin Tools (`/api/admin`)
- Manage **Working Hours**, **Busy Slots**, and **Holidays**  
- `GET /pending` — List pending appointments  
- `PUT /appointment/{id}/approve` — Approve appointment  
- `PUT /appointment/{id}/reject` — Reject appointment with mail  
- `POST /manual` — Manually create appointments  
- `POST /complete/{id}` — Mark appointment as done and log price  
- `PUT /appointment/{id}/cancel` — Admin cancels with reason  
- `GET /search-users` — Search for registered users  

### 💰 Expense Management
#### `/api/expenses/types`
- `GET` — List all expense types  
- `POST` — Add new expense type  

#### `/api/expenses/entries`
- `GET` — Get expenses by date range  
- `POST` — Log a new expense  

### 📊 Statistics (`/api/statistics`)
- `GET /appointments-timeline?range=monthly`  
- `GET /top-busiest-days?days=30`  
- `GET /service-type-distribution?days=30`  
- `GET /day-of-week-distribution?days=30`  
- `GET /total-revenue?barberId=&startDate=&endDate=`  
- `GET /revenue-by-month`  
- `GET /revenue-by-weekday`  
- `GET /profit-summary`  
- `GET /monthly-profit`  

---

## 🔑 Authentication

All endpoints under `/api/admin`, `/api/appointment`, and `/api/statistics` require a valid **JWT token** via:

```
Authorization: Bearer <your-token>
```

Some endpoints support Google login via `POST /api/auth/google-login`.

---

## 📂 Sample API Usage

```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "admin@hair.com",
  "password": "Admin123!"
}
```

Response:

```json
{
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": "Mehmet Admin"
}
```

---

## 🧪 Running the Project

1. Clone this repository:
   ```bash
   git clone https://github.com/your-org/mehmethairdesigner-backend.git
   ```

2. Navigate into the project directory:
   ```bash
   cd MehmetHairDesigner.Server
   ```

3. Update `appsettings.json` with your SQL Server connection string and JWT secret.

4. Run migrations and update database:
   ```bash
   dotnet ef database update
   ```

5. Run the application:
   ```bash
   dotnet run
   ```

6. Access Swagger (if enabled):
   ```
   http://localhost:5000/swagger
   ```

---

## 📌 Developer Notes

- Make sure roles like `Admin`, `User`, `Customer` are seeded initially.  
- Most endpoints require authentication and follow role-based authorization.  
- Statistics calculations depend on both **appointments** and **expense entries**.  
- You can integrate this API with any frontend framework like React, Angular, or Blazor.  

---

## 📫 Contact

For contributions, issues, or questions, feel free to open an issue or contact the maintainer.
