---
title: 'Procedura: creare gestori eventi in fase di esecuzione'
description: Informazioni su come creare un gestore eventi in fase di esecuzione con il Progettazione Windows Form in Visual Studio. Questa azione consente di connettere i gestori eventi in fase di esecuzione.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- Windows Forms, event handling
- event handlers [Windows Forms], creating
- run time [Windows Forms], creating event handlers at
- examples [Windows Forms], event handling
- Button control [Windows Forms], event handlers
ms.assetid: 2e7c9e1a-61fe-444d-8113-3c5bacf1c8cb
ms.openlocfilehash: 857076c46377b3276154d9b193d4bbe51841828f
ms.sourcegitcommit: dc2feef0794cf41dbac1451a13b8183258566c0e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/24/2020
ms.locfileid: "85325802"
---
# <a name="how-to-create-event-handlers-at-run-time-for-windows-forms"></a>Procedura: Creare gestori eventi in fase di esecuzione per Windows Forms

Oltre a creare eventi usando il Progettazione Windows Form in Visual Studio, è anche possibile creare un gestore eventi in fase di esecuzione. Questa azione consente di connettere i gestori eventi in base alle condizioni nel codice in fase di esecuzione invece di connetterli all'avvio iniziale del programma.

## <a name="create-an-event-handler-at-run-time"></a>Creare un gestore eventi in fase di esecuzione

1. Aprire il modulo a cui si desidera aggiungere un gestore eventi.

2. Aggiungere un metodo al modulo con la firma del metodo per l'evento che si desidera gestire.

     Se, ad esempio, si stava gestendo l' <xref:System.Windows.Forms.Control.Click> evento di un <xref:System.Windows.Forms.Button> controllo, si creerebbe un metodo come il seguente:

    ```vb
    Private Sub Button1_Click(ByVal sender As Object, ByVal e As EventArgs)
       ' Add event handler code here.
    End Sub
    ```

    ```csharp
    private void button1_Click(object sender, System.EventArgs e)
    {
    // Add event handler code here.
    }
    ```

    ```cpp
    private:
       void button1_Click(System::Object ^ sender,
          System::EventArgs ^ e)
       {
          // Add event handler code here.
       }
    ```

3. Aggiungere un codice al gestore dell'evento appropriato per l'applicazione.

4. Stabilire per quale modulo o controllo si desidera creare un gestore eventi.

5. In un metodo nella classe del modulo, aggiungere il codice che specifica il gestore eventi per gestire l'evento. Ad esempio, il codice seguente specifica che il gestore eventi `button1_Click` gestisce l' <xref:System.Windows.Forms.Control.Click> evento di un <xref:System.Windows.Forms.Button> controllo:

    ```vb
    AddHandler Button1.Click, AddressOf Button1_Click
    ```

    ```csharp
    button1.Click += new EventHandler(button1_Click);
    ```

    ```cpp
    button1->Click += gcnew System::EventHandler(this, &Form1::button1_Click);
    ```

     Il <xref:System.ComponentModel.EventHandlerList.AddHandler%2A> metodo illustrato nel codice Visual Basic precedente stabilisce un gestore dell'evento click per il pulsante.

## <a name="see-also"></a>Vedi anche

- [Creazione di gestori eventi in Windows Form](creating-event-handlers-in-windows-forms.md)
- [Panoramica sui gestori eventi](event-handlers-overview-windows-forms.md)
- [Risoluzione dei problemi relativi ai gestori eventi ereditati in Visual Basic](../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)
