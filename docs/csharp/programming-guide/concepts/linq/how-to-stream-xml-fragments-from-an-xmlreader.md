---
title: Come eseguire il flusso di frammenti XML da un XmlReader (C
ms.date: 07/20/2015
ms.assetid: 4a8f0e45-768a-42e2-bc5f-68bdf0e0a726
ms.openlocfilehash: f7914d33622518f983a685dd2e844a25fd3ca15f
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2020
ms.locfileid: "75714646"
---
# <a name="how-to-stream-xml-fragments-from-an-xmlreader-c"></a>Come eseguire il flusso di frammenti XML da un XmlReader (C

Quando è necessario elaborare file XML di grandi dimensioni, potrebbe risultare impossibile caricare in memoria l'intero albero XML. In questo argomento viene illustrato come generare il flusso di frammenti tramite <xref:System.Xml.XmlReader>.  
  
 Uno dei modi più efficaci per usare un oggetto <xref:System.Xml.XmlReader> per leggere oggetti <xref:System.Xml.Linq.XElement> consiste nello scrivere un metodo dell'asse personalizzato. Un metodo dell'asse restituisce in genere una raccolta, ad esempio <xref:System.Collections.Generic.IEnumerable%601> di <xref:System.Xml.Linq.XElement>, come illustrato nell'esempio di questo argomento. Nel metodo dell'asse personalizzato, dopo avere creato il frammento XML chiamando il metodo <xref:System.Xml.Linq.XNode.ReadFrom%2A>, restituire la raccolta usando `yield return`. In questo modo si fornisce la semantica di esecuzione posticipata al metodo dell'asse personalizzato.  
  
 Quando si crea un albero XML da un oggetto <xref:System.Xml.XmlReader>, <xref:System.Xml.XmlReader> deve essere posizionato su un elemento. Il metodo <xref:System.Xml.Linq.XNode.ReadFrom%2A> restituisce risultati solo dopo aver letto il tag di chiusura dell'elemento.  
  
 Se si desidera creare un albero parziale, è possibile creare un'istanza di <xref:System.Xml.XmlReader>, posizionare il lettore sul nodo da convertire in un albero <xref:System.Xml.Linq.XElement> e quindi creare l'oggetto <xref:System.Xml.Linq.XElement>.  
  
L'argomento [Come trasmettere frammenti XML con accesso alle informazioni di intestazione (C )](./how-to-stream-xml-fragments-with-access-to-header-information.md) contiene informazioni e un esempio su come trasmettere un documento più complesso.
  
 L'argomento Come eseguire la [trasformazione di flusso di documenti XML di grandi dimensioni (C )](./how-to-perform-streaming-transform-of-large-xml-documents.md) contiene un esempio di utilizzo di LINQ to XMLLINQ to XML per trasformare documenti XML di grandi dimensioni mantenendo un footprint di memoria ridotto.  
  
## <a name="example"></a>Esempio  
 In questo esempio viene creato un metodo dell'asse personalizzato. È possibile eseguire una query utilizzando una query LINQ. Il metodo dell'asse personalizzato `StreamRootChildDoc` è progettato specificamente per leggere un documento contenente un elemento `Child` ripetuto.  
  
```csharp  
static IEnumerable<XElement> StreamRootChildDoc(StringReader stringReader)  
{  
    using (XmlReader reader = XmlReader.Create(stringReader))  
    {  
        reader.MoveToContent();  
        // Parse the file and display each of the nodes.  
        while (reader.Read())  
        {  
            switch (reader.NodeType)  
            {  
                case XmlNodeType.Element:  
                    if (reader.Name == "Child") {  
                        XElement el = XElement.ReadFrom(reader) as XElement;  
                        if (el != null)  
                            yield return el;  
                    }  
                    break;  
            }  
        }  
    }  
}  
  
static void Main(string[] args)  
{  
    string markup = @"<Root>  
      <Child Key=""01"">  
        <GrandChild>aaa</GrandChild>  
      </Child>  
      <Child Key=""02"">  
        <GrandChild>bbb</GrandChild>  
      </Child>  
      <Child Key=""03"">  
        <GrandChild>ccc</GrandChild>  
      </Child>  
    </Root>";  
  
    IEnumerable<string> grandChildData =  
        from el in StreamRootChildDoc(new StringReader(markup))  
        where (int)el.Attribute("Key") > 1  
        select (string)el.Element("GrandChild");  
  
    foreach (string str in grandChildData) {  
        Console.WriteLine(str);  
    }  
}  
```  
  
 Nell'esempio viene prodotto l'output seguente:  
  
```output  
bbb  
ccc  
```  
  
 In questo esempio il documento di origine è molto piccolo. Tuttavia, anche contenesse milioni di elementi `Child`, il footprint di memoria di questo esempio sarebbe comunque ridotto.  
