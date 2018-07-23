# Out Of The Box Secure Methods/Algorithms 

This section describes the different security methods (SL, SM, etc)
available and the specific out of the box algorithms.

An integral part of the data masking process is to use algorithms to
mask each data element. You specify which algorithm to use on each
individual data element (domain) on the Masking's tab. There, you define
a unique domain for each element and then associate the classification
and algorithm you want to use for each domain.

Delphix offers a the following set of Algorithms right out of the box:

## Secure Lookup Algorithm

Secure lookup is the most commonly used type of algorithm. It is easy to
generate and works with different languages. When this algorithm
replaces real, sensitive data with fictional data, it is possible that
it will create repeating data patterns, known as “collisions.” For
example, the names “Tom” and “Peter” could both be masked as “Matt.”
Because names and addresses naturally recur in real data, this mimics an
actual data set. However, if you want the masking engine to mask all
data into unique outputs, you should use segment mapping.

## Sement Mapping Algorithm

Segment mapping algorithms produce no overlaps or repetitions in the
masked data. They let you create unique masked values by dividing a
target value into separate segments and masking each segment
individually.

You can mask up to a maximum of 36 values using segment mapping. You
might use this method if you need columns with unique values, such as
Social Security Numbers, primary key columns, or foreign key columns.
When using segment mapping algorithms for primary and foreign keys, in
order to make sure they match, you must use the same segment mapping
algorithm for each. You can set the algorithm to produce alphanumeric
results (letters and numbers) or only numbers.

With segment mapping, you can set the algorithm to ignore specific
characters. For example, you can choose to ignore dashes \[-\] so that
the same Social Security Number will be identified no matter how it is
formatted. You can also preserve certain values. For example, to
increase the randomness of masked values, you can preserve a single
number such as 5 wherever it occurs. Or if you want to leave some
information unmasked, such as the last four digits of Social Security
numbers, you can preserve that information.

### Segment Mapping Example

Perhaps you have an account number for which you need to create a
segment mapping algorithm. You can separate the account number into
segments, preserving the first two-character segment, replacing a
segment with a specific value, and preserving a hyphen. The following is
a sample value for this account number:

NM831026-04

*Where:*

  - **NM** is a plan code number that you want to preserve, always a
    two-character alphanumeric code.

  - **831026** is the uniquely identifiable account number. To ensure
    that you do not inadvertently create actual account numbers, you
    can replace the first two digits with a sequence that never
    appears in your account numbers in that location. (For example,
    you can replace the first two digits with 98 because 98 is never
    used as the first two digits of an account number.) To do that,
    you want to split these six digits into two segments.

  - **-04** is a location code. You want to preserve the hyphen and
    you can replace the two digits with a number within a range (in
    this case, a range of 1 to 77).

## Mapping Algorithm

A mapping algorithm allows you to state what values will replace the
original data. It sequentially maps original data values to masked
values that are pre-populated to a lookup table through the Masking
Engine user interface. There will be no collisions in the masked data,
because it always matches the same input to the same output. For example
“David” will always become “Ragu,” and “Melissa” will always become
“Jasmine.” The algorithm checks whether an input has already been
mapped; if so, the algorithm changes the data to its designated output.

You can use a mapping algorithm on any set of values, of any length, but
you must know how many values you plan to mask. You must supply AT
MINIMUM the same number of values as the number of unique values you are
masking; more is acceptable. For example, if there are 10,000 unique
values in the column you are masking you must give the mapping algorithm
AT LEAST 10,000
values.

!!! info
    When you use a mapping algorithm, you cannot mask more than one table at a time. You must mask tables serially.

## Binary Lookup Algorithm

A Binary Lookup Algorithm is much like the Secure Lookup Algorithm, but
is used when entire files are stored in a specific column. This
algorithm replaces objects that appear in object columns. For example,
if a bank has an object column that stores images of checks, you can use
a binary lookup algorithm to mask those images. The Delphix Engine
cannot change data within images themselves, such as the names on X-rays
or driver’s licenses. However, you can replace all such images with a
new, fictional image. This fictional image is provided by the owner of
the original data.

## Tokenization Algorithm

A tokenization algorithm is the only type of algorithm that allows you
to reverse its masking. For example, you can use a tokenization
algorithm to mask data before you send it to an external vendor for
analysis. The vendor can then identify accounts that need attention
without having any access to the original, sensitive data. Once you have
the vendor’s feedback, you can reverse the masking and take action on
the appropriate accounts.

Like mapping, a tokenization algorithm creates a unique token for each
input such as “David” or “Melissa.” The actual data (for example, names
and addresses) are converted into tokens that have similar properties to
the original data – such as text and length – but no longer convey any
meaning. The Delphix Masking Engine stores both the token and the
original so that you can reverse masking later.

## Min Max Algorithm

The Delphix Masking Engine provides a "Min Max Algorithm" to normalize
data within a range – for example, 10 to 400. Values that are extremely
high or low in certain categories allow viewers to infer someone’s
identity, even if their name has been masked. For example, a salary of
$1 suggests a company’s CEO, and some age ranges suggest higher
insurance risk. You can use a min max algorithm to move all values of
this kind into the midrange. This algorithm allows you to make sure that
all the values in the database are within a specified range.

If the **Out of range Replacement Values** checkbox is selected, a
default value is used when the input cannot be evaluated.

## Data Cleansing Algorithm

A data cleansing algorithm does not perform any masking. Instead, it
standardizes varied spellings, misspellings, and abbreviations for the
same name. For example, “Ariz,” “Az,” and “Arizona” can all be cleansed
to “AZ.” Use this algorithm if the target data needs to be in a standard
format prior to masking.

## Free Text Algorithm

A free text redaction algorithm helps you remove sensitive data that
appears in free-text columns such as “Notes.” This type of algorithm
requires some expertise to use, because you must set it to recognize
sensitive data within a block of text.

One challenge is that individual words might not be sensitive on their
own, but together they can be. The algorithm uses profiler sets to
determine what information it needs to mask. You can decide which
expressions the algorithm uses to search for material such as addresses.
For example, you can set the algorithm to look for “St,” “Cir,” “Blvd,”
and other words that suggest an address. You can also use pattern
matching to identify potentially sensitive information. For example, a
number that takes the form 123-45-6789 is likely to be a Social Security
Number.

You can use a free text redaction algorithm to show or hide information
by displaying either a “black list” or a “white list.”

**Blacklist** – Designated material will be redacted (removed). For
example, you can set a blacklist to hide patient names and addresses.
The blacklist feature will match the data in the lookup file to the
input file.

**Whitelist** – ONLY designated material will be visible. For example,
if a drug company wants to assess how often a particular drug is being
prescribed, you can use a white list so that only the name of the drug
will appear in the notes. The whitelist feature enables you to mask data
using both the lookup file and a profile set.

For either option, a list of words can be imported from an external text
file or alternatively, you can use Profiler Sets to match words based on
regular expressions, defined within Profiler Expressions. You can also
specify the redaction value that will replace the masked words. Regular
expressions defined using Profiler Sets will match individual words
within the input text, rather than phrases.
