---
search:
  boost: 2
---

# How to create new CSC user account

There are two different types of CSC user accounts: ordinary accounts for general use (which you can get with or without Haka or Virtu) and machine-to-machine robot accounts for managing services.

!!! Note

    **Haka** is the identity federation of the Finnish universities, polytechnics and research institutions. Users are able to access federation services using a single user account and password. User identities are provided by the users home organizations.
    
    **Virtu** is a convenient and fast single sign-on for browser-enabled systems across organisational boundaries. Virtu is used by Finnish government agencies.

## Getting an account with Haka or Virtu

!!! Note 
    If you are trying to access the [LUMI web interface](https://www.lumi.csc.fi) or [LUMI-O](https://www.auth.lumidata.eu),
    please see the [LUMI documentation](https://docs.lumi-supercomputer.eu/firststeps/accessLUMI/) on how to get an account.

If your home organization is a member of the Haka or Virtu federation, you can create an account yourself. For registration, you will need a mobile device that has an authentication app for setting up the multi-factor authentication

1. Go to [MyCSC](http://my.csc.fi).
1. Click _Create account_
1. Click _Virtu_ or _Haka_ depending on which federation your home organization is a member of.
1. Select your home organization and log in to their identity service.
1. Fill in your information on the _Sign up_ page.
1. You will receive an email message containing a link to MyCSC where you can set your CSC account password.
1. If you are signing up with _Virtu_ you will be prompted to [set up your CSC MFA](../accounts/mfa.md#step-2-scan-qr-code) after setting your CSC accounts password. If you are signing up with _Haka_, you might already have a working MFA login integrated with your Haka login, and you will be asked to sign in with the Haka MFA. If your home organisation doesn't provide Haka MFA, you will be guided to set up CSC MFA.
1. You will receive a confirmation via email after successfully registering your CSC user account.

## Getting an account without Haka or Virtu

The preferred registration method is to log in using Haka or Virtu. If you do not have this option available, please ask your project manager to [contact CSC Service Desk](../support/contact.md).

This mostly applies to foreign collaborators of Finland-based research
groups, but ask your project manager to contact CSC and provide details about your use case and we will check your eligibility.

!!! Note

    If you cannot use Haka or Virtu, and do not have a project to
    join, you can get an account if your home organization has a
    contract with CSC or you have been granted resources in a
    program. Contact servicedesk@csc.fi and provide details
    about your use case, and we will check your eligibility.

## User accounts for courses

### For participants

If you are attending a course which is utilising CSC's services you need to create your own CSC user account with Haka or Virtu if you don't yet have one. Please see instructions above. 

### For organisers/teachers

CSC does not provide temporary training specific user accounts for courses anymore. If the participant does not yet have a user account, it needs to be created. The course organiser can then invite participants to the course project. If you're not able to create CSC user accounts, please [contact CSC Service Desk](../support/contact.md).

Please read carefully our guidance if you wish to have a course for your students using CSC's services. We request that you will create the project well in advance as soon as you have the list of the participants. And when the project is ready you are able to start sending out the invitations to your participants. 

Please see instructions on [how to create the course project](how-to-create-new-project.md#course)


## Getting a machine-to-machine robot account

If you are a registered CSC user and need another account for managing
services that you run in the CSC services, we can create a
machine-to-machine robot account for you. Please note that each service requires it's own unique robot account. Send the following
information to servicedesk@csc.fi.

* Project identifier (e.g. 2001679, uef4713) of the project your
  service uses
* The CSC service your service uses (e.g. cPouta, Rahti)
* Your mobile number (to which the password are sent via SMS)


