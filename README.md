[![Build Status](https://travis-ci.org/frithnanth/perl6-File-Metadata-Libextractor.svg?branch=master)](https://travis-ci.org/frithnanth/perl6-File-Metadata-Libextractor)

NAME
====

File::Metadata::Libextractor - Use libextractor to read file metadata

SYNOPSIS
========

    use File::Metadata::Libextractor;

    #| This program extracts all the information about a file
    sub MAIN($file! where { .IO.f // die "file '$file' not found" })
    {
      my File::Metadata::Libextractor $e .= new;
      my @info = $e.extract($file);
      for @info -> %record {
        for %record.kv -> $k, $v {
          say "$k: $v"
        }
        say '-' x 50;
      }
    }

DESCRIPTION
===========

File::Metadata::Libextractor provides an OO interface to libextractor in order to query files' metadata.

As the Libextractor site ([https://www.gnu.org/software/libextractor](https://www.gnu.org/software/libextractor)) states, it is able to read information in the following file types:

  * HTML

  * MAN

  * PS

  * DVI

  * OLE2 (DOC, XLS, PPT)

  * OpenOffice (sxw)

  * StarOffice (sdw)

  * FLAC

  * MP3 (ID3v1 and ID3v2)

  * OGG

  * WAV

  * S3M (Scream Tracker 3)

  * XM (eXtended Module)

  * IT (Impulse Tracker)

  * NSF(E) (NES music)

  * SID (C64 music)

  * EXIV2

  * JPEG

  * GIF

  * PNG

  * TIFF

  * DEB

  * RPM

  * TAR(.GZ)

  * LZH

  * LHA

  * RAR

  * ZIP

  * CAB

  * 7-ZIP

  * AR

  * MTREE

  * PAX

  * CPIO

  * ISO9660

  * SHAR

  * RAW

  * XAR FLV

  * REAL

  * RIFF (AVI)

  * MPEG

  * QT

  * ASF

Also, various additional MIME types are detected.

new()
-----

Creates a **File::Metadata::Libextractor** object; it needs no argument.

extract($file where .IO.f // fail "file '$file' not found" --> List)
--------------------------------------------------------------------

Reads all the possible information from an existing file, or fails if the file doesn't exist. The output **List** is actually a List of Hashes. Each hash has the following keys:

  * mime-type The file's mime-type

  * plugin-name The name of the plugin the library used to find out the information

  * plugin-type The plugin subtype used for the operation

  * plugin-format The format of the plugin's output

  * data-type The value returned by the plugin subtype

The possible values for **plugin-format** are:

  * EXTRACTOR_METAFORMAT_UNKNOWN

  * EXTRACTOR_METAFORMAT_UTF8

  * EXTRACTOR_METAFORMAT_BINARY

  * EXTRACTOR_METAFORMAT_C_STRING

The possible values for the **plugin-type** field are listed in File::Metadata::Libextractor::Constants, in the EXTRACTOR_MetaType enum (231 values so far).

Prerequisites
=============

This module requires the libextractor library to be installed. Please follow the instructions below based on your platform:

Debian or Ubuntu Linux
----------------------

    sudo apt-get install libextractor3

The module looks for a library called libextractor.so.3 .

Installation
============

To install it using zef (a module management tool):

    $ zef install File::Metadata::Libextractor

Testing
=======

To run the tests:

    $ prove -e "perl6 -Ilib"

AUTHOR
======

Fernando Santagata <nando.santagata@gmail.com>

COPYRIGHT AND LICENSE
=====================

Copyright 2018 Fernando Santagata

This library is free software; you can redistribute it and/or modify it under the Artistic License 2.0.

