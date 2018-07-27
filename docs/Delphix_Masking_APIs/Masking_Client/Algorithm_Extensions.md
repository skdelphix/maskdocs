# Algorithm Extensions

## Models

### **Algorithm**

> **algorithmName
> (maxLength=500)**
> 
> [*String*](#string)
> Equivalent to the algorithm name saved by the user through the GUI.
> For out of the box algorithms, this will be a similar name as that in
> the GUI, but presented in a more user-friendly
> format.
> 
> **algorithmType**
> 
> [*String*](#string)
> The type of algorithm
> 
> **Enum:**
> 
> *BINARY\_LOOKUP*
> 
> *CLEANSING*
> 
> *LOOKUP*
> 
> *MAPPLET*
> 
> *MAPPING*
> 
> *MINMAX*
> 
> *REDACTION*
> 
> *SEGMENT*
> 
> *TOKENIZATION*
> 
> **createdBy (optional; readOnly;
> maxLength=255)**
> 
> [*String*](#string)
> The name of the user that created the algorithm
> 
> **description (optional;
> maxLength=255)**
> 
> [*String*](#string)
> The description of the algorithm
> 
> **algorithmExtension (optional)**
> 
> *Object*

### **AlgorithmExtension**

### **BinaryLookupExtension**

> **fileReferenceIds (optional;
> maxLength=36)**
> 
> [*array\[String\]*](#string)
> A list of file reference UUID values returned from the endpoint for
> uploading files to the Masking Engine.

### **DataCleansingExtension**

> **fileReferenceId
> (optional)**
> 
> [*String*](#string)
> The reference UUID value returned from the endpoint for uploading
> files to the Masking Engine. The file should contain a newline
> separated list of {value, replacement} pairs separated by the
> delimiter. No extraneous whitespace should be present.
> 
> **delimiter (optional; minLength=1; maxLength=50;
> default="=")**
> 
> [*String*](#string)
> The delimiter string used to separate {value, replacement} pairs in
> the uploaded file

### **FreeTextRedactionExtension**

> **blackListRedaction (optional;
> default=true)**
> 
> [*Boolean*](#boolean)
> Black list redaction if true, white list redaction if false.
> 
> **lookupFileReferenceId (optional;
> maxLength=36)**
> 
> [*String*](#string)
> The reference UUID value returned from the endpoint for uploading the
> lookup file to the Masking Engine.
> 
> **lookupRedactionValue (optional;
> maxLength=255)**
> 
> [*String*](#string)
> The value to use to redact items matching entries specified in the
> lookup file.
> 
> **profileSetId
> (optional)**
> 
> [*Integer*](#integer)
> The ID number of the profile set for defining the pattern matching to
> use for identifying values for redaction. format: int32
> 
> **profileSetRedactionValue (optional;
> maxLength=255)**
> 
> [*String*](#string)
> The value to use to redact items matching patterns defined by the
> profile set.

### **MappingExtension**

> **fileReferenceId
> (optional)**
> 
> [*String*](#string)
> The reference UUID value returned from the endpoint for uploading
> files to the Masking Engine. The file should contain a newline
> separated list of mapping values.
> 
> **ignoreCharacters (optional; minimum=32;
> maximum=126)**
> 
> [*array\[Integer\]*](#integer)
> The integer ASCII values of characters to ignore in the column data to
> map

### **MappletExtension**

> **mappletInput (optional;
> maxLength=500)**
> 
> [*String*](#string)
> The name of the input variable for the custom algorithm
> 
> **mappletOutput (optional;
> maxLength=500)**
> 
> [*String*](#string)
> The name of the output variable for the custom algorithm
> 
> **fileReferenceId (optional;
> maxLength=36)**
> 
> [*String*](#string)
> The reference UUID value returned from the endpoint for uploading
> files to the Masking Engine.

### **MinMaxExtension**

> **minValue (optional;
> minimum=0)**
> 
> [*Integer*](#integer)
> The minimum value for a Number range used in conjunction with
> maxValue. This field cannot be combined with minDate or maxDate.
> format: int32
> 
> **maxValue (optional;
> minimum=1)**
> 
> [*Integer*](#integer)
> The maximum value for a Number range used in conjunction with and must
> be greater than minValue. This field cannot be combined with minDate
> or maxDate. format: int32
> 
> **minDate
> (optional)**
> 
> [*date*](#date)
> The minimum value for a Date range used in conjunction with maxDate.
> The Date must be specified in one of the following formats according
> to RFC 3339 Section 5.6: "yyyy-MM-dd", "yyyy-MM-dd'T'HH:mm:ss.SSSZ",
> "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", or "EEE, dd MMM yyyy HH:mm:ss zzz". If
> a timezone is not specified, the Date will be interpreted as UTC. This
> field cannot be combined with minValue or maxValue. format: date
> 
> **maxDate
> (optional)**
> 
> [*date*](#date)
> The maximum value for a Date range used in conjunction with and must
> be greater than minDate. The Date must be specified in one of the
> following formats according to RFC 3339 Section 5.6: "yyyy-MM-dd",
> "yyyy-MM-dd'T'HH:mm:ss.SSSZ", "yyyy-MM-dd'T'HH:mm:ss.SSS'Z'", or "EEE,
> dd MMM yyyy HH:mm:ss zzz". If a timezone is not specified, the Date
> will be interpreted as UTC. This field cannot be combined with
> minValue or maxValue. format: date
> 
> **outOfRangeDefaultValue (optional;
> maxLength=255)**
> 
> [*String*](#string)
> The default replacement value for any value that is out-of-range.

### **SecureLookupExtension**

> **fileReferenceId (optional;
> maxLength=36)**
> 
> [*String*](#string)
> The reference UUID value returned from the endpoint for uploading
> files to the Masking Engine.

### **SegmentMappingExtension**

> **preservedRanges
> (optional)**
> 
> [*array\[SegmentMappingPreservedRange\]*](#segmentmappingpreservedrange)
> List of character {offset, length} values specifying ranges of the
> real value to preserve. Offsets begin at 0
> 
> **ignoreCharacters
> (optional)**
> 
> [*array\[Integer\]*](#integer)
> List of decimal values specifying ASCII characters to ignore (not
> mask, not count as part of any segment) in the real value. For
> example, 65 would ignore 'A'
> 
> **segments (optional; minItems=2; maxItems=36)**
> 
> *array\[SegmentMappingSegment\]*

### **SegmentMappingPreservedRange**

> **offset
> (optional)**
> 
> [*Integer*](#integer)
> The character offset of the range of input to preserve
> 
> **length
> (optional)**
> 
> [*Integer*](#integer)
> The character length of the range of input to preserve

### **SegmentMappingSegment**

> **length (optional; minimum=1;
> maximum=4)**
> 
> [*Integer*](#integer)
> The length of the segment in digits. This must be 1 for alpha-numeric
> segments
> 
> **minInt (optional; minimum=0;
> maximum=9999)**
> 
> [*Integer*](#integer)
> The minimum value of the integer output range of the mapping function
> 
> **maxInt (optional; minimum=0;
> maximum=9999)**
> 
> [*Integer*](#integer)
> The maximum value of the integer output range of the mapping function
> 
> **minChar (optional; minLength=1;
> maxLength=1)**
> 
> [*String*](#string)
> The minimum value of the character output range of the mapping
> function
> 
> **maxChar (optional; minLength=1;
> maxLength=1)**
> 
> [*String*](#string)
> The maximum value of the character output range of the mapping
> function
> 
> **explicitRange
> (optional)**
> 
> [*String*](#string)
> Explicitly specify the output range. Format depends on segment type
> and size
> 
> **minRealInt (optional; minimum=0;
> maximum=9999)**
> 
> [*Integer*](#integer)
> The minimum value of the integer range specifying which real values
> will be masked
> 
> **maxRealInt (optional; minimum=0;
> maximum=9999)**
> 
> [*Integer*](#integer)
> The maximum value of the integer range specifying which real values
> will be masked
> 
> **minRealChar (optional; minLength=1;
> maxLength=1)**
> 
> [*String*](#string)
> The minimum value of the character range specifying which real values
> will be masked
> 
> **maxRealChar (optional; minLength=1;
> maxLength=1)**
> 
> [*String*](#string)
> The maximum value of the character range specifying which real values
> will be masked
> 
> **explicitRealRange
> (optional)**
> 
> [*String*](#string)
> Explicitly specify the range of input values that should be masked.
> Format depends on segment type and size
