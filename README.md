python-color-logger
===================

A ColorizingStreamHandler forked from Vinay Sajip logutils:  https://bitbucket.org/vinay.sajip/logutils/

The original code for this project was written by Vinay Sajip and is hosted at: https://bitbucket.org/vinay.sajip/logutils/

pthon-color-logger forked this project at version 0.3.3 to add support for curstom coloring 
in class derioved from ColorizingStreamHandler

Example:

```
class ColorHandler(ColorizingStreamHandler):
    def __init__(self, *args, **kwargs):
        super(ColorHandler, self).__init__(*args, **kwargs)
        self.level_map = {
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
            'class':'vagabond.logger.logger.ColorHandler',
            'info':'white',
            'level': 'DEBUG',
            'formatter': 'detailed',
            'stream': 'ext://sys.stdout',
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
}


L = logging.getLogger('info')
L.info("Hello world")

<font style="color: green"> Some green text </span>
//<span style="color: green"> Some green text </span>
```

