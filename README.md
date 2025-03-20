# Django Authentication System

A robust Django backend authentication system with JWT token support, created for managing users with different roles (doctor, patient, admin).

## Features

- User registration and login
- Token-based authentication
- Password hashing and security
- Role-based user management (doctor, patient, admin)
- Custom user model
- Django admin integration
- RESTful API endpoints

## Prerequisites

- Python 3.8 or higher
- MySQL Server
- pip (Python package manager)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/your-repository-name.git
cd your-repository-name
```

2. Create a virtual environment:
```bash
python -m venv venv

# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create a MySQL database:
```bash
# Login to MySQL
mysql -u root -p

# Create the database
CREATE DATABASE your_database_name CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

# Create a user for the database (optional but recommended)
CREATE USER 'your_database_user'@'localhost' IDENTIFIED BY 'your_database_password';

# Grant privileges to the user
GRANT ALL PRIVILEGES ON your_database_name.* TO 'your_database_user'@'localhost';

# Apply changes
FLUSH PRIVILEGES;

# Exit MySQL
EXIT;
```

5. Configure database settings:

Update the `DATABASES` configuration in `auth_project/settings.py`:
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'your_database_name',
        'USER': 'your_database_user',
        'PASSWORD': 'your_database_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

6. Run migrations:
```bash
python manage.py makemigrations
python manage.py migrate
```

7. Create a superuser:
```bash
python manage.py createsuperuser
```

8. Start the development server:
```bash
python manage.py runserver
```

## API Endpoints

### Registration
```
POST /api/users/register/
```
Request body:
```json
{
  "email": "user@example.com",
  "password": "secure_password",
  "password_confirm": "secure_password",
  "first_name": "John",
  "last_name": "Doe",
  "role": "patient",
  "bio": "Patient bio here" 
}
```

### Login
```
POST /api/users/login/
```
Request body:
```json
{
  "email": "user@example.com",
  "password": "secure_password"
}
```
Response:
```json
{
  "user": {
    "id": 1,
    "email": "user@example.com",
    "first_name": "John",
    "last_name": "Doe",
    "role": "patient",
    "profile_picture": null,
    "bio": "Patient bio here"
  },
  "token": "9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
}
```

### Get User Details (Authenticated)
```
GET /api/users/me/
```
Headers:
```
Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b
```



### Get user details (authenticate with token)
```bash
curl -X GET http://127.0.0.1:8000/api/users/me/ \
  -H "Authorization: Token YOUR_AUTH_TOKEN_HERE"
```

## Admin Interface

Access the Django admin interface at `http://127.0.0.1:8000/admin/` using your superuser credentials.

## Project Structure

```
auth_project/
├── auth_project/         # Main project configuration
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py       # Project settings
│   ├── urls.py           # Main URL configuration
│   └── wsgi.py
│
├── users/                # Users app
│   ├── __init__.py
│   ├── admin.py          # Admin configuration
│   ├── migrations/       # Database migrations
│   ├── models.py         # User model
│   ├── serializers.py    # API serializers
│   ├── urls.py           # API endpoints
│   └── views.py          # API views
│
├── manage.py             # Django management script
├── requirements.txt      # Project dependencies
└── README.md             # Project documentation
```

## Security Considerations

- Passwords are securely hashed using Django's authentication system
- Token-based authentication for API access
- CSRF protection for form submissions
- Input validation and serialization
