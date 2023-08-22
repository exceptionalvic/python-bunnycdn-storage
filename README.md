# bunnycdn-storage

This package provides Bunny.net file storage for Django.
An improved and working version. Thanks to Will Meyers' [django-bunny-storage](https://github.com/willmeyers/django-bunny-storage).

## Package Installation

`bunnycdn-storage` requires Python >= 3.7 and Django >= 3.0

```bash
pip install bunnycdn-storage
```

## Package Configuration

Details to configure Bunny.net Storage.

To use:

1. Add `bunnycdn_storage` to your `INSTALLED_APPS` in `settings.py` file

```python
INSTALLED_APPS = [
    ...
    'bunnycdn_storage',
    ...
]
```

2. Add `BUNNY_USERNAME` and `BUNNY_PASSWORD` to your settings.

```python
BUNNY_USERNAME = 'your_bunny_username'

BUNNY_PASSWORD = 'your_bunny_password'

# This is optional
BUNNY_REGION = 'de'
```

The above settings must match the storage zone and password of your Bunny.net account. To find Storage zone *Username* and *Password*, open the FTP & API Access under Storage in your Bunny.net dashboard.

Note: You must include `BUNNY_REGION` if you choose another region other than the default Falkenstein region, **DE**. 

3. Change the MEDIA_URL in `settings.py` file.

```python
MEDIA_URL = 'https://your_zone.b-cdn.net/' # This is your Pull Zone linked hostname
```

The `MEDIA_URL` corresponds to the linked Pull Zone you setup in the Bunny.net dashboard.

4. Change the default file storage in `settings.py` file.

```python
DEFAULT_FILE_STORAGE = 'bunnycdn_storage.storage.BunnyCDNStorage'
```

#### Displaying Media in Template

This setup uses media url context processor to serve media. Refer to the documentation in [Django](https://docs.djangoproject.com/en/dev/ref/settings/#std:setting-MEDIA_URL) for more details.

5. Add `django.template.context_processors.media` in the `context_processors` option of TEMPLATES in `settings.py` file.

```python
...
'django.template.context_processors.media',
...
```

To load media properly without getting 404, use:

```html
<img src="{{ MEDIA_URL }}{{ your_model.file }}" />
```

That's it.