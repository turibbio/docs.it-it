---
title: 'Procedura: creare attività precalcolate'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- tasks, creating pre-computed
ms.assetid: a73eafa2-1f49-4106-a19e-997186029b58
ms.openlocfilehash: 88f0782380d21858bc5dd0fc0fbf63bbf85403b8
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84289993"
---
# <a name="how-to-create-pre-computed-tasks"></a>Procedura: creare attività precalcolate
In questo documento viene descritto come utilizzare il metodo <xref:System.Threading.Tasks.Task.FromResult%2A?displayProperty=nameWithType> per recuperare i risultati di operazioni di download asincrone contenute in una cache. Tramite il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> viene restituito un oggetto <xref:System.Threading.Tasks.Task%601> finito contenente il valore fornito come relativa proprietà <xref:System.Threading.Tasks.Task%601.Result%2A>. Questo metodo è utile quando si esegue un'operazione asincrona che restituisce un oggetto <xref:System.Threading.Tasks.Task%601> e il risultato di tale oggetto <xref:System.Threading.Tasks.Task%601> è già calcolato.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente vengono scaricate stringhe dal Web. Viene definito il metodo `DownloadStringAsync`. Tramite questo metodo vengono scaricate stringhe dal Web in modo asincrono. In questo esempio viene inoltre utilizzato un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> per memorizzare nella cache i risultati di operazioni precedenti. Se l'indirizzo di input viene mantenuto in questa cache, in `DownloadStringAsync` viene utilizzato il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> per produrre un oggetto <xref:System.Threading.Tasks.Task%601> con il contenuto in corrispondenza dell'indirizzo in questione. In caso contrario, tramite `DownloadStringAsync` viene scaricato il file dal Web e viene aggiunto il risultato alla cache.  
  
 [!code-csharp[TPL_CachedDownloads#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_cacheddownloads/cs/cacheddownloads.cs#1)]
 [!code-vb[TPL_CachedDownloads#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_cacheddownloads/vb/cacheddownloads.vb#1)]  
  
 In questo esempio viene calcolato il tempo necessario per scaricare più stringhe due volte. Per il secondo set di operazioni di download deve essere impiegato meno tempo del primo poiché i risultati sono contenuti nella cache. Il metodo <xref:System.Threading.Tasks.Task.FromResult%2A> consente al metodo `DownloadStringAsync` di creare oggetti di <xref:System.Threading.Tasks.Task%601> contenenti questi risultati precalcolati.  
  
## <a name="see-also"></a>Vedere anche

- [Programmazione asincrona basata su attività](task-based-asynchronous-programming.md)
