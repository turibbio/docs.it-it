---
title: Serializzazione e metadati
ms.date: 03/30/2017
ms.assetid: 619ecf1c-1ca5-4d66-8934-62fe7aad78c6
ms.openlocfilehash: cc9adf0e6627ef3190e74fea5d4f0f3afd581811
ms.sourcegitcommit: b16c00371ea06398859ecd157defc81301c9070f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/06/2020
ms.locfileid: "81389223"
---
# <a name="serialization-and-metadata"></a>Serializzazione e metadati

Se l'applicazione serializza e deserializza oggetti, potrebbe essere necessario aggiungere voci al file di direttive di runtime (rd.xml) per assicurarsi che i metadati necessari siano presenti in fase di esecuzione. Esistono due categorie di serializzatori e ciascuna richiede una gestione differente nel file di direttive di runtime:  
  
- Serializzatori di terze parti basati su reflection. Richiedono modifiche al file di direttive di runtime e sono descritti nella sezione successiva.  
  
- Serializzatori non basati su Reflection presenti nella libreria di classi .NET Framework. Possono richiedere modifiche al file di direttive di runtime e sono descritti nella sezione [Serializzatori Microsoft](#Microsoft).  
  
<a name="ThirdParty"></a>
## <a name="third-party-serializers"></a>Serializzatori di terze parti

 I serializzatori di terze parti, incluso Newtonsoft.JSON, sono in genere basati su reflection. Dato un oggetto binario di grandi dimensioni (BLOB) di dati serializzati, i campi dati vengono assegnati a un tipo concreto cercando i campi del tipo di destinazione per nome. Come minimo, l'uso di queste librerie causa eccezioni [MissingMetadataException](missingmetadataexception-class-net-native.md) per ogni oggetto <xref:System.Type> che si prova a serializzare o deserializzare in una raccolta `List<Type>`.  
  
 Il modo più semplice per risolvere i problemi causati da metadati mancanti per questi serializzatori è raccogliere i tipi che verranno usati nella serializzazione in un singolo spazio dei nomi (ad esempio `App.Models`) e applicarvi una direttiva metadati `Serialize`:  
  
```xml  
<Namespace Name="App.Models" Serialize="Required PublicAndInternal" />  
```  
  
 Per informazioni sulla sintassi usata nell'esempio, vedere [ \<Namespace> elemento](namespace-element-net-native.md).  
  
<a name="Microsoft"></a>
## <a name="microsoft-serializers"></a>Serializzatori Microsoft

 Nonostante le classi <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> e <xref:System.Xml.Serialization.XmlSerializer> non si basino sulla reflection, richiedono che il codice venga generato in base all'oggetto da serializzare o deserializzare. I costruttori di overload per ciascun serializzatore includono un parametro <xref:System.Type> che specifica il tipo da serializzare o deserializzare. Il modo in cui si specifica che il tipo nel codice definisce l'azione che l'utente deve accettare, come illustrato nelle due sezioni.  
  
### <a name="typeof-used-in-the-constructor"></a>typeof usato nel costruttore

 Se si chiama un costruttore di queste classi di serializzazione e si include l'operatore [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) di C# nella chiamata al metodo, **non è necessario eseguire alcuna operazione aggiuntiva**. Ad esempio, in ognuna delle seguenti chiamate a un costruttore di classe di serializzazione, la parola chiave `typeof` viene usata come parte dell'espressione passata al costruttore.  
  
 [!code-csharp[ProjectN#5](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#5)]  
  
 Il compilatore .NET Native gestirà automaticamente il codice.  
  
### <a name="typeof-used-outside-the-constructor"></a>typeof usato fuori dal costruttore

 Se si chiama un costruttore di queste classi di serializzazione e si usa l'operatore [typeof](../../csharp/language-reference/operators/type-testing-and-cast.md#typeof-operator) di C# al di fuori dell'espressione fornita al parametro del costruttore <xref:System.Type> , come nel codice seguente, il compilatore .NET native non può risolvere il tipo:  
  
 [!code-csharp[ProjectN#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#6)]  
  
 In questo caso, è necessario specificare il tipo nel file di direttive di runtime con l'aggiunta di una voce simile alla seguente:  
  
```xml  
<Type Name="DataSet" Browse="Required Public" />  
```  
  
 Analogamente, se si chiama un costruttore come <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29> e si fornisce una matrice di <xref:System.Type> oggetti aggiuntivi da serializzare, come nel codice seguente, il compilatore .NET native non può risolvere questi tipi.  
  
 [!code-csharp[ProjectN#7](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/serialize1.cs#7)]  
  
Aggiungere voci come le seguenti per ogni tipo al file di direttive di runtime:  
  
```xml  
<Type Name="t" Browse="Required Public" />  
```  
  
Per informazioni sulla sintassi usata nell'esempio, vedere [ \<Type> elemento](type-element-net-native.md).  
  
## <a name="see-also"></a>Vedi anche

- [Riferimento a file di configurazione di direttive di runtime (rd.xml)](runtime-directives-rd-xml-configuration-file-reference.md)
- [Elementi direttiva di runtime](runtime-directive-elements.md)
- [\<Type>Elemento](type-element-net-native.md)
- [\<Namespace>Elemento](namespace-element-net-native.md)
