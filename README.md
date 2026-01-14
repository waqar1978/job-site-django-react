# Job Portal Platform

A full-stack job portal platform connecting developers with companies, built with Django REST Framework and React. This project demonstrates senior-level full-stack development skills including RESTful API design, custom authentication, recommendation algorithms, and modern frontend architecture.

## 🎯 Project Overview

This is a comprehensive job portal platform that enables:
- **Developers** to create profiles, showcase skills, and find job opportunities
- **Companies** to post jobs, search for candidates, and hire developers
- **Matching System** that intelligently matches developers to jobs based on skills and availability

## 🏗️ System Architecture

See detailed architecture diagrams in:
- **[Backend Architecture](./backend/README.md#-architecture-overview)** - Complete backend system architecture
- **[Frontend Architecture](./frontend/README.md#-architecture-overview)** - Complete frontend system architecture

## 🚀 Tech Stack

### Backend
- **Django 3.1.7** - High-level Python web framework
- **Django REST Framework 3.12.2** - RESTful API toolkit
- **Djoser** - Authentication system
- **JWT** - Token-based authentication
- **PostgreSQL/SQLite** - Database
- **Gunicorn** - WSGI HTTP Server

### Frontend
- **React 17.0.1** - UI library
- **Redux 4.0.5** - State management
- **React Router** - Routing
- **React Bootstrap** - UI components
- **Axios** - HTTP client

## 📁 Project Structure

```
django-react-job-site-/
├── backend/                 # Django REST API
│   ├── accounts/           # Custom user authentication
│   ├── profiles/           # User profiles and related data
│   ├── jobs/               # Job posting management
│   ├── assessments/        # Technical assessments
│   ├── helpers/            # Utility functions
│   ├── job_portal/         # Django project config
│   ├── requirements.txt    # Python dependencies
│   └── README.md           # Backend documentation
│
├── frontend/               # React SPA
│   ├── src/
│   │   ├── actions/        # Redux actions
│   │   ├── components/     # React components
│   │   ├── reducers/       # Redux reducers
│   │   ├── screens/        # Page components
│   │   └── store.js        # Redux store
│   ├── package.json        # Node dependencies
│   └── README.md           # Frontend documentation
│
└── README.md               # This file
```

## ✨ Key Features

### For Developers
- ✅ Create and manage comprehensive profiles
- ✅ Showcase skills with ratings
- ✅ Add work experience and education
- ✅ Set availability and preferred roles
- ✅ Browse and apply to jobs
- ✅ Take technical assessments
- ✅ Get matched with relevant jobs

### For Companies
- ✅ Post job listings with required skills
- ✅ Search and filter developers
- ✅ View developer profiles
- ✅ Get intelligent recommendations
- ✅ Manage company profile
- ✅ Track hiring needs

### Platform Features
- ✅ Custom JWT authentication system
- ✅ Intelligent recommendation algorithm
- ✅ Technical assessment system
- ✅ Real-time job matching
- ✅ Responsive design
- ✅ RESTful API architecture

## 🚀 Quick Start

### Prerequisites
- Python 3.9+
- Node.js 14+
- PostgreSQL (for production) or SQLite (for development)

### Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run migrations
python manage.py migrate

# Create superuser
python manage.py createsuperuser

# Run development server
python manage.py runserver
```

Backend API will be available at `http://localhost:8000`

### Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Start development server
npm start
```

Frontend will be available at `http://localhost:3000`

## 📚 Documentation

- **[Backend README](./backend/README.md)** - Complete backend documentation with API endpoints, architecture, and deployment guide
- **[Frontend README](./frontend/README.md)** - Complete frontend documentation with component structure, state management, and deployment guide


## 🎯 API Endpoints Overview

### Authentication
- `POST /auth/users/` - User registration
- `POST /auth/jwt/create/` - Login
- `POST /auth/jwt/refresh/` - Refresh token

### Users & Profiles
- `GET /user/list` - List users
- `GET|POST /user/profile` - Profile management
- `GET|POST /user/user_skills` - Skills management
- `GET|POST /user/experience` - Experience management
- `GET|POST /user/education` - Education management

### Jobs
- `GET|POST /job/` - Job management
- `GET /job/list` - List all jobs
- `GET|POST /job/skills` - Job skills

### Recommendations
- `POST /user/recommend/list` - Get recommended users

### Assessments
- `GET /question/first` - Get first question
- `GET /question/next/<id>` - Get next question
- `POST /question/submit` - Submit answer

See [Backend README](./backend/README.md) for complete API documentation.

## 🧪 Testing

### Backend Tests
```bash
cd backend
python manage.py test
```

### Frontend Tests
```bash
cd frontend
npm test
```

## 🚀 Deployment

### Backend Deployment (Heroku)
```bash
cd backend
heroku create your-app-name
git push heroku main
heroku run python manage.py migrate
```

### Frontend Deployment
```bash
cd frontend
npm run build
# Deploy build/ folder to Netlify, Vercel, or AWS S3
```

See individual README files for detailed deployment instructions.

## 🔧 Environment Variables

### Backend (.env)
```env
SECRET_KEY=your-secret-key
DEBUG=False
DATABASE_URL=postgresql://user:password@localhost/dbname
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-password
```

### Frontend (.env)
```env
REACT_APP_API_URL=http://localhost:8000
REACT_APP_ENV=development
```

## 📊 Database Schema

The platform uses a relational database with the following main entities:
- **UserAccount** - Custom user model
- **Profile** - User profile information
- **Job** - Job postings
- **Skills** - Job and user skills
- **Experience** - Work experience
- **Education** - Educational background
- **Assessments** - Questions and answers

See [Backend README](./backend/README.md) for detailed database schema.

## 🎨 UI/UX Features

- **Responsive Design** - Works on all devices
- **Modern UI** - Clean and intuitive interface
- **Form Validation** - Client and server-side validation
- **Error Handling** - User-friendly error messages
- **Loading States** - Smooth loading indicators
- **Toast Notifications** - Alert system for user feedback

## 🔒 Security Features

- JWT token-based authentication
- Password hashing and validation
- CORS configuration
- CSRF protection
- SQL injection prevention
- XSS protection
- Secure file uploads

## 📈 Performance Optimizations

### Backend
- Database query optimization
- Caching strategies
- Connection pooling
- Efficient serialization

### Frontend
- Code splitting
- Lazy loading
- Component memoization
- Bundle optimization
- Image optimization

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License.

## 👨‍💻 Author

**Senior Full-Stack Developer**

### Backend Expertise
- Django & Django REST Framework
- Custom authentication systems
- RESTful API design
- Database design and optimization
- Algorithm implementation
- Security best practices

### Frontend Expertise
- React & Redux
- Component architecture
- State management
- Modern JavaScript (ES6+)
- Responsive design
- Performance optimization

## 🙏 Acknowledgments

- Django and Django REST Framework teams
- React and Redux communities
- All open-source contributors
- Bootstrap team for UI components

## 📞 Contact & Support

For questions, issues, or contributions, please open an issue on GitHub.

---

**Built with ❤️ using Django REST Framework and React**

**Status**: ✅ Production Ready

**Last Updated**: 2024

