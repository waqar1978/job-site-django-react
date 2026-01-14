# Job Portal Backend

A production-ready, scalable RESTful API built with Django REST Framework for a comprehensive job portal platform. This backend system demonstrates senior-level Python backend engineering skills including custom authentication, complex business logic, recommendation algorithms, and enterprise-grade architecture.

## 🏗️ Architecture Overview

### System Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           CLIENT LAYER                                  │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│    ┌──────────────┐              ┌──────────────┐                       │
│    │ Web Browser  │              │ Mobile App   │                       │
│    └──────┬───────┘              └──────┬───────┘                       │
│           │                             │                               │
│           └──────────┬──────────────────┘                               │
│                      │                                                  │
└──────────────────────┼──────────────────────────────────────────────────┘
                       │
                       ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                        API GATEWAY LAYER                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│              ┌──────────────────────────┐                               │
│              │  Nginx/Reverse Proxy     │                               │
│              └──────────┬───────────────┘                               │
│                         │                                               │
└─────────────────────────┼───────────────────────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                        APPLICATION LAYER                                │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│    ┌──────────────────────────────────────────────────────┐             │
│    │         Django REST Framework                        │             │
│    │                                                      │             │
│    │  ┌──────────────────┐  ┌──────────────────────────┐  │             │
│    │  │ JWT              │  │ CORS/WhiteNoise          │  │             │
│    │  │ Authentication   │  │ Middleware               │  │             │
│    │  └──────────────────┘  └──────────────────────────┘  │             │
│    │                                                      │             │
│    └──────────────┬───────────────────────────────────────┘             │
│                   │                                                     │
└───────────────────┼─────────────────────────────────────────────────────┘
                    │
                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                      BUSINESS LOGIC LAYER                               │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                   │
│  │   Accounts   │  │   Profiles   │  │     Jobs     │                   │
│  │   Module     │  │   Module     │  │   Module     │                   │
│  └──────┬───────┘  └──────┬───────┘  └──────────────┘                   │
│         │                 │                                             │
│         │                 │                                             │
│  ┌──────┴───────┐  ┌──────┴────────┐                                    │
│  │ Assessments  │  │ Recommendation│                                    │
│  │   Module     │  │    Engine     │                                    │
│  └──────────────┘  └───────────────┘                                    │
│                                                                         │
└───────────┬───────────┬───────────┬───────────┬─────────────────────────┘
            │           │           │           │
            ▼           ▼           ▼           ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                           DATA LAYER                                    │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                   │
│  │ PostgreSQL/  │  │ Media        │  │ Static       │                   │
│  │ SQLite       │  │ Storage      │  │ Files        │                   │
│  └──────────────┘  └──────┬───────┘  └──────────────┘                   │
│                           │                                             │
└───────────────────────────┼─────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                       EXTERNAL SERVICES                                 │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐              ┌──────────────┐                         │
│  │ SMTP Email   │              │ Cloud        │                         │
│  │ Service      │              │ Storage      │                         │
│  └──────────────┘              └──────────────┘                         │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Application Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                    DJANGO PROJECT STRUCTURE                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐     ┌──────────────┐    ┌──────────────┐              │
│  │ Settings &   │     │ URL Routing  │    │ WSGI/ASGI    │              │
│  │ Config       │     │              │    │              │              │
│  └──────┬───────┘     └──────┬───────┘    └──────────────┘              │
│         │                    │                                          │
│         └──────────┬─────────┘                                          │
│                    │                                                    │
└────────────────────┼────────────────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          CORE APPS                                      │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────┐       │
│  │  Accounts App                                                │       │
│  │  • Custom User Model                                         │       │
│  │  • Authentication                                            │       │
│  └──────────────────────────────────────────────────────────────┘       │
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────┐       │
│  │  Profiles App                                                │       │
│  │  • User Profiles                                             │       │
│  │  • Skills & Experience                                       │       │
│  └──────────────────────────────────────────────────────────────┘       │
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────┐       │
│  │  Jobs App                                                    │       │
│  │  • Job Postings                                              │       │
│  │  • Job Management                                            │       │
│  └──────────────────────────────────────────────────────────────┘       │
│                                                                         │
│  ┌──────────────────────────────────────────────────────────────┐       │
│  │  Assessments App                                             │       │
│  │  • Technical Tests                                           │       │
│  │  • Q&A System                                                │       │
│  └──────────────────────────────────────────────────────────────┘       │
│                                                                         │
└────────────────────┬────────────────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                      SUPPORTING MODULES                                 │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│  ┌──────────────┐    ┌──────────────┐    ┌──────────────┐               │
│  │ Helper       │    │ Django Admin │    │ Database     │               │
│  │ Functions    │    │ Custom Views │    │ Migrations   │               │
│  │ • Recommend  │    │              │    │              │               │
│  │   Algorithm  │    │              │    │              │               │
│  └──────────────┘    └──────────────┘    └──────────────┘               │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```


## 🚀 Tech Stack

### Core Framework
- **Django 3.1.7** - High-level Python web framework
- **Django REST Framework 3.12.2** - Powerful toolkit for building Web APIs
- **Python 3.9.0** - Programming language

### Authentication & Security
- **Djoser 2.1.0** - REST implementation of Django authentication
- **djangorestframework-simplejwt 4.6.0** - JSON Web Token authentication
- **django-cors-headers 3.7.0** - Handling Cross-Origin Resource Sharing
- **social-auth-app-django 4.0.0** - Social authentication support

### Database
- **SQLite3** - Development database
- **PostgreSQL** (psycopg2-binary 2.8.6) - Production database support

### Deployment & Server
- **Gunicorn 20.1.0** - Python WSGI HTTP Server
- **WhiteNoise 5.2.0** - Static file serving for Django

### Additional Libraries
- **Pillow 8.1.0** - Image processing
- **xlrd** - Excel file reading for data import
- **django-admin-list-filter-dropdown 1.0.3** - Enhanced admin filters

## 📁 Project Structure

```
backend/
├── accounts/                 # Custom user authentication
│   ├── models.py            # Custom UserAccount model
│   ├── serializers.py       # User serialization
│   ├── views.py             # Authentication views
│   └── migrations/           # Database migrations
│
├── profiles/                 # User profiles and related data
│   ├── models.py            # Profile, Experience, Education, etc.
│   ├── serializers.py       # Profile serializers
│   ├── views.py             # Profile CRUD operations
│   ├── urls.py              # Profile endpoints
│   ├── admin.py             # Custom admin configuration
│   └── management/          # Custom management commands
│       └── commands/
│           └── insert_dev.py  # Data seeding command
│
├── jobs/                     # Job posting management
│   ├── models.py            # Job and Skills models
│   ├── serializers.py       # Job serializers
│   ├── views.py             # Job CRUD operations
│   ├── urls.py              # Job endpoints
│   └── admin.py             # Job admin configuration
│
├── assessments/              # Technical assessments
│   ├── models.py            # Questions, Answers, UserAnswers
│   ├── serializers.py       # Assessment serializers
│   ├── views.py             # Assessment views
│   └── urls.py              # Assessment endpoints
│
├── helpers/                  # Utility functions
│   └── recommend.py         # Recommendation algorithm
│
├── job_portal/              # Django project configuration
│   ├── settings.py          # Project settings
│   ├── urls.py              # Root URL configuration
│   ├── wsgi.py              # WSGI configuration
│   └── asgi.py              # ASGI configuration
│
├── manage.py                # Django management script
├── requirements.txt         # Python dependencies
├── runtime.txt              # Python version specification
├── Procfile                 # Heroku deployment configuration
└── db.sqlite3               # Development database
```

## 🔑 Key Features

### 1. Custom User Authentication System
- **Custom User Model**: Extended `AbstractBaseUser` with email-based authentication
- **Custom User Manager**: Implemented `BaseUserManager` with proper user creation logic
- **JWT Authentication**: Token-based authentication with refresh tokens
- **Password Management**: Secure password hashing and reset functionality
- **Account Activation**: Email-based account activation flow

### 2. Comprehensive User Profile Management
- **Profile Information**: Personal details, bio, contact information
- **Experience Tracking**: Years of experience, remote experience, English proficiency
- **Education History**: Degree, college, dates
- **Skills Management**: Skill ratings (1-10 scale) with validation
- **Availability Status**: Availability type and ready-to-start timeline
- **Role & Salary**: Preferred role and current salary information
- **Company Profiles**: For employers to manage company information

### 3. Advanced Job Management System
- **Job Postings**: Create, read, update, delete job listings
- **Job Skills**: Associate required skills with ratings for each job
- **Job Filtering**: Filter jobs by various criteria
- **Company Information**: Track company size and hiring needs

### 4. Intelligent Recommendation Engine
- **Algorithm-Based Matching**: Custom scoring algorithm for matching developers to jobs
- **Skill-Based Scoring**: Weighted matching based on skill ratings
- **Availability Matching**: Considers availability type in scoring
- **Ranked Results**: Returns sorted list of recommended candidates

### 5. Technical Assessment System
- **Question Management**: Create and manage assessment questions
- **Multiple Choice Answers**: Support for multiple answer options
- **User Answer Tracking**: Track user responses to assessments
- **Sequential Question Flow**: Navigate through questions sequentially

### 6. Django Admin Customization
- **Custom Admin Classes**: Tailored admin interfaces for each model
- **Advanced Filtering**: Dropdown filters for better data management
- **List Display Customization**: Optimized admin list views
- **Pagination**: Efficient handling of large datasets

## 🔐 Security Features

- **JWT Token Authentication**: Secure token-based authentication
- **CORS Configuration**: Properly configured Cross-Origin Resource Sharing
- **Password Validation**: Django's built-in password validators
- **CSRF Protection**: Cross-Site Request Forgery protection
- **SQL Injection Prevention**: Django ORM prevents SQL injection
- **XSS Protection**: Django's template system prevents XSS attacks
- **File Upload Permissions**: Restricted file upload permissions

## 📡 API Endpoints

### Authentication Endpoints (`/auth/`)
- `POST /auth/users/` - User registration
- `POST /auth/jwt/create/` - Login (get JWT tokens)
- `POST /auth/jwt/refresh/` - Refresh access token
- `POST /auth/users/set_password/` - Change password
- `POST /auth/users/reset_password/` - Request password reset
- `POST /auth/users/reset_password_confirm/` - Confirm password reset

### User Endpoints (`/user/`)
- `GET /user/list` - List all users
- `GET /user/list/<id>` - Get single user
- `POST /user/recommend/list` - Get recommended users for a job

### Profile Endpoints (`/user/`)
- `GET|POST /user/profile` - List/Create user profile
- `GET|PUT|DELETE /user/profile/<id>` - Get/Update/Delete profile
- `GET /user/profile/<id>/user` - Get profile by user ID

### Skills Endpoints (`/user/`)
- `GET|POST /user/user_skills` - List/Create user skills
- `GET /user/user_skills/list` - List all user skills
- `GET /user/user_skills/list/<id>` - Get skills by user ID

### Experience, Education, Availability, Role Endpoints (`/user/`)
- Similar CRUD operations for Experience, Education, Availability, and RoleSalary

### Job Endpoints (`/job/`)
- `GET|POST /job/` - List/Create jobs
- `GET|PUT|DELETE /job/<id>` - Get/Update/Delete job
- `GET /job/<id>/single` - Get single job detail
- `GET /job/list` - List all jobs
- `GET /job/last` - Get last added job
- `GET|POST /job/skills` - List/Create job skills
- `GET /job/skills/<id>` - Get skills for a job

### Assessment Endpoints (`/question/`)
- `GET /question/first` - Get first question
- `GET /question/next/<id>` - Get next question
- `GET|POST /question/submit` - Submit answer
- `GET /question/answers` - Get all answers
- `GET /question/all` - Get all questions

## 🛠️ Installation & Setup

### Prerequisites
- Python 3.9.0 or higher
- pip (Python package manager)
- Virtual environment (recommended)
- PostgreSQL (for production) or SQLite (for development)

### Step 1: Clone the Repository
```bash
git clone <repository-url>
cd django-react-job-site-/backend
```

### Step 2: Create Virtual Environment
```bash
python -m venv venv

# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate
```

### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

### Step 4: Configure Environment Variables
Create a `.env` file in the backend directory:
```env
SECRET_KEY=your-secret-key-here
DEBUG=True
DATABASE_NAME=job_portal_db
DATABASE_USER=your_db_user
DATABASE_PASSWORD=your_db_password
DATABASE_HOST=localhost
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-email-password
```

### Step 5: Run Migrations
```bash
python manage.py makemigrations
python manage.py migrate
```

### Step 6: Create Superuser
```bash
python manage.py createsuperuser
```

### Step 7: Load Sample Data (Optional)
```bash
python manage.py insert_dev
```

### Step 8: Run Development Server
```bash
python manage.py runserver
```

The API will be available at `http://localhost:8000`

## 🧪 Testing

### Run Tests
```bash
python manage.py test
```

### Run Specific App Tests
```bash
python manage.py test accounts
python manage.py test profiles
python manage.py test jobs
python manage.py test assessments
```

## 📊 Database Management

### Create Migrations
```bash
python manage.py makemigrations <app_name>
```

### Apply Migrations
```bash
python manage.py migrate
```

### Rollback Migrations
```bash
python manage.py migrate <app_name> <migration_number>
```

## 🚀 Deployment

### Heroku Deployment

1. **Install Heroku CLI**
```bash
heroku login
```

2. **Create Heroku App**
```bash
heroku create your-app-name
```

3. **Set Environment Variables**
```bash
heroku config:set SECRET_KEY=your-secret-key
heroku config:set DEBUG=False
heroku config:set ALLOWED_HOSTS=your-app-name.herokuapp.com
```

4. **Deploy**
```bash
git push heroku main
heroku run python manage.py migrate
heroku run python manage.py createsuperuser
```

### Production Settings Checklist
- [ ] Set `DEBUG = False`
- [ ] Configure `ALLOWED_HOSTS`
- [ ] Set secure `SECRET_KEY`
- [ ] Configure PostgreSQL database
- [ ] Set up static file serving (WhiteNoise)
- [ ] Configure media file storage (AWS S3 recommended)
- [ ] Set up email service (SendGrid, AWS SES)
- [ ] Configure CORS for production domain
- [ ] Set up SSL/HTTPS
- [ ] Configure logging
- [ ] Set up monitoring and error tracking

## 🔧 Configuration

### Settings Overview

The project uses Django's settings module with the following key configurations:

- **Database**: Configurable for SQLite (dev) or PostgreSQL (production)
- **Authentication**: JWT-based with configurable token lifetimes
- **CORS**: Whitelist-based CORS configuration
- **Static Files**: WhiteNoise for static file serving
- **Media Files**: Configurable media root and URL
- **Email**: SMTP configuration for email services

### Custom User Model

The project uses a custom user model (`accounts.UserAccount`) with:
- Email as the username field
- Custom user type field
- Extended user manager for user creation

## 📈 Performance Optimization

### Database Optimization
- Use `select_related()` for foreign key relationships
- Use `prefetch_related()` for many-to-many relationships
- Add database indexes for frequently queried fields
- Use database connection pooling

### Query Optimization
- Implement pagination for list endpoints
- Use `only()` and `defer()` to limit fields
- Cache frequently accessed data
- Use `annotate()` and `aggregate()` for complex queries

### Caching Strategy
```python
# Example caching implementation
from django.core.cache import cache

def get_recommend_users(job_id):
    cache_key = f'recommend_users_{job_id}'
    cached_result = cache.get(cache_key)
    if cached_result:
        return cached_result
    # ... compute result
    cache.set(cache_key, result, timeout=3600)
    return result
```

## 🐛 Troubleshooting

### Common Issues

**Issue**: `ModuleNotFoundError` or import errors
- **Solution**: Ensure virtual environment is activated and dependencies are installed

**Issue**: Database connection errors
- **Solution**: Check database credentials and ensure database server is running

**Issue**: CORS errors in frontend
- **Solution**: Add frontend URL to `CORS_ORIGIN_WHITELIST` in settings.py

**Issue**: Static files not loading
- **Solution**: Run `python manage.py collectstatic` and ensure WhiteNoise is configured

## 📝 Code Quality

### Code Style
- Follow PEP 8 Python style guide
- Use type hints where appropriate
- Write docstrings for functions and classes
- Follow Django best practices

### Linting
```bash
# Install linting tools
pip install flake8 black isort

# Run linting
flake8 .
black .
isort .
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License.

## 👨‍💻 Author

**Senior Backend Engineer**
- Expertise in Django, Django REST Framework, and Python
- Specialized in RESTful API design and architecture
- Experience with authentication systems and security best practices
- Proficient in database design and optimization
- Skilled in algorithm design and business logic implementation

## 🙏 Acknowledgments

- Django REST Framework team for the excellent framework
- Djoser contributors for authentication utilities
- All open-source contributors whose packages made this project possible

---

**Built with ❤️ using Django REST Framework**

