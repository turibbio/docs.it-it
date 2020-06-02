---
title: Scrittura di attributi personalizzati
ms.date: 07/17/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- multiple attribute instances
- AttributeTargets enumeration
- attributes [.NET Framework], custom
- AllowMultiple property
- custom attributes
- AttributeUsageAttribute class, custom attributes
- Inherited property
- attribute classes, declaring
ms.assetid: 97216f69-bde8-49fd-ac40-f18c500ef5dc
ms.openlocfilehash: d05df02bfc75e9aeb2c583a831bcee8b7b971206
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84276131"
---
# <a name="writing-custom-attributes"></a>Scrittura di attributi personalizzati
Per progettare attributi personalizzati, non è necessario apprendere molti nuovi concetti. Se si ha familiarità con la programmazione orientata agli oggetti e si è in grado di progettare le classi, si ha già gran parte delle conoscenze necessarie. Gli attributi personalizzati sono essenzialmente classi tradizionali che derivano direttamente o indirettamente da <xref:System.Attribute?displayProperty=nameWithType>. Analogamente alle classi tradizionali, gli attributi personalizzati contengono metodi che archiviano e recuperano dati.  
  
 I passaggi fondamentali per progettare classi di attributi personalizzati sono i seguenti:  
  
- [Applicazione di AttributeUsageAttribute](#applying-the-attributeusageattribute)  
  
- [Dichiarazione della classe di attributi](#declaring-the-attribute-class)  
  
- [Dichiarazione di costruttori](#declaring-constructors)  
  
- [Dichiarazione delle proprietà](#declaring-properties)  
  
 Questa sezione illustra ognuno di questi passaggi e termina con [esempio di attributo personalizzato](#custom-attribute-example).  
  
## <a name="applying-the-attributeusageattribute"></a>Applicazione di AttributeUsageAttribute  
 La dichiarazione di attributo personalizzato inizia con <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>, che definisce alcune delle caratteristiche chiave della classe di attributi. Ad esempio, è possibile specificare se l'attributo può essere ereditato da altre classi o gli elementi a cui può essere applicato l'attributo. Il frammento di codice seguente illustra come usare <xref:System.AttributeUsageAttribute>.  
  
 [!code-cpp[Conceptual.Attributes.Usage#5](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#5)]
 [!code-csharp[Conceptual.Attributes.Usage#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#5)]
 [!code-vb[Conceptual.Attributes.Usage#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#5)]  
  
 L'oggetto <xref:System.AttributeUsageAttribute> ha tre membri importanti per la creazione di attributi personalizzati: [AttributeTargets](#attributetargets-member), [Inherited](#inherited-property)e [AllowMultiple](#allowmultiple-property).  
  
### <a name="attributetargets-member"></a>Membro AttributeTargets  
 Nell'esempio precedente è specificato <xref:System.AttributeTargets.All?displayProperty=nameWithType>, a indicare che questo attributo può essere applicato a tutti gli elementi di programma. In alternativa, è possibile specificare <xref:System.AttributeTargets.Class?displayProperty=nameWithType>, a indicare che l'attributo può essere applicato solo a una classe, oppure <xref:System.AttributeTargets.Method?displayProperty=nameWithType>, a indicare che l'attributo può essere applicato solo a un metodo. Questa procedura può essere usata per contrassegnare tutti gli elementi di programma per la descrizione mediante un attributo personalizzato.  
  
 È anche possibile passare più valori <xref:System.AttributeTargets>. Il frammento di codice seguente specifica che un attributo personalizzato può essere applicato a qualsiasi classe o metodo.  
  
 [!code-cpp[Conceptual.Attributes.Usage#6](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#6)]
 [!code-csharp[Conceptual.Attributes.Usage#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#6)]
 [!code-vb[Conceptual.Attributes.Usage#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#6)]  
  
### <a name="inherited-property"></a>Proprietà Inherited  
 La proprietà <xref:System.AttributeUsageAttribute.Inherited%2A?displayProperty=nameWithType> indica se l'attributo può essere ereditato da classi derivate dalle classi a cui è applicato l'attributo. Questa proprietà accetta un flag `true` (valore predefinito) o `false`. Nell'esempio seguente `MyAttribute` ha il valore predefinito `true` per <xref:System.AttributeUsageAttribute.Inherited%2A> mentre per `YourAttribute` il valore di <xref:System.AttributeUsageAttribute.Inherited%2A> è `false`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#7](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#7)]
 [!code-csharp[Conceptual.Attributes.Usage#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#7)]
 [!code-vb[Conceptual.Attributes.Usage#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#7)]  
  
 I due attributi vengono quindi applicati a un metodo nella classe base `MyClass`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#9](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#9)]
 [!code-csharp[Conceptual.Attributes.Usage#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#9)]
 [!code-vb[Conceptual.Attributes.Usage#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#9)]  
  
 Infine, la classe `YourClass` viene ereditata dalla classe base `MyClass`. Il metodo `MyMethod` mostra `MyAttribute`, ma non `YourAttribute`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#10](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#10)]
 [!code-csharp[Conceptual.Attributes.Usage#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#10)]
 [!code-vb[Conceptual.Attributes.Usage#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#10)]  
  
### <a name="allowmultiple-property"></a>Proprietà AllowMultiple  
 La proprietà <xref:System.AttributeUsageAttribute.AllowMultiple%2A?displayProperty=nameWithType> indica se in un elemento possono esistere istanze multiple dell'attributo. Se è impostata su `true`, sono consentite istanze multiple. Se invece è impostata su `false` (valore predefinito), è consentita solo un'istanza.  
  
 Nell'esempio seguente `MyAttribute` ha il valore predefinito `false` per <xref:System.AttributeUsageAttribute.AllowMultiple%2A> mentre il valore di `YourAttribute` è `true`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#11](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#11)]
 [!code-csharp[Conceptual.Attributes.Usage#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#11)]
 [!code-vb[Conceptual.Attributes.Usage#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#11)]  
  
 Quando vengono applicate istanze multiple di questi attributi, `MyAttribute` genera un errore del compilatore. L'esempio di codice seguente mostra l'uso valido di `YourAttribute` e l'uso non valido di `MyAttribute`.  
  
 [!code-cpp[Conceptual.Attributes.Usage#13](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#13)]
 [!code-csharp[Conceptual.Attributes.Usage#13](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#13)]
 [!code-vb[Conceptual.Attributes.Usage#13](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#13)]  
  
 Se le proprietà <xref:System.AttributeUsageAttribute.AllowMultiple%2A> e <xref:System.AttributeUsageAttribute.Inherited%2A> sono entrambe impostate su `true`, una classe ereditata da un'altra classe può ereditare un attributo e determinare l'applicazione di un'altra istanza dello stesso attributo nella stessa classe figlio. Se la proprietà <xref:System.AttributeUsageAttribute.AllowMultiple%2A> è impostata su `false`, i valori degli attributi nella classe padre verranno sovrascritti dalle nuove istanze dello stesso attributo nella classe figlio.  
  
## <a name="declaring-the-attribute-class"></a>Dichiarazione della classe di attributi  
 Dopo avere applicato <xref:System.AttributeUsageAttribute>, è possibile iniziare a definire le specifiche dell'attributo. La dichiarazione di una classe di attributi è simile alla dichiarazione di una classe tradizionale, come dimostrato dal codice seguente.  
  
 [!code-cpp[Conceptual.Attributes.Usage#14](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#14)]
 [!code-csharp[Conceptual.Attributes.Usage#14](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#14)]
 [!code-vb[Conceptual.Attributes.Usage#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#14)]  
  
 Questa definizione di attributo dimostra quanto segue:  
  
- Le classi di attributi devono essere dichiarate come classi pubbliche.  
  
- Per convenzione, il nome della classe di attributi termina con la parola **Attribute**. Sebbene non sia obbligatorio, questa convenzione è consigliabile per migliorare la leggibilità. Quando l'attributo è applicato, l'inclusione della parola Attribute è facoltativa.  
  
- Tutte le classi di attributi devono ereditare direttamente o indirettamente da <xref:System.Attribute?displayProperty=nameWithType>.  
  
- In Microsoft Visual Basic tutte le classi di attributi personalizzati devono avere l'attributo <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>.  
  
## <a name="declaring-constructors"></a>Dichiarazione dei costruttori  
 Gli attributi, così come le classi tradizionali, vengono inizializzati con costruttori. Il frammento di codice seguente illustra un tipico costruttore di attributi. Questo costruttore pubblico accetta un parametro e imposta una variabile membro sul valore del parametro.  
  
 [!code-cpp[Conceptual.Attributes.Usage#15](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#15)]
 [!code-csharp[Conceptual.Attributes.Usage#15](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#15)]
 [!code-vb[Conceptual.Attributes.Usage#15](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#15)]  
  
 È possibile eseguire l'overload del costruttore per supportare diverse combinazioni di valori. Se si definisce anche una [proprietà](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)) per la classe di attributi personalizzati, è possibile usare una combinazione di parametri denominati e posizionali quando si inizializza l'attributo. In genere, tutti i parametri obbligatori vengono definiti come posizionali e tutti i parametri facoltativi come denominati In questo caso, l'attributo non può essere inizializzato senza il parametro obbligatorio. Tutti gli altri parametri sono facoltativi. Si noti che, in Visual Basic, i costruttori di una classe Attribute non devono usare un argomento ParamArray.  
  
 L'esempio di codice seguente illustra come applicare un attributo che usa il costruttore precedente mediante i parametri obbligatori e facoltativi. Presuppone che l'attributo abbia un valore booleano obbligatorio e una proprietà stringa facoltativa.  
  
 [!code-cpp[Conceptual.Attributes.Usage#17](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#17)]
 [!code-csharp[Conceptual.Attributes.Usage#17](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#17)]
 [!code-vb[Conceptual.Attributes.Usage#17](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#17)]  
  
## <a name="declaring-properties"></a>Dichiarazione delle proprietà  
 Se si vuole definire un parametro denominato o fornire un modo semplice per restituire i valori archiviati dall'attributo, dichiarare una [proprietà](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2013/65zdfbdt(v=vs.120)). Le proprietà dell'attributo devono essere dichiarate come entità pubbliche con una descrizione del tipo di dati che verrà restituito. Definire la variabile che conterrà il valore della proprietà e associarla ai metodi **get** e **set** . L'esempio di codice seguente illustra come implementare una semplice proprietà nell'attributo.  
  
 [!code-cpp[Conceptual.Attributes.Usage#16](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#16)]
 [!code-csharp[Conceptual.Attributes.Usage#16](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#16)]
 [!code-vb[Conceptual.Attributes.Usage#16](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#16)]  
  
## <a name="custom-attribute-example"></a>esempio di attributo personalizzato  
 Questa sezione include le informazioni precedenti e illustra come progettare un semplice attributo che documenta le informazioni sull'autore di una sezione di codice. L'attributo in questo esempio archivia il nome e il livello del programmatore e specifica se il codice è stato rivisto. Usa tre variabili private per archiviare i valori effettivi da salvare. Ogni variabile è rappresentata da una proprietà pubblica che ottiene e imposta i valori. Infine, il costruttore è definito con due parametri obbligatori.  
  
 [!code-cpp[Conceptual.Attributes.Usage#4](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#4)]
 [!code-csharp[Conceptual.Attributes.Usage#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#4)]
 [!code-vb[Conceptual.Attributes.Usage#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#4)]  
  
 Questo attributo può essere applicato usando il nome completo `DeveloperAttribute`oppure il nome abbreviato `Developer`in uno dei modi seguenti.  
  
 [!code-cpp[Conceptual.Attributes.Usage#12](../../../samples/snippets/cpp/VS_Snippets_CLR/conceptual.attributes.usage/cpp/source2.cpp#12)]
 [!code-csharp[Conceptual.Attributes.Usage#12](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.attributes.usage/cs/source2.cs#12)]
 [!code-vb[Conceptual.Attributes.Usage#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.attributes.usage/vb/source2.vb#12)]  
  
 Il primo esempio mostra l'attributo applicato solo con i parametri denominati obbligatori, mentre il secondo esempio mostra l'attributo applicato con i parametri sia obbligatori che facoltativi.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Attribute?displayProperty=nameWithType>
- <xref:System.AttributeUsageAttribute?displayProperty=nameWithType>
- [Attributi](index.md)
