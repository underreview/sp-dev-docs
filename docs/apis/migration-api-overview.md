---
title: "SharePoint Migration API Introduction"
description: "This article provides an introduction to SharePoint Migration API."
ms.date: 16/01/2024
ms.author: ranren
author: UnderReview
manager: dapodean
search.appverid: MET150
ms.subservice: migration-tool
ms.localizationpriority: high
---

# SharePoint Migration API Introduction

The SharePoint Migration API imports contents into SharePoint at scale. It processes content and manifest packages as jobs in a queue. The API provides process status and logs, making it easy to monitor the progress of each migration job.

Use Migration API to migrate content from file shares, SharePoint Server, and other cloud-based services.

[!Note]
 Don't use Migration API for Tenant-to-Tenant (T2T) migrations, when contents from one SharePoint tenant moves to another. If you're planning a T2T migration, check [T2T migration solution](link to T2T solution).

## Migration steps overview

Start a migration job with three steps. Check the guidance in each of the steps in this section.

### Prepare the content

Package the contents in the defined format and upload to Azure Blob Storage Containers as the content package.

Check [Content package](contentpackage.md) to see the detailed requirements.

### Create the manifest files

Based on the contents, create manifest files in XML format, and upload to Azure Blob Storage Containers as the manifest package.

Check [Manifest files](manifest.md) to see the detailed requirements.

### Use Migration API to start migration and get status

Use ``ProvisionMigrationContainers`` method to provision the containers, upload the content package and Manifest into respective containers. Check [Use Azure Blob Storage Containers and Azure Queues with Migration API](azure.md) for details. You can also use your own containers and queues if needed.

`CreateMigrationJob` method creates a migration job, which is queued up for processing. Migration API manages the queue and returns status and logs. Use `CreateMigrationEncrypted` method to migrate encrypted contents.

Upon creation of a new migration job, Migration API returns the Job ID, Track the status of the import with ``GetMigrationJobStatus`` method if needed, with the Azure Queue supplied.

Migration API generates logs in the manifest container. Check the log entries for migration results.

## Best Practice

### Use app-based authentication

Migration generates workload to the SPO backend differently from end user generated traffic. To properly allocate resources with our elastic capability, only use app-based authentication in your migration solution.

Don't use user mode in your migration solution. Running migration in user mode triggers increased throttling, resulting in poor performance.

To learn more on how to register an app ID and how to implement app-based authentication, check [How to register an app ID](https://learn.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-registration-portal) and [Microsoft Graph Auth guidance](https://learn.microsoft.com/en-us/graph/auth).

### Microsoft Entra ID Permissions

Microsoft Entra ID provides two type of permission: Delegated Permission and Application Permissions. Check[
Permissions and consent in the Azure Active Directory v1.0 endpoint](https://learn.microsoft.com/en-us/azure/active-directory/develop/v1-permissions-and-consent) for details.

For SharePoint and OneDrive migration scenarios, follow the Microsoft Entra ID permission specification.

For migration tools that rely on end user signed in and presence, use Delegated permission.

For service-based migration tools that run without a signed-in user present, such as applications that run as background services, use Application permission.

### App IDs

You can choose to share a single App ID to cover multiple migration solutions created, or create individual App ID for each of the products. Make sure to register App IDs. Sharing App IDs doesn't affect performance or throttling.

### Keep destination SPO site unactivated

To avoid migration issues, deactivate the target site for users until the migration completion. The source could remain active, allowing read and write to keep productivity. Switch users to the new SPO destination sites after migration completion.

## Performance

Migration API processes jobs through a queue mechanism with pre-configured workload management settings. Migration API processes the jobs on a best-effort basis, without Service Level Agreement (SLA) or guaranteed performance.

### Optimize migration performance

In order to ensure optimal performance for your migration projects, it's important to plan carefully, especially when dealing with large-scale migrations. For more information on how to estimate timespans and optimize performance, see our [performance guide](https://learn.microsoft.com/en-us/sharepointmigration/sharepoint-online-and-onedrive-migration-speed).

### I'm seeing throttling messages

To ensure good user experiences for all Microsoft 365 customers, SharePoint uses throttling to protect the SharePoint Online infrastructure. Avoid getting throttled by following [throttling guidance](https://aka.ms/spo429).

## Special Topics

### Migrating sharing events of files and folders

Check [Sharing events](https://learn.microsoft.com/en-us/sharepoint/dev/apis/migration-api-shared) article for instructions when migrating shared events metadata with files and folders.

### Web Parts

Use SPMT's Web Part serializer DLL to migrate Web Parts into SharePoint. Check [Migrate Web Parts}(https://learn.microsoft.com/en-us/sharepoint/dev/apis/migrate-webparts-with-migrationapi) for instructions.


