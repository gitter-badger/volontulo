# volontulo

[![Join the chat at https://gitter.im/CodeForPoznan/volontulo](https://badges.gitter.im/CodeForPoznan/volontulo.svg)](https://gitter.im/CodeForPoznan/volontulo?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[![Join the chat at https://gitter.im/stxnext-csr/volontulo](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/stxnext-csr/volontulo?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://travis-ci.org/stxnext-csr/volontulo.svg)](https://travis-ci.org/stxnext-csr/volontulo)
[![codecov.io](http://codecov.io/github/stxnext-csr/volontulo/coverage.svg?branch=master)](http://codecov.io/github/stxnext-csr/volontulo?branch=master)

![Volontulo logo](/apps/volontulo/frontend/img/volo_logo.png)

Web portal for collaboration of community volunteers with organizations and institutions. 

## Semi-automated Project Set Up

Install system dependecies
```
sudo bin/install_dependencies
```
Setup virtualenv, python packages, run migration and gulp.
```
bin/setup
```
Activate virtualenv.
```
source env/bin/activate
```
Django commands
```
python manage.py COMMAND --settings=volontulo_org.settings.dev
```

## Manual Project Set Up

Usage of virtualenv is recommended. Assuming you use Virtualenvwrapper:
```
mkvirtualenv --no-site-packages venv_name
```
To install project dependencies use pip and choose the correct file (production, development, etc.)
```
pip install -r requirements/dev.txt
```

Copy the Local Configuration file:
```
cp etc/local_config.yaml.sample local_config.yaml
vim local_config.yaml
```

Fill the Local Configuration Values.
To generate "secret_key", you can use
```head -c 64 /dev/urandom | base64 -w 0```
For Windows users may be used simple:
```
python -c "import uuid; print str(uuid.uuid4()).replace('-', '')"
```

If the site is supposed to be served under different domain than volontulo.org or volontuloapp.org
and you are not in development environment, fill the "allowed_host" value. Otherwise
it can be left blank.

### Gulp Instalation

Gulp is used to prepare and serve all static files into `/apps/volontulo/static/volontulo` so Django can use them
```
cd /apps/volontulo
npm install
```
Windows can have problems with unix paths, so it is practical to install Gulp globally (with `sudo` on linux)
```
npm install -g gulp
```
### Using Gulp
In development
```
gulp watch
```
Otherwise
```
gulp build
```
To convert svg icons to base64 format that ultimately is compiled to CSS, use:
```
gulp build_icons
```
Icons in .svg format should be placed at `\volontulo\apps\volontulo\frontend\icons\`.  
That will allow their usage in SCSS like so: `@extend %asterisk-icon;` as an element background.

### Running the App in development mode
Choose the appriopriate settings file  
Run server
```
python manage.py runserver --settings=volontulo_org.settings.dev
```
Now you able to access the development site:
[http://localhost:8000](http://localhost:8000)

### Running tests
To run the project tests:
```
python manage.py test --settings=volontulo_org.settings.dev -v 3
```

### Initial admin credentials
 * user: admin@volontuloapp.org
 * pass: stx123
