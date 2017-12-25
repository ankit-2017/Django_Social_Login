# Google Login in Django

install social_django app in your system
Run following command in cmd or terminal

   ### **_pip install social_django_**


After installing app create a django project open settings.py file then add app in INSTALLED APP

### INSATALLED_APPS = [
'''
[comment]: # (....some app......,)

**'login_app'**,   <!--- this app you will create in your project --->
**'social_django'**,   <!--- <--  installed app --->
'''  

]

Now apply migartion 
manage.py migrate

It'll migrate installed app (social_django) in our project



