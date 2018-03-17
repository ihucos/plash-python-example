# plash-python-example
An example of using python with plash

Calling the executable file `./bin/python` builds the container and gives you the python shell (since there where no arguemnts). That `./bin/python` executable behaves just as any other executable and can for example be put in `PATH`. 
If the file `requirements.txt` changes the python executable will be rebuild with the buid output going to stderr, so for other scripts relying on the custom python executable, rebuilds will be perceived only as a delay and stderr output.

The `./bin/runserver` script inherits from the executable python build script and starts the server, it is also a normal process and can for example be daemonized with [supervisord](http://supervisord.org/).

```
$ bin/python                                                                                   
Fetch  [0%|10%|20%|30%|40%|50%|60%|70%|80%|90%|100%]                                                                           
Ignored 13 dev files                                                                                                           
+ apk update                                                                                                                   
fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/main/x86_64/APKINDEX.tar.gz                                                   
fetch http://dl-cdn.alpinelinux.org/alpine/v3.7/community/x86_64/APKINDEX.tar.gz                                               
v3.7.0-124-g0e68619b57 [http://dl-cdn.alpinelinux.org/alpine/v3.7/main]       
...
...
...
Successfully installed Jinja2-2.10 MarkupSafe-1.0 Werkzeug-0.14.1 certifi-2018.1.18 chardet-3.0.4 click-6.7 flask-0.12.2 idna-2
.6 itsdangerous-0.24 requests-2.18.4 urllib3-1.22                                                                             
You are using pip version 9.0.1, however version 9.0.2 is available.                                                           
You should consider upgrading via the 'pip install --upgrade pip' command.                                                     
--:                                                                                                                           
Python 3.6.3 (default, Nov 21 2017, 14:55:19)                                                                                 
[GCC 6.4.0] on linux                                                                                                           
Type "help", "copyright", "credits" or "license" for more information.                                                         
>>> exit()

$ bin/python  # second run is cached, changes in requirements.txt invalidate the cache
Python 3.6.3 (default, Nov 21 2017, 14:55:19)                                                                                 
[GCC 6.4.0] on linux                                                                                                           
Type "help", "copyright", "credits" or "license" for more information.                                                         
>>> exit()

$ bin/runserver # runserver uses the python image as base iamge
+ touch /entrypoint                                                                                                           
+ echo #!/bin/sh                                                                                                               
+ echo export FLASK_APP=app.py                                                                                                 
+ echo exec flask run --host=localhost                                                                                         
+ chmod 755 /entrypoint                                                                                                       
--:                                                                                                                           
 * Serving Flask app "app"                                                                                                     
 * Running on http://localhost:5000/ (Press CTRL+C to quit)    
```

## some recipes

Run shell in container
`plash run --include bin/runserver`

### Status
Works but api not stable and small details that need more thought and real usage
