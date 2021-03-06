## aymmetric cryptography

[Asymmetric Encryption/Decryption in Python] -> (https://nitratine.net/blog/post/asymmetric-encryption-and-decryption-in-python/)

[Cryptography] -> (https://cryptography.io/en/stable/)

[Asymmetric Cryptography with Python] -> (https://medium.com/@ashiqgiga07/asymmetric-cryptography-with-python-5eed86772731)

[Asymmetric Encrypting of sensitive data in memory (Python)] -> (https://towardsdatascience.com/asymmetric-encrypting-of-sensitive-data-in-memory-python-e20fdebc521c)


## symmetric cryptography

[Symmetric encryption] -> https://livebook.manning.com/book/practical-python-security/chapter-4/35

[Fernet (symmetric encryption) using Cryptography module in Python] -> https://www.geeksforgeeks.org/fernet-symmetric-encryption-using-cryptography-module-in-python/ 

[Cipher Symmetric encryption with AES] -> https://cryptography.io/en/latest/hazmat/primitives/symmetric-encryption/
[example code (cipher package)] -> https://gist.github.com/btoueg/f71b62f456550da42ea9f4a4bd907d21
                                -> https://www.programcreek.com/python/example/103098/cryptography.hazmat.primitives.ciphers.modes.GCM

[Fernet (symmetric encryption) ] -> https://cryptography.io/en/latest/fernet/

[symmetric-vs-asymmetric-encryption] -> (https://www.trentonsystems.com/blog/symmetric-vs-asymmetric-encryption)

[Advanced Encryption Standard (AES)] -> (fastest and most secure symmetric encryption)



## sentry

[django-sentry docs] -> (https://docs.sentry.io/platforms/python/guides/django/)
                        (https://github.com/settings/connections/applications/Iv1.bcf13fc7ffcdd602)


## grafana

[grafanalib docs] -> (https://grafanalib.readthedocs.io/en/stable/getting-started.html)
[django-prometheus] -> (https://github.com/korfuri/django-prometheus/)


## django-storages (amazon s3)

[django-storages docs] -> (https://django-storages.readthedocs.io/en/latest/backends/amazon-S3.html)
[Setup Amazon S3 in a Django] -> (https://simpleisbetterthancomplex.com/tutorial/2017/08/01/how-to-setup-amazon-s3-in-a-django-project.html)




## DEPLOYMENT 
    
    """  GUNICORN  """


##     installation

    # requirements: Python 3.x >= 3.5 

    [ python3 -m pip install gunicorn ]

    # async workers

    [== python3 -m pip install greenlet ==]
    [== python3 -m pip install eventlet ==]
    [== python3 -m pip install gunicorn[eventlet] ==]
    [== python3 -m pip install gevent ==]
    [== python3 -m pip install gunicorn[gevent] ==]

    [== python3 -m pip install gunicorn[setproctitle] ==] # Enables setting the process name

    ## on Ubuntu

    [== sudo apt update ==]
    [== sudo apt install gunicorn ==]




##    running gunicorn

    # commands

    [== gunicorn [OPTIONS] [WSGI_APP] ==]   # [WSGI_APP] is of the pattern $(module_name):$(variable_name)


    def app(environ, start_response):
        """Simplest possible application object"""
        data = b'Hello, World!\n'
        status = '200 OK'
        response_headers = [
            ('Content-type', 'text/plain'),
            ('Content-Length', str(len(data)))
        ]
        start_response(status, response_headers)
        return iter([data])

    # e.x: [== gunicorn --workers=2 test:app ==] 

    def create_app():
        app = FrameworkApp()
        ...
        return app

    # e.x: [== gunicorn --workers=2 'test:create_app()' ==]




##    Commonly used arguments

    [ -c CONFIG, --config=CONFIG ]
    [ -b BIND, --bind=BIND ]
    [ -w WORKERS, --workers=WORKERS ]
    [ -k WORKERCLASS, --worker-class=WORKERCLASS ]
    [ -n APP_NAME, --name=APP_NAME ]
    


##    Configuration Overview

    # Gunicorn reads configuration information from five places

    1) """ [Environment Variables]  Gunicorn first reads environment variables for some configuration settings.  """
    
    2) """ [Framework Settings]  Gunicorn then reads configuration from a framework specific configuration file. Currently this only affects Paster applications.  """
    
    3) """ [Configuration File]  The third source of configuration information is an optional configuration file gunicorn.conf.py searched in the current working directory or specified using a command line argument. Anything specified in this configuration file will override any framework specific settings.  """
    
    4) """ [GUNICORN_CMD_ARGS]  The fourth place of configuration information are command line arguments stored in an environment variable named GUNICORN_CMD_ARGS  """
    
    5) """ [Command Line]  Lastly, the command line arguments used to invoke Gunicorn are the final place considered for configuration settings. If an option is specified on the command line, this is the value that will be used.  """


    # To print resolved configuration

    [== gunicorn --print-config APP_MODULE ==] (gunicorn --print-config proroot.wsgi)


    # To check resolved configuration

    [== gunicorn --check-config APP_MODULE ==] (gunicorn --check-config proroot.wsgi)



##    Settings

    

