# plash-python-example
An example of using python with plash

Calling the executable file `./bin/python` builds the container and gives you the python shell (since there where no arguemnts). That `./bin/python` executable behaves just as any other executable and can for example be put in `PATH`. 
If the file `requirements.txt` changes the python executable will be rebuild with the buid output going to stderr, so for other scripts relying on the custom python executable, rebuilds will be perceived only as a delay and stderr output.

The `./bin/runserver` script inherits from the executable python build script and starts the server, it is also a normal process and can for example be daemonized with [supervisord](http://supervisord.org/).

### Status
Works but api not stable and small details that need more thought and real usage
