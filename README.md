osg-ca-generator
===============

A CLI utility and python library for quick creation of dummy, DigiCert-like or
CILogon-like CAs and certificates for the purpose of osg-testing.

Command-Line Interface
----------------------

```
Usage: osg-ca-generator [options]

Generate or load pre-existing DigiCert-like CAs for testing OSG software.

Options:
  --version             show program's version number and exit
  -h, --help            show this help message and exit
  -e DAYS, --expire-days=DAYS
                        The number of days before test CAs or certificates expire
  -f, --force           Overwrite any existing CAs or certificates
  --cilogon             Create CILogon-like CAs and certificates instead
  --host                Create a host certificate using the test CA
  -u USER, --user=USER  Create a user certificate for the specified user using the test CA
  -p PASSWORD, --pass=PASSWORD
                        Set the user certificate's password. Default: None
```

Python Library
--------------

```
NAME
    cagen - Create DigiCert-like OSG test CAs and certificates

FILE
    /usr/lib/python2.6/site-packages/osg-ca-generator/cagen.py

CLASSES
    __builtin__.object
        CA
    exceptions.Exception(exceptions.BaseException)
        CertException

    class CA(__builtin__.object)
     |  DigiCert-like certificate authorities (CAs) that can be used to generate
     |  host or user certificates.
     |
     |  Pre-existing CAs can be loaded via the subject name and __init__()
     |  (without the force option) or by its path with load().
     |
     |  Methods defined here:
     |
     |  __init__(self, subject, days=10, force=False, mimic='digicert')
     |      Create a CA (and crl) with the given subject.
     |
     |      days - specifies the number of days before the certificate expires
     |      force - will overwrite any existing certs and keys if set to True
     |      mimic - type of CA/certs to mimic: 'cilogon' or 'digicert' (default)
     |
     |  crl(self, days=10)
     |      Create CRL file for the CA instance
     |
     |      days - specifies the number of days before the certificate expires
     |
     |  hostcert(self, days=10)
     |      Creates a host certificate (hostcert.pem) and host key (hostkey.pem)
     |      in /etc/grid-security from the given CA instance.
     |
     |      days - specifies the number of days before the certificate expires
     |
     |      Returns strings:
     |      Host certificate subject, host certificate path, host certificate key path
     |
     |  usercert(self, username, password, days=10)
     |      Creates a user cert (usercert.pem) and user key (userkey.pem)
     |      in ~username/.globus/ from the given CA instance.
     |
     |      days - specifies the number of days before the certificate expires
     |
     |      Returns strings:
     |      User certificate subject, user certificate path, user certificate key path
     |
     |  ----------------------------------------------------------------------
     |  Class methods defined here:
     |
     |  load(cls, ca_path) from __builtin__.type
     |      Load a CA from the location given by ca_path
     |
     |  ----------------------------------------------------------------------
     |  Data descriptors defined here:
     |
     |  __dict__
     |      dictionary for instance variables (if defined)
     |
     |  __weakref__
     |      list of weak references to the object (if defined)

    class CertException(exceptions.Exception)
     |  Exception class for certificate errors
     |
     |  Method resolution order:
     |      CertException
     |      exceptions.Exception
     |      exceptions.BaseException
     |      __builtin__.object
     |
     |  Data descriptors defined here:
     |
     |  __weakref__
     |      list of weak references to the object (if defined)
     |
     |  ----------------------------------------------------------------------
     |  Methods inherited from exceptions.Exception:
     |
     |  __init__(...)
     |      x.__init__(...) initializes x; see help(type(x)) for signature
     |
     |  ----------------------------------------------------------------------
     |  Data and other attributes inherited from exceptions.Exception:
     |
     |  __new__ = <built-in method __new__ of type object>
     |      T.__new__(S, ...) -> a new object with type S, a subtype of T
     |
     |  ----------------------------------------------------------------------
     |  Methods inherited from exceptions.BaseException:
     |
     |  __delattr__(...)
     |      x.__delattr__('name') <==> del x.name
     |
     |  __getattribute__(...)
     |      x.__getattribute__('name') <==> x.name
     |
     |  __getitem__(...)
     |      x.__getitem__(y) <==> x[y]
     |
     |  __getslice__(...)
     |      x.__getslice__(i, j) <==> x[i:j]
     |
     |      Use of negative indices is not supported.
     |
     |  __reduce__(...)
     |
     |  __repr__(...)
     |      x.__repr__() <==> repr(x)
     |
     |  __setattr__(...)
     |      x.__setattr__('name', value) <==> x.name = value
     |
     |  __setstate__(...)
     |
     |  __str__(...)
     |      x.__str__() <==> str(x)
     |
     |  __unicode__(...)
     |
     |  ----------------------------------------------------------------------
     |  Data descriptors inherited from exceptions.BaseException:
     |
     |  __dict__
     |
     |  args
     |
     |  message

FUNCTIONS
    certificate_info(path)
        Extracts and returns the subject and issuer from an X.509 certificate.

DATA
    PIPE = -1
```
