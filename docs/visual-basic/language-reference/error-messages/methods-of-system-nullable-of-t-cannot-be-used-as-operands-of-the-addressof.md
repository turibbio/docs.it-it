---
title: È impossibile utilizzare i metodi di "System.Nullable (Of T)" come operandi dell'operatore "AddressOf".
ms.date: 07/20/2015
f1_keywords:
- vbc32126
- bc32126
helpviewer_keywords:
- BC32126
ms.assetid: 2325668b-e2ad-40ee-a1ec-30450236c20d
ms.openlocfilehash: 61c6fe7c33b3292066e653304ded43a863413723
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84397220"
---
# <a name="methods-of-systemnullableof-t-cannot-be-used-as-operands-of-the-addressof-operator"></a><span data-ttu-id="feaac-102">È impossibile utilizzare i metodi di "System.Nullable (Of T)" come operandi dell'operatore "AddressOf".</span><span class="sxs-lookup"><span data-stu-id="feaac-102">Methods of 'System.Nullable(Of T)' cannot be used as operands of the 'AddressOf' operator</span></span>
<span data-ttu-id="feaac-103">Un'istruzione usa l' `AddressOf` operatore con un operando che rappresenta una routine della <xref:System.Nullable%601> struttura.</span><span class="sxs-lookup"><span data-stu-id="feaac-103">A statement uses the `AddressOf` operator with an operand that represents a procedure of the <xref:System.Nullable%601> structure.</span></span>  
  
 <span data-ttu-id="feaac-104">**ID errore:** BC32126</span><span class="sxs-lookup"><span data-stu-id="feaac-104">**Error ID:** BC32126</span></span>  
  
## <a name="to-correct-this-error"></a><span data-ttu-id="feaac-105">Per correggere l'errore</span><span class="sxs-lookup"><span data-stu-id="feaac-105">To correct this error</span></span>  
  
- <span data-ttu-id="feaac-106">Sostituire il nome della stored procedure nella `AddressOf` clausola con un operando che non è un membro di <xref:System.Nullable%601> .</span><span class="sxs-lookup"><span data-stu-id="feaac-106">Replace the procedure name in the `AddressOf` clause with an operand that is not a member of <xref:System.Nullable%601>.</span></span>  
  
- <span data-ttu-id="feaac-107">Scrivere una classe che esegue il wrapping del metodo di <xref:System.Nullable%601> che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="feaac-107">Write a class that wraps the method of <xref:System.Nullable%601> that you want to use.</span></span> <span data-ttu-id="feaac-108">Nell'esempio seguente, la `NullableWrapper` classe definisce un nuovo metodo denominato `GetValueOrDefault` .</span><span class="sxs-lookup"><span data-stu-id="feaac-108">In the following example, the `NullableWrapper` class defines a new method named `GetValueOrDefault`.</span></span> <span data-ttu-id="feaac-109">Poiché questo nuovo metodo non è un membro di <xref:System.Nullable%601> , può essere applicato a `nullInstance` , un'istanza di un tipo nullable, per formare un argomento per `AddressOf` .</span><span class="sxs-lookup"><span data-stu-id="feaac-109">Because this new method is not a member of <xref:System.Nullable%601>, it can be applied to `nullInstance`, an instance of a nullable type, to form an argument for `AddressOf`.</span></span>  
  
```vb  
Module Module1  
  
    Delegate Function Deleg() As Integer  
  
    Sub Main()  
        Dim nullInstance As New Nullable(Of Integer)(1)  
  
        Dim del As Deleg  
  
        ' GetValueOrDefault is a method of the Nullable generic  
        ' type. It cannot be used as an operand of AddressOf.  
        ' del = AddressOf nullInstance.GetValueOrDefault  
  
        ' The following line uses the GetValueOrDefault method  
        ' defined in the NullableWrapper class.  
        del = AddressOf (New NullableWrapper(  
            Of Integer)(nullInstance)).GetValueOrDefault  
  
        Console.WriteLine(del.Invoke())  
    End Sub  
  
    Class NullableWrapper(Of T As Structure)  
        Private m_Value As Nullable(Of T)  
  
        Sub New(ByVal Value As Nullable(Of T))  
            m_Value = Value  
        End Sub  
  
        Public Function GetValueOrDefault() As T  
            Return m_Value.Value  
        End Function  
    End Class  
End Module  
```  
  
## <a name="see-also"></a><span data-ttu-id="feaac-110">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="feaac-110">See also</span></span>

- <xref:System.Nullable%601>
- [<span data-ttu-id="feaac-111">Operatore AddressOf</span><span class="sxs-lookup"><span data-stu-id="feaac-111">AddressOf Operator</span></span>](../operators/addressof-operator.md)
- [<span data-ttu-id="feaac-112">Tipi di valore Nullable</span><span class="sxs-lookup"><span data-stu-id="feaac-112">Nullable Value Types</span></span>](../../programming-guide/language-features/data-types/nullable-value-types.md)
- [<span data-ttu-id="feaac-113">Generic Types in Visual Basic</span><span class="sxs-lookup"><span data-stu-id="feaac-113">Generic Types in Visual Basic</span></span>](../../programming-guide/language-features/data-types/generic-types.md)
