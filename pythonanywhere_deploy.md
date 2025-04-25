# Deploying to PythonAnywhere

This guide walks through deploying this Django portfolio project to PythonAnywhere.

## 1. Sign up and Log in to PythonAnywhere

- Create an account at [PythonAnywhere](https://www.pythonanywhere.com/) if you don't have one
- Log in to your account

## 2. Set up a Web App

1. Go to the Web tab
2. Click "Add a new web app"
3. Choose "Manual configuration"
4. Select Python version (Python 3.10 or 3.11 recommended)
5. Click Next

## 3. Clone the Repository

1. Open a Bash console from the Dashboard
2. Clone your repository:
   ```
   git clone https://github.com/VickyVignesh2002/portfolio_2025.git
   ```

## 4. Set up a Virtual Environment

1. In the Bash console, create a virtual environment:
   ```
   cd ~/portfolio_2025
   python -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```

## 5. Configure the Web App

1. Go back to the Web tab
2. In the "Code" section:
   - Set "Source code" to `/home/yourusername/portfolio_2025`
   - Set "Working directory" to `/home/yourusername/portfolio_2025`
   - Set "WSGI configuration file" - click on the link to edit it

3. Modify the WSGI file:
   - Delete all the sample code
   - Add the following (replace `yourusername` with your PythonAnywhere username):

   ```python
   import os
   import sys

   # Add your project directory to the sys.path
   path = '/home/yourusername/portfolio_2025'
   if path not in sys.path:
       sys.path.insert(0, path)

   # Set environment variable to tell Django where your settings.py is
   os.environ['DJANGO_SETTINGS_MODULE'] = 'personal_portfolio.settings'

   # Serve Django via WSGI
   from django.core.wsgi import get_wsgi_application
   application = get_wsgi_application()
   ```

4. In the "Virtualenv" section:
   - Enter the path to your virtualenv: `/home/yourusername/portfolio_2025/venv`

5. In the "Static files" section, add:
   - URL: `/static/`
   - Path: `/home/yourusername/portfolio_2025/static`
   
   And:
   - URL: `/media/`
   - Path: `/home/yourusername/portfolio_2025/media`

## 6. Update settings.py

In your local_settings.py file (that won't be used in production):
- Keep DEBUG = True
- Keep ALLOWED_HOSTS = []

In your main settings.py, make sure:
- DEBUG = False
- ALLOWED_HOSTS includes your PythonAnywhere domain: `['yourusername.pythonanywhere.com']`

## 7. Database and Static Files Setup

1. In the Bash console:
   ```
   cd ~/portfolio_2025
   python manage.py migrate
   python manage.py collectstatic
   ```

2. Create a superuser:
   ```
   python manage.py createsuperuser
   ```

## 8. Reload the Web App

Go back to the Web tab and click the "Reload" button for your web app.

Your portfolio site should now be live at: `https://yourusername.pythonanywhere.com`