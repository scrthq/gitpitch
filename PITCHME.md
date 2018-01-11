@title[Introduction]

## <span class="gold">OneLogin</span> Administration

***

#### Policies & Procedures

---

@title[Objectives]

## <span class="gold">Objectives</span>

***

During this training session, we're going to cover...  
* key terms used when talking about SAML SSO
* what goes into a typical SAML integration
* deeper dive into SAML
* troubleshooting tips and tricks

---

@title[Key Terms]

## <span class="gold">Key</span> Terms

***

**_SAML_**: Security Assertion Markup Language  
**_IdP_**: Identity Provider (in our case, OneLogin)  
**_SP_**: Service Provider (application)  
**_Connector_**: Another term for application in OneLogin

---

@title[High-Level Overview]

## <span class="gold">High-Level</span> Overview

***

There are a few layers to create when integrating a new application with OneLogin. Here is what's needed for a typical SAML build out...  

@fa[arrow-down]

+++
@title[AD Group]
#### Active Directory group created to enable the application for members

@fa[arrow-down]

+++
@title[Connector]

#### SAML connector built in OneLogin (aka SAML application)

@fa[arrow-down]

+++
@title[Role]

#### Role built in OneLogin that gives role members access to the SAML connector (because applications aren't assigned directly to users)

@fa[arrow-down]

+++
@title[Mapping]

#### Mapping built in OneLogin that assigns the new role to the AD group members (memberof contains `OneLogin-#{application}`)

@fa[arrow-right]

---

@title[AD Group]