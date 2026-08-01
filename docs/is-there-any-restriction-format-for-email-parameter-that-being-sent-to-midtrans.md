---
updatedAt: 2025-11-11T00:12:34.000Z
---

Fetch the complete documentation index at: https://docs.midtrans.com/llms.txt. Use this file to discover all available pages before exploring further.

# Is there any restriction format for email parameter that being sent to Midtrans?

Yes, Midtrans validates customer email formats for certain payment methods such as Permata VA, CIMB Clicks, Telkomsel Cash, KlikBCA, Mandiri Ecash, and Indomaret.

We are using regex logic for this validation. Please focus on the value that is allowed by this logic, you can refer to the below explanation:

interface Constants \{\
String ATOM = "\[a-z0-9!#$%&'\*+/=?^\_\`\{|}\~-]";\
String DOMAIN = "(" + ATOM + "+(\\." + ATOM + "+)+";\
String IP\_DOMAIN = "\\\[\[0-9]\{1,3}\\.\[0-9]\{1,3}\\.\[0-9]\{1,3}\\.\[0-9]\{1,3}\\]";

String PATTERN =\
"^$|^" + ATOM + "+(\\." + ATOM + "+)\*@"

+DOMAIN

+"|"

+IP\_DOMAIN

+")$";\
}

**ATOM** is a combination of alphanumeric.\
**DOMAIN** is a combination of DOT(".") and ATOM.\
**IP\_DOMAIN** is a combination of DOT(".") and numbers with a maximum length are 3.

Example :\
The right PATTERN <midtrans@midtrans.com>\
The wrong PATTERN <midtrans..@midtrans.com>