python-color-logger
===================

Simple custom color logging for python.

The original code for this project was written by Vinay Sajip and is hosted at: https://bitbucket.org/vinay.sajip/logutils/
the original documentation for this project is at: http://plumberjack.blogspot.co.uk/2010/12/colorizing-logging-output-in-terminals.html

pthon-color-logger forked this project at version 0.3.3 to add support for custom coloring 
in classses derived from ColorizingStreamHandler.

Install: 

#####pip install python-color-logger


Example:

```
#!/usr/bin/env python
import logging
import logging.config

from logutils.colorize import ColorizingStreamHandler

class ColorHandler(ColorizingStreamHandler):
    def __init__(self, *args, **kwargs):
        super(ColorHandler, self).__init__(*args, **kwargs)
        self.level_map = {
                # Provide you custom coloring information here
                logging.DEBUG: (None, 'blue', False),
                logging.INFO: (None, 'green', False),
                logging.WARNING: (None, 'yellow', False),
                logging.ERROR: (None, 'red', False),
                logging.CRITICAL: ('red', 'white', True),
        }
CONFIG = {
    'version':1,
    'disable_existing_loggers': True,
    'handlers':{
        'console': {
            '()':ColorHandler,
            'info':'white',
            'level': 'DEBUG',
            'formatter': 'detailed',
            'stream': 'ext://sys.stdout',
        },
    },
    'formatters': {
        'detailed': {
            'format': '%(asctime)s %(module)s line:%(lineno)-4d %(levelname)-8s %(message)s',
        },
    },
    'loggers': {
        'info': {
            'level':'DEBUG',
            'handlers':['console'],
        },
    },
}

logging.config.dictConfig(CONFIG)
L = logging.getLogger('info')

L.debug("Hello world") # output should be in blue
L.info("Hello world") # output should be in green
L.warn("Hello world") # output should be in yellow
L.error("Hello world") # output should be in red
L.critical("Hello world") # output should be in white with a red back ground

```
