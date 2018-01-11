@title[Introduction]

## <span class="gold">OneLogin</span> Administration

***

#### Policies & Procedures

<br>

@fa[arrow-right]

---

@title[Objectives]

## <span class="gold">Objectives</span>

***

During this training session, we're going to cover...  
* key terms used when talking about SAML SSO
* what goes into a typical SAML integration
* deeper dive into SAML
* troubleshooting tips and tricks

<br>

@fa[arrow-right]

---

@title[Key Terms]

## <span class="gold">Key</span> Terms

***

**_SAML_**: Security Assertion Markup Language  
**_IdP_**: Identity Provider (in our case, OneLogin)  
**_SP_**: Service Provider (application)  
**_Connector_**: Another term for application in OneLogin
**_Form-Based Auth_**: Forms authentication (not SAML authentication)

<br>

@fa[arrow-right]

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
```powershell
if ($user.MemberOf -contains 'AD-Group-Name') {
    $user.Role = $Role
}
```

<br>

@fa[arrow-right]

---

@title[Deep dive]

## <span class="gold">Deep</span> Dive

***

A closer look at what a normal application integration looks like.

<br>

@fa[arrow-down]

+++
@title[Existing Connectors - 1]
#### Existing Connectors

***

Some vendors may have a pre-built SAML connector available in OneLogin's Application catalog. Once a new SSO setup request is received for "NewApp", it's a good idea to Existing Connectors first in OneLogin.


<br>

@fa[arrow-down]

+++
@title[Existing Connectors - 2]
#### Existing Connectors

***

You can check the connector catalog by clicking the blue New App button from your OneLogin home page or by going to Apps > Add Apps. Search for the application name in the request.

<br>

@fa[arrow-down]

+++
@title[Existing Connectors - Note]
#### Existing Connectors

***

<span class="gold"><b>Some organizations may not support Forms-Based Auth. If this is the case, you must find a _SAML 2.0_ connector (some applications may support SAML but only have the Forms-Based connector available pre-built.</span></b>

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 1]
#### Developer Intro

***

After checking for existing applications, it's time for a follow-up with the vendor or application developer.

Items to cover during this introductory call/email chain...

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 2]
#### Developer Intro

***

Is their application able to handle SAML?

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 3]
#### Developer Intro

***

Is their a pre-built SAML connector already available in OneLogin's app catalog? (this typically makes setup much quicker)

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 4]
#### Developer Intro

***

Do they have an implementation guide handy or know exactly what we need to provide them?

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 5]
#### Developer Intro

***

What information do we need to provide them, i.e. SAML SSO URL's, IdP certificate, or connector metadata file?

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 6]
#### Developer Intro

***

What is the SAML assertion consumer URL (ACS URL) for the application that we will need to send SAML assertions to?

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 7]
#### Developer Intro

***

What user attributes is the application expecting us to send in the SAML assertion? 

If it's just the email address (default NameId), then there shouldn't be any changes to the default connector attributes needed.

<br>

@fa[arrow-down]

+++
@title[Developer Intro - 8]
#### Developer Intro

***

Does the application expect anything like Role ID's to be passed in the SAML assertion as well? (this would be used for something similar to how roles are assigned when authenticating to our AWS accounts, for example)

<br>

@fa[arrow-down]

+++
@title[AD Groups - 1]
#### AD Groups

***

A common pattern is to build out AD Groups that correlate to each SAML application environment and/or role, i.e. `OneLogin-AWSDev_Developers` or `OneLogin-Blackline_Prd`. 

<br>

@fa[arrow-down]

+++
@title[AD Groups - 2]
#### AD Groups

***

If you are building a SAML connector for 4 environments that have 4 roles for each environment, the current model is to build 16 groups out (one for each unique account+role combo).

AWS OneLogin groups are a good example of this.

<br>

@fa[arrow-down]

+++
@title[SAML Connector - 1]
#### SAML Connector

***

If there is not an existing pre-built SAML connector for the application, you will need to build out a custom connector.

<br>

@fa[arrow-down]

+++
@title[SAML Connector - 2]
#### SAML Connector

***

Go to the OneLogin connector catalog and search for **SAML Test**. Choose `SAML Test Connector (IdP)`.

<br>

@fa[arrow-down]

+++
@title[OneLogin Role]
#### OneLogin Role

***

OneLogin connectors are provided via Roles. Users receive connectors via assignment to specific roles.

<br>

@fa[arrow-down]

+++
@title[OneLogin Mapping]
#### OneLogin Mapping

***

OneLogin mappings provide logic that assigns users to Roles based on AD Group membership.