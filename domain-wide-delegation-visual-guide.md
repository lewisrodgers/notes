# Domain-wide delegation — a visual guide

An application may want to access user data without the need for manual authorization by that user. This involves authorizing a service account to access data on behalf of the user — also referred to as domain-wide delegation (DwD) of authority.

For a detailed step-by-step guide in enabling DwD see: [Perform G Suite Domain-Wide Delegation of Authority](https://developers.google.com/admin-sdk/directory/v1/guides/delegation)

The steps boil down to this:

1. A service account is created with DwD enabled
2. A json keyfile – or credentials – are downloaded
3. These credentials are used within an application
4. The API used (Admin SDK, Calendar, Drive, etc) and its scopes are determined within the application
5. The service account client ID and scopes are applied to the G Suite Admin console

Visually, how the pieces fit together looks something like this...

![overview]

## Separation of concerns

At the enterprise level, there'll be multiple teams or individuals responsible for different aspects of GCP and G Suite administration. Which means, there's going to be some level of coordination when it comes setting up DwD for an application that needs it.

Here's an example of what this might look like...

![complete]

There are distinct roles responsible for providing and consuming each of these things. Let's say: 

1. A developer from the App Dev team
2. The GCP admin* from the Operations team
3. And the G Suite domain admininstrator from some other part of IT

The Security team would be a factor in this dance as well, but left out for brevity.

_*GCP Admin is a generalized term I'm using to refer to someone who has the permissions to create service accounts, whether it be a GCP Project Owner or a Service Account Admin._

![roles]

## The Developer

In our scenario, App Dev wants to build an application that accesses user data on the domain. They determine the APIs and list of API scopes to be used. What's missing is the credentials needed for authentication between the application and G Suite domain. 

![app-scopes]

## The GCP Admin

In order to get the credentials, App Dev asks the GCP Admin for a service account with DwD enabled. The GCP Admin chooses a service account and makes the json keyfile available to the developers.

![service-account-request]

## The G Suite Admin

The last step is to register the application with the G Suite domain. To do this, the G Suite Admin needs to know the client ID of the service account and API scopes the application will use. They'll add these values to the [Manage client API access](https://support.google.com/a/answer/162106?hl=en) page of the G Suite console.

![gsuite-admin]

## Resources
* [Using OAuth 2.0 for Server to Server Applications](https://developers.google.com/identity/protocols/OAuth2ServiceAccount)
* [Perform G Suite Domain-Wide Delegation of Authority](https://developers.google.com/admin-sdk/directory/v1/guides/delegation)
* [Perform Google Apps domain-wide delegation of authority](https://developers.google.com/+/domains/authentication/delegation)
* [OAuth: Managing API client access](https://support.google.com/a/answer/162106?hl=en)

[overview]: img/overview.png
[roles]: img/roles.png
[app-scopes]: img/app_scopes.png
[service-account-request]: img/service_account.png
[gsuite-admin]: img/gsuite_admin.png
[complete]: img/complete.png