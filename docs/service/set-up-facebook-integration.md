---
# This basic template provides core metadata fields for Markdown articles on docs.superoffice.com.

# Mandatory fields.
title: set_up_facebook_integration_for_service       # (Required) Very important for SEO. Intent in a unique string of 43-59 chars including spaces.
description: Set up Facebook integration for Service # (Required) Important for SEO. Recommended character length is 115-145 characters including spaces.
author: {github-id}             # Your GitHub alias.
keywords:
so.topic: howto                # article, howto, reference, concept, guide

# Optional fields. Don't forget to remove # if you need a field.
# so.envir:                     # cloud or onsite
# so.client:                    # online, web, win, pocket, or mobile
---

# Facebook integration with Customer Service

With the integration, you will be able to import messages and comments from page wall as requests in Customer Service. You will also be able to reply to these messages/comments, and they will be posted back on Facebook.

> [!WARNING]
> **Facebook integration and Cambridge Analytica:** Facebook is currently making changes to their API after the Cambridge Analytica scandal. This means that the Facebook integration that is part of our tests is no longer working, and for any customer/partner who have not used this in a while or try to set it up now. We are unsure if and how it affects sites that have been in use all the time. Read more in this [forum post][1].

## Before you begin

* Create an account with [developer access on Facebook][2].
* [Create a Facebook page][3] where Service will get posts and post back replies to.

Screens may differ, but if you experience problems, please contact our [support][4].

## Create an application on Facebook

First, you will need to create an application on Facebook with the user you want to retrieve messages from, or the owner of the page.

1. Go to [http://developers.facebook.com/apps][5] (make sure you are signed in to Facebook) or click **apps** from developers.facebook.com.

2. Click **Create a new App** or **Add a new App** if you have other apps already.

3. You will be presented with the dialog to **Create a New App ID** where you add **Display Name** and **Contact Email,** note that the Display name is who will be posting messages on your page later.

4. Under category choose **Apps for Pages**

![x][6]

5. After you click **Create App ID** you will be redirected to the **Add Product,** but move up to **Settings**.

![x][7]

  * Add Platform:

![x][8]

  * Choose Website:

![x][9]

  * Add a Site URL:
    * Customer Service installation **with** FastCgi: `Https://support.yourdomain.com/scripts/admin.fcgi?action=registerFacebook`
    * Customer Service installation **without** FastCgi: `https://support.yourdomain.com/scripts/admin.exe?action=registerFacebook`

![x][10]

6. When you are done you will need to make your app available, this is done under **App Review** and change it to *Yes*.

![x][11]

> [!NOTE]
> **The site URLs must be available on the internet since Facebook will be pushing changes to this URL.** And the URLs must be running on HTTPS since we are using WebHooks and Facebook will only allow this via the secure protocol.

## Get the AppId and AppSecret for setup in Service

This is found under **Dashboard**. If the App secret is hidden, click to show and write it down. You will need these when you authenticate later.

 ![x][12]

Note that the App ID in this screenshot is just an example.

## Get your Facebook PageID

You also need to provide a **Page ID**. The Page ID can be obtained by Going to the About screen for your page:

 ![x][13]

## Add new Facebook inbox in Service

You need to configure Service to retrieve messages from Facebook using the application you just created. Make sure that you are either logged out of Facebook, or logged in with the same user you used when creating the application. Failing to do so will result in incorrect behavior.

1. Go to Settings->E-mail and click the **New Facebook application** icon.

![x][14]

2. Enter the **Application ID** and **Page ID** which you noted earlier.

![][15]

3. Fill in the rest of the information and click **Ok**.

4. You will now be redirected to Facebook, where it will ask for some permission for the application you created.

![x][16]

5. You will now be asked for the Client secret which is the same as the App Secret from your Facebook application. Click **OK**.

6. When done you will see your Facebook account together with the other mailboxes.

By default, the integration will start to import messages the time when you add the App Secret on the mail box. Old posts on your page will not be added.

> [!TIP]
> To manually post messages to Facebook, add Facebook as one of the recipients on a ticket.

![x][17]

## Troubleshooting

```json
{ "error": { "message": "Invalid redirect_uri: Given URL is not allowed by the Application configuration.", "type": "OAuthException", "code": 191 } }
```

If you receive this error after you have added Application ID and Page ID inside Customer Service:

* Verify that the site URL you gave in your Facebook application is correct and points to your Customer Service installation:. The URL should included `admin.fcgi?` if Service has FastCGI; `admin.exe?`without.

* Verify that the URL is available on the internet. Otherwise, Facebook will not be able to reach it.

* Make sure you are running Service on HTTPS:

[From Facebook documentation:][18]
New Webhook subscriptions must use a secure HTTPS callback URL as of v2.5. With the next version of the Graph API we will stop sending updates to non-HTTPS callback URLs.
If you need more information about setting up HTTPS for your callback URL, check out [the Getting Started guide][18] from Let's Encrypt and [the SSL Certificate Installation instructions][20] from Digicert.

<!-- Referenced links -->
[1]:https://community.superoffice.com/en/technical/Forum/rooms/topic/superoffice-product-group/customer-service/our-facebook-integration-and-cambridge-analytica/
[2]: https://developers.facebook.com/
[3]: https://www.facebook.com/pages/create/
[4]: http://support.superoffice.com/
[5]: http://developers.facebook.com/apps
[6]: media/facebooknewappid.png
[7]: media/facebookappsettings.png
[8]: media/facebookaddplatform.png
[9]: media/facebookwebsite.png
[10]: media/facebookregisterurl.png
[11]: media/facebookappreview.png
[12]: media/facebookappidandsecret.png
[13]: media/facebookpageid.png
[14]: media/facebookservicenewfbapp.png
[15]: media/facebookserviceproperties.png
[16]: media/2managepages.jpg
[17]: media/facebookreply.png
[18]: https://developers.facebook.com/docs/graph-api/webhooks
[19]: https://letsencrypt.org/getting-started/
[20]: https://www.digicert.com/ssl-certificate-installation.htm