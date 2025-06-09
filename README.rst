This fork
=========

TinyMCE license was changed from MIT in 6.x to dual license (commercial and GPL) in 7.x.
As such the upgrades done by jazzband to the original repository of django-tinymce are
scarcely usable for most commercial projects.

This repository forks the original one including fixes for Django 5.2 support and newer
version of Python but replaces TinyMCE with the latest 6.8.6 version released.

There won't be any more releases of TinyMCE 6.x but for sake of completeness the
upgrade process was:

1. download latest version (6.8.6 at https://download.tiny.cloud/tinymce/community/tinymce_6.8.6.zip)
2. replace the `tinymce/static/tinymce` directory with the contents of the zip file
3. download language packs from https://download.tiny.cloud/tinymce/community/languagepacks/6/langs.zip , unzip the file into `tinymce/static/tinymce/langs`
4. run terser on all JS files to remove sourceMappingURL and comments:
```
cd tinymce/static/tinymce
for file in `fdfind .js`; do terser "$file" -o "${file%.js}.js" --comments false --source-map "includeSources=false"; done
```

This DOES remove the version comment from both TinyMCE and its plugins, however what version it's being uses
should be clear from the `pyproject.toml` file since it mentions `branch =  tinymce_6.8.6`).
According to Snyk, this version doesn't have any direct vulnerabilities (...for now):

https://security.snyk.io/package/npm/tinymce


django-tinymce
==============

**django-tinymce** is a Django application that contains a widget to render a form field as a TinyMCE editor.

It supports Python 3.9+ and Django 4.2 to 5.2. Using TinyMCE 6.8.4.

.. image:: https://jazzband.co/static/img/badge.svg
        :target: https://jazzband.co/
        :alt: Jazzband

.. image:: https://img.shields.io/pypi/v/django-tinymce.svg
        :target: https://pypi.python.org/pypi/django-tinymce

.. image:: https://img.shields.io/pypi/pyversions/django-tinymce.svg
        :target: https://pypi.python.org/pypi/django-tinymce

.. image:: https://img.shields.io/pypi/djversions/django-tinymce.svg
        :target: https://pypi.org/project/django-tinymce/

.. image:: https://img.shields.io/pypi/dm/django-tinymce.svg
        :target: https://pypi.python.org/pypi/django-tinymce

.. image:: https://github.com/jazzband/django-tinymce/workflows/Test/badge.svg
   :target: https://github.com/jazzband/django-tinymce/actions
   :alt: GitHub Actions

.. image:: https://codecov.io/gh/jazzband/django-tinymce/branch/master/graph/badge.svg
   :target: https://codecov.io/gh/jazzband/django-tinymce
   :alt: Code coverage


Quickstart
==========

Install django-tinymce:

.. code-block:: bash

    $ pip install django-tinymce

Add tinymce to INSTALLED_APPS in settings.py for your project:

.. code-block:: python

    INSTALLED_APPS = (
        ...
        'tinymce',
    )

Add tinymce.urls to urls.py for your project:

.. code-block:: python

    urlpatterns = [
        ...
        path('tinymce/', include('tinymce.urls')),
    ]

In your code:

.. code-block:: python

    from django.db import models
    from tinymce.models import HTMLField

    class MyModel(models.Model):
        ...
        content = HTMLField()

**django-tinymce** uses staticfiles so everything should work as expected, different use cases (like using widget instead of HTMLField) and other stuff is available in documentation.

Documentation
=============

https://django-tinymce.readthedocs.org/

Support and updates
===================

Use github issues https://github.com/jazzband/django-tinymce/issues

License
=======

Originally written by Joost Cassee.

This program is licensed under the MIT License (see LICENSE.txt)
