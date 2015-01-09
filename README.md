# Logging example in Python

Demonstrates the preferred log format for eLife applications written in Python.

_Why be so formal about this?_ These log files are eventually parsed by other 
programs and the bits are extracted, used in calculations, stored, etc. 

Many applications with many different logging formats means more work for me. 

[__KISS__](http://en.wikipedia.org/wiki/KISS_principle)

* Python docs for the `logging` module can be found here:
https://docs.python.org/2/library/logging.html
* I use Unix time `%(created)f` rather than the `YMD` format because Unix time 
is used natively by [Riemann](http://riemann.io) (our realtime monitor).
