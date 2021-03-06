---
title: Gestione avanzata dell'input penna
ms.date: 03/30/2017
f1_keywords:
- AutoGeneratedOrientationPage
helpviewer_keywords:
- System.Windows.Input.StylusPlugIns classes
- InkCanvas control [WPF]
- ink [WPF], advanced handling
ms.assetid: abc8481a-f983-416f-b051-9168ac8b2ba3
ms.openlocfilehash: 840ab08faebe760a38ef344fd1c41818a838250b
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62008941"
---
# <a name="advanced-ink-handling"></a>Gestione avanzata dell'input penna
Il [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] viene fornito con il <xref:System.Windows.Controls.InkCanvas>, ed è un elemento che è possibile inserire nell'applicazione per iniziare immediatamente a raccogliere e visualizzare input penna. Tuttavia, se il <xref:System.Windows.Controls.InkCanvas> controllo non fornisce un livello sufficiente di controllo, è possibile mantenere il controllo a un livello superiore personalizzando proprie classi di raccolta e input penna per il rendering usando <xref:System.Windows.Input.StylusPlugIns>.  
  
 Il <xref:System.Windows.Input.StylusPlugIns> classi forniscono un meccanismo per l'implementazione del controllo di basso livello tramite <xref:System.Windows.Input.Stylus> input e il rendering dinamico dell'input penna. Il <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn> classe fornisce un meccanismo per implementare il comportamento personalizzato e applicarlo al flusso di dati provenienti dal dispositivo stilo per prestazioni ottimali. Il <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer>, specializzata <xref:System.Windows.Input.StylusPlugIns.StylusPlugIn>, consente di personalizzare in modo dinamico i dati di input penna per il rendering in tempo reale in altri termini, il <xref:System.Windows.Input.StylusPlugIns.DynamicRenderer> disegna input penna digitale immediatamente come <xref:System.Windows.Input.StylusPoint> dati vengono generati in modo che sembri "fluire" dallo stilo dispositivo.  
  
## <a name="in-this-section"></a>In questa sezione  
 [Personalizzare il rendering dell'input penna](custom-rendering-ink.md)  
  [Intercettazione dell'input dello stilo](intercepting-input-from-the-stylus.md)  
  [Creazione di un controllo di input penna](creating-an-ink-input-control.md)  
  [Modello di threading dell'input penna](the-ink-threading-model.md)
