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

<br>

@fa[arrow-down]

+++
@title[AD Group]
#### AD Group

***

This should be the first item you create. Membership in this group will provide the application in that user's OneLogin page.

<br>

@fa[arrow-down]

+++
@title[Connector]

#### SAML Connector

***

This is the actual application in OneLogin.

<br>

@fa[arrow-down]

+++
@title[Role]

#### OneLogin Role

***

Roles include one or more connectors. Users in a role receive the connectors included with it.

<br>

@fa[arrow-down]

+++
@title[Mapping]

#### OneLogin Mapping  

***

Mappings allow you to create logic between the AD group and OneLogin role, i.e. 
```
  if User's 
    `MemberOf` 
  contains 
    `AD-Group-Name`
  assign user to role 
    `Role-Name`
```

<br>

@fa[arrow-right]

---

@title[Deep dive]

***

