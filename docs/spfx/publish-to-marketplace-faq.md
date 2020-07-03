---
title: Publish SharePoint Framework applications to the marketplace - FAQ
description: Frequently asked questions about publishing SharePoint Framework applications to the marketplace
ms.date: 06/25/2020
ms.prod: sharepoint
localization_priority: Priority
---

# Publish SharePoint Framework applications to the marketplace - FAQ

Following are some of the most frequently asked questions regarding publishing SharePoint Framework applications to the marketplace.

## Is it required to configure web parts to be isolated for publishing in the marketplace

No, it is not required to configure web parts to be isolated. It is fully up to you to decide if your web parts should be isolated or not and you can use either mode in the application you publish to the marketplace.

## Can I request additional API permissions for my solution

Yes, if your solution needs additional API permissions to work as intended, then you should request these permissions to be granted in your solution’s manifest. Please note, that the marketplace verification team could ask you to justify access to the permissions that you have requested when verifying your submission.

## Can I expose my web parts in Office add-ins

At this moment exposing SharePoint Framework web parts in Office add-ins is in preview and is not yet supported in solutions published in the marketplace.

## Can I include library components in my solution

Yes, library components are fully supported in solutions published to the marketplace.

## Can I use a custom Microsoft Teams manifest

When building SharePoint Framework web parts, you can choose to [expose them in SharePoint and Microsoft Teams as personal apps or tabs](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction). To use your web parts in Teams you can either generate the manifest and the Teams solution package yourself or have the SharePoint Framework generate it for you. Creating the manifest manually gives you more flexibility and allows you to create multi-tab personal apps.

At this moment, the marketplace does not support embedding custom Teams manifests in SharePoint Framework packages. You can expose your web parts in Teams using the manifest auto-generated by SharePoint Framework.

If your web part requires configuration and you expose it as a personal Teams app, you need to implement a custom UI yourself to allow users to configure it.