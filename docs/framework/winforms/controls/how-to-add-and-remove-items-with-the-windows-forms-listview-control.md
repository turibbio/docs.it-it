---
title: Aggiungere e rimuovere elementi con il controllo ListView
description: Informazioni su come aggiungere e rimuovere un elemento con il controllo ListView di Windows Forms specificando l'elemento e assegnando loro le proprietà.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ListView control [Windows Forms], populating
- list views [Windows Forms], adding list items
- ListView control [Windows Forms], adding list items
ms.assetid: 1b35a80a-edd8-495f-a807-a28c4aae52c6
ms.openlocfilehash: db374ded69bcbd93527381d75a8ff751a1c9abe6
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618090"
---
# <a name="how-to-add-and-remove-items-with-the-windows-forms-listview-control"></a>Procedura: aggiungere e rimuovere elementi tramite il controllo ListView di Windows Form
Il processo di aggiunta di un elemento a un <xref:System.Windows.Forms.ListView> controllo Windows Forms è costituito principalmente dalla specifica dell'elemento e dall'assegnazione di proprietà. L'aggiunta o la rimozione di elementi elenco può essere eseguita in qualsiasi momento.  
  
### <a name="to-add-items-programmatically"></a>Per aggiungere elementi a livello di codice  
  
1. Usare il <xref:System.Windows.Forms.ListView.ListViewItemCollection.Add%2A> metodo della <xref:System.Windows.Forms.ListView.Items%2A> Proprietà.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#11)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#11)]  
  
### <a name="to-remove-items-programmatically"></a>Per rimuovere elementi a livello di codice  
  
1. Usare il <xref:System.Windows.Forms.ListView.ListViewItemCollection.RemoveAt%2A> <xref:System.Windows.Forms.ListView.ListViewItemCollection.Clear%2A> metodo o della <xref:System.Windows.Forms.ListView.Items%2A> Proprietà. Il <xref:System.Windows.Forms.ListView.ListViewItemCollection.RemoveAt%2A> metodo rimuove un singolo elemento. il <xref:System.Windows.Forms.ListView.ListViewItemCollection.Clear%2A> metodo rimuove tutti gli elementi dall'elenco.  
  
     [!code-csharp[System.Windows.Forms.ListViewLegacyTopics#12](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/CS/Class1.cs#12)]
     [!code-vb[System.Windows.Forms.ListViewLegacyTopics#12](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListViewLegacyTopics/VB/Class1.vb#12)]  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.ListView>
- [Controllo ListView](listview-control-windows-forms.md)
- [Cenni preliminari sul controllo ListView](listview-control-overview-windows-forms.md)
