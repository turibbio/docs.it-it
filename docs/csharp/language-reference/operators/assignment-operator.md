---
title: Operatori di assegnazione - Riferimento in C
ms.date: 09/10/2019
f1_keywords:
- =_CSharpKeyword
helpviewer_keywords:
- = operator [C#]
ms.assetid: d802a6d5-32f0-42b8-b180-12f5a081bfc1
ms.openlocfilehash: 420b41f586a6980d40cf1171eef00dad37bf5abf
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/14/2020
ms.locfileid: "79399252"
---
# <a name="assignment-operators-c-reference"></a>Operatori di assegnazione (riferimenti per C

L'operatore di assegnazione `=` assegna il valore dell'operando a destra a una variabile, una [proprietà](../../programming-guide/classes-and-structs/properties.md) o un elemento [indicizzatore](../../programming-guide/indexers/index.md) indicato dall'operando a sinistra. Il risultato di un'espressione di assegnazione è il valore assegnato all'operando a sinistra. Il tipo dell'operando destro deve corrispondere al tipo dell'operando sinistro o essere convertibile in modo implicito in esso.

L'operatore di assegnazione `=` è associativo a destra, ovvero un'espressione nel formato

```csharp
a = b = c
```

viene valutata come

```csharp
a = (b = c)
```

L'esempio seguente illustra l'utilizzo dell'operatore di assegnazione con una variabile locale, una proprietà e un elemento indicizzatore come operando sul lato sinistro:

[!code-csharp-interactive[simple assignment](snippets/AssignmentOperator.cs#Simple)]

## <a name="ref-assignment-operator"></a>Operatore di assegnazione ref

A partire da C# 7.3, è possibile usare l'operatore di assegnazione ref `= ref` per riassegnare una variabile [locale ref](../keywords/ref.md#ref-locals) o [locale ref readonly](../keywords/ref.md#ref-readonly-locals). L'esempio seguente illustra l'uso dell'operatore di assegnazione ref:

[!code-csharp[ref assignment operator](snippets/AssignmentOperator.cs#RefAssignment)]

Nel caso dell'operatore di assegnazione ref, entrambi gli operandi devono essere dello stesso tipo.

## <a name="compound-assignment"></a>Assegnazione composta

Per un operatore binario `op`, un'espressione di assegnazione composta in formato

```csharp
x op= y
```

equivale a

```csharp
x = x op y
```

con la differenza che `x` viene valutato una sola volta.

L'assegnazione composta è supportata da operatori [aritmetici](arithmetic-operators.md#compound-assignment), [logici booleani](boolean-logical-operators.md#compound-assignment) e [logici bit per bit e shift](bitwise-and-shift-operators.md#compound-assignment).

## <a name="null-coalescing-assignment"></a>Assegnazione di valori Null

A partire dalla versione 8.0 di C, è possibile `??=` utilizzare l'operatore di assegnazione null-coalescing per assegnare il valore del relativo operando di destra al relativo operando di sinistra solo se l'operando di sinistra restituisce `null`. Per ulteriori informazioni, vedere il [?? e ?? :](null-coalescing-operator.md) articolo degli operatori.

## <a name="operator-overloadability"></a>Overload degli operatori

Un tipo definito dall'utente non può [eseguire l'overload](operator-overloading.md) dell'operatore di assegnazione. Tuttavia, un tipo definito dall'utente può definire una conversione implicita in un altro tipo. In questo modo il valore di un tipo definito dall'utente può essere assegnato a una variabile, una proprietà o un elemento indicizzatore di un altro tipo. Per altre informazioni, vedere [Operatori di conversione definiti dall'utente](user-defined-conversion-operators.md).

Un tipo definito dall'utente non può eseguire in modo esplicito l'overload di un operatore di assegnazione composta. Tuttavia, se un tipo definito dall'utente esegue l'overload di un operatore `op`binario , anche l'operatore, `op=` se esistente, viene sottoposto a overload in modo implicito.

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

Per altre informazioni, vedere la sezione [Operatori di assegnazione](~/_csharplang/spec/expressions.md#assignment-operators) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).

Per ulteriori informazioni sull'operatore `= ref`di assegnazione dei riferimenti , vedere la [nota](~/_csharplang/proposals/csharp-7.3/ref-local-reassignment.md)della proposta di funzionalità .

## <a name="see-also"></a>Vedere anche

- [Informazioni di riferimento su C#](../index.md)
- [Operatori C#](index.md)
- [ref (parola chiave)](../keywords/ref.md)
