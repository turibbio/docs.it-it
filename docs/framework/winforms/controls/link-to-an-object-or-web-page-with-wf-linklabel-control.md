---
title: Collegamento a un oggetto o a una pagina Web con il controllo LinkLabel
description: Informazioni su come creare collegamenti di tipo Web a un oggetto o a una pagina Web con il controllo LinkLabel Windows Forms.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [Windows Forms], LinkLabel control
- Windows Forms, linking to objects
- Web page link control
- linking [Windows Forms], to other forms
- Windows Forms, linking to Web pages
- links [Windows Forms], to other forms
- LinkLabel control [Windows Forms], linking to object or Web page
- LinkLabel control [Windows Forms], examples
ms.assetid: 6c91c975-3cb7-4504-82f0-fc6255f8fb85
ms.openlocfilehash: a5fb1c03e9a8d82fe77f4133ba04c42114787d23
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618312"
---
# <a name="how-to-link-to-an-object-or-web-page-with-the-windows-forms-linklabel-control"></a>Procedura: eseguire il collegamento a un oggetto o a una pagina Web con il controllo LinkLabel di Windows Form

Il <xref:System.Windows.Forms.LinkLabel> controllo Windows Forms consente di creare collegamenti di tipo Web nel form. Quando si fa clic sul collegamento, è possibile modificarne il colore per indicare che è stato visitato il collegamento. Per ulteriori informazioni sulla modifica del colore, vedere [procedura: modificare l'aspetto del controllo LinkLabel Windows Forms](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md).

## <a name="linking-to-another-form"></a>Collegamento a un altro modulo

#### <a name="to-link-to-another-form-with-a-linklabel-control"></a>Per creare un collegamento a un altro form con un controllo LinkLabel

1. Impostare la <xref:System.Windows.Forms.LinkLabel.Text%2A> proprietà su una didascalia appropriata.

2. Impostare la <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> proprietà per determinare la parte della didascalia che verrà indicata come collegamento. Il modo in cui viene indicato dipende dalle proprietà correlate all'aspetto dell'etichetta di collegamento. Il <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> valore è rappresentato da un <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> oggetto contenente due numeri, la posizione iniziale del carattere e il numero di caratteri. La <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> proprietà può essere impostata nell'finestra proprietà o nel codice in un modo simile al seguente:

    ```vb
    ' In this code example, the link area has been set to begin
    ' at the first character and extend for eight characters.
    ' You may need to modify this based on the text entered in Step 1.
    LinkLabel1.LinkArea = New LinkArea(0, 8)
    ```

    ```csharp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1.LinkArea = new LinkArea(0,8);
    ```

    ```cpp
    // In this code example, the link area has been set to begin
    // at the first character and extend for eight characters.
    // You may need to modify this based on the text entered in Step 1.
    linkLabel1->LinkArea = LinkArea(0,8);
    ```

3. Nel <xref:System.Windows.Forms.LinkLabel.LinkClicked> gestore dell'evento richiamare il <xref:System.Windows.Forms.Form.Show%2A> metodo per aprire un altro form nel progetto e impostare la <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> proprietà su `true` .

    > [!NOTE]
    > Un'istanza della <xref:System.Windows.Forms.LinkLabelLinkClickedEventArgs> classe contiene un riferimento al <xref:System.Windows.Forms.LinkLabel> controllo su cui è stato fatto clic, pertanto non è necessario eseguire il cast dell' `sender` oggetto.

    ```vb
    Protected Sub LinkLabel1_LinkClicked(ByVal Sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       ' Show another form.
       Dim f2 As New Form()
       f2.Show
       LinkLabel1.LinkVisited = True
    End Sub
    ```

    ```csharp
    protected void linkLabel1_LinkClicked(object sender, System. Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       // Show another form.
       Form f2 = new Form();
       f2.Show();
       linkLabel1.LinkVisited = true;
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          // Show another form.
          Form ^ f2 = new Form();
          f2->Show();
          linkLabel1->LinkVisited = true;
       }
    ```

## <a name="linking-to-a-web-page"></a>Collegamento a una pagina Web

Il <xref:System.Windows.Forms.LinkLabel> controllo può essere utilizzato anche per visualizzare una pagina Web con il browser predefinito.

#### <a name="to-start-internet-explorer-and-link-to-a-web-page-with-a-linklabel-control"></a>Per avviare Internet Explorer e collegarsi a una pagina Web con un controllo LinkLabel

1. Impostare la <xref:System.Windows.Forms.LinkLabel.Text%2A> proprietà su una didascalia appropriata.

2. Impostare la <xref:System.Windows.Forms.LinkLabel.LinkArea%2A> proprietà per determinare la parte della didascalia che verrà indicata come collegamento.

3. Nel <xref:System.Windows.Forms.LinkLabel.LinkClicked> gestore eventi, nel mezzo di un blocco di gestione delle eccezioni, chiamare una seconda procedura che imposta la <xref:System.Windows.Forms.LinkLabel.LinkVisited%2A> proprietà su `true` e utilizza il <xref:System.Diagnostics.Process.Start%2A> metodo per avviare il browser predefinito con un URL. Per usare il <xref:System.Diagnostics.Process.Start%2A> metodo è necessario aggiungere un riferimento allo <xref:System.Diagnostics?displayProperty=nameWithType> spazio dei nomi.

    > [!IMPORTANT]
    > Se il codice riportato di seguito viene eseguito in un ambiente con attendibilità parziale, ad esempio in un'unità condivisa, il compilatore JIT ha esito negativo quando `VisitLink` viene chiamato il metodo. L' `System.Diagnostics.Process.Start` istruzione causa una richiesta di collegamento che ha esito negativo. Intercettando l'eccezione quando `VisitLink` viene chiamato il metodo, il codice seguente assicura che se il compilatore JIT non riesce, l'errore viene gestito normalmente.

    ```vb
    Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, _
       ByVal e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) _
       Handles LinkLabel1.LinkClicked
       Try
          VisitLink()
       Catch ex As Exception
          ' The error message
          MessageBox.Show("Unable to open link that was clicked.")
       End Try
    End Sub

    Sub VisitLink()
       ' Change the color of the link text by setting LinkVisited
       ' to True.
       LinkLabel1.LinkVisited = True
       ' Call the Process.Start method to open the default browser
       ' with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com")
    End Sub
    ```

    ```csharp
    private void linkLabel1_LinkClicked(object sender, System.Windows.Forms.LinkLabelLinkClickedEventArgs e)
    {
       try
       {
          VisitLink();
       }
       catch (Exception ex )
       {
          MessageBox.Show("Unable to open link that was clicked.");
       }
    }

    private void VisitLink()
    {
       // Change the color of the link text by setting LinkVisited
       // to true.
       linkLabel1.LinkVisited = true;
       //Call the Process.Start method to open the default browser
       //with a URL:
       System.Diagnostics.Process.Start("http://www.microsoft.com");
    }
    ```

    ```cpp
    private:
       void linkLabel1_LinkClicked(System::Object ^  sender,
          System::Windows::Forms::LinkLabelLinkClickedEventArgs ^  e)
       {
          try
          {
             VisitLink();
          }
          catch (Exception ^ ex)
          {
             MessageBox::Show("Unable to open link that was clicked.");
          }
       }
    private:
       void VisitLink()
       {
          // Change the color of the link text by setting LinkVisited
          // to true.
          linkLabel1->LinkVisited = true;
          // Call the Process.Start method to open the default browser
          // with a URL:
          System::Diagnostics::Process::Start("http://www.microsoft.com");
       }
    ```

## <a name="see-also"></a>Vedere anche

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- [Panoramica del controllo LinkLabel](linklabel-control-overview-windows-forms.md)
- [Procedura: modificare l'aspetto del controllo LinkLabel di Windows Form](how-to-change-the-appearance-of-the-windows-forms-linklabel-control.md)
- [Controllo LinkLabel](linklabel-control-windows-forms.md)
