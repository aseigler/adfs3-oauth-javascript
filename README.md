# adfs3-oauth-javascript
ADFS 3.0 (2012 R2 version) compatible OAuth2 test application in javascript, using https://github.com/kjur/jsrsasign

Required strings:

1. Federation service name, like fs.contoso.com - get this from (Get-AdfsProperties).HostName
2. Test site name - this is where you put the html file.  If you saved the file as 'Default.htm' in directory 'pathname' and web server is https://www.contoso.com, use https://www.contoso.com/pathname/

Required ADFS config:

1. An ADFS client - Add-AdfsClient -ClientId https://www.contoso.com/pathname/ -Name ADFS3-OAuth-Javascript -RedirectUri https://www.contoso.com/pathname/
2. A relying party trust - Add-AdfsRelyingPartyTrust -Name ADFS3-OAuth-Javascript -Identifier https://www.contoso.com/pathname/ -IssuanceAuthorizationRules ' => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");' -IssuanceTransformRules 'c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"] => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = ";employeeNumber,givenName,sn,mail;{0}", param = c.Value);'

Plug the strings into the appropriate boxes on the HTML form and use the buttons navigate through.
