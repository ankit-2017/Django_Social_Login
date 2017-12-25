# Google Login in Django

install social_django app in your system
Run following command in cmd or terminal
## Installation
#### **pip install social-auth-app-django**

After installing app create a django project open settings.py file then add app in INSTALLED APP

### INSATALLED_APPS = [

    'login_app',    <-- this app you will create in your project 
    'social_django',     <--  installed app
]

Now apply migration 
manage.py migrate

It'll migrate installed app (social_django) in our project
## Configuration
Add this line at the end of **MIDDLEWARE_CLASSES**

MIDDLEWARE_CLASSES = [

    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.auth.middleware.SessionAuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',

    'social_django.middleware.SocialAuthExceptionMiddleware',  # <--
]


Add following last two lines of _social_django_ context processor
### TEMPLATES = [

    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',

                'social_django.context_processors.backends',  # <--
                'social_django.context_processors.login_redirect' # <--
            ],
        },
    },
]


Add following social provider in your **AUTHENTICATION_BACKENDS**

### AUTHENTICATION_BACKENDS = (

    'social_core.backends.github.GithubOAuth2',
    'social_core.backends.twitter.TwitterOAuth',
    'social_core.backends.facebook.FacebookOAuth2',
    'social_core.backends.google.GoogleOAuth2',
    

    'django.contrib.auth.backends.ModelBackend',
)

Create google client ID and Secret key 
Add Google Client ID and Source key

    SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = 'your google app CLIENT ID'  # CLIENT ID
    SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = 'your Google app secret key'
    
Define where page will redirect after successful authentication

    LOGIN_REDIRECT_URL = '/home/'
    
In urls.py add social django app urls

#### **urlpatterns** = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', social_login),
    url(r'^home/$',home),
    url(r'^oauth/', include('social_django.urls', namespace='social')),  #<--
    
    ---other urls---
]


Create a html page with a link to redirect to google authentication page
in social_login.html

    <a  href="{% url 'social:begin' 'google-oauth2' %}">GOOGLE LOGIN</a>
    
Now create home.html and add following lines

    <h2>
    WELCOME MR. <b>{{user.username}}</b>
    </h2><br>
    

In views.py create function

    from django.shortcuts import render
    from django.http import *
    from django.contrib import auth
    
    def social_login(request):
    	return render(request, 'social_login.html')
    
    def home(request):  #<--
    	return render(request, 'home.html')


    
    
    
    



