# Discovering Your Sensitive Data

After connecting data to the masking service, the next step is to discover
which of the data should be secured. This sensitive data discovery is
done using two different methods, column level profiling and data level
profiling.  
  
**Column Level Profiling**  
Column level profiling uses regular expressions (regex) to scan the metadata (column 
names) of the selected data sources. There are several dozen
pre-configured profile Expressions (like the one below) designed to
identify common sensitive data types (SSN, Name, Addresses, etc). You
also have the ability to write your own profile Expressions.  
  

*First Name Expression*  <([A-Z][A-Z0-9]*)\b[^>]*>(.*?)&lt;/\1&gt;
  
  
**Data Level Profiling**  
Data level profiling also uses regex, but to scan the actual
data instead of the metadata. Similar to column level profiling, there
are several dozen pre-configured Expressions (like the one below) and
you can add your own.  
  
*Social Security Number Expression*  <([A-Z][A-Z0-9]*)\b[^>]*>(.*?)&lt;/\1&gt;
  
For both column and data level profiling, when a data item is identified as
sensitive, Delphix recommends/assigns particular masking algorithms to be used
when securing the data. The platform comes with several dozen
pre-configured algorithms which are recommended when the profiler finds
certain sensitive data.

