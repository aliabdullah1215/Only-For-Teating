# Data Diet

Data Diet is an AI-powered nutrition platform that helps users generate personalized diet plans, track their nutrition journey, and connect with approved nutrition specialists through a structured web experience rather than a generic chatbot conversation.

The project is built as a full-stack web application with:

- A `React + Vite` frontend
- A `Django REST Framework` backend
- `JWT` authentication
- `PostgreSQL` database support
- AI nutrition plan generation powered by the `Groq API`

## Overview

Many people struggle to find trustworthy and personalized nutrition guidance. Most advice online is too general, while professional consultations can be expensive or difficult to access.

Data Diet addresses this by offering a platform where users can:

- Enter their body data, goals, activity level, health conditions, and food preferences
- Generate personalized AI nutrition plans
- Review a structured plan with calories, macros, meals, alternatives, and shopping lists
- Save previous plans and revisit them later
- Access approved nutrition specialists through the platform
- Use separate role-based flows for clients and doctors

This makes Data Diet more than a chatbot. It is a guided nutrition product with structured input, validated workflows, saved history, and specialist access.

## Features

### Client Features

- User registration and login
- Secure JWT-based authentication
- Personalized nutrition questionnaire
- AI-generated diet plan based on user profile
- Structured nutrition plan output
- Daily calorie and macro summary
- Meal-by-meal plan breakdown
- Ingredient substitutions
- Meal alternatives
- Shopping list generation
- Plan history and saved plans
- Medical support section for approved doctors

### Doctor Features

- Register with doctor role
- Access dedicated doctor dashboard
- Submit doctor application
- Upload certificate/documentation
- Await admin approval
- Appear in approved doctors listing once accepted

### Platform Features

- Role-based route protection
- Client and doctor dashboards
- Backend profile validation before AI generation
- Plan persistence using JSON-based storage
- Support for future expansion into tracking, assessments, and ongoing guidance

## Why This Project

Unlike general AI chat tools, Data Diet is designed around a specific use case: nutrition planning.

Instead of asking users to write a perfect prompt, the system collects structured health and lifestyle information, validates it, and converts it into a usable nutrition plan. The output is stored, organized, and tied to the user account, making it practical for repeated use.

## Tech Stack

### Frontend

- React 19
- Vite
- React Router
- Axios
- Context API

### Backend

- Python
- Django
- Django REST Framework
- SimpleJWT
- django-cors-headers

### Database

- PostgreSQL

### AI Integration

- Groq API

## Project Structure

```text
Data-Diet/
├── backend/
│   ├── ai_plans/
│   ├── core/
│   ├── users/
│   ├── media/
│   └── manage.py
├── frontend/
│   ├── src/
│   │   ├── api/
│   │   ├── app/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── context/
│   │   ├── features/
│   │   ├── pages/
│   │   ├── routes/
│   │   └── styles/
│   └── package.json
├── README.md
├── Idea Development Documentation.md
└── Project Charter Development.md
```

## Main User Roles

### 1. Client

A client can:

- Create an account
- Log in securely
- Fill out the nutrition questionnaire
- Generate a personalized AI nutrition plan
- View saved plans
- Access medical support resources

### 2. Doctor

A doctor can:

- Register with the doctor role
- Log in to a dedicated dashboard
- Submit an application with professional documentation
- Wait for approval from the administration
- Become visible in the approved doctors directory

## Nutrition Plan Workflow

The AI plan generation flow is designed to be structured and practical.

### Input Collected

The system gathers user information across multiple sections such as:

- Goal
- Body data
- Activity level
- Health conditions
- Allergies
- Dietary restrictions
- Food preferences
- Budget sensitivity
- Meal behavior
- Output preferences

### AI Output Includes

- Daily calorie target
- Daily macros
- Plan goal summary
- Multi-day meal plan
- Meal tags
- Preparation time
- Cost estimation
- Ingredient substitutions
- Meal alternatives
- Shopping list
- Fallback notes when needed

## API Overview

Base URL:

```text
http://localhost:8000/api/
```

### Authentication

- `POST /api/token/`
- `POST /api/token/refresh/`

### Users

- `POST /api/users/register/`
- `POST /api/users/login/`
- `GET /api/users/me/`

### Doctor Applications

- `GET /api/users/doctor-application/`
- `POST /api/users/doctor-application/`

### Doctors Directory

- `GET /api/users/approved-doctors/`

### AI Plans

- `POST /api/ai-plans/generate/`
- `GET /api/ai-plans/`
- `GET /api/ai-plans/<id>/`

## Getting Started

### Prerequisites

Make sure you have the following installed:

- Python 3.x
- Node.js and npm
- PostgreSQL
- Git

## Backend Setup

1. Move into the backend directory:

```powershell
cd backend
```

2. Create a virtual environment:

```powershell
python -m venv venv
```

3. Activate the virtual environment:

```powershell
.\venv\Scripts\Activate.ps1
```

4. Install dependencies:

```powershell
pip install django djangorestframework djangorestframework-simplejwt django-cors-headers psycopg2-binary requests
```

5. Create a `.env` file based on `.env.example` and add your Groq configuration:

```env
GROQ_API_KEY=your_groq_api_key_here
GROQ_MODEL=llama-3.3-70b-versatile
```

6. Configure PostgreSQL in `backend/core/settings.py`

Update the database settings with your local credentials.

7. Run migrations:

```powershell
python manage.py migrate
```

8. Start the backend server:

```powershell
python manage.py runserver
```

Backend runs on:

```text
http://localhost:8000/
```

## Frontend Setup

1. Open a second terminal
2. Move into the frontend directory:

```powershell
cd frontend
```

3. Install dependencies:

```powershell
npm install
```

4. Start the development server:

```powershell
npm run dev
```

Frontend usually runs on:

```text
http://localhost:5173/
```

## Environment Variables

Example backend environment configuration:

```env
GROQ_API_KEY=your_groq_api_key_here
GROQ_MODEL=llama-3.3-70b-versatile
```

## Authentication and Authorization

Data Diet uses JWT authentication for protected API access.

The platform supports two main roles:

- `client`
- `doctor`

Protected routes are separated by role:

- Client routes under `/client`
- Doctor routes under `/doctor`

This ensures each user only accesses the features intended for their role.

## Current Scope

This repository currently covers the MVP foundation for Data Diet, including:

- Authentication
- Role-based dashboards
- Doctor applications
- Approved doctor listing
- AI-powered nutrition plan generation
- Plan persistence and retrieval

Some pages and sections are still scaffolded for future development, so the project should be considered an in-progress MVP.

## Limitations

Current known limitations include:

- No dedicated backend `requirements.txt` yet
- Database configuration still needs cleanup for full environment-based setup
- Some pages are placeholders for future features
- The project is currently configured for development use
- The AI guidance should be treated as support, not a medical replacement

## Future Improvements

Possible next steps for the project include:

- Weekly follow-up and progress tracking
- Smarter plan adaptation based on user results
- Arabic and multilingual support
- More localized meal plans for regional diets
- Admin review dashboard for doctor applications
- Better analytics and nutritional indicators
- Notifications and reminders
- Automated tests
- Production deployment pipeline
- Mobile-friendly expansion or dedicated mobile app

## Safety Note

Data Diet is intended to support healthier decision-making and improve access to nutrition guidance. It should not be treated as a replacement for licensed medical diagnosis or urgent clinical care. Users with medical conditions should be encouraged to consult qualified professionals.

## Team

- Ali Summan — Project Manager
- Omar Al-Anazi — Frontend Developer
- Mohammed Basulaiman — Full-Stack Developer
- Hussam Al-Mutairi — Backend Developer

## Documentation

Additional project documentation included in the repository:

- `Idea Development Documentation.md`
- `Project Charter Development.md`

## License

This project currently does not define a formal license. Add one before public distribution if needed.
