---
author: mcleanbyron
ms.assetid: 571697B7-6064-4C50-9A68-1374F2C3F931
description: Learn how to use the Windows.Services.Store namespace to implement a trial version of your app.
title: Implement a trial version of your app
keywords: free trial
keywords: free trial period
keywords: free trial code example
keywords: free trial code sample
---

# Implement a trial version of your app

If you enable customers to use your app for free during a trial period, you can entice your customers to upgrade to the full version of your app by excluding or limiting some features during the trial period. Determine which features should be limited before you begin coding, then make sure that your app only allows them to work when a full license has been purchased. You can also enable features, such as banners or watermarks, that are shown only during the trial, before a customer buys your app.

Apps that target Windows 10, version 1607 or later can use members of the [StoreContext](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.aspx) class in the [Windows.Services.Store](https://msdn.microsoft.com/library/windows/apps/windows.services.store.aspx) namespace to determine if the user has a trial license for your app and be notified if the state of the license changes while your app is running.

>**Note** This article is applicable to apps that target Windows 10, version 1607 or later. If your app targets an earlier version of Windows 10, you must use the [Windows.ApplicationModel.Store](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.store.aspx) namespace instead of the **Windows.Services.Store** namespace. For more information, see [In-app purchases and trials using the Windows.ApplicationModel.Store namespace](in-app-purchases-and-trials-using-the-windows-applicationmodel-store-namespace.md).

## Guidelines for implementing a trial version

The current license state of your app is stored as properties of the [StoreAppLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.aspx) class. Typically, you put the functions that depend on the license state in a conditional block, as we describe in the next step. When considering these features, make sure you can implement them in a way that will work in all license states.

Also, decide how you want to handle changes to the app's license while the app is running. Your trial app can be full-featured, but have in-app ad banners where the paid-for version doesn't. Or, your trial app can disable certain features, or display regular messages asking the user to buy it.

Think about the type of app you're making and what a good trial or expiration strategy is for it. For a trial version of a game, a good strategy is to limit the amount of game content that a user can play. For a trial version of a utility, you might consider setting an expiration date, or limiting the features that a potential buyer can use.

For most non-gaming apps, setting an expiration date works well, because users can develop a good understanding of the complete app. Here are a few common expiration scenarios and your options for handling them.

-   **Trial license expires while the app is running**

    If the trial expires while your app is running, your app can:

    -   Do nothing.
    -   Display a message to your customer.
    -   Close.
    -   Prompt your customer to buy the app.

    The best practice is to display a message with a prompt for buying the app, and if the customer buys it, continue with all features enabled. If the user decides not to buy the app, close it or remind them to buy the app at regular intervals.

-   **Trial license expires before the app is launched**

    If the trial expires before the user launches the app, your app won't launch. Instead, users see a dialog box that gives them the option to purchase your app from the Store.

-   **Customer buys the app while it is running**

    If the customer buys your app while it is running, here are some actions your app can take.

    -   Do nothing and let them continue in trial mode until they restart the app.
    -   Thank them for buying or display a message.
    -   Silently enable the features that are available with a full-license (or disable the trial-only notices).

Be sure to explain how your app will behave during and after the free trial period so your customers won't be surprised by your app's behavior. For more info about describing your app, see [Create app descriptions](https://msdn.microsoft.com/library/windows/apps/mt148529).

## Prerequisites

This example has the following prerequisites:
* A Visual Studio project for a Universal Windows Platform (UWP) app that targets Windows 10, version 1607 or later.
* You have created an app in the Windows Dev Center dashboard that is configured as a [free trial](https://msdn.microsoft.com/windows/uwp/publish/set-app-pricing-and-availability), and this app is published and available in the Store. This can be an app that you want to release to customers, or it can be a basic app that meets minimum [Windows App Certification Kit](https://developer.microsoft.com/windows/develop/app-certification-kit) requirements that you are using for testing purposes only. For more information, see the [testing guidance](in-app-purchases-and-trials.md#testing).

The code in this example assumes:
* The code runs in the context of a [Page](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.page.aspx) that contains a [ProgressRing](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.progressring.aspx) named ```workingProgressRing``` and a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) named ```textBlock```. These objects are used to indicate that an asynchronous operation is occurring and to display output messages, respectively.
* The code file has a **using** statement for the **Windows.Services.Store** namespace.
* The app is a single-user app that runs only in the context of the user that launched the app. For more information, see [In-app purchases and trials](in-app-purchases-and-trials.md#api_intro).

## Code example

When your app is initializing, get the [StoreAppLicense](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storeapplicense.aspx) object for your app and handle the [OfflineLicensesChanged](https://msdn.microsoft.com/library/windows/apps/windows.services.store.storecontext.offlinelicenseschanged.aspx) event to receive notifications when the license changes while the app is running. For example, the app's license could change if the trial period expires or the customer buys the app through a Store. When the license changes, get the new license and enable or disable a feature of your app accordingly.

At this point, if a user bought the app, it is a good practice to provide feedback to the user that the licensing status has changed. You might need to ask the user to restart the app if that's how you've coded it. But make this transition as seamless and painless as possible.


```csharp
private StoreContext context = null;
private StoreAppLicense appLicense = null;

// Call this while your app is initializing.
private async void InitializeLicense()
{
    if (context == null)
    {
        context = StoreContext.GetDefault();
    }

    workingProgressRing.IsActive = true;
    appLicense = await context.GetAppLicenseAsync();
    workingProgressRing.IsActive = false;

    // Register for the licenced changed event.
    context.OfflineLicensesChanged += context_OfflineLicensesChanged;
}

private async void context_OfflineLicensesChanged(StoreContext sender, object args)
{
    // Reload the license.
    workingProgressRing.IsActive = true;
    appLicense = await context.GetAppLicenseAsync();
    workingProgressRing.IsActive = false;

    if (appLicense.IsActive)
    {
        if (appLicense.IsTrial)
        {
            textBlock.Text = $"This is the trial version. Expiration date: {appLicense.ExpirationDate}";

            // Show the features that are available during trial only.
        }
        else
        {
            // Show the features that are available only with a full license.
        }
    }
}
```

## Related topics

* [In-app purchases and trials](in-app-purchases-and-trials.md)
* [Get product info for apps and add-ons](get-product-info-for-apps-and-add-ons.md)
* [Get license info for apps and add-ons](get-license-info-for-apps-and-add-ons.md)
* [Enable in-app purchases of apps and add-ons](enable-in-app-purchases-of-apps-and-add-ons.md)
* [Enable consumable add-on purchases](enable-consumable-add-on-purchases.md)