# Logging example

The preferred log format for eLife applications.

`<timestamp> - <log level> - <process name> - <program section> - <message>`

__Why be so formal about this?__ These log files are eventually parsed by other 
programs and the bits are extracted, used in calculations, stored, etc. 

Many applications with many different logging formats means more work for me. 
[__KISS__](http://en.wikipedia.org/wiki/KISS_principle)

Examples:

* `1420811950.9472651 - DEBUG - elife-api - somemodule.py - a message goes here`
* `1420811950.9472651 - INFO - elife-bot - somemodule.py - a message goes here`
* `1420811950.9472651 - WARN - SimpleScraper.js - func_name - a message goes here`
* `1420811950.9472651 - ERROR - foo - somemodule.py - a message goes here`
* `1420811950.9472651 - CRITICAL - bar - somemodule.py - a message goes here`
* `1420811950 - INFO - baz - somemodule.py - a message goes here`

__timestamp__: the time in seconds since the epoch as a floating point or integer 
number.

__log level__: one of DEBUG, INFO, WARN, ERROR or CRITICAL

__process name__: name of the running program

__program section__: where in the program this log entry originated.

__message__: a free form message; may include hyphens; avoid line breaks.

## Python

Use this formatter:

`%(created)f - %(levelname)s - %(processName)s - %(name)s - %(message)s`

The included example can be run with: 

`cd python && ./main.py`

Python docs for the `logging` module are here: 
https://docs.python.org/2/library/logging.html#logrecord-attributes

## Javascript

...

## notes

I use Unix time `%(created)f` rather than the `YMD` format because Unix time 
is used natively by [Riemann](http://riemann.io) (our realtime monitor).
