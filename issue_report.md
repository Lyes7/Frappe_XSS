### Summary
_We've identified a security concern in our Frappe application that allows a user with low privileges to upload a potentially harmful HTML file. When an admin later reviews the submitted form, the attached file executes a script, leading to the unauthorized takeover of the admin's session. Despite the use of HttpOnly cookies, we've also discovered a way to extract the Session ID (SID) from the homepage HTML response._

### Details
_The issue stems from how our application handles file attachments during form submissions. Specifically, the lack of proper checks and filters on attached HTML files enables the execution of arbitrary code when viewed by an admin. The vulnerable code can be traced to functions within [specific file/module names or paths].

It's crucial to note that for this exploit to work, the attached file must be marked as Public rather than Private. Public attachments open directly in a new tab, making it easier for the malicious script to run when an admin reviews the form._

### PoC
_
Create a user account with low privileges.
Submit a form with an attached HTML file containing a malicious script, marked as Public.
As an admin, access and review the form, including the attached HTML file.
Observe the execution of the malicious script, resulting in session theft..

Additional method to retrieve SID:

Access the homepage and retrieve the HTML response.
Implement a script to extract the SID from the HTML response, bypassing the HttpOnly flag._

### Impact
_This vulnerability poses a significant security risk, allowing an attacker with low privileges to compromise an admin's session. The attacker can run arbitrary code, potentially gaining unauthorized access to sensitive information and performing actions on behalf of the admin.

This report emphasizes the importance of securely handling attachments marked as Public and underscores the need for enhanced validation and filtering of file attachments._
