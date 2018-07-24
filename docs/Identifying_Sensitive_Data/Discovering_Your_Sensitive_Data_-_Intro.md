# Discovering Your Sensitive Data

After connecting data to the masking service, the next step is discover
which of the data should be secured. This sensitive data discovery is
done using two different methods, column level profiling and data level
profiling.  
  
**Column Level Profiling**  
Column level profiling uses REGEX expressions to scan the column names
(metadata) of the select data sources. There are several dozen
pre-configured profile expressions (like the one below) designed to
identify common sensitive data types (SSN, Name, Addresses, etc). You
also have the ability to write/import your own profile expressions.  
  
|Type -------------    | Expression --------------           |
|First Name Expression | <([A-Z][A-Z0-9]*)\b[^>]*>(.*?)</\1> |
  
  
**Data Level Profiling**  
Data level profiling also uses REGEX expressions, but to scan the actual
data instead of the metadata. Similar to column level profiling, there
are several dozen pre-configured expressions (like the one below) and
you can write/import your own.  
  
  
  
For both column and data level profiling, when a data is identified as
sensitive, Delphix recommends/assigns particular algorithms to be used
when securing the data. The platform comes with several dozen
pre-configured algorithms which are recommended when the profiler finds
certain sensitive data.

##
