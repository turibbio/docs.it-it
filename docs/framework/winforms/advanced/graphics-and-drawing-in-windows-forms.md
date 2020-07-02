---
title: Grafica e disegno
description: Informazioni sugli oggetti grafici, penna, pennello e colore e su come eseguire attività quali la creazione di forme, il disegno di testo o la visualizzazione di immagini in Windows Forms.
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms]
- graphics [Windows Forms], using in Windows Forms
- GDI+, using in managed code
- drawing [Windows Forms]
ms.assetid: 362532c5-1a06-4257-bdc8-723461009ede
ms.openlocfilehash: 58d8cde6aa102225cf9e3c342efe37218c818307
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618402"
---
# <a name="graphics-and-drawing-in-windows-forms"></a>Grafica e disegno in Windows Form
Il Common Language Runtime utilizza un'implementazione avanzata di Windows Graphics Device Interface (GDI) denominato GDI+. Con GDI+ è possibile creare grafica, creare testo e modificare immagini grafiche come oggetti. GDI+ è progettato per offrire prestazioni e facilità di utilizzo. È possibile utilizzare GDI+ per eseguire il rendering di immagini grafiche in Windows Forms e controlli. Sebbene non sia possibile utilizzare GDI+ direttamente nei Web Form, è possibile visualizzare immagini grafiche tramite il controllo server Web Image.  
  
 In questa sezione sono disponibili argomenti che introducono le nozioni di base sulla programmazione GDI+. Anche se non è da considerarsi come un riferimento esaustivo, la sezione contiene informazioni sugli oggetti <xref:System.Drawing.Graphics>, <xref:System.Drawing.Pen>, <xref:System.Drawing.Brush> e <xref:System.Drawing.Color> e riporta informazioni su come creare forme, testo o visualizzare immagini. Per ulteriori informazioni, vedere [riferimento a GDI+](/windows/desktop/gdiplus/-gdiplus-class-gdi-reference).  
  
 Se si preferisce iniziare subito, vedere [Guida introduttiva alla programmazione grafica](getting-started-with-graphics-programming.md), che include argomenti su come usare il codice per disegnare linee, forme, testo e altro in Windows Form.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Panoramica sulla grafica](graphics-overview-windows-forms.md)  
 Fornisce un'introduzione alle classi gestite relative agli elementi grafici.  
  
 [Informazioni sul codice gestito GDI+](about-gdi-managed-code.md)  
 Fornisce informazioni sulle classi GDI+ gestite.  
  
 [Utilizzo di classi grafiche gestite](using-managed-graphics-classes.md)  
 Viene illustrato come completare una serie di attività usando le classi gestite GDI+.  
  
## <a name="reference"></a>Informazioni di riferimento  
 <xref:System.Drawing>  
 Fornisce accesso alle funzionalità grafiche di base GDI+.  
  
 <xref:System.Drawing.Drawing2D>  
 Fornisce funzionalità grafica vettoriale e bidimensionale avanzata.  
  
 <xref:System.Drawing.Imaging>  
 Fornisce funzionalità avanzate per la creazione di immagini GDI+.  
  
 <xref:System.Drawing.Text>  
 Fornisce funzionalità tipografiche GDI+ avanzate. Le classi presenti in questo spazio dei nomi consentono la creazione e l'uso di raccolte di tipi di carattere.  
  
 <xref:System.Drawing.Printing>  
 Fornisce funzionalità di stampa.  
  
## <a name="related-sections"></a>Sezioni correlate  
 [Disegno e rendering di controlli personalizzati](../controls/custom-control-painting-and-rendering.md)  
 Spiega in dettaglio come fornire codice per i controlli di disegno.
