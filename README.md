# Blog Backend API 🚀

A modern, full-featured blog backend API built with **FastAPI**, featuring user authentication, post management, comments, file uploads, and search functionality.

## ✨ Features

- 🔐 **JWT Authentication** - Secure user registration and login
- 📝 **Post Management** - Create, read, update, delete blog posts
- 💬 **Comment System** - Users can comment on posts
- 📁 **File Uploads** - Image upload support for posts
- 🔍 **Search Functionality** - Search posts by title, content, or summary
- 📊 **Admin Features** - User management and content moderation
- 🚀 **Fast Performance** - Built with FastAPI for high performance
- 📚 **Auto Documentation** - Interactive API docs with Swagger UI

## 🛠️ Tech Stack

- **FastAPI** - Modern, fast web framework for building APIs
- **SQLAlchemy** - SQL toolkit and ORM
- **SQLite** - Lightweight database (easily switchable to PostgreSQL)
- **JWT** - JSON Web Tokens for authentication
- **Pydantic** - Data validation using Python type annotations
- **Uvicorn** - ASGI server for running the application

## 🚀 Quick Start

### Prerequisites

- Python 3.8+
- pip (Python package installer)

### Installation

1. **Clone the repository:**
```bash
git clone https://github.com/phungvannarich-kepler-aavn/blog-backend.git
cd blog-backend
```

2. **Create a virtual environment:**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies:**
```bash
pip install -r requirements.txt
```

4. **Run the application:**
```bash
python main.py
```

The API will be available at `http://localhost:8000`

## 📖 API Documentation

Once the server is running, you can access:

- **Interactive API docs**: http://localhost:8000/docs
- **ReDoc documentation**: http://localhost:8000/redoc
- **OpenAPI schema**: http://localhost:8000/openapi.json

## 🔗 API Endpoints

### Health Check
- `GET /health` - Health check endpoint for monitoring

### Authentication
- `POST /auth/register` - Register a new user
- `POST /auth/login` - Login user
- `GET /auth/me` - Get current user info

### Posts
- `GET /posts/` - Get all published posts (with pagination)
- `GET /posts/{slug}` - Get a specific post by slug
- `POST /posts/` - Create a new post (authenticated)
- `PUT /posts/{post_id}` - Update a post (authenticated, author only)
- `DELETE /posts/{post_id}` - Delete a post (authenticated, author only)

### Comments
- `GET /posts/{post_id}/comments` - Get comments for a post
- `POST /comments/` - Create a new comment (authenticated)

### File Uploads
- `POST /upload/` - Upload an image file (authenticated)

### Search
- `GET /search/?q=query` - Search posts by title, content, or summary

## 🔧 Configuration

### Environment Variables

Create a `.env` file in the root directory:

```env
SECRET_KEY=your-super-secret-key-here
DATABASE_URL=sqlite:///./blog.db
ACCESS_TOKEN_EXPIRE_MINUTES=30
UPLOAD_DIR=uploads
```

### Database

The application uses SQLite by default. To use PostgreSQL:

1. Install PostgreSQL dependencies:
```bash
pip install psycopg2-binary
```

2. Update the database URL in `main.py`:
```python
SQLALCHEMY_DATABASE_URL = "postgresql://user:password@localhost/blog_db"
```

## 🧪 Testing

### Using curl

1. **Register a user:**
```bash
curl -X POST "http://localhost:8000/auth/register" \
  -H "Content-Type: application/json" \
  -d '{"username": "testuser", "email": "test@example.com", "password": "testpass123"}'
```

2. **Login:**
```bash
curl -X POST "http://localhost:8000/auth/login?username=testuser&password=testpass123"
```

3. **Create a post:**
```bash
curl -X POST "http://localhost:8000/posts/" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title": "My First Post", "content": "This is the content of my first post!", "is_published": true}'
```

### Using the Interactive Docs

Visit http://localhost:8000/docs to use the built-in Swagger UI for testing all endpoints.

## 🏗️ Project Structure

```
blog-backend/
├── main.py              # Main FastAPI application
├── requirements.txt     # Python dependencies
├── README.md           # This file
├── .env                # Environment variables (create this)
└── uploads/            # Uploaded files directory (auto-created)
```

## 🔒 Security Features

- **Password Hashing** - Passwords are hashed using bcrypt
- **JWT Tokens** - Secure authentication with configurable expiration
- **CORS Protection** - Configured for frontend integration
- **Input Validation** - All inputs are validated using Pydantic models
- **File Type Validation** - Only image files are allowed for uploads

## 🚀 Deployment

### Using Docker

1. Create a `Dockerfile`:
```dockerfile
FROM python:3.9-slim

WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .
EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

2. Build and run:
```bash
docker build -t blog-backend .
docker run -p 8000:8000 blog-backend
```

### Using Heroku

1. Create a `Procfile`:
```
web: uvicorn main:app --host 0.0.0.0 --port $PORT
```

2. Deploy to Heroku following their standard process.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

Created by [phungvannarich-kepler-aavn](https://github.com/phungvannarich-kepler-aavn)

---

**Happy Blogging!** 🎉