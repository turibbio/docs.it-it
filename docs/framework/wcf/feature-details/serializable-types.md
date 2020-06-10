---
title: Tipi serializzabili
ms.date: 03/30/2017
ms.assetid: f1c8539a-6a79-4413-b294-896f0957b2cd
ms.openlocfilehash: e65fcb93c5c36bb289b825cef58b3adc6f5155f5
ms.sourcegitcommit: cdb295dd1db589ce5169ac9ff096f01fd0c2da9d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84586104"
---
# <a name="serializable-types"></a>Tipi serializzabili
Per impostazione predefinita, <xref:System.Runtime.Serialization.DataContractSerializer> serializza tutti i tipi visibili pubblicamente. Vengono serializzati i campi e le proprietà di lettura/scrittura pubblici del tipo.  
  
 È possibile modificare il comportamento predefinito applicando gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> ai tipi e ai membri. Questa funzionalità può essere utile quando sono presenti tipi non controllati dall'utente e non modificabili per aggiungere attributi. <xref:System.Runtime.Serialization.DataContractSerializer> riconosce tali tipi non contrassegnati.  
  
## <a name="serialization-defaults"></a>Impostazioni predefinite di serializzazione  
 È possibile applicare gli attributi <xref:System.Runtime.Serialization.DataContractAttribute> e <xref:System.Runtime.Serialization.DataMemberAttribute> per controllare in modo esplicito o personalizzare la serializzazione di tipi e membri. È inoltre possibile applicare tali attributi ai campi privati. Tuttavia, anche i tipi non contrassegnati con questi attributi vengono serializzati e deserializzati. Vengono applicate le regole e le eccezioni seguenti:  
  
- Tramite <xref:System.Runtime.Serialization.DataContractSerializer> viene dedotto un contratto dati dai tipi senza attributi usando le proprietà predefinite dei tipi appena creati.  
  
- Vengono serializzati tutti i campi e le proprietà pubblici con metodi `get` e `set` pubblici, a meno che non venga applicato l'attributo <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> a tale membro.  
  
- La semantica di serializzazione è simile a quella di <xref:System.Xml.Serialization.XmlSerializer>.  
  
- Nei tipi non contrassegnati vengono serializzati solo i tipi pubblici con costruttori privi di parametri. L'eccezione a questa regola è <xref:System.Runtime.Serialization.ExtensionDataObject> usato con l'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject>.  
  
- I campi di sola lettura, le proprietà senza un metodo `get` o `set` e quelle con metodi `set` o `get` interni o privati non vengono serializzati. Tali proprietà vengono ignorate e non viene generata alcuna eccezione, salvo nel caso di raccolte con sola funzione di accesso get.  
  
- Gli attributi <xref:System.Xml.Serialization.XmlSerializer> (ad esempio `XmlElement`, `XmlAttribute`, `XmlIgnore`, `XmlInclude` e così via) vengono ignorati.  
  
- Se non si applica l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> a un tipo specificato, il serializzatore ignora qualsiasi membro del tipo a cui viene applicato l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute>.  
  
- La proprietà <xref:System.Runtime.Serialization.DataContractSerializer.KnownTypes%2A> è supportata nei tipi non contrassegnati con l'attributo <xref:System.Runtime.Serialization.DataContractAttribute>. È compreso il supporto per l'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute> nei tipi non contrassegnati.  
  
- Per rifiutare esplicitamente il processo di serializzazione per membri, proprietà o campi pubblici, applicare l'attributo <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> a tale membro.  
  
## <a name="inheritance"></a>Ereditarietà  
 I tipi non contrassegnati (tipi senza l'attributo <xref:System.Runtime.Serialization.DataContractAttribute>) possono ereditare da tipi che dispongono di tale attributo, ma l'operazione opposta non è consentita, pertanto i tipi con l'attributo non possono ereditare da tipi non contrassegnati. Questa regola viene applicata principalmente per garantire la compatibilità con il codice scritto nelle versioni precedenti di .NET Framework.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute>
- <xref:System.Runtime.Serialization.DataContractAttribute>
- <xref:System.Runtime.Serialization.DataMemberAttribute>
- <xref:System.Xml.Serialization.XmlSerializer>
- [Types Supported by the Data Contract Serializer](types-supported-by-the-data-contract-serializer.md)
