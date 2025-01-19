# Django REST - Snippets

### Development steps

1. Create venv: ```python -m venv venv```
2. Activate venv: ```.\venv\Scripts\activate```
3. Install Django, Django REST and pygments module: ```python -m pip install django djangorestframework pygments```
4. Create template: ```django-admin startproject mysite```
5. Generate basic directory structure for app: ```python manage.py startapp snippets```
6. Add snippets to INSTALLED_APPS from settings
7. Create snippet model and serializers
8. Add views to list snippets
9. Create paths for url patterns
10. Render instances (test)
11. Make migrations from app: ```python manage.py makemigrations snippets```
12. Migrate changes from app: ```python manage.py migrate snippets```
13. Run Django shell: ```python manage.py shell```
14. Create snippet instances
15. Serialize instance and render data
16. Deserialize instance
17. Make requests to API (test) with httpie: ```pip install httpie```
18. Create requirements file and list modules: ```python -m pip freeze > requirements.txt```
19. Create user model, serializer and view
20. Create path for user model and api auth

### Step details
14. Create snippets instances with Django shell:
```python
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from rest_framework.renderers import JSONRenderer
from rest_framework.parsers import JSONParser

snippet = Snippet(code='foo = "bar"\n')
snippet.save()

snippet = Snippet(code='print("hello, world")\n')
snippet.save()
```

15. Serialize instance and render data into json:
```python
serializer = SnippetSerializer(snippet)
serializer.data

content = JSONRenderer().render(serializer.data)
content
```

16. Deserialize instance:
```python
# Parse a stream into Python native datatypes
import io

stream = io.BytesIO(content)
data = JSONParser().parse(stream)

# Restorenative datatypes into a object instance
serializer = SnippetSerializer(data=data)
serializer.is_valid()

serializer.validated_data
serializer.save()
```

17. Get list of snippets:
```http http://127.0.0.1:8000/snippets/ --unsorted```

Get particular snippet:
```http http://127.0.0.1:8000/snippets/1/ --unsorted```
