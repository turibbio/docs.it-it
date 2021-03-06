---
title: Creazione di un'istanza di un oggetto DateTimeOffset
description: Informazioni su come creare un'istanza di un oggetto DateTimeOffset (creare un'istanza di) in .NET. Informazioni sui valori letterali data & ora, sui costruttori, sulla conversione implicita dei tipi & altro.
ms.date: 04/10/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- instantiating time zone objects
- time zone objects [.NET Framework], instantiation
- DateTimeOffset structure, converting to DateTime
- DateTimeOffset structure, instantiating
ms.assetid: 9648375f-d368-4373-a976-3332ece00c0a
ms.openlocfilehash: c2b71a2a98353a4ec9ed249acf18939dd4740e99
ms.sourcegitcommit: 5fd4696a3e5791b2a8c449ccffda87f2cc2d4894
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84768898"
---
# <a name="instantiating-a-datetimeoffset-object"></a>Creazione di un'istanza di un oggetto DateTimeOffset

La <xref:System.DateTimeOffset> struttura offre diversi modi per creare nuovi <xref:System.DateTimeOffset> valori. Molti di essi corrispondono direttamente ai metodi disponibili per creare istanze dei nuovi <xref:System.DateTime> valori, con miglioramenti che consentono di specificare l'offset del valore di data e ora rispetto all'ora UTC (Coordinated Universal Time). In particolare, è possibile creare un'istanza di un <xref:System.DateTimeOffset> valore nei modi seguenti:

- Utilizzando un valore letterale di data e ora.

- Chiamando un <xref:System.DateTimeOffset> costruttore.

- Convertendo in modo implicito un valore in <xref:System.DateTimeOffset> valore.

- Analizzando la rappresentazione di stringa di una data e dell'ora.

In questo argomento vengono forniti maggiori dettagli ed esempi di codice in cui vengono illustrati questi metodi di creazione di un'istanza di nuovi <xref:System.DateTimeOffset> valori.

## <a name="date-and-time-literals"></a>Valori letterali data e ora

Per i linguaggi che lo supportano, uno dei modi più comuni per creare un'istanza di un <xref:System.DateTime> valore consiste nel fornire la data e l'ora come valore letterale hardcoded. Il codice di Visual Basic seguente, ad esempio, crea un <xref:System.DateTime> oggetto il cui valore è il 1 gennaio 2008, alle 10:00.

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#1)]

<xref:System.DateTimeOffset>i valori possono essere inizializzati anche con valori letterali di data e ora quando si usano linguaggi che supportano i valori <xref:System.DateTime> letterali. Il codice Visual Basic seguente, ad esempio, crea un <xref:System.DateTimeOffset> oggetto.

[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#2)]

Come mostra l'output della console, il <xref:System.DateTimeOffset> valore creato in questo modo viene assegnato all'offset del fuso orario locale. Ciò significa che un <xref:System.DateTimeOffset> valore assegnato usando un valore letterale carattere non identifica un singolo momento se il codice viene eseguito in computer diversi.

## <a name="datetimeoffset-constructors"></a>Costruttori DateTimeOffset

Il <xref:System.DateTimeOffset> tipo definisce sei costruttori. Quattro di esse corrispondono direttamente ai <xref:System.DateTime> costruttori, con un parametro aggiuntivo di tipo <xref:System.TimeSpan> che definisce l'offset di data e ora rispetto all'ora UTC. Questi consentono di definire un <xref:System.DateTimeOffset> valore in base al valore dei singoli componenti di data e ora. Il codice seguente, ad esempio, usa questi quattro costruttori per creare un'istanza di <xref:System.DateTimeOffset> oggetti con valori identici di 7/1/2008 12:05 AM + 01:00.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#3)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#3)]

Si noti che, quando il valore dell' <xref:System.DateTimeOffset> oggetto di cui è stata creata un'istanza usando un <xref:System.Globalization.PersianCalendar> oggetto come uno degli argomenti per il relativo costruttore viene visualizzato nella console, viene espresso come data nel calendario gregoriano anziché nel calendario persiano. Per restituire una data utilizzando il calendario persiano, vedere l'esempio nell' <xref:System.Globalization.PersianCalendar> argomento.

Gli altri due costruttori creano un <xref:System.DateTimeOffset> oggetto da un <xref:System.DateTime> valore. Il primo di questi ha un solo parametro, il <xref:System.DateTime> valore da convertire in un <xref:System.DateTimeOffset> valore. L'offset del valore risultante <xref:System.DateTimeOffset> dipende dalla <xref:System.DateTime.Kind%2A> proprietà dell'unico parametro del costruttore. Se il valore è <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> , l'offset viene impostato su un valore uguale a <xref:System.TimeSpan.Zero?displayProperty=nameWithType> . In caso contrario, l'offset viene impostato su un valore uguale a quello del fuso orario locale. Nell'esempio seguente viene illustrato l'utilizzo di questo costruttore per creare un'istanza di <xref:System.DateTimeOffset> oggetti che rappresentano l'ora UTC e il fuso orario locale:

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#4)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#4)]

> [!NOTE]
> La chiamata dell'overload del <xref:System.DateTimeOffset> costruttore che dispone di un singolo <xref:System.DateTime> parametro equivale all'esecuzione di una conversione implicita di un <xref:System.DateTime> valore in un <xref:System.DateTimeOffset> valore.

Il secondo costruttore che crea un <xref:System.DateTimeOffset> oggetto da un <xref:System.DateTime> valore ha due parametri: il <xref:System.DateTime> valore da convertire e un <xref:System.TimeSpan> valore che rappresenta l'offset di data e ora rispetto all'ora UTC. Questo valore di offset deve corrispondere alla <xref:System.DateTime.Kind%2A> proprietà del primo parametro del costruttore oppure <xref:System.ArgumentException> viene generata un'eccezione. Se la <xref:System.DateTime.Kind%2A> proprietà del primo parametro è <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> , il valore del secondo parametro deve essere <xref:System.TimeSpan.Zero?displayProperty=nameWithType> . Se la <xref:System.DateTime.Kind%2A> proprietà del primo parametro è <xref:System.DateTimeKind.Local?displayProperty=nameWithType> , il valore del secondo parametro deve essere l'offset del fuso orario del sistema locale. Se la <xref:System.DateTime.Kind%2A> proprietà del primo parametro è <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> , l'offset può essere qualsiasi valore valido. Il codice seguente illustra le chiamate a questo costruttore per convertire <xref:System.DateTime> <xref:System.DateTimeOffset> i valori.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#5)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#5)]

## <a name="implicit-type-conversion"></a>Conversione implicita di tipi

Il <xref:System.DateTimeOffset> tipo supporta una conversione implicita di tipi: da un <xref:System.DateTime> valore a un <xref:System.DateTimeOffset> valore. Una conversione implicita di tipi è una conversione da un tipo in un altro che non richiede un cast esplicito (in C#) o una conversione esplicita (in Visual Basic) e nella quale non vengono perse informazioni. Rende possibile la scrittura di codice come il seguente.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#6)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#6)]

L'offset del valore risultante <xref:System.DateTimeOffset> dipende dal <xref:System.DateTime.Kind%2A?displayProperty=nameWithType> valore della proprietà. Se il valore è <xref:System.DateTimeKind.Utc?displayProperty=nameWithType> , l'offset viene impostato su un valore uguale a <xref:System.TimeSpan.Zero?displayProperty=nameWithType> . Se il valore è <xref:System.DateTimeKind.Local?displayProperty=nameWithType> o <xref:System.DateTimeKind.Unspecified?displayProperty=nameWithType> , l'offset viene impostato su un valore uguale a quello del fuso orario locale.

## <a name="parsing-the-string-representation-of-a-date-and-time"></a>Analisi della rappresentazione di stringa di una data e di un'ora

Il <xref:System.DateTimeOffset> tipo supporta quattro metodi che consentono di convertire la rappresentazione di stringa di una data e di un'ora in un <xref:System.DateTimeOffset> valore:

- <xref:System.DateTimeOffset.Parse%2A>, che tenta di convertire la rappresentazione di stringa di una data e di un'ora in un <xref:System.DateTimeOffset> valore e genera un'eccezione se la conversione non riesce.

- <xref:System.DateTimeOffset.TryParse%2A>, che tenta di convertire la rappresentazione di stringa di una data e di un'ora in un <xref:System.DateTimeOffset> valore e restituisce `false` se la conversione non riesce.

- <xref:System.DateTimeOffset.ParseExact%2A>, che tenta di convertire in un valore la rappresentazione di stringa di una data e di un'ora in un formato specificato <xref:System.DateTimeOffset> . Il metodo genera un'eccezione se la conversione non riesce.

- <xref:System.DateTimeOffset.TryParseExact%2A>, che tenta di convertire in un valore la rappresentazione di stringa di una data e di un'ora in un formato specificato <xref:System.DateTimeOffset> . Il metodo restituisce `false` se la conversione non riesce.

Nell'esempio seguente vengono illustrate le chiamate a ognuno di questi quattro metodi di conversione di stringhe per creare un'istanza di un <xref:System.DateTimeOffset> valore.

[!code-csharp[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/cs/Instantiate.cs#7)]
[!code-vb[System.DateTimeOffset.Conceptual.Instantiate#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.DateTimeOffset.Conceptual.Instantiate/vb/Instantiate.vb#7)]

## <a name="see-also"></a>Vedere anche

- [Date, ore e fusi orari](index.md)
