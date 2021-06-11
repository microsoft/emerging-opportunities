# Verifiable Credentials News

Verifiable Credentials (VCs) allows to validate information about people, organizations, and other entities.

Each VC is created by an **issuer** which is an organization or entity that asserts about a **subject** to which a credential is issued.

VC contains attributes about the subjects to which they are issued, e.g., for a university diploma includes student’s field of study, year of graduation, and grade point average, etc.

  * A **subject** who receives the credential becomes the holder of the that credential which they store in their wallet – a mobile app on subject’s device
  * A **verifier** is a person or organization or thing who will verify the information shared by the subject
    * For example, a student applies for a job, the employer requests access to view student’s digital diploma, employer (verifier) will verify the information contained the credential stored in the student wallet which is shared by the student with employer

![image](https://user-images.githubusercontent.com/26188338/121603491-153f0c00-ca06-11eb-9c83-abf1f4f9d917.png)

Link to projects: 

- [Decentralized Identity and Verifiable Credential - Overview](https://github.com/microsoft/Decentralized-Identity-and-Verifiable-Credentials)

## Future Sprint

TBD

## Past Sprints

> Sprint 23

The team built a fictitious use case using Azure AD Verifiable Credential service which is in public preview.

The solution covers the key concepts and tools such as [Decentralized Identifiers (DID)](https://www.w3.org/TR/did-core/), [Verifiable Credentials (VC)](https://www.w3.org/TR/vc-data-model/), [Microsoft Authenticator](https://www.microsoft.com/en-us/account/authenticator), [Microsoft VC SDK and REST API](https://github.com/microsoft/VerifiableCredentials-Verification-SDK-Typescript), etc.

### Use Case

To showcase the features and capabilities of Verifiable Credentials (VC), a simple use case where an employees receives employment credentials by logging into their companies internal portal. Using their employee credentials, they can receive tax-exempt credentials of their organization by going to government website and sharing their employee credentials. Using their employee and government tax-exempt credentials they can avail the benefits offered by a partner company (Wood grove).

The project delivered the following services:

*	[Employee Internal Portal](https://duwamish.powerappsportals.com/) is developed as a Azure Power Portal application backed by Azure AD as Identity Provider (IdP)
*	[Government Website](https://vcdemogovtapp.azurewebsites.net/) is developed as a simple web application and deployed to Azure App Service
*	[Partner Portal](https://woodgrovevc.powerappsportals.com/) is developed as a Azure Power Portal application backed by Azure AD B2C as Identity Provider (IdP)
*	[API Service](https://verifiablecredentialapi.azurewebsites.net/swagger/v1/swagger.json) which integrates the Microsoft REST API and SDK is developed as a DotNet API service and deployed to Azure App Service






### Would you like to be involved?
*link to MS Form will be coming soon*
