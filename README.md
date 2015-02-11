# Logging

The preferred log format for eLife applications.

`<timestamp> - <log level> - <process name> - <program section> - <message>`

__Why be so formal about this?__ These log files are eventually parsed by other 
programs and the extracted bits are used in calculations, stored, displayed, etc.

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

# Logging in production

Storage is cheap, logging is easy, so why wouldn't we log everything we possibly 
can and keep it around forever?

* data must be transformed into information, otherwise it's worthless

All other reasons derive from this one. If logging data is not used then it's 
just noise.

__INFO__ is the default level for all applications in production. 

__DEBUG__ log statements are discarded by monitoring applications and will not 
be stored.

## retention

All _application_ log messages sent to the monitoring server will be kept for 
__12 months__. This is _entirely arbitrary_ and handled by the `logrotate` 
application.

All _audit_ log messages sent to the monitoring server will be kept 
__indefinitely__, or, as long as some business rule tells us. This rule will be 
encapsulated entirely within code.

## audit logs

Auditing is a _type_ of logging. 

Auditing within an application exists because there is a business requirement 
to do so. A regular log message might be _'user "joe" logged in'_, but becomes 
part of the audit trail when there is a business requirement to track a user's
activities through a system.

If a formal audit log is required, it _must_ go to it's own log file.

## S3 bucket access

Logging for an S3 bucket should only be enabled if:

1. a person explicitly wants it monitored
2. the bucket is acting as a server and is the only point of access to that data  

All S3 access logs should go to the logging bucket `elife-log-data` with the 
name of the originating bucket as the prefix.
