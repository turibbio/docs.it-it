---
title: 'Procedura: Appiattire un percorso curvo in una linea'
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [Windows Forms], flattening curves into lines
- curves [Windows Forms], flattening
- GraphicsPath object
- paths [Windows Forms], flattening
- drawing [Windows Forms], flattening curves
ms.assetid: e654b8de-25f4-4735-9208-42e4514a589c
ms.openlocfilehash: d59a802618ddd5080c651e822ed4c09641f7f170
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2019
ms.locfileid: "64645360"
---
# <a name="how-to-flatten-a-curved-path-into-a-line"></a>Procedura: Appiattire un percorso curvo in una linea
Oggetto <xref:System.Drawing.Drawing2D.GraphicsPath> oggetto archivia una sequenza di spline di Bézier e righe. È possibile aggiungere diversi tipi di curve (puntini di sospensione, archi e spline cardinali) in un percorso, ma ogni curva viene convertito in una spline di Bézier prima di essere archiviato nel percorso. Rendere flat un percorso è costituito ogni spline di Bézier nel percorso di conversione in una sequenza di linee rette. Nella figura seguente mostra un percorso di prima e dopo l'appiattimento.  
  
 ![Linee rette e curve](./media/aboutgdip02-art32a.gif "AboutGdip02_Art32A")  
  
### <a name="to-flatten-a-path"></a>Per trasformare un percorso  
  
- chiamare il <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> metodo di un <xref:System.Drawing.Drawing2D.GraphicsPath> oggetto. Il <xref:System.Drawing.Drawing2D.GraphicsPath.Flatten%2A> metodo riceve un argomento di appiattimento che specifica la distanza massima tra il percorso appiattito e il percorso originale.  
  
## <a name="see-also"></a>Vedere anche

- <xref:System.Drawing.Drawing2D.GraphicsPath?displayProperty=nameWithType>
- [Linee, curve e forme](lines-curves-and-shapes.md)
- [Costruzione e creazione di percorsi](constructing-and-drawing-paths.md)
