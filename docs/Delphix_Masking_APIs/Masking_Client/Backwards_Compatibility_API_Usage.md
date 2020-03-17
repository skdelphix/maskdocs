# Backwards Compatibility API Usage

!!! note
    In all examples, replace **&lt;myMaskingEngine&gt;** with the hostname or IP address of your virtual machine. |

In all examples, replace **&lt;myMaskingEngine&gt;** with the hostname or IP
address of your virtual machine.

## API Versioning Context

The Masking API being shipped with the 5.2 series of releases of the
Delphix Masking Engine is version **v5.0.0** in accordance with the
Semantic Versioning format:
[<span class="underline">http://semver.org/</span>](http://semver.org/).
In subsequent maintenance and major releases of the Masking product, the
Masking API may be updated and a new API version will be released *(e.g.
**v5.0.1**, **v5.1.0**, etc).* As scripts using the new Masking API are
being written, they must reference an explicit API version or else there
are no guarantees that the scripts will work on future releases of the
Masking product.

## Pinning Down a Version Number To Guarantee Backwards-Compatibility

**'http://&lt;myMaskingEngine&gt;/masking/api/v5.0.0/environments'**

This is the format for specifying a version in the URL of an API request
targeting the **environments** endpoints. The only possible version
value for the Masking API in the first 5.2 release is **v5.0.0**. As
more releases of the Masking product are shipped in the future, the set
of possible versions will expand.

Scripts that specifically pin down the version of the Masking API in the
URL will continue to work upon future upgrades of the Masking
product--even if a newer version of the API is available in the future
Masking product–with the exception that
[Incubating API Endpoints](Incubating_API_Endpoints/)
are never guaranteed to be backwards-compatible.

For example, consider the scenario where a script is being developed
today with a pinned down version **v5.0.0** in the URL of the API
requests. Upon upgrade to a future release of the Masking product that
has the API **v5.1.0** available, the same, untouched script that was
developed with the pinned down version **v5.0.0** in the URL of the API
requests is expected to continue working. That said, in order to
leverage any new features of the API **v5.1.0**, the original script
will need to be updated to specify the new API version in the URL, and
the requests may need to be updated to conform to the new API
specification.

## Omitted Version Numbers

**'http://&lt;myMaskingEngine&gt;/masking/api/environments'**

This is the format for not specifying a version in the URL of an API
request targeting the **environments** endpoints. When the API version
number is omitted, the latest API version is taken as a default. In the
first 5.2 release, an API request with an omitted version number will be
interpreted as a request against the **v5.0.0** version of the API. In a
future release that hypothetically has the API **v5.3.0** available, an
API request with an omitted version number will be interpreted as a
request against the **v5.3.0** version of the API.

Scripts that omit the version of the Masking API in the URL are not
guaranteed to work upon future upgrades of the Masking product because
the API specification may change between versions, and requests that
conform to the old API specification may not work on the new API
specification.
