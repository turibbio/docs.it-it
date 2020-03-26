---
title: 'Procedura: convertire un elemento'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], translations
ms.assetid: 461c8273-15df-42f6-8672-89ba22887cc0
ms.openlocfilehash: addff0e22fb3f27ea924887809c0635aeb3ad67d
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111972"
---
# <a name="how-to-translate-an-element"></a><span data-ttu-id="d7484-102">Procedura: convertire un elemento</span><span class="sxs-lookup"><span data-stu-id="d7484-102">How to: Translate an Element</span></span>
<span data-ttu-id="d7484-103">In questo esempio viene illustrato come convertire <xref:System.Windows.Media.TranslateTransform>(spostare) un elemento utilizzando un oggetto .</span><span class="sxs-lookup"><span data-stu-id="d7484-103">This example shows how to translate (move) an element by using a <xref:System.Windows.Media.TranslateTransform>.</span></span>  
  
 <span data-ttu-id="d7484-104">La <xref:System.Windows.Media.TranslateTransform> classe è particolarmente utile per spostare gli elementi all'interno di pannelli che non supportano il posizionamento assoluto.</span><span class="sxs-lookup"><span data-stu-id="d7484-104">The <xref:System.Windows.Media.TranslateTransform> class is especially useful for moving elements inside panels that do not support absolute positioning.</span></span> <span data-ttu-id="d7484-105">Ad esempio, applicando <xref:System.Windows.Media.TranslateTransform> a <xref:System.Windows.UIElement.RenderTransform%2A> alla proprietà di un elemento, è <xref:System.Windows.Controls.StackPanel> <xref:System.Windows.Controls.DockPanel>possibile spostare un elemento all'interno di un oggetto o .</span><span class="sxs-lookup"><span data-stu-id="d7484-105">For example, by applying a <xref:System.Windows.Media.TranslateTransform> to the <xref:System.Windows.UIElement.RenderTransform%2A> property of an element, you can move an element within a <xref:System.Windows.Controls.StackPanel> or <xref:System.Windows.Controls.DockPanel>.</span></span>  
  
 <span data-ttu-id="d7484-106">Utilizzare <xref:System.Windows.Media.TranslateTransform.X%2A> la proprietà <xref:System.Windows.Media.TranslateTransform> dell'oggetto per specificare la quantità, in pixel, per spostare l'elemento lungo l'asse x.</span><span class="sxs-lookup"><span data-stu-id="d7484-106">Use the <xref:System.Windows.Media.TranslateTransform.X%2A> property of the <xref:System.Windows.Media.TranslateTransform> to specify the amount, in pixels, to move the element along the x-axis.</span></span> <span data-ttu-id="d7484-107">Utilizzare <xref:System.Windows.Media.TranslateTransform.Y%2A> la proprietà per specificare la quantità, in pixel, per spostare l'elemento lungo l'asse y.</span><span class="sxs-lookup"><span data-stu-id="d7484-107">Use the <xref:System.Windows.Media.TranslateTransform.Y%2A> property to specify the amount, in pixels, to move the element along the y-axis.</span></span> <span data-ttu-id="d7484-108">Infine, applicare <xref:System.Windows.Media.TranslateTransform> l'oggetto alla <xref:System.Windows.UIElement.RenderTransform%2A> proprietà dell'elemento.</span><span class="sxs-lookup"><span data-stu-id="d7484-108">Finally, apply the <xref:System.Windows.Media.TranslateTransform> to the <xref:System.Windows.UIElement.RenderTransform%2A> property of the element.</span></span>  
  
 <span data-ttu-id="d7484-109">L'esempio seguente <xref:System.Windows.Media.TranslateTransform> usa un oggetto per spostare un elemento di 50 pixel a destra e di 50 pixel verso il basso.</span><span class="sxs-lookup"><span data-stu-id="d7484-109">The following example uses a <xref:System.Windows.Media.TranslateTransform> to move an element 50 pixels to the right and 50 pixels down.</span></span>  
  
## <a name="example"></a><span data-ttu-id="d7484-110">Esempio</span><span class="sxs-lookup"><span data-stu-id="d7484-110">Example</span></span>  
 [!code-xaml[transformsSample#53](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/TranslateTransformExample.xaml#53)]  
  
 <span data-ttu-id="d7484-111">Per l'esempio completo, vedere Esempio di [trasformazioni 2D](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms).</span><span class="sxs-lookup"><span data-stu-id="d7484-111">For the complete sample, see [2D Transforms Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms).</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="d7484-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d7484-112">See also</span></span>

- [<span data-ttu-id="d7484-113">Cenni preliminari sulle trasformazioni</span><span class="sxs-lookup"><span data-stu-id="d7484-113">Transforms Overview</span></span>](transforms-overview.md)
