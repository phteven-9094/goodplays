# goodplays

A Goodreads-like app where users can add video games to lists, look up game details, and manage their gaming library.

## Features

- User authentication and profiles
- Game library management with lists (backlog, currently playing, completed, upcoming, wishlist)
- Game search and discovery using IGDB API
- Game ratings and reviews
- Personal gaming statistics and insights
- Social features (following users, sharing lists)

## Development Steps

### Phase 1: Project Setup

1. Initialize Python project with FastAPI backend
2. Set up database schema with SQLAlchemy/Alembic
3. Configure environment variables and secrets management
4. Set up CI/CD pipeline with GitHub Actions
5. Initialize frontend (React/Vue.js)

### Phase 2: Core Backend APIs

1. User authentication and authorization (JWT tokens)
2. User management endpoints
3. Game data integration with IGDB API
4. Game list management (CRUD operations)
5. Rating and review system
6. Search and filtering functionality

### Phase 3: Frontend Development

1. Authentication pages (login, register, profile)
2. Game search and browse interface
3. Game details pages
4. Personal library and list management
5. Dashboard with statistics
6. Responsive mobile design

### Phase 4: Advanced Features

1. Social features (user following, public profiles)
2. Recommendation engine
3. Import/export functionality
4. Advanced filtering and sorting
5. Gaming statistics and insights

### Phase 5: Deployment & Optimization

1. Production deployment to AWS
2. Performance optimization
3. Monitoring and logging
4. Error handling and validation
5. Security hardening

## API Endpoints

### Authentication

- `POST /auth/register` - User registration
- `POST /auth/login` - User login
- `POST /auth/refresh` - Token refresh
- `DELETE /auth/logout` - User logout

### Users

- `GET /users/me` - Get current user profile
- `PUT /users/me` - Update user profile
- `GET /users/{user_id}` - Get public user profile
- `GET /users/{user_id}/lists` - Get user's public lists

### Games

- `GET /games/search` - Search games via IGDB
- `GET /games/{game_id}` - Get game details
- `POST /games/{game_id}/cache` - Cache game data locally
- `GET /games/trending` - Get trending games

### Lists

- `GET /lists` - Get user's game lists
- `POST /lists` - Create new list
- `PUT /lists/{list_id}` - Update list
- `DELETE /lists/{list_id}` - Delete list
- `POST /lists/{list_id}/games` - Add game to list
- `DELETE /lists/{list_id}/games/{game_id}` - Remove game from list

### Reviews & Ratings

- `POST /games/{game_id}/reviews` - Create review
- `GET /games/{game_id}/reviews` - Get game reviews
- `PUT /reviews/{review_id}` - Update review
- `DELETE /reviews/{review_id}` - Delete review

### Reviews & Ratings

- `POST /games/{game_id}/reviews` - Create review
- `GET /games/{game_id}/reviews` - Get game reviews
- `PUT /reviews/{review_id}` - Update review
- `DELETE /reviews/{review_id}` - Delete review

## Directory Structure

```

goodplays/
├── backend/
│ ├── app/
│ │ ├── **init**.py
│ │ ├── main.py # FastAPI app entry point
│ │ ├── core/
│ │ │ ├── **init**.py
│ │ │ ├── config.py # App configuration
│ │ │ ├── security.py # JWT and auth utilities
│ │ │ └── database.py # Database connection
│ │ ├── models/
│ │ │ ├── **init**.py
│ │ │ ├── user.py # User model
│ │ │ ├── game.py # Game model
│ │ │ ├── list.py # GameList model
│ │ │ ├── review.py # Review model
│ │ │ └── associations.py # Many-to-many tables
│ │ ├── schemas/
│ │ │ ├── **init**.py
│ │ │ ├── user.py # User Pydantic schemas
│ │ │ ├── game.py # Game schemas
│ │ │ ├── list.py # List schemas
│ │ │ └── review.py # Review schemas
│ │ ├── api/
│ │ │ ├── **init**.py
│ │ │ ├── deps.py # API dependencies
│ │ │ └── v1/
│ │ │ ├── **init**.py
│ │ │ ├── auth.py # Auth endpoints
│ │ │ ├── users.py # User endpoints
│ │ │ ├── games.py # Game endpoints
│ │ │ ├── lists.py # List endpoints
│ │ │ └── reviews.py # Review endpoints
│ │ ├── services/
│ │ │ ├── **init**.py
│ │ │ ├── igdb_client.py # IGDB API integration
│ │ │ ├── user_service.py # User business logic
│ │ │ ├── game_service.py # Game business logic
│ │ │ └── list_service.py # List business logic
│ │ ├── crud/
│ │ │ ├── **init**.py
│ │ │ ├── base.py # Base CRUD operations
│ │ │ ├── user.py # User CRUD
│ │ │ ├── game.py # Game CRUD
│ │ │ ├── list.py # List CRUD
│ │ │ └── review.py # Review CRUD
│ │ └── utils/
│ │ ├── **init**.py
│ │ ├── exceptions.py # Custom exceptions
│ │ └── helpers.py # Utility functions
│ ├── alembic/ # Database migrations
│ ├── tests/
│ │ ├── **init**.py
│ │ ├── conftest.py
│ │ ├── test_auth.py
│ │ ├── test_users.py
│ │ ├── test_games.py
│ │ └── test_lists.py
│ ├── requirements.txt
│ ├── alembic.ini
│ └── Dockerfile
├── frontend/
│ ├── public/
│ ├── src/
│ │ ├── components/
│ │ │ ├── auth/
│ │ │ ├── games/
│ │ │ ├── lists/
│ │ │ └── common/
│ │ ├── pages/
│ │ ├── services/
│ │ ├── store/
│ │ ├── utils/
│ │ └── App.js
│ ├── package.json
│ └── Dockerfile
├── infrastructure/
│ ├── terraform/
│ │ ├── main.tf
│ │ ├── variables.tf
│ │ ├── outputs.tf
│ │ └── modules/
│ └── docker-compose.yml
├── .github/
│ └── workflows/
│ ├── backend-ci.yml
│ └── frontend-ci.yml
├── .gitignore
├── README.md
├── docker-compose.yml
└── .env.example

## AWS Resources Required

### Core Infrastructure

- **ECS Fargate** - Container hosting for backend and frontend
- **Application Load Balancer** - Traffic distribution and SSL termination
- **RDS PostgreSQL** - Primary database
- **ElastiCache Redis** - Caching and session storage
- **S3** - Static file storage and frontend hosting
- **CloudFront** - CDN for global content delivery

### Security & Authentication

- **AWS Cognito** - User authentication (alternative to custom JWT)
- **AWS Secrets Manager** - Store API keys and database credentials
- **VPC** - Network isolation and security groups

### Monitoring & Logging

- **CloudWatch** - Application monitoring and logging
- **AWS X-Ray** - Application tracing
- **SNS** - Alert notifications

### CI/CD

- **ECR** - Container image registry
- **CodeBuild** - CI/CD pipeline
- **CodePipeline** - Deployment automation

### Optional Enhancements

- **Lambda** - Serverless functions for background tasks
- **SQS** - Message queuing for async processing
- **API Gateway** - API management and rate limiting
- **Route 53** - DNS management
- **Certificate Manager** - SSL certificate management

## External APIs

- **IGDB API** - Game data, images, and metadata
- **Steam API** - Additional game data and user import (optional)
- **Twitch API** - Required for IGDB API access

## Technology Stack

### Backend

- **Python 3.11+**
- **uv** - Fast Python package manager
- **FastAPI** - Modern web framework
- **SQLAlchemy** - ORM
- **Alembic** - Database migrations
- **Pydantic** - Data validation
- **PyJWT** - JWT token handling
- **pytest** - Testing framework

### Frontend

- **React** or **Vue.js** - Frontend framework
- **TypeScript** - Type safety
- **Axios** - HTTP client
- **React Router** - Navigation
- **Material-UI** or **Tailwind CSS** - UI components

### Database

- **PostgreSQL** - Primary database
- **Redis** - Caching and sessions

### DevOps

- **Docker** - Containerization
- **Terraform** - Infrastructure as code
- **GitHub Actions** - CI/CD pipeline

## Getting Started

### Prerequisites
- Python 3.11+
- [uv](https://docs.astral.sh/uv/getting-started/installation/) package manager

### Installation
```

1. Clone the repository

   ```bash
   git clone <repository-url>
   cd goodplays
   ```

2. Navigate to backend directory
   ```bash
   cd backend
   ```
3. Install dependencies with uv
   ```bash
   uv sync
   ```
4. Copy environment file and configure
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```
5. Set up database migrations
   ```bash
   uv run alembix upgrade head
   ```
6. Run development server
   ```bash
   uv run uvicorn app.main:app --reload
   ```
7. Access API documentation at http://localhost:8000/docs

```
### Development Commands
```

```python
# Install new dependency
uv add fastapi

# Install development dependency
uv add --dev pytest

# Run tests
uv run pytest

# Run with specific Python version
uv run --python 3.11 uvicorn app.main:app --reload

# Update dependencies
uv sync --upgrade

# Create virtual environment manually (optional)
uv venv
source .venv/bin/activate  # On macOS/Linux
```

```
## Environment Variables

- `DATABASE_URL` - PostgreSQL connection string
- `REDIS_URL` - Redis connection string
- `SECRET_KEY` - JWT secret key
- `IGDB_CLIENT_ID` - IGDB API client ID
- `IGDB_CLIENT_SECRET` - IGDB API client secret
- `AWS_ACCESS_KEY_ID` - AWS credentials
- `AWS_SECRET_ACCESS_KEY` - AWS credentials
- `AWS_REGION` - AWS region
```
