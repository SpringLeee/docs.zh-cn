---
title: 如何使用 XmlWriter 填充 XML 树 (LINQ to XML) (C#)
ms.date: 07/20/2015
ms.assetid: cd5674d1-5c54-4efc-ba68-e23b2875295f
ms.openlocfilehash: f48843af403f2ee0e6d2850deab009a143f55dc7
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2020
ms.locfileid: "75345763"
---
# <a name="how-to-populate-an-xml-tree-with-an-xmlwriter-linq-to-xml-c"></a>如何使用 XmlWriter 填充 XML 树 (LINQ to XML) (C#)
填充 XML 树的一种方式是使用 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 创建一个 <xref:System.Xml.XmlWriter>，然后写入 <xref:System.Xml.XmlWriter>。 XML 树将用写入到 <xref:System.Xml.XmlWriter> 的所有节点进行填充。  
  
 在与预期会向 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)] 写入数据的另一个类（如 <xref:System.Xml.XmlWriter>）一起使用 <xref:System.Xml.Xsl.XslCompiledTransform> 时，通常应使用此方法。  
  
## <a name="example"></a>示例  
 <xref:System.Xml.Linq.XContainer.CreateWriter%2A> 可能在调用 XSLT 转换时使用。 本示例创建一个 XML 树，从该 XML 树创建一个 <xref:System.Xml.XmlReader>，创建一个新文档，然后创建要写入到新文档的 <xref:System.Xml.XmlWriter>。 示例然后调用 XSLT 转换，传入 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter>。 在转换成功完成后，使用转换的结果，填充新的 XML 树。  
  
```csharp  
string xslMarkup = @"<?xml version='1.0'?>  
<xsl:stylesheet xmlns:xsl='http://www.w3.org/1999/XSL/Transform' version='1.0'>  
    <xsl:template match='/Parent'>  
        <Root>  
            <C1>  
            <xsl:value-of select='Child1'/>  
            </C1>  
            <C2>  
            <xsl:value-of select='Child2'/>  
            </C2>  
        </Root>  
    </xsl:template>  
</xsl:stylesheet>";  
  
XDocument xmlTree = new XDocument(  
    new XElement("Parent",  
        new XElement("Child1", "Child1 data"),  
        new XElement("Child2", "Child2 data")  
    )  
);  
  
XDocument newTree = new XDocument();  
using (XmlWriter writer = newTree.CreateWriter())  
{  
    // Load the style sheet.  
    XslCompiledTransform xslt = new XslCompiledTransform();  
    xslt.Load(XmlReader.Create(new StringReader(xslMarkup)));  
  
    // Execute the transformation and output the results to a writer.  
    xslt.Transform(xmlTree.CreateReader(), writer);  
}  
  
Console.WriteLine(newTree);  
```  
  
 该示例产生下面的输出：  
  
```xml  
<Root>  
  <C1>Child1 data</C1>  
  <C2>Child2 data</C2>  
</Root>  
```  
  
## <a name="see-also"></a>另请参阅

- <xref:System.Xml.Linq.XContainer.CreateWriter%2A>
- <xref:System.Xml.XmlWriter>
- <xref:System.Xml.Xsl.XslCompiledTransform>
- [创建 XML 树 (C#)](./linq-to-xml-overview.md)
