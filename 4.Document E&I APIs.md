### 4. Document External and Internal APIs

#### External APIs

**1. Groq API**
- **Purpose:** Generates personalized nutrition plans from the normalized client profile.
- **Why it was chosen:** It supports fast LLM inference and returns structured JSON through a chat-completions style API, which fits the project’s AI nutrition-plan workflow.
- **Used by:** Django backend only
- **Endpoint used by the project:** `https://api.groq.com/openai/v1/chat/completions`

---

#### Internal API Endpoints

| URL Path | Method | Input Format | Output Format | Description |
|---|---|---|---|---|
| `/api/users/register/` | `POST` | JSON | JSON | Registers a new user as `client` or `doctor` |
| `/api/users/login/` | `POST` | JSON | JSON | Authenticates user and returns tokens plus user info |
| `/api/users/me/` | `GET` | Authorization header (`Bearer token`) | JSON | Returns the current authenticated user |
| `/api/users/doctor-application/` | `GET` | Authorization header | JSON | Returns the current doctor’s submitted application |
| `/api/users/doctor-application/` | `POST` | `multipart/form-data` | JSON | Submits a new doctor application with certificate upload |
| `/api/users/approved-doctors/` | `GET` | Authorization header | JSON | Returns approved doctors for client medical support |
| `/api/ai-plans/generate/` | `POST` | JSON | JSON | Generates a nutrition plan from a normalized client profile |
| `/api/token/` | `POST` | JSON | JSON | Returns JWT access and refresh tokens |
| `/api/token/refresh/` | `POST` | JSON | JSON | Returns a new JWT access token using a refresh token |

---

#### Endpoint Details

**1. Register User**
- **URL:** `/api/users/register/`
- **Method:** `POST`
- **Input:** JSON

```json
{
  "username": "sara",
  "email": "sara@example.com",
  "password": "StrongPass123",
  "role": "client"
}
```

- **Output:** JSON

```json
{
  "user": {
    "id": 1,
    "username": "sara",
    "email": "sara@example.com",
    "role": "client"
  },
  "message": "User registered successfully!"
}
```

---

**2. Login User**
- **URL:** `/api/users/login/`
- **Method:** `POST`
- **Input:** JSON

```json
{
  "username": "sara",
  "password": "StrongPass123"
}
```

- **Output:** JSON

```json
{
  "refresh": "jwt_refresh_token",
  "access": "jwt_access_token",
  "user": {
    "id": 1,
    "username": "sara",
    "email": "sara@example.com",
    "role": "client"
  },
  "message": "Login successful"
}
```

---

**3. Obtain JWT Token Pair**
- **URL:** `/api/token/`
- **Method:** `POST`
- **Input:** JSON

```json
{
  "username": "sara",
  "password": "StrongPass123"
}
```

- **Output:** JSON

```json
{
  "refresh": "jwt_refresh_token",
  "access": "jwt_access_token"
}
```

**Note:** This is the authentication endpoint currently used by the frontend login service.

---

**4. Refresh JWT Access Token**
- **URL:** `/api/token/refresh/`
- **Method:** `POST`
- **Input:** JSON

```json
{
  "refresh": "jwt_refresh_token"
}
```

- **Output:** JSON

```json
{
  "access": "new_jwt_access_token"
}
```

---

**5. Get Current User**
- **URL:** `/api/users/me/`
- **Method:** `GET`
- **Input:** Authorization header
- **Output:** JSON

```json
{
  "id": 1,
  "username": "sara",
  "email": "sara@example.com",
  "role": "client"
}
```

---

**6. Submit Doctor Application**
- **URL:** `/api/users/doctor-application/`
- **Method:** `POST`
- **Input:** `multipart/form-data`

**Form Fields**
- `full_name`
- `age`
- `specialty`
- `phone_number`
- `contact_email`
- `certificate_file`

- **Output:** JSON

```json
{
  "id": 4,
  "full_name": "Dr. Ahmad Ali",
  "age": 38,
  "specialty": "Clinical Nutrition",
  "phone_number": "+966500000000",
  "contact_email": "doctor@example.com",
  "certificate_file": "doctor_certificates/file.pdf",
  "certificate_file_url": "http://localhost:8000/media/doctor_certificates/file.pdf",
  "status": "pending",
  "reviewed_at": null,
  "created_at": "2026-04-17T12:00:00Z",
  "updated_at": "2026-04-17T12:00:00Z"
}
```

---

**7. Get Doctor Application Status**
- **URL:** `/api/users/doctor-application/`
- **Method:** `GET`
- **Input:** Authorization header
- **Output:** JSON

```json
{
  "id": 4,
  "full_name": "Dr. Ahmad Ali",
  "age": 38,
  "specialty": "Clinical Nutrition",
  "phone_number": "+966500000000",
  "contact_email": "doctor@example.com",
  "certificate_file_url": "http://localhost:8000/media/doctor_certificates/file.pdf",
  "status": "pending",
  "reviewed_at": null,
  "created_at": "2026-04-17T12:00:00Z",
  "updated_at": "2026-04-17T12:00:00Z"
}
```

---

**8. Get Approved Doctors**
- **URL:** `/api/users/approved-doctors/`
- **Method:** `GET`
- **Input:** Authorization header
- **Output:** JSON array

```json
[
  {
    "id": 4,
    "username": "doctor1",
    "full_name": "Dr. Ahmad Ali",
    "specialty": "Clinical Nutrition",
    "phone_number": "+966500000000",
    "contact_email": "doctor@example.com"
  }
]
```

---

**9. Generate AI Nutrition Plan**
- **URL:** `/api/ai-plans/generate/`
- **Method:** `POST`
- **Input:** JSON

```json
{
  "profile": {
    "age": 28,
    "weight_kg": 70,
    "height_cm": 165,
    "sex": "female"
  },
  "goal": {
    "type": "weight_loss",
    "pace": "moderate"
  },
  "activity": {
    "level": "moderate"
  },
  "health": {},
  "preferences": {},
  "behavior": {},
  "output_preferences": {
    "language": "en"
  }
}
```

- **Output:** JSON

```json
{
  "summary": {
    "daily_calories": 1800,
    "daily_macros": {
      "protein_g": 130,
      "carbs_g": 170,
      "fat_g": 60
    },
    "plan_goal": "weight_loss"
  },
  "days": [
    {
      "day_number": 1,
      "title": "Day 1",
      "meals": []
    }
  ],
  "shopping_list": [
    "Chicken breast",
    "Oats",
    "Greek yogurt"
  ],
  "plan_tags": [
    "high_protein",
    "balanced"
  ],
  "fallback_message": ""
}
```

