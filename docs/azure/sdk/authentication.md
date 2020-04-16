---
title: 使用用于 .NET 的 Azure 库进行身份验证
description: 在用于 .NET 的 Azure 库中进行身份验证
ms.date: 08/22/2018
ms.custom: azure-sdk-dotnet
ms.openlocfilehash: e562b60da0a2d34f716e80d3d5d0d0b5e55b0cdb
ms.sourcegitcommit: 34dc3c0d0d0a1cc418abff259d9daa8078d00b81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2020
ms.locfileid: "81433144"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="fe851-103">使用用于 .NET 的 Azure 库进行身份验证</span><span class="sxs-lookup"><span data-stu-id="fe851-103">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="fe851-104">使用连接字符串连接到服务</span><span class="sxs-lookup"><span data-stu-id="fe851-104">Connect to services with connection strings</span></span>

<span data-ttu-id="fe851-105">大多数 Azure 服务库要求使用连接字符串或密钥进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="fe851-105">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="fe851-106">例如，SQL 数据库使用标准的 SQL 连接字符串：</span><span class="sxs-lookup"><span data-stu-id="fe851-106">For example, SQL Database uses a standard SQL connection string:</span></span>

```csharp
var builder = new SqlConnectionStringBuilder();
builder.DataSource = "example.database.windows.net";
builder.InitialCatalog = "MyDatabase";
builder.UserID = "sampleuser@example"; // Format user ID as "user@server"
builder.Password = password;
builder.Encrypt = true;
builder.TrustServerCertificate = true;

using (var conn = new SqlConnection(builder.ConnectionString))
{
    conn.Open();
    // Do things with the connection...
    // ...
}
```

<span data-ttu-id="fe851-107">Azure 存储使用存储密钥：</span><span class="sxs-lookup"><span data-stu-id="fe851-107">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="fe851-108">服务连接字符串用于其他 Azure 服务，如[CosmosDB、Redis](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db)[的 Azure 缓存](/azure/azure-cache-for-redis/cache-dotnet-how-to-use-azure-redis-cache)和服务[总线](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues)，您可以使用 Azure 门户、CLI 或 PowerShell 获取这些字符串。</span><span class="sxs-lookup"><span data-stu-id="fe851-108">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Azure Cache for Redis](/azure/azure-cache-for-redis/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span> <span data-ttu-id="fe851-109">还可以使用用于 .NET 的 Azure 管理库来查询资源，以便在代码中生成连接字符串。</span><span class="sxs-lookup"><span data-stu-id="fe851-109">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span>

<span data-ttu-id="fe851-110">以下代码片段使用管理库创建存储帐户连接字符串：</span><span class="sxs-lookup"><span data-stu-id="fe851-110">This snippet uses the management libraries to create a storage account connection string:</span></span>

```csharp
// Get a storage account
var storage = azure.StorageAccounts.GetByResourceGroup("myResourceGroup", "myStorageAccount");

// Extract the keys
var storageKeys = storage.GetKeys();

// Build the connection string
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

// Connect
var account = CloudStorageAccount.Parse(storageConnectionString);

// Do things with the account here...
```

<span data-ttu-id="fe851-111">其他库要求应用程序使用[服务主体](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects)运行，该服务主体授权应用程序使用授予的凭据来运行。</span><span class="sxs-lookup"><span data-stu-id="fe851-111">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="fe851-112">此配置类似于管理库的下列基于对象的身份验证步骤。</span><span class="sxs-lookup"><span data-stu-id="fe851-112">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <a name="azure-management-libraries-for-net-authentication"></a><a name="mgmt-auth"></a><span data-ttu-id="fe851-113">用于 .NET 的 Azure 管理库身份验证</span><span class="sxs-lookup"><span data-stu-id="fe851-113">Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](../includes/create-sp.md)]

<span data-ttu-id="fe851-114">创建服务主体后，可以使用两个选项对服务主体进行身份验证，以创建和管理资源。</span><span class="sxs-lookup"><span data-stu-id="fe851-114">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="fe851-115">对于这两个选项，您需要将以下 NuGet 包添加到项目中。</span><span class="sxs-lookup"><span data-stu-id="fe851-115">For both options you will need to add the following NuGet packages to your project.</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="fe851-116">使用令牌凭据进行身份验证</span><span class="sxs-lookup"><span data-stu-id="fe851-116">Authenticate with token credentials</span></span>

<span data-ttu-id="fe851-117">第一种方法是在代码中生成令牌凭据对象。</span><span class="sxs-lookup"><span data-stu-id="fe851-117">The first method is to build the token credential object in code.</span></span> <span data-ttu-id="fe851-118">应将凭据安全存储在配置文件、注册表或 Azure KeyVault 中。</span><span class="sxs-lookup"><span data-stu-id="fe851-118">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId,
    AzureEnvironment.AzureGlobalCloud);
```

<span data-ttu-id="fe851-119">使用在创建服务主体时获得的 JSON 输出中的 *clientId*、*clientSecret* 和 *tenantId* 值。</span><span class="sxs-lookup"><span data-stu-id="fe851-119">Use the *clientId*, *clientSecret*, and *tenantId* values from the JSON output when you created the service principal.</span></span>

<span data-ttu-id="fe851-120">然后，创建入口点 `Azure` 对象以开始使用 API：</span><span class="sxs-lookup"><span data-stu-id="fe851-120">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="file-based-authentication"></a><a name="mgmt-file"></a><span data-ttu-id="fe851-121">基于文件的身份验证</span><span class="sxs-lookup"><span data-stu-id="fe851-121">File-based authentication</span></span>

<span data-ttu-id="fe851-122">使用基于文件的身份验证可将服务主体凭据放入纯文本文件，并在文件系统中对其进行保护。</span><span class="sxs-lookup"><span data-stu-id="fe851-122">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](../includes/file-based-auth.md)]

<span data-ttu-id="fe851-123">读取该文件的内容，并创建入口点 `Azure` 对象以开始使用 API：</span><span class="sxs-lookup"><span data-stu-id="fe851-123">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```