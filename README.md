# DNN.Authentication.SAML
SAML 2.0 Authentication Provider

A free, open source authentication provider for DNN.

You can now Single Sign On from a remote website (if it has implemented SAML) to your DNN Portal.

## SAML
https://en.wikipedia.org/wiki/Security_Assertion_Markup_Language
Security Assertion Markup Language (SAML) is an open standard for exchanging authentication and authorization data between parties, in particular, between an identity provider and a service provider. SAML is an XML-based markup language for security assertions (statements that service providers use to make access-control decisions). SAML is also:

A set of XML-based protocol messages
A set of protocol message bindings
A set of profiles (utilizing all of the above)
The single most important use case that SAML addresses is web browser single sign-on (SSO). Single sign-on is relatively easy to accomplish within a security domain (using cookies, for example) but extending SSO across security domains is more difficult and resulted in the proliferation of non-interoperable proprietary technologies. The SAML Web Browser SSO profile was specified and standardized to promote interoperability.

https://en.wikipedia.org/wiki/Identity_provider_(SAML)
A SAML identity provider is a system entity that issues authentication assertions in conjunction with a single sign-on (SSO) profile of the Security Assertion Markup Language (SAML).

In the SAML domain model, a SAML authority is any system entity that issues SAML assertions.[OS 1] Two important examples of SAML authorities are the authentication authority and the attribute authority.

Available at GitHub
https://github.com/AccordLMS/AccordLMS.SAML

## Current Features
- Single SIgn On to a DNN site from a remot site using a SAML identity provider
- Match your DNN Profile properties and User properties with SAML Claims
- Sync these values during a User login 
- Creates and Syncs a new DNN User during login if it doesn't exist
- Can assign users to roles identified in an incoming SAML Attribute.  (Creating roles as needed in DNN as well)
- Can remove a user from roles if they are not included in the passed SAML Attribute

* Minimum DNN Version *

DNN 7.4.2 and later supported


Please feel free to utilized the provider and let us know if you encounter any problems.  We have used it for several or our LMS clients and it is stable and working without problem.  Contact any of the GitHub contributors for assistance (within reason).  Also, please submit pull requests if you add features.  Our team will review then and then include in the master release.

## Configuration

To set up the SAML authentication module, follow these steps:

1. Access the module settings:
   - Navigate to the Persona Bar
   - Go to Extensions > Installed Modules > Authentication Systems

2. Locate the DNN.Authentication.SAML Provider:
   - Click on the Edit icon next to it

3. In the Site Settings Tab, enter the following information:

   - **IDP URL**: The web address of your SAML Identity Provider
   
   - **Service Consumer URL**: The URL of your DNN login page where the SAML Assertion will be received as a POST request
   
   - **Our Entity ID**: A unique identifier for your DNN site, typically its URL. This value would be configured with your SAML Identity Provider when registering the DNN website as Application
   
   - **X509 Certificate**: The public key of your SAML Identity Provider, used to verify the SAML Assertion signature
   
   - **Redirect URL**: The page users should be directed to after successfully logging in

Ensure all information is accurate and matches the settings in your SAML Identity Provider's configuration.

## User Profile Mapping

To map SAML claims attributes to the DNN user profile, specify the name of the claim attribute you wish to use. 

You can view the SAML response in the DNN event log, which will show you the attributes that are being passed. This can help you ensure that the mapping is set up correctly.

If these values are left blank, the module will default to use the following attribute mappings to try create the DNN user profile:
- firstName
- lastName
- email
- displayName

When authenticating for the first time, _If these values are not mapped correctly, the DNN user will not be created and you will not be able to log in to the site._

## Troubleshooting

Debugging information can be found in the DNN Event Log. If you are experiencing issues, check the event log for any error messages or debug information. You'll need to make sure that your DNN instance is set to log Debug level messages. 
Update your `DotNetNuke.log4net.config`.

Change the root level to `DEBUG`:
```
  <root>
    <level value="DEBUG" />
    <appender-ref ref="RollingFile" />
  </root>
  ```
