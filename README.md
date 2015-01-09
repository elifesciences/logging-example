# Logging example in Python

Demonstrates the preferred log format for eLife applications.

_Why be so formal about this?_ These log files are eventually parsed by other 
programs and the bits are extracted, used in calculations, stored, etc. 

Many applications with many different logging formats means more work for me. 

[__KISS__](http://en.wikipedia.org/wiki/KISS_principle)

## notes

* using Unix time `%(created)f` rather than the YMD format as Unix time is what 
Riemann (realtime monitor that consumes these parsed log files) uses natively.
