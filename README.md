Python DBAPI 2.0 for Datascope
==============================

This is a implementation of the DBAPI 2.0 database API standard for the Datascope database system designed by [Boulder Real Time Technologies](http://brtt.com).


Summary
-------

The purpose of this module is to abstract processing programs from any specific database backend. See the [PEP 249 -- Python Database API Specification v2.0](http://www.python.org/dev/peps/pep-0249/) for details on the specifications, and the python class, function and method docstrings for details on the implementation.

Customizations
--------------
### NULL support

Datascope has no NULL type, each field defines its own value which compares equal to NULL. Therefore, NULLs must be explicitly looked up and converted, at a slight performance overhead. This can be enabled for this module by setting the Cursor attribute `CONVERT_NULL` to `True`. All fields in any rows returned the the `fetch*` methods will contain a python `None` for any NULL value. 

### Factory support

This module supports row factory classes similar to those of the sqlite3 (among others) implementation of the DBAPI. Instances of a Cursor or Connection have a attribute called `row_factory`. Setting this attribute to a special class constuctor which has the format: `GenericRowFactory(cursor, row)` allows for the custom building of rows. The default row returned by the `fetch*` methods is the standard `tuple`. Currently this module has three pre-defined row factory classes:
* NamedTupleRow - Rows of python namedtuples with attribute-style access to each item.
* OrderedDictRow - Rows of python OrderedDict instances.
* UTCOrdDictRow - Identical to OrderedDictRow, with any field comparing to 'dbTIME' converted to an ObsPy UTCDateTime object.

Contact
-------

Copyright 2013 Mark Williams at [Nevada Seismological Laboratory](http://www.seismo.unr.edu/Faculty/29)

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

