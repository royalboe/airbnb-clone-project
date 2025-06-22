# AIRBNB-CLONE-PROJECT

A backend-focused Airbnb clone built with Django REST Framework to master API design, authentication, and database architecture. 

## Team Roles

- Backend Developer: Responsible for implementing API endpoints, database schemas, and business logic.
- Database Administrator: Manages database design, indexing, and optimizations.
- DevOps Engineer: Handles deployment, monitoring, and scaling of the backend services.
- QA Engineer: Ensures the backend functionalities are thoroughly tested and meet quality standards.

## Technology Stack

- Django: A high-level Python web framework used for building the RESTful API.
- Django REST Framework: Provides tools for creating and managing RESTful APIs.
- PostgreSQL: A powerful relational database used for data storage.
- GraphQL: Allows for flexible and efficient querying of data.
- Celery: For handling asynchronous tasks such as sending notifications or processing payments.
- Redis: Used for caching and session management.
- Docker: Containerization tool for consistent development and deployment environments.
- CI/CD Pipelines: Automated pipelines for testing and deploying code changes.

## Database Design

- User: A user can have multiple properties
  - username: Unique user login
  - email: User's emaill address
  - password: User's password (hashed)
  - bio: Short description abour the user
  - is_host: Marks if the user can post properties
  - profile_picture: Optional profile picture
  - join_at: When user joined
- Property: A property can only belong to one user. It has 1:N relationship with PropertyImage
  - title: Name of the property
  - description: Detailed description of the property
  - location: City property is located
  - price_per_night: Price per night in currency
  - max_guests: Maximum number of allowed guests
  - address: The property fulll address
  - host(foreign key): The host who created the property
  - created_at: When property was added
- PropertyImage: Image files for properties, one property can have multiple images
  - property(foreign key): The related property
  - image: Image file
- Booking: Booking for each property by users
  - guest(foreign key): The guest that made the booking
  - property(foreign key): Property being booked
  - check_in: Start date of stay
  - check_out: End date of stay
  - total_price: Totla cost for the booking duration
  - created_at: When booking was made
- Review: Review left by a guest after their stay; one to one relatonship with booking
  - booking: One review per booking
  - rating: Rating for booking
  - comment: Optional written feedback
  - created_at: Whent he review was posted
- Payment: Payment for the booking, one to one relationship with booking
  - booking: One payment per booking
  - payment_status: Status: Pending, Completed, Failed
  - amount: Total payment amount
  - transaction_id: Unique payment reference
  - payment_method: Payment type
  - created_id: When payment was made

 ## Feature Breakdown

1. User Authentication
Endpoints: /users/, /users/{user_id}/
Features: Register new users, authenticate, and manage user profiles.
2. Property Management
Endpoints: /properties/, /properties/{property_id}/
Features: Create, update, retrieve, and delete property listings.
3. Booking System
Endpoints: /bookings/, /bookings/{booking_id}/
Features: Make, update, and manage bookings, including check-in and check-out details.
4. Payment Processing
Endpoints: /payments/
Features: Handle payment transactions related to bookings.
5. Review System
Endpoints: /reviews/, /reviews/{review_id}/
Features: Post and manage reviews for properties.
6. Database Optimizations
Indexing: Implement indexes for fast retrieval of frequently accessed data.
Caching: Use caching strategies to reduce database load and improve performance.


## API Security

Ensuring robust security is critical in a platform handling sensitive data such as user profiles, bookings, and payments. The following security measures will be implemented:

1. Authentication
Use JWT (JSON Web Tokens) or Token-based Authentication to verify the identity of users.
Authenticated users will receive secure tokens upon login to access protected endpoints.
Passwords will be hashed using a secure algorithm (e.g., Argon2 or Django’s default PBKDF2).

2. Authorization
Role-based access control will be enforced (e.g., only hosts can create/edit properties).
Permissions will be used to restrict access to actions based on user type and ownership of data.

3. Rate Limiting
Prevent brute force attacks and API abuse by implementing request throttling.
Tools like Django REST Framework's throttling classes will be configured for key endpoints.

4. Input Validation & Serialization
All input data will be validated through DRF serializers to avoid injection attacks and malformed requests.
Strict type checking, length validation, and sanitation will be enforced.

5. HTTPS Enforcement
All API communications will be over HTTPS to ensure end-to-end encryption of requests and responses (especially in production deployments).

6. CSRF Protection
For web-based frontend clients using cookies, CSRF protection will be enabled to prevent cross-site request forgery.

7. CORS Configuration
CORS (Cross-Origin Resource Sharing) will be configured to allow only approved frontend origins to interact with the API.

8. Sensitive Data Handling
Payment data, user credentials, and session tokens will never be exposed in logs or error messages.

Environment variables (.env) will be used to securely store secrets like API keys and DB credentials.

## CI/CD Pipeline

ChatGPT said:
Here’s what you can include under the CI/CD Pipeline section of your README.md for the Airbnb Clone Project, written clearly and ready to paste:

🚀 CI/CD Pipeline
To ensure consistent integration and deployment of code changes, this project will utilize a CI/CD (Continuous Integration/Continuous Deployment) pipeline.

✅ What is CI/CD?
- Continuous Integration (CI) involves automatically building, testing, and validating code whenever changes are pushed to the repository.
- Continuous Deployment (CD) automates the delivery of tested code to production or staging environments.
This process improves development speed, reduces bugs in production, and ensures the project remains in a deployable state at all times.

🛠️ Tools Used
- GitHub Actions: Automates workflows such as testing, linting, and deployment upon push or pull requests.
- Docker: Containerizes the application to ensure consistent behavior across different environments.
- Heroku / Render / AWS / Railway (Optional): A platform-as-a-service (PaaS) provider that can host the deployed application.

🔄 Planned Workflow
- Code Push: Developer pushes code to a GitHub branch (e.g., main, dev).
- Automated Tests: GitHub Actions runs unit tests using pytest or Django’s test framework.
- Linting & Formatting: Code is checked using tools like flake8 or black.
- Build Docker Image: The code is containerized into an image.
- Deploy: If on the main branch and all checks pass, the app is deployed automatically to the hosting provider.
- Notify: Developers are notified about build/deploy status via GitHub or Slack integration.

 
