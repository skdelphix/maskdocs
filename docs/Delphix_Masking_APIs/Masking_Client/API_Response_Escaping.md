# API Response Escaping

In Masking API responses, a backslash character (`\`) is escaped with an additional backslash character (`\\`). Special attention should be paid to this behavior in scenarios where an API response is passed to another system as an input, for example, an automation system.

In such cases, a response might need special handling to convert the double backslash sequence (`\\`) back to a single backslash (`\`).

For example, consider the `POST /ssh-key` API for creating/installing an SSH Key. The result when the `POST /ssh-key` API is called with a file name that contains `\`, such as `\key.txt`, is shown below.

**Response Body:**

```
{
  "errorMessage": "SSH Key file name should not contain [\\, ;, %, ?, :]"
}
```