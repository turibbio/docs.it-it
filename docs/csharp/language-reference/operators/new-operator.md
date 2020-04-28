---
title: Operatore new - Riferimenti per C#
ms.date: 06/25/2019
helpviewer_keywords:
- new operator keyword [C#]
ms.assetid: a212b697-a79b-4105-9923-1f7b108036e8
ms.openlocfilehash: ed18c42cd28412a967c94a65c2a92b0b75097b52
ms.sourcegitcommit: 5988e9a29cedb8757320817deda3c08c6f44a6aa
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/28/2020
ms.locfileid: "82199729"
---
# <a name="new-operator-c-reference"></a>Operatore new (riferimenti per C#)

L'operatore `new` consente di creare una nuova istanza di un tipo.

È anche possibile usare la parola chiave `new` come [modificatore di dichiarazione di membro](../keywords/new-modifier.md) o come [vincolo di tipo generico](../keywords/new-constraint.md).

## <a name="constructor-invocation"></a>Chiamata di un costruttore

Per creare una nuova istanza di un tipo, in genere si chiama uno dei [costruttori](../../programming-guide/classes-and-structs/constructors.md) del tipo in questione tramite l'operatore `new`:

[!code-csharp-interactive[invoke constructor](snippets/NewOperator.cs#Constructor)]

È possibile usare un [inizializzatore di oggetto o insieme](../../programming-guide/classes-and-structs/object-and-collection-initializers.md) con l'operatore `new` per creare un'istanza di un oggetto e inizializzare l'oggetto in un'unica istruzione, come illustrato nell'esempio seguente:

[!code-csharp-interactive[constructor with initializer](snippets/NewOperator.cs#ConstructorWithInitializer)]

## <a name="array-creation"></a>creazione di matrici

È possibile usare l'operatore `new` per creare un'istanza di matrice, come illustrato nell'esempio seguente:

[!code-csharp-interactive[create array](snippets/NewOperator.cs#Array)]

Usare la sintassi di inizializzazione di una matrice per creare un'istanza di una matrice e popolarla con elementi in un'unica istruzione. L'esempio seguente illustra diversi modi per eseguire questa operazione:

[!code-csharp-interactive[initialize array](snippets/NewOperator.cs#ArrayInitialization)]

Per altre informazioni sulle matrici, vedere [Matrici](../../programming-guide/arrays/index.md).

## <a name="instantiation-of-anonymous-types"></a>Creazione di istanze di tipi anonimi

Per creare un'istanza di un [tipo anonimo](../../programming-guide/classes-and-structs/anonymous-types.md), usare l'operatore `new` e la sintassi dell'inizializzatore di oggetto:

[!code-csharp-interactive[anonymous type](snippets/NewOperator.cs#AnonymousType)]

## <a name="destruction-of-type-instances"></a>Eliminazione di istanze di tipi

Non è necessario eliminare definitivamente istanze di tipi create in precedenza. Le istanze dei tipi riferimento e valore vengono eliminate definitivamente in modo automatico. Le istanze dei tipi valore vengono eliminate definitivamente non appena viene eliminato definitivamente il contesto che le contiene. Le istanze dei tipi di riferimento vengono distrutte dal [Garbage Collector](../../../standard/garbage-collection/index.md) in un momento non specificato dopo che è stato rimosso l'ultimo riferimento.

Per le istanze di tipo che contengono risorse non gestite, ad esempio un handle di file, è consigliabile usare la pulizia deterministica per assicurarsi che le risorse che contengono siano rilasciate il prima possibile. Per altre informazioni, vedere le informazioni di riferimento dell'API <xref:System.IDisposable?displayProperty=nameWithType> e l'articolo sull'[ istruzione using ](../keywords/using-statement.md).

## <a name="operator-overloadability"></a>Overload degli operatori

Un tipo definito dall'utente non può eseguire l'overload dell'operatore `new`.

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

Per altre informazioni, vedere la sezione [Operatore new](~/_csharplang/spec/expressions.md#the-new-operator) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Vedere anche

- [Informazioni di riferimento su C#](../index.md)
- [Operatori C#](index.md)
- [Inizializzatori di oggetto e di raccolta](../../programming-guide/classes-and-structs/object-and-collection-initializers.md)
