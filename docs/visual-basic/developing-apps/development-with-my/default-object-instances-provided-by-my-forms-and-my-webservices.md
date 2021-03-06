---
title: Istanze predefinite degli oggetti fornite da My.Forms e My.WebServices
ms.date: 07/20/2015
helpviewer_keywords:
- My.WebServices object [Visual Basic], developing applications
- My.Forms object [Visual Basic], developing applications
- rapid application development (RAD), My.Forms
- rapid application development (RAD), My.WebServices
ms.assetid: de930027-9108-4f0c-b97c-5e7db4d6ef79
ms.openlocfilehash: 141f2f5f98499498d3c6732f7ae8d0abe6259ed9
ms.sourcegitcommit: 45c8eed045779b70a47b23169897459d0323dc89
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "84990250"
---
# <a name="default-object-instances-provided-by-myforms-and-mywebservices-visual-basic"></a>Istanze predefinite degli oggetti fornite da My.Forms e My.WebServices (Visual Basic)

Gli oggetti [My. Forms](../../language-reference/objects/my-forms-object.md) e [My. WebServices](../../language-reference/objects/my-webservices-object.md) consentono di accedere ai moduli, alle origini dati e ai servizi Web XML utilizzati dall'applicazione. Forniscono l'accesso tramite raccolte di *istanze predefinite* di ognuno di questi oggetti.  
  
## <a name="default-instances"></a>Istanze predefinite  

 Un'istanza predefinita è un'istanza della classe fornita dal runtime e non è necessario dichiararla e crearne un'istanza usando le `Dim` `New` istruzioni e. Nell'esempio seguente viene illustrato come dichiarare e creare un'istanza di una <xref:System.Windows.Forms.Form> classe denominata e `Form1` come ora è possibile ottenere un'istanza predefinita di questa <xref:System.Windows.Forms.Form> classe tramite `My.Forms` .  
  
 [!code-vb[VbVbcnMy#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#5)]  
  
 [!code-vb[VbVbcnMy#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMy/VB/Class1.vb#6)]  
  
 L' `My.Forms` oggetto restituisce una raccolta di istanze predefinite per ogni `Form` classe esistente nel progetto. Analogamente, `My.WebServices` fornisce un'istanza predefinita della classe proxy per ogni servizio Web a cui è stato creato un riferimento nell'applicazione.  
  
## <a name="see-also"></a>Vedere anche

- [Oggetto My.Forms](../../language-reference/objects/my-forms-object.md)
- [Oggetto My.WebServices](../../language-reference/objects/my-webservices-object.md)
- [Dipendenza di My dal tipo di progetto](how-my-depends-on-project-type.md)
