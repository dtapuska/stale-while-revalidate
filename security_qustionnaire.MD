# Security Questionnaire Results for TAG Review

From [questionnaire](https://www.w3.org/TR/security-privacy-questionnaire)

# Does this specification deal with personally-identifiable information?
No

# Does this specification deal with high-value data?
No

# Does this specification introduce new state for an origin that persists across browsing sessions?
No

# Does this specification expose persistent, cross-origin state to the web?
Yes. It is conceivable that you could determine if a resource is stale and that would indicate that you
loaded a page containing the stale resource within the max-age of the given resource. This already
exists when it is within the max-age so I'm not sure there is anything new exposed here.

# Does this specification expose any other data to an origin that it doesn’t currently have access to?
No

# Does this specification enable new script execution/loading mechanisms?
No

# Does this specification allow an origin access to a user’s location?
No

# Does this specification allow an origin access to aspects of a user’s local computing environment?
No

# Does this specification allow an origin access to other devices?
No

# Does this specification expose temporary identifiers to the web?
No

# Does this specification distinguish between behavior in first-party and third-party contexts?
No

# How should this specification work in the context of a user agent’s "incognito" mode?
N/A

# Does this specification persist data to a user’s local device? 
N/A

# Does this specification have a "Security Considerations" and "Privacy Considerations" section?
N/A

# Does this specification allow downgrading default security characteristics?
N/A
