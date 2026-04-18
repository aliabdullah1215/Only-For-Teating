### 5. Plan SCM and QA Strategies

#### SCM Strategy

The project should use **Git** as the source control management tool, with a simple branch structure that supports ongoing MVP development and safe integration.

**Branching Strategy**
- `main`: production-ready code only
- `develop`: integration branch for completed features before production release
- `feature/<feature-name>`: used for individual tasks such as `feature/ai-plan-validation` or `feature/doctor-application-ui`
- `fix/<issue-name>`: used for bug fixes
- `hotfix/<issue-name>`: reserved for urgent production fixes

**SCM Process**
- Each new feature or bug fix should be developed in its own branch.
- Developers should make small, regular commits with clear messages.
- All completed work should be submitted through a **Pull Request** into `develop`.
- Pull Requests should be reviewed before merging.
- After validation in `develop`, stable increments should be merged into `main`.

**Code Review Rules**
- Reviewers should verify:
  - correctness of business logic
  - API contract consistency between React and Django
  - role-based access control for `client` and `doctor`
  - input validation and error handling
  - no sensitive configuration values are hardcoded in production code
- Pull Requests should not be merged without at least one review.

---

#### QA Strategy

The QA approach for this MVP should combine **manual testing**, **API testing**, **unit testing**, and **basic build validation**.

**1. Front-End QA**
- **Linting Tool:** ESLint
- **Current validation available:** `npm run lint`
- **Recommended tests:**
  - component tests for authentication screens
  - component tests for AI questionnaire flow
  - component tests for nutrition plan rendering and local edit actions
- **Recommended tools:**
  - React Testing Library
  - Vitest or Jest

**2. Back-End QA**
- **Current framework:** Django test framework is available, but automated tests are still minimal
- **Recommended tests:**
  - unit tests for serializers and permission classes
  - unit tests for AI profile validation and generated plan validation
  - integration tests for:
    - registration
    - login
    - current user endpoint
    - doctor application submission
    - approved doctors retrieval
    - AI plan generation endpoint
- **Recommended tools:**
  - Django `TestCase`
  - Django REST Framework API test tools
  - Postman for manual API verification

**3. Manual Testing for Critical User Flows**
The following flows should be tested manually in every major release:
- client registration and login
- doctor registration and login
- doctor application submission with file upload
- client AI questionnaire completion
- AI nutrition plan generation
- local meal/ingredient replacement actions
- approved doctor listing in Medical Support
- token expiry and refresh behavior

**4. API Testing**
- Use **Postman** to validate request/response behavior for all backend endpoints.
- Maintain a Postman collection for:
  - authentication endpoints
  - doctor application endpoints
  - AI plan generation endpoint

**5. Build and Deployment Validation**
- Frontend:
  - run `npm run lint`
  - run `npm run build`
- Backend:
  - run Django tests
  - verify migrations
  - verify environment variables such as database configuration and `GROQ_API_KEY`

---

#### Deployment Pipeline Plan

The project should use two environments:

**Staging**
- Used for integration testing before production
- Deployed from `develop`
- Validates end-to-end flows with real backend/frontend integration

**Production**
- Used for final release
- Deployed only from `main`
- Requires successful review and staging validation before release

**Recommended Pipeline Stages**
1. Pull latest branch
2. Install dependencies
3. Run frontend linting
4. Run frontend build
5. Run backend tests
6. Apply database migrations
7. Deploy to staging or production based on branch

---

#### Summary

**SCM**
- Git-based workflow
- `main`, `develop`, `feature/*`, `fix/*`, `hotfix/*`
- Pull requests and code review required before merge

**QA**
- ESLint for frontend quality checks
- Django test framework for backend validation
- Postman for API verification
- Manual testing for critical MVP user journeys
- Staging before production deployment

