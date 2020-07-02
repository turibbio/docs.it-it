---
title: Stampa con anteprima di stampa
description: Informazioni su come aggiungere servizi di anteprima di stampa all'applicazione tramite il Windows Forms controllo PrintPreviewDialog.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- printing [Windows Forms], using print preview
- printing [Windows Forms], with print preview
- print preview
ms.assetid: 4a16f7e2-ae10-4485-b0ae-3d558334d0fe
ms.openlocfilehash: abcf77db40f648df1a0cd49922bb49e5c9407811
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85621613"
---
# <a name="how-to-print-in-windows-forms-using-print-preview"></a><span data-ttu-id="087f2-103">Procedura: stampare in Windows Form tramite l'anteprima di stampa</span><span class="sxs-lookup"><span data-stu-id="087f2-103">How to: Print in Windows Forms Using Print Preview</span></span>
<span data-ttu-id="087f2-104">Nella programmazione di Windows Form è comune offrire servizi di anteprima di stampa oltre che di stampa.</span><span class="sxs-lookup"><span data-stu-id="087f2-104">It is very common in Windows Forms programming to offer print preview in addition to printing services.</span></span> <span data-ttu-id="087f2-105">Per aggiungere facilmente i servizi di anteprima di stampa all'applicazione, usare un controllo <xref:System.Windows.Forms.PrintPreviewDialog> in combinazione con la logica di gestione degli eventi <xref:System.Drawing.Printing.PrintDocument.PrintPage> per la stampa di un file.</span><span class="sxs-lookup"><span data-stu-id="087f2-105">An easy way to add print preview services to your application is to use a <xref:System.Windows.Forms.PrintPreviewDialog> control in combination with the <xref:System.Drawing.Printing.PrintDocument.PrintPage> event-handling logic for printing a file.</span></span>  
  
### <a name="to-preview-a-text-document-with-a-printpreviewdialog-control"></a><span data-ttu-id="087f2-106">Per visualizzare in anteprima un documento di testo con un controllo PrintPreviewDialog</span><span class="sxs-lookup"><span data-stu-id="087f2-106">To preview a text document with a PrintPreviewDialog control</span></span>  
  
1. <span data-ttu-id="087f2-107">Aggiungere un oggetto <xref:System.Windows.Forms.PrintPreviewDialog>, un oggetto <xref:System.Drawing.Printing.PrintDocument>e due stringhe al form.</span><span class="sxs-lookup"><span data-stu-id="087f2-107">Add a <xref:System.Windows.Forms.PrintPreviewDialog>, <xref:System.Drawing.Printing.PrintDocument>, and two strings to your form.</span></span>  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#1)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#1)]  
  
2. <span data-ttu-id="087f2-108">Impostare la proprietà <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> sul documento da stampare, quindi aprire e leggere il contenuto del documento fino alla stringa aggiunta in precedenza.</span><span class="sxs-lookup"><span data-stu-id="087f2-108">Set the <xref:System.Drawing.Printing.PrintDocument.DocumentName%2A> property to the document you wish to print, and open and read the document's contents to the string you added previously.</span></span>  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#2](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#2)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#2](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#2)]  
  
3. <span data-ttu-id="087f2-109">Come per la stampa del documento, nel gestore eventi <xref:System.Drawing.Printing.PrintDocument.PrintPage> usare la proprietà <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> della classe <xref:System.Drawing.Printing.PrintPageEventArgs> e il contenuto del file per calcolare le righe per pagina ed eseguire il rendering del contenuto del documento.</span><span class="sxs-lookup"><span data-stu-id="087f2-109">As you would for printing the document, in the <xref:System.Drawing.Printing.PrintDocument.PrintPage> event handler, use the <xref:System.Drawing.Printing.PrintPageEventArgs.Graphics%2A> property of the <xref:System.Drawing.Printing.PrintPageEventArgs> class and the file contents to calculate lines per page and render the document's contents.</span></span> <span data-ttu-id="087f2-110">Dopo la generazione di ogni pagina, controllare se si tratta dell'ultima pagina e impostare la proprietà <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> della classe <xref:System.Drawing.Printing.PrintPageEventArgs> di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="087f2-110">After each page is drawn, check to see if it is the last page, and set the <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> property of the <xref:System.Drawing.Printing.PrintPageEventArgs> accordingly.</span></span> <span data-ttu-id="087f2-111">L'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> viene generato finché la proprietà <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> non assume valore `false`.</span><span class="sxs-lookup"><span data-stu-id="087f2-111">The <xref:System.Drawing.Printing.PrintDocument.PrintPage> event is raised until <xref:System.Drawing.Printing.PrintPageEventArgs.HasMorePages%2A> is `false`.</span></span> <span data-ttu-id="087f2-112">Al termine del rendering del documento, reimpostare la stringa da sottoporre a rendering.</span><span class="sxs-lookup"><span data-stu-id="087f2-112">When the document has finished rendering, reset the string to be rendered.</span></span> <span data-ttu-id="087f2-113">Assicurarsi inoltre che l'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> sia associato al relativo metodo di gestione degli eventi.</span><span class="sxs-lookup"><span data-stu-id="087f2-113">Also, make sure the <xref:System.Drawing.Printing.PrintDocument.PrintPage> event is associated with its event-handling method.</span></span>  
  
    > [!NOTE]
    > <span data-ttu-id="087f2-114">Se è stata implementata la stampa nell'applicazione, è possibile che i passaggi 2 e 3 siano già stati completati.</span><span class="sxs-lookup"><span data-stu-id="087f2-114">You may have already completed steps 2 and 3 if you have implemented printing in your application.</span></span>  
  
     <span data-ttu-id="087f2-115">Nell'esempio di codice seguente il gestore eventi viene usato per stampare il file "testPage.txt" con lo stesso tipo di carattere usato nel form.</span><span class="sxs-lookup"><span data-stu-id="087f2-115">In the following code example, the event handler is used to print the "testPage.txt" file in the same font used on the form.</span></span>  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#3](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#3)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#3](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#3)]  
  
4. <span data-ttu-id="087f2-116">Impostare la proprietà <xref:System.Windows.Forms.PrintPreviewDialog.Document%2A> del controllo <xref:System.Windows.Forms.PrintPreviewDialog> sul componente <xref:System.Drawing.Printing.PrintDocument> nel form.</span><span class="sxs-lookup"><span data-stu-id="087f2-116">Set the <xref:System.Windows.Forms.PrintPreviewDialog.Document%2A> property of the <xref:System.Windows.Forms.PrintPreviewDialog> control to the <xref:System.Drawing.Printing.PrintDocument> component on the form.</span></span>  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#5](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#5)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#5](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#5)]  
  
5. <span data-ttu-id="087f2-117">Chiamare il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> sul controllo <xref:System.Windows.Forms.PrintPreviewDialog> .</span><span class="sxs-lookup"><span data-stu-id="087f2-117">Call the <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> method on the <xref:System.Windows.Forms.PrintPreviewDialog> control.</span></span> <span data-ttu-id="087f2-118">In genere la chiamata al metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> si esegue dal metodo di gestione degli eventi <xref:System.Windows.Forms.Control.Click> di un pulsante.</span><span class="sxs-lookup"><span data-stu-id="087f2-118">You would typically call <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> from the <xref:System.Windows.Forms.Control.Click> event-handling method of a button.</span></span> <span data-ttu-id="087f2-119">Chiamando il metodo <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> viene generato l'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> e viene eseguito il rendering dell'output sul controllo <xref:System.Windows.Forms.PrintPreviewDialog> .</span><span class="sxs-lookup"><span data-stu-id="087f2-119">Calling <xref:System.Windows.Forms.CommonDialog.ShowDialog%2A> raises the <xref:System.Drawing.Printing.PrintDocument.PrintPage> event and renders the output to the <xref:System.Windows.Forms.PrintPreviewDialog> control.</span></span> <span data-ttu-id="087f2-120">Quando l'utente fa clic sull'icona di stampa nella finestra di dialogo, l'evento <xref:System.Drawing.Printing.PrintDocument.PrintPage> viene generato di nuovo, inviando l'output alla stampante anziché alla finestra di dialogo di anteprima.</span><span class="sxs-lookup"><span data-stu-id="087f2-120">When the user clicks the print icon on the dialog, the <xref:System.Drawing.Printing.PrintDocument.PrintPage> event is raised again, sending the output to the printer instead of the preview dialog.</span></span> <span data-ttu-id="087f2-121">Questo è il motivo per cui alla fine del processo di rendering nel passaggio 3 la stringa viene reimpostata.</span><span class="sxs-lookup"><span data-stu-id="087f2-121">This is why the string is reset at the end of the rendering process in step 3.</span></span>  
  
     <span data-ttu-id="087f2-122">L'esempio di codice seguente illustra il metodo di gestione degli eventi <xref:System.Windows.Forms.Control.Click> per un pulsante nel form.</span><span class="sxs-lookup"><span data-stu-id="087f2-122">The following code example shows the <xref:System.Windows.Forms.Control.Click> event-handling method for a button on the form.</span></span> <span data-ttu-id="087f2-123">Questo metodo chiama i metodi per la lettura del documento e la visualizzazione della finestra di dialogo di anteprima.</span><span class="sxs-lookup"><span data-stu-id="087f2-123">This event-handling method calls the methods to read the document and show the print preview dialog.</span></span>  
  
     [!code-csharp[System.Drawing.Printing.PrintPreviewExample#4](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#4)]
     [!code-vb[System.Drawing.Printing.PrintPreviewExample#4](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#4)]  
  
## <a name="example"></a><span data-ttu-id="087f2-124">Esempio</span><span class="sxs-lookup"><span data-stu-id="087f2-124">Example</span></span>  
 [!code-csharp[System.Drawing.Printing.PrintPreviewExample#0](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/CS/Form1.cs#0)]
 [!code-vb[System.Drawing.Printing.PrintPreviewExample#0](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.Printing.PrintPreviewExample/VB/Form1.vb#0)]  
  
## <a name="compiling-the-code"></a><span data-ttu-id="087f2-125">Compilazione del codice</span><span class="sxs-lookup"><span data-stu-id="087f2-125">Compiling the Code</span></span>  
 <span data-ttu-id="087f2-126">L'esempio presenta i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="087f2-126">This example requires:</span></span>  
  
- <span data-ttu-id="087f2-127">Riferimenti agli assembly System, System.Windows.Forms e System.Drawing.</span><span class="sxs-lookup"><span data-stu-id="087f2-127">References to the System, System.Windows.Forms, System.Drawing assemblies.</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="087f2-128">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="087f2-128">See also</span></span>

- [<span data-ttu-id="087f2-129">Procedura: stampare un file di testo con più pagine in Windows Form</span><span class="sxs-lookup"><span data-stu-id="087f2-129">How to: Print a Multi-Page Text File in Windows Forms</span></span>](how-to-print-a-multi-page-text-file-in-windows-forms.md)
- [<span data-ttu-id="087f2-130">Supporto per la stampa in Windows Form</span><span class="sxs-lookup"><span data-stu-id="087f2-130">Windows Forms Print Support</span></span>](windows-forms-print-support.md)
- [<span data-ttu-id="087f2-131">Stampa più protetta in Windows Form</span><span class="sxs-lookup"><span data-stu-id="087f2-131">More Secure Printing in Windows Forms</span></span>](../more-secure-printing-in-windows-forms.md)
