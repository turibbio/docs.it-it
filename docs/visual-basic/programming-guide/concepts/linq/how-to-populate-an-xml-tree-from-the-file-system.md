---
title: 'Procedura: Popolare un albero XML dal file system'
ms.date: 07/20/2015
ms.assetid: 34eec79e-7945-4ba8-9f74-d05bb8ec67f6
ms.openlocfilehash: a3898b63f24bb87ab5e0de47685c36d61f09250b
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84396532"
---
# <a name="how-to-populate-an-xml-tree-from-the-file-system-visual-basic"></a><span data-ttu-id="0759d-102">Procedura: popolare un albero XML dal file System (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0759d-102">How to: Populate an XML Tree from the File System (Visual Basic)</span></span>
<span data-ttu-id="0759d-103">Un'applicazione utile e comune degli alberi XML è data dall'utilizzo come archivio dati nome/valore gerarchico.</span><span class="sxs-lookup"><span data-stu-id="0759d-103">A common and useful application of XML trees is as a hierarchical name/value data store.</span></span> <span data-ttu-id="0759d-104">È possibile popolare un albero XML con dati gerarchici e quindi eseguirvi query, trasformarla e, se necessario, serializzarla.</span><span class="sxs-lookup"><span data-stu-id="0759d-104">You can populate an XML tree with hierarchical data, and then query it, transform it, and if necessary, serialize it.</span></span> <span data-ttu-id="0759d-105">In questo scenario di utilizzo molte delle caratteristiche semantiche specifiche di XML, quali gli spazi dei nomi e il comportamento degli spazi vuoti, non sono rilevanti.</span><span class="sxs-lookup"><span data-stu-id="0759d-105">In this usage scenario, many of the XML specific semantics, such as namespaces and white space behavior, are not important.</span></span> <span data-ttu-id="0759d-106">L'albero XML viene invece usato come piccolo database gerarchico in memoria per singolo utente.</span><span class="sxs-lookup"><span data-stu-id="0759d-106">Instead, you are using the XML tree as a small, in memory, single user hierarchical database.</span></span>  
  
## <a name="example"></a><span data-ttu-id="0759d-107">Esempio</span><span class="sxs-lookup"><span data-stu-id="0759d-107">Example</span></span>  
 <span data-ttu-id="0759d-108">Nell'esempio seguente un albero XML viene popolato dal file system locale tramite la ricorsione.</span><span class="sxs-lookup"><span data-stu-id="0759d-108">The following example populates an XML tree from the local file system using recursion.</span></span> <span data-ttu-id="0759d-109">Viene quindi eseguita una query sull'albero per calcolare le dimensioni totali di tutti i file dell'albero.</span><span class="sxs-lookup"><span data-stu-id="0759d-109">It then queries the tree, calculating the total of the sizes of all files in the tree.</span></span>  
  
```vb  
Module Module1  
    Function CreateFileSystemXmlTree(ByVal source As String) As XElement  
        Dim di As DirectoryInfo = New DirectoryInfo(source)  
        Return <Dir Name=<%= di.Name %>>  
                   <%= From d In Directory.GetDirectories(source) _  
                       Select CreateFileSystemXmlTree(d) %>  
                   <%= From fi In di.GetFiles() _  
                       Select <File>  
                                  <Name><%= fi.Name %></Name>  
                                  <Length><%= fi.Length %></Length>  
                              </File> %>  
               </Dir>  
    End Function  
  
    Sub Main()  
        Dim fileSystemTree As XElement = CreateFileSystemXmlTree("C:/Tmp")  
        Console.WriteLine(fileSystemTree)  
        Console.WriteLine("------")  
        Dim totalFileSize As Long = _  
            ( _  
                From f In fileSystemTree...<File> _  
                Select CLng(f.<Length>(0)) _  
            ).Sum()  
        Console.WriteLine("Total File Size:{0}", totalFileSize)  
    End Sub  
End Module  
```  
  
 <span data-ttu-id="0759d-110">In questo esempio viene prodotto un output simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="0759d-110">This example produces output similar to the following:</span></span>  
  
```xml  
<Dir Name="Tmp">  
  <Dir Name="ConsoleApplication1">  
    <Dir Name="bin">  
      <Dir Name="Debug">  
        <File>  
          <Name>ConsoleApplication1.exe</Name>  
          <Length>4608</Length>  
        </File>  
        <File>  
          <Name>ConsoleApplication1.pdb</Name>  
          <Length>11776</Length>  
        </File>  
        <File>  
          <Name>ConsoleApplication1.vshost.exe</Name>  
          <Length>9568</Length>  
        </File>  
        <File>  
          <Name>ConsoleApplication1.vshost.exe.manifest</Name>  
          <Length>473</Length>  
        </File>  
      </Dir>  
    </Dir>  
    <Dir Name="obj">  
      <Dir Name="Debug">  
        <Dir Name="TempPE" />  
        <File>  
          <Name>ConsoleApplication1.csproj.FileListAbsolute.txt</Name>  
          <Length>322</Length>  
        </File>  
        <File>  
          <Name>ConsoleApplication1.exe</Name>  
          <Length>4608</Length>  
        </File>  
        <File>  
          <Name>ConsoleApplication1.pdb</Name>  
          <Length>11776</Length>  
        </File>  
      </Dir>  
    </Dir>  
    <Dir Name="Properties">  
      <File>  
        <Name>AssemblyInfo.cs</Name>  
        <Length>1454</Length>  
      </File>  
    </Dir>  
    <File>  
      <Name>ConsoleApplication1.csproj</Name>  
      <Length>2546</Length>  
    </File>  
    <File>  
      <Name>ConsoleApplication1.sln</Name>  
      <Length>937</Length>  
    </File>  
    <File>  
      <Name>ConsoleApplication1.suo</Name>  
      <Length>10752</Length>  
    </File>  
    <File>  
      <Name>Program.cs</Name>  
      <Length>269</Length>  
    </File>  
  </Dir>  
</Dir>  
------  
Total File Size:59089  
```  
  
## <a name="see-also"></a><span data-ttu-id="0759d-111">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="0759d-111">See also</span></span>

- [<span data-ttu-id="0759d-112">Tecniche di query avanzate (LINQ to XML) (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="0759d-112">Advanced Query Techniques (LINQ to XML) (Visual Basic)</span></span>](advanced-query-techniques-linq-to-xml.md)
