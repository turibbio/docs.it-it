---
title: Indicizzatori nelle interfacce - Guida per programmatori C#
ms.date: 02/08/2020
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: 9ce6e4f0e0533c2880c6241f44409435248a336a
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84287480"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a>Indicizzatori nelle interfacce (Guida per programmatori C#)

Gli indicizzatori possono essere dichiarati su una [interfaccia](../../language-reference/keywords/interface.md). Le funzioni di accesso degli indicizzatori di interfaccia differiscono dalle funzioni di accesso degli indicizzatori di [classe](../../language-reference/keywords/class.md) per gli aspetti seguenti:

- Le funzioni di accesso di interfaccia non usano modificatori.
- Una funzione di accesso di interfaccia non dispone in genere di un corpo.

Lo scopo della funzione di accesso è indicare se l'indicizzatore è di lettura/scrittura, di sola lettura o di sola scrittura. È possibile fornire un'implementazione per un indicizzatore definito in un'interfaccia, ma si tratta di una situazione rara. Gli indicizzatori in genere definiscono un'API per accedere ai campi dati e i campi dati non possono essere definiti in un'interfaccia.

Nell'esempio seguente viene illustrata la funzione di accesso di un indicizzatore di interfaccia:

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#DefineIndexer)]

È necessario che la firma di un indicizzatore sia diversa dalle firme di tutti gli altri indicizzatori dichiarati nella stessa interfaccia.

## <a name="example"></a>Esempio

Nell'esempio seguente viene illustrato come implementare gli indicizzatori di interfaccia.

[!code-csharp[Implement](~/samples/snippets/csharp/interfaces/indexers.cs#ImplementInterface)]

[!code-csharp[DefineInterface](~/samples/snippets/csharp/interfaces/indexers.cs#ExampleCode)]

Nell'esempio precedente era possibile adottare l'implementazione esplicita del membro dell'interfaccia usando il nome completo del membro dell'interfaccia. Ad esempio

```csharp
string IIndexInterface.this[int index]
{
}
```

Il nome completo, tuttavia, è necessario soltanto per evitare l'ambiguità quando la classe implementa più di un'interfaccia con la stessa firma di indicizzatore. Se una classe `Employee` implementa, ad esempio, due interfacce, `ICitizen` e `IEmployee`, ed entrambe le interfacce hanno la stessa firma di indicizzatore, sarà necessaria l'implementazione esplicita del membro dell'interfaccia. In altre parole, la dichiarazione di indicizzatore seguente:

```csharp
string IEmployee.this[int index]
{
}
```

implementa l'indicizzatore nell'interfaccia `IEmployee`, mentre la dichiarazione seguente:

```csharp
string ICitizen.this[int index]
{
}
```

implementa l'indicizzatore nell'interfaccia `ICitizen`.

## <a name="see-also"></a>Vedere anche

- [Guida per programmatori C#](../index.md)
- [Indicizzatori](./index.md)
- [Proprietà](../classes-and-structs/properties.md)
- [Interfacce](../interfaces/index.md)
