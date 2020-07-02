---
title: Aggiungere e rimuovere schede con TabControl
description: Informazioni su come aggiungere e rimuovere schede con il controllo Windows Forms TabControl, che contiene due controlli TabPage. Accedere a queste schede tramite la proprietà TabPages.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tabs [Windows Forms], removing from pages
- TabPage control
- TabControl control [Windows Forms], adding and removing tabs
- tabs [Windows Forms], adding to pages
- tab pages
ms.assetid: 66d4dfca-41e8-44e3-9c80-fb7ac4cb1619
ms.openlocfilehash: 7e67d0bbc13bd7d9c8835dc6fb9b9c5c9333b8bf
ms.sourcegitcommit: e02d17b2cf9c1258dadda4810a5e6072a0089aee
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85618077"
---
# <a name="how-to-add-and-remove-tabs-with-the-windows-forms-tabcontrol"></a><span data-ttu-id="2e773-104">Procedura: aggiungere e rimuovere schede tramite il controllo TabControl Windows Form</span><span class="sxs-lookup"><span data-stu-id="2e773-104">How to: Add and Remove Tabs with the Windows Forms TabControl</span></span>
<span data-ttu-id="2e773-105">Per impostazione predefinita, un <xref:System.Windows.Forms.TabControl> controllo contiene due <xref:System.Windows.Forms.TabPage> controlli.</span><span class="sxs-lookup"><span data-stu-id="2e773-105">By default, a <xref:System.Windows.Forms.TabControl> control contains two <xref:System.Windows.Forms.TabPage> controls.</span></span> <span data-ttu-id="2e773-106">È possibile accedere a queste schede tramite la <xref:System.Windows.Forms.TabControl.TabPages%2A> Proprietà.</span><span class="sxs-lookup"><span data-stu-id="2e773-106">You can access these tabs through the <xref:System.Windows.Forms.TabControl.TabPages%2A> property.</span></span>  
  
### <a name="to-add-a-tab-programmatically"></a><span data-ttu-id="2e773-107">Per aggiungere una scheda a livello di codice</span><span class="sxs-lookup"><span data-stu-id="2e773-107">To add a tab programmatically</span></span>  
  
- <span data-ttu-id="2e773-108">Usare il <xref:System.Windows.Forms.TabControl.TabPageCollection.Add%2A> metodo della <xref:System.Windows.Forms.TabControl.TabPages%2A> Proprietà.</span><span class="sxs-lookup"><span data-stu-id="2e773-108">Use the <xref:System.Windows.Forms.TabControl.TabPageCollection.Add%2A> method of the <xref:System.Windows.Forms.TabControl.TabPages%2A> property.</span></span>  
  
    ```vb  
    Dim myTabPage As New TabPage()  
    myTabPage.Text = "TabPage" & (TabControl1.TabPages.Count + 1)  
    TabControl1.TabPages.Add(myTabPage)  
    ```  
  
    ```csharp  
    string title = "TabPage " + (tabControl1.TabCount + 1).ToString();  
    TabPage myTabPage = new TabPage(title);  
    tabControl1.TabPages.Add(myTabPage);  
    ```  
  
    ```cpp  
    String^ title = String::Concat("TabPage ",  
       (tabControl1->TabCount + 1).ToString());  
    TabPage^ myTabPage = gcnew TabPage(title);  
    tabControl1->TabPages->Add(myTabPage);  
    ```  
  
### <a name="to-remove-a-tab-programmatically"></a><span data-ttu-id="2e773-109">Per rimuovere una scheda a livello di codice</span><span class="sxs-lookup"><span data-stu-id="2e773-109">To remove a tab programmatically</span></span>  
  
- <span data-ttu-id="2e773-110">Per rimuovere le schede selezionate, utilizzare il <xref:System.Windows.Forms.TabControl.TabPageCollection.Remove%2A> metodo della <xref:System.Windows.Forms.TabControl.TabPages%2A> Proprietà.</span><span class="sxs-lookup"><span data-stu-id="2e773-110">To remove selected tabs, use the <xref:System.Windows.Forms.TabControl.TabPageCollection.Remove%2A> method of the <xref:System.Windows.Forms.TabControl.TabPages%2A> property.</span></span>  
  
     <span data-ttu-id="2e773-111">-oppure-</span><span class="sxs-lookup"><span data-stu-id="2e773-111">-or-</span></span>  
  
- <span data-ttu-id="2e773-112">Per rimuovere tutte le schede, usare il <xref:System.Windows.Forms.TabControl.TabPageCollection.Clear%2A> metodo della <xref:System.Windows.Forms.TabControl.TabPages%2A> Proprietà.</span><span class="sxs-lookup"><span data-stu-id="2e773-112">To remove all tabs, use the <xref:System.Windows.Forms.TabControl.TabPageCollection.Clear%2A> method of the <xref:System.Windows.Forms.TabControl.TabPages%2A> property.</span></span>  
  
    ```vb  
    ' Removes the selected tab:  
    TabControl1.TabPages.Remove(TabControl1.SelectedTab)  
    ' Removes all the tabs:  
    TabControl1.TabPages.Clear()  
    ```  
  
    ```csharp  
    // Removes the selected tab:  
    tabControl1.TabPages.Remove(tabControl1.SelectedTab);  
    // Removes all the tabs:  
    tabControl1.TabPages.Clear();  
    ```  
  
    ```cpp  
    // Removes the selected tab:  
    tabControl1->TabPages->Remove(tabControl1->SelectedTab);  
    // Removes all the tabs:  
    tabControl1->TabPages->Clear();  
    ```  
  
## <a name="see-also"></a><span data-ttu-id="2e773-113">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="2e773-113">See also</span></span>

- [<span data-ttu-id="2e773-114">Cenni preliminari sul controllo TabControl</span><span class="sxs-lookup"><span data-stu-id="2e773-114">TabControl Control Overview</span></span>](tabcontrol-control-overview-windows-forms.md)
- [<span data-ttu-id="2e773-115">Procedura: aggiungere un controllo a un oggetto TabPage</span><span class="sxs-lookup"><span data-stu-id="2e773-115">How to: Add a Control to a Tab Page</span></span>](how-to-add-a-control-to-a-tab-page.md)
- [<span data-ttu-id="2e773-116">Procedura: disabilitare le schede</span><span class="sxs-lookup"><span data-stu-id="2e773-116">How to: Disable Tab Pages</span></span>](how-to-disable-tab-pages.md)
- [<span data-ttu-id="2e773-117">Procedura: modificare l'aspetto del controllo TabControl Windows Form</span><span class="sxs-lookup"><span data-stu-id="2e773-117">How to: Change the Appearance of the Windows Forms TabControl</span></span>](how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)
