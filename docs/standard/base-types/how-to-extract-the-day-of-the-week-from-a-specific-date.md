---
title: 'Procedura: Estrarre il giorno della settimana da una data specifica'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- formatting [.NET Framework], dates
- DateTime.DayOfWeek property
- DateTime.ToString method
- dates [.NET Framework], retrieving week information
- DateTimeOffset.DayOfWeek property
- dates [.NET Framework], day of week
- Weekday function
- day of week [.NET Framework]
- extracting day of week
- weekday names
- WeekdayName function
- numbers [.NET Framework], day of week
- formatting [.NET Framework], time
- DateTimeOffset.ToString method
- full weekday names
ms.assetid: 1c9bef76-5634-46cf-b91c-9b9eb72091d7
ms.openlocfilehash: 128ff4887601431f75981f13b51a11469e65d65c
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84290474"
---
# <a name="how-to-extract-the-day-of-the-week-from-a-specific-date"></a>Procedura: Estrarre il giorno della settimana da una data specifica
.NET Framework consente di determinare in modo semplice il giorno ordinale della settimana e di visualizzare il nome del giorno della settimana localizzato per una data specifica. Un valore enumerato che indica il giorno della settimana corrispondente a una determinata data è specificato dalla proprietà <xref:System.DateTime.DayOfWeek%2A> o <xref:System.DateTimeOffset.DayOfWeek%2A>. Al contrario, il recupero del nome del giorno della settimana è un'operazione di formattazione che può essere eseguita effettuando la chiamata a un metodo di formattazione, ad esempio il metodo `ToString` del valore di data e ora o il metodo <xref:System.String.Format%2A?displayProperty=nameWithType>. In questo argomento viene illustrato come eseguire queste operazioni di formattazione.  
  
### <a name="to-extract-a-number-indicating-the-day-of-the-week-from-a-specific-date"></a>Per estrarre un numero che indica il giorno della settimana da una data specifica  
  
1. Se si usa la rappresentazione di stringa di una data, convertirla in un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> tramite il metodo statico <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> o <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType>.  
  
2. Usare la proprietà <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> o <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> per recuperare un valore <xref:System.DayOfWeek> che indica il giorno della settimana.  
  
3. Se necessario, eseguire il cast (in C#) o convertire (in Visual Basic) il valore <xref:System.DayOfWeek> in un valore integer.  
  
 Nell'esempio seguente è visualizzato un valore integer che rappresenta il giorno della settimana di una data specifica.  
  
 [!code-csharp[Formatting.Howto.WeekdayName#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/weekdaynumber7.cs#7)]
 [!code-vb[Formatting.Howto.WeekdayName#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/weekdaynumber7.vb#7)]  
  
### <a name="to-extract-the-abbreviated-weekday-name-from-a-specific-date"></a>Per estrarre il nome del giorno della settimana abbreviato da una data specifica  
  
1. Se si usa la rappresentazione di stringa di una data, convertirla in un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> tramite il metodo statico <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> o <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType>.  
  
2. È possibile estrarre il nome del giorno della settimana abbreviato delle impostazioni di cultura correnti o di impostazioni di cultura specifiche:  
  
    1. Per estrarre il nome del giorno della settimana abbreviato per le impostazioni di cultura correnti, chiamare il metodo di istanza <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> o <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> del valore di data e ora e passare la stringa "ddd" come parametro `format`. Nell'esempio seguente viene illustrata la chiamata al metodo <xref:System.DateTime.ToString%28System.String%29>.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname1.cs#1)]
         [!code-vb[Formatting.Howto.WeekdayName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname1.vb#1)]  
  
    2. Per estrarre il nome del giorno della settimana abbreviato per impostazioni cultura specifiche, chiamare il <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> metodo di istanza o del valore di data e ora <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> . Passare la stringa "ddd" come parametro `format`. Passare un oggetto <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.DateTimeFormatInfo> che rappresenta le impostazioni di cultura per cui si vuole recuperare il nome del giorno della settimana come parametro `provider`. Nel codice seguente viene illustrata una chiamata al metodo <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> usando un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni di cultura fr-FR.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/abbrname2.cs#2)]
         [!code-vb[Formatting.Howto.WeekdayName#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/abbrname2.vb#2)]  
  
### <a name="to-extract-the-full-weekday-name-from-a-specific-date"></a>Per estrarre il nome del giorno della settimana esteso da una data specifica  
  
1. Se si usa la rappresentazione di stringa di una data, convertirla in un valore <xref:System.DateTime> o <xref:System.DateTimeOffset> tramite il metodo statico <xref:System.DateTime.Parse%2A?displayProperty=nameWithType> o <xref:System.DateTimeOffset.Parse%2A?displayProperty=nameWithType>.  
  
2. È possibile estrarre il nome del giorno della settimana esteso delle impostazioni di cultura correnti o di impostazioni di cultura specifiche:  
  
    1. Per estrarre il nome del giorno della settimana per le impostazioni cultura correnti, chiamare il metodo di istanza o del valore di data e ora <xref:System.DateTime.ToString%28System.String%29?displayProperty=nameWithType> <xref:System.DateTimeOffset.ToString%28System.String%29?displayProperty=nameWithType> e passare la stringa "dddd" come `format` parametro. Nell'esempio seguente viene illustrata la chiamata al metodo <xref:System.DateTime.ToString%28System.String%29>.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname4.cs#4)]
         [!code-vb[Formatting.Howto.WeekdayName#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname4.vb#4)]  
  
    2. Per estrarre il nome del giorno della settimana per impostazioni cultura specifiche, chiamare il metodo di istanza o del valore di data e ora <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> <xref:System.DateTimeOffset.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> . Passare la stringa "dddd" come parametro `format`. Passare un oggetto <xref:System.Globalization.CultureInfo> o <xref:System.Globalization.DateTimeFormatInfo> che rappresenta le impostazioni di cultura per cui si vuole recuperare il nome del giorno della settimana come parametro `provider`. Nel codice seguente viene illustrata una chiamata al metodo <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29> usando un oggetto <xref:System.Globalization.CultureInfo> che rappresenta le impostazioni di cultura es-ES.  
  
         [!code-csharp[Formatting.Howto.WeekdayName#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/fullname5.cs#5)]
         [!code-vb[Formatting.Howto.WeekdayName#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/fullname5.vb#5)]  
  
## <a name="example"></a>Esempio  
 Nell'esempio vengono illustrate le chiamate alle proprietà <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> e <xref:System.DateTimeOffset.DayOfWeek%2A?displayProperty=nameWithType> e i metodi <xref:System.DateTime.ToString%2A?displayProperty=nameWithType> e <xref:System.DateTimeOffset.ToString%2A?displayProperty=nameWithType> per recuperare il numero che rappresenta il giorno della settimana, il nome del giorno della settimana abbreviato e il nome del giorno della settimana esteso per una data specifica.  
  
 [!code-csharp[Formatting.Howto.WeekdayName#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/example6.cs#6)]
 [!code-vb[Formatting.Howto.WeekdayName#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example6.vb#6)]  
  
 I singoli linguaggi possono offrire funzionalità che duplicano o completano la funzionalità offerta da .NET Framework. In Visual Basic, ad esempio, sono disponibili due funzioni di questo tipo:  
  
- `Weekday`, che restituisce un numero che indica il giorno della settimana di una data specifica. Considera che il valore ordinale del primo giorno della settimana sia pari a uno, mentre la proprietà <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> considera che questo sia pari a zero.  
  
- `WeekdayName`, che restituisce il nome della settimana nelle impostazioni di cultura correnti, corrispondente a un numero di giorno della settimana specifico.  
  
 Nell'esempio seguente viene illustrato l'uso delle funzioni `Weekday` e `WeekdayName` di Visual Basic.  
  
 [!code-vb[Formatting.HowTo.WeekdayName#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/example9.vb#9)]  
  
 È anche possibile usare il valore restituito dalla proprietà <xref:System.DateTime.DayOfWeek%2A?displayProperty=nameWithType> per recuperare il nome del giorno della settimana di una data specifica. È necessario effettuare una chiamata al metodo <xref:System.Enum.ToString%2A> sul valore <xref:System.DayOfWeek> restituito dalla proprietà. Questa tecnica non restituisce tuttavia un nome del giorno della settimana localizzato per le impostazioni di cultura correnti, come illustrato nell'esempio seguente.  
  
 [!code-csharp[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/cs/Howto1.cs#8)]
 [!code-vb[Formatting.HowTo.WeekdayName#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.WeekdayName/vb/Howto1.vb#8)]

## <a name="see-also"></a>Vedere anche

- [Stringhe di formato di data e ora standard](standard-date-and-time-format-strings.md)
- [Stringhe di formato di data e ora personalizzato](custom-date-and-time-format-strings.md)
