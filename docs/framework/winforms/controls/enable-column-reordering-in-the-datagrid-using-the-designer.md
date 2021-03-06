---
title: Abilitare il riordinamento delle colonne nel controllo DataGridView usando la finestra di progettazione
ms.date: 03/30/2017
helpviewer_keywords:
- DataGridView control [Windows Forms], column order
- Windows Forms, columns
- columns [Windows Forms], reordering
- data [Windows Forms], displaying
ms.assetid: d82bd69c-6799-4439-a32c-91139c5901d1
ms.openlocfilehash: 14dc1081a8608c6e6add67f641c4b55825d2fc81
ms.sourcegitcommit: 44a7cd8687f227fc6db3211ccf4783dc20235e51
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/26/2020
ms.locfileid: "77626971"
---
# <a name="how-to-enable-column-reordering-in-the-windows-forms-datagridview-control-using-the-designer"></a>Procedura: abilitare il riordinamento delle colonne nel controllo DataGridView di Windows Form utilizzando la finestra di progettazione
Quando si visualizzano i dati visualizzati in un controllo <xref:System.Windows.Forms.DataGridView> di Windows Forms, gli utenti talvolta desiderano confrontare i valori in colonne specifiche. Questo può risultare scomodo se le colonne sono ampiamente separate nel controllo, soprattutto se gli utenti devono scorrere orizzontalmente per visualizzare tutte le colonne di interesse. È possibile semplificare l'attività di confronto dei valori di colonna consentendo agli utenti di riordinare le colonne. Quando si Abilita il riordinamento delle colonne, gli utenti possono spostare una colonna in una nuova posizione trascinando l'intestazione di colonna con il mouse.

 Per la procedura seguente è necessario un progetto di **applicazione Windows** con un modulo contenente un controllo <xref:System.Windows.Forms.DataGridView>. Per informazioni sulla configurazione di un progetto di questo tipo, vedere [procedura: creare un progetto Windows Forms Application](/visualstudio/ide/step-1-create-a-windows-forms-application-project) e [procedura: aggiungere controlli a Windows Forms](how-to-add-controls-to-windows-forms.md).

## <a name="to-enable-column-reordering"></a>Per abilitare il riordinamento delle colonne

- Fare clic sul glifo azioni della finestra di progettazione (![piccola freccia nera](./media/designer-actions-glyph.gif)) nell'angolo superiore destro del controllo <xref:System.Windows.Forms.DataGridView>, quindi selezionare **Abilita riordinamento colonne**.

## <a name="see-also"></a>Vedere anche

- <xref:System.Windows.Forms.DataGridView>
- <xref:System.Windows.Forms.DataGridView.AllowUserToOrderColumns%2A?displayProperty=nameWithType>
- [Procedura: Bloccare le colonne nel controllo DataGridView di Windows Form usando la finestra di progettazione](freeze-columns-in-the-datagrid-using-the-designer.md)
- [Procedura: creare un progetto di Windows Forms Application](/visualstudio/ide/step-1-create-a-windows-forms-application-project)
- [Procedura: Aggiungere controlli a un Windows Forms](how-to-add-controls-to-windows-forms.md)
