---
title: Equivalenza dei contratti dati
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data contracts [WCF], equivalence
ms.assetid: f06f3c7e-c235-4ec1-b200-68142edf1ed1
ms.openlocfilehash: b96a32f5e11ed4808f8f35d02802afd1f48c3072
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84601322"
---
# <a name="data-contract-equivalence"></a>Equivalenza dei contratti dati
Perché un client possa inviare correttamente dati di un certo tipo a un servizio o perché un servizio possa inviare correttamente dati a un client, non è necessario che il tipo inviato sia presente nell'estremità ricevente. L'unico requisito è che i contratti dati di entrambi i tipi siano equivalenti. (A volte, non è necessaria un'equivalenza rigorosa, come descritto in [controllo delle versioni dei contratti dati](data-contract-versioning.md)).  
  
 Perché i contratti dati siano equivalenti devono avere lo stesso spazio dei nomi e lo stesso nome. Ogni membro dati su uno lato deve inoltre avere un membro dati equivalente sull'altro lato.  
  
 Perché i membri dati siano equivalenti devono avere lo stesso nome. Devono inoltre rappresentare lo stesso tipo di dati, che significa che i rispettivi contratti dati devono essere equivalenti.  
  
> [!NOTE]
> Sia per i nomi e gli spazi dei nomi dei contratti dati sia per i nomi dei membri dati viene fatta distinzione tra maiuscole e minuscole.  
  
 Per ulteriori informazioni sui nomi e sugli spazi dei nomi dei contratti dati, nonché sui nomi dei membri dati, vedere [nomi di contratto dati](data-contract-names.md).  
  
 Se sullo stesso lato (mittente o ricevitore) sono presenti due tipi e i contratti dati non sono equivalenti (ad esempio, hanno membri dati diversi), è necessario assegnare loro un nome e uno spazio dei nomi differenti. In caso contrario, è possibile che vengano generate eccezioni.  
  
 I contratti dati per i tipi seguenti sono equivalenti:  
  
 [!code-csharp[C_DataContractNames#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#5)]
 [!code-vb[C_DataContractNames#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#5)]  
  
## <a name="data-member-order-and-data-contract-equivalence"></a>Ordine dei membri dati ed equivalenza dei contratti dati  
 L'utilizzo della proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> della classe <xref:System.Runtime.Serialization.DataMemberAttribute> può influire sull'equivalenza dei contratti dati. Per essere equivalenti, i contratti dati devono avere membri disposti nello stesso ordine. L'ordine predefinito è quello alfabetico. Per ulteriori informazioni, vedere l' [ordine dei membri dati](data-member-order.md).  
  
 Il codice seguente, ad esempio, comporta contratti dati equivalenti.  
  
 [!code-csharp[C_DataContractNames#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#6)]
 [!code-vb[C_DataContractNames#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#6)]  
  
 Il codice seguente non comporta invece contratti dati equivalenti.  
  
 [!code-csharp[C_DataContractNames#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#7)]
 [!code-vb[C_DataContractNames#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#7)]  
  
## <a name="inheritance-interfaces-and-data-contract-equivalence"></a>Ereditarietà, interfacce ed equivalenza dei contratti dati  
 Quando viene determinata l'equivalenza, un contratto dati che eredita da un altro contratto dati viene trattato come se fosse un contratto dati che include tutti i membri dati del tipo di base. Tenere presente che l'ordine dei membri dati deve corrispondere e che i membri del tipo di base precedono nell'ordine i membri del tipo derivato. Inoltre, se due membri dati hanno lo stesso valore di ordine, come nell'esempio di codice seguente, l'ordinamento di questi membri dati è alfabetico. Per ulteriori informazioni, vedere l' [ordine dei membri dati](data-member-order.md).  
  
 Nell'esempio seguente il contratto dati per il tipo `Employee` è equivalente al contratto dati per il tipo `Worker`.  
  
 [!code-csharp[C_DataContractNames#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#8)]
 [!code-vb[C_DataContractNames#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#8)]  
  
 Quando vengono passati parametri e restituiti valori tra un client e un servizio, non è possibile inviare un contratto dati relativo a una classe di base se l'endpoint ricevente prevede un contratto dati relativo a una classe derivata. Questo comportamento è conforme ai principi di base della programmazione orientata a oggetti. Nell'esempio precedente, non è possibile inviare un oggetto di tipo `Person` quando `Employee` è previsto un oggetto.  
  
 Un contratto dati relativo a una classe derivata può essere inviato quando è previsto un contratto dati relativo a una classe di base soltanto se l'endpoint ricevente "riconosce" il tipo derivato usando la classe <xref:System.Runtime.Serialization.KnownTypeAttribute>. Per ulteriori informazioni, vedere [tipi noti del contratto dati](data-contract-known-types.md). Nell'esempio precedente un oggetto di tipo `Employee` può essere inviato se è previsto un oggetto di tipo `Person`, ma solo se il codice del ricevitore usa la classe <xref:System.Runtime.Serialization.KnownTypeAttribute> per includerlo nell'elenco dei tipi noti.  
  
 Quando vengono passati parametri e restituiti valori tra applicazioni, se il tipo previsto è un'interfaccia è come se fosse di tipo <xref:System.Object>. Poiché ogni tipo deriva in fondo da <xref:System.Object>, ogni contratto dati deriva in ultima istanza dal contratto dati relativo a <xref:System.Object>. Quando è prevista un'interfaccia è pertanto possibile passare qualsiasi tipo di contratto dati. Sono necessari passaggi aggiuntivi per lavorare correttamente con le interfacce. Per ulteriori informazioni, vedere [tipi noti del contratto dati](data-contract-known-types.md).  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- [Ordine dei membri dati](data-member-order.md)
- [Tipi conosciuti di contratto dati](data-contract-known-types.md)
- [Nomi di contratto dati](data-contract-names.md)
