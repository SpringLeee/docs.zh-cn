---
ms.openlocfilehash: 8e077d5cde6e824af5aac3742308593f1d91dd92
ms.sourcegitcommit: a9b8945630426a575ab0a332e568edc807666d1b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "80391177"
---
### <a name="static-files-csv-content-type-changed-to-standards-compliant"></a>静态文件：CSV 内容类型已更改为符合标准

在 ASP.NET Core 5.0 中，[静态文件中间件](/aspnet/core/fundamentals/static-files)用于 .csv  文件的默认 `Content-Type` 响应标头值已更改为符合标准的值 `text/csv`。

有关此问题的讨论，请参阅 [dotnet/aspnetcore#17385](https://github.com/dotnet/AspNetCore/issues/17385)。

#### <a name="version-introduced"></a>引入的版本

5.0 预览版 1

#### <a name="old-behavior"></a>旧行为

使用 `Content-Type` 标头值 `application/octet-stream`。

#### <a name="new-behavior"></a>新行为

使用 `Content-Type` 标头值 `text/csv`。

#### <a name="reason-for-change"></a>更改原因

符合 [RFC 7111](https://tools.ietf.org/html/rfc7111#section-5.1) 标准。

#### <a name="recommended-action"></a>建议操作

如果此更改影响你的应用，则可以自定义文件扩展名到 MIME 类型的映射。 若要还原到 `application/octet-stream` MIME 类型，请在 `Startup.Configure` 中修改 <xref:Microsoft.AspNetCore.Builder.StaticFileExtensions.UseStaticFiles%2A> 方法调用。 例如：

```csharp
var provider = new FileExtensionContentTypeProvider();
provider.Mappings[".csv"] = MediaTypeNames.Application.Octet;

app.UseStaticFiles(new StaticFileOptions
{
    ContentTypeProvider = provider
});
```

有关自定义映射的详细信息，请参阅 [FileExtensionContentTypeProvider](/aspnet/core/fundamentals/static-files#fileextensioncontenttypeprovider)。

#### <a name="category"></a>类别

ASP.NET Core

#### <a name="affected-apis"></a>受影响的 API

<xref:Microsoft.AspNetCore.StaticFiles.FileExtensionContentTypeProvider?displayProperty=nameWithType>

<!--

#### Affected APIs

`T:Microsoft.AspNetCore.StaticFiles.FileExtensionContentTypeProvider`

-->
