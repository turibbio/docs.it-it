---
title: + Operatori + e += - Riferimenti per C#
ms.date: 04/23/2020
f1_keywords:
- +_CSharpKeyword
- +=_CSharpKeyword
helpviewer_keywords:
- addition operator [C#]
- concatenation operator [C#]
- delegate combination [C#]
- + operator [C#]
- addition assignment operator [C#]
- event subscription [C#]
- += operator [C#]
ms.assetid: 93e56486-bb42-43c1-bd43-60af11e64e67
ms.openlocfilehash: 18364d80b8117fd4074c2c4231eac07c76829bb3
ms.sourcegitcommit: 8b02d42f93adda304246a47f49f6449fc74a3af4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82135737"
---
# <a name="-and--operators-c-reference"></a>Operatori + e += (Riferimenti per C#)

Gli `+` operatori `+=` e sono supportati dai tipi numerici [integrali](../builtin-types/integral-numeric-types.md) e a [virgola mobile](../builtin-types/floating-point-numeric-types.md) incorporati, dal tipo di [stringa](../builtin-types/reference-types.md#the-string-type) e dai tipi [delegati](../builtin-types/reference-types.md#the-delegate-type) .

Per informazioni sull'operatore aritmetico `+`, vedere le sezioni [Operatori più e meno unari](arithmetic-operators.md#unary-plus-and-minus-operators) e [Operatore di addizione +](arithmetic-operators.md#addition-operator-) dell'articolo [Operatori aritmetici](arithmetic-operators.md).

## <a name="string-concatenation"></a>Concatenazione di stringhe

Quando uno o entrambi gli operandi sono di tipo [stringa](../builtin-types/reference-types.md#the-string-type), l' `+` operatore concatena le rappresentazioni di stringa dei relativi operandi (la rappresentazione di stringa `null` di è una stringa vuota):

[!code-csharp-interactive[string concatenation](snippets/AdditionOperator.cs#AddStrings)]

A partire da C# 6, l' [interpolazione di stringhe](../tokens/interpolated.md) rappresenta un modo più pratico per formattare le stringhe:

[!code-csharp-interactive[string interpolation](snippets/AdditionOperator.cs#UseStringInterpolation)]

## <a name="delegate-combination"></a>Combinazione di delegati

Per gli operandi con lo stesso tipo [delegato](../builtin-types/reference-types.md#the-delegate-type), l'operatore `+` restituisce una nuova istanza di delegato che, quando viene chiamata, richiama l'operando di sinistra e quindi quello di destra. Se uno degli operandi è `null`, l'operatore `+` restituisce il valore di un altro operando, che può essere anch'esso `null`. L'esempio seguente mostra in che modo è possibile combinare delegati con l'operatore `+`:

[!code-csharp-interactive[delegate combination](snippets/AdditionOperator.cs#AddDelegates)]

Per eseguire la rimozione dei delegati, usare l' [ `-` operatore](subtraction-operator.md#delegate-removal).

Per altre informazioni sui tipi delegate, vedere [Delegati](../../programming-guide/delegates/index.md).

## <a name="addition-assignment-operator-"></a>Operatore di assegnazione di addizione +=

Un'espressione che usa l'operatore `+=`, ad esempio

```csharp
x += y
```

equivale a

```csharp
x = x + y
```

con la differenza che `x` viene valutato una sola volta.

Nell'esempio seguente viene illustrato l'uso dell'operatore `+=`:

[!code-csharp-interactive[+= examples](snippets/AdditionOperator.cs#AddAndAssign)]

È anche possibile usare l'operatore `+=` per specificare un metodo del gestore eventi quando si sottoscrive un [evento](../keywords/event.md). Per altre informazioni, vedere [Procedura: Sottoscrivere e annullare la sottoscrizione di eventi](../../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).

## <a name="operator-overloadability"></a>Overload degli operatori

Un tipo definito dall'utente può eseguire l'[overload](operator-overloading.md) dell'operatore `+`. Quando viene eseguito l'overload di un operatore `+` binario, viene eseguito in modo implicito anche l'overload dell'operatore `+=`. Un tipo definito dall'utente non può eseguire l'overload dell'operatore `+=` in modo esplicito.

## <a name="c-language-specification"></a>Specifiche del linguaggio C#

Per altre informazioni, vedere le sezioni [Operatore + unario](~/_csharplang/spec/expressions.md#unary-plus-operator) e [Operatore addizione](~/_csharplang/spec/expressions.md#addition-operator) della [specifica del linguaggio C#](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Vedi anche

- [Informazioni di riferimento su C#](../index.md)
- [Operatori C#](index.md)
- [Come concatenare più stringhe](../../how-to/concatenate-multiple-strings.md)
- [Events](../../programming-guide/events/index.md)
- [Operatori aritmetici](arithmetic-operators.md)
- [operatori-and-=](subtraction-operator.md)
