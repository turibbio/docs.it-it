---
title: Utilizzo di calendari
ms.date: 04/01/2019
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- globalization [.NET], calendars
- calendars, global applications
- global applications, calendars
- world-ready applications, calendars
- international applications [.NET], calendars
- culture, calendars
ms.assetid: 0c1534e5-979b-4c8a-a588-1c24301aefb3
ms.openlocfilehash: d15bafd097c72515a33bed7dd85d88aef54246ba
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84280894"
---
# <a name="work-with-calendars"></a>Usare i calendari

Sebbene un valore di data e ora rappresenti un momento, la relativa rappresentazione di stringa è dipendente dalle impostazioni cultura e dipende sia dalle convenzioni utilizzate per visualizzare i valori di data e ora da impostazioni cultura specifiche che dal calendario utilizzato dalle impostazioni cultura. In questo argomento viene illustrato il supporto dei calendari in .NET e viene illustrato l'utilizzo delle classi calendario quando si utilizzano i valori di data.

## <a name="calendars-in-net"></a>Calendari in .NET

Tutti i calendari in .NET derivano dalla <xref:System.Globalization.Calendar?displayProperty=nameWithType> classe, che fornisce l'implementazione del calendario di base. Una delle classi che eredita dalla classe <xref:System.Globalization.Calendar> è la classe <xref:System.Globalization.EastAsianLunisolarCalendar>, che è la classe di base per tutti i calendari lunisolari. .NET include le implementazioni di calendario seguenti:

- <xref:System.Globalization.ChineseLunisolarCalendar>, che rappresenta il calendario lunisolare cinese.

- <xref:System.Globalization.GregorianCalendar>, che rappresenta il calendario gregoriano. Questo calendario viene ulteriormente suddiviso in sottotipi, ad esempio la versione araba e francese mediorientale, definiti dall'enumerazione <xref:System.Globalization.GregorianCalendarTypes?displayProperty=nameWithType>. La proprietà <xref:System.Globalization.GregorianCalendar.CalendarType%2A?displayProperty=nameWithType> specifica il sottotipo del calendario gregoriano.

- <xref:System.Globalization.HebrewCalendar>, che rappresenta il calendario ebraico.

- <xref:System.Globalization.HijriCalendar>, che rappresenta il calendario Hijri.

- <xref:System.Globalization.JapaneseCalendar>, che rappresenta il calendario giapponese.

- <xref:System.Globalization.JapaneseLunisolarCalendar>, che rappresenta il calendario lunisolare giapponese.

- <xref:System.Globalization.JulianCalendar>, che rappresenta il calendario giuliano.

- <xref:System.Globalization.KoreanCalendar>, che rappresenta il calendario coreano.

- <xref:System.Globalization.KoreanLunisolarCalendar>, che rappresenta il calendario lunisolare coreano.

- <xref:System.Globalization.PersianCalendar>, che rappresenta il calendario persiano.

- <xref:System.Globalization.TaiwanCalendar>, che rappresenta il calendario taiwanese.

- <xref:System.Globalization.TaiwanLunisolarCalendar>, che rappresenta il calendario lunisolare taiwanese.

- <xref:System.Globalization.ThaiBuddhistCalendar>, che rappresenta il calendario buddista thailandese.

- <xref:System.Globalization.UmAlQuraCalendar>, che rappresenta il calendario Um Al Qura.

Un calendario può essere utilizzato in uno dei due modi seguenti:

- Come calendario utilizzato da impostazioni cultura specifiche. Ogni oggetto <xref:System.Globalization.CultureInfo> dispone di un calendario corrente, che rappresenta il calendario utilizzato attualmente dall'oggetto. Le rappresentazioni di stringa di tutti i valori di data e ora riflettono automaticamente le impostazioni cultura correnti e il relativo calendario corrente. In genere, il calendario corrente è il calendario predefinito delle impostazioni cultura. <xref:System.Globalization.CultureInfo>gli oggetti hanno anche calendari facoltativi, che includono calendari aggiuntivi che le impostazioni cultura possono usare.

- Come calendario autonomo indipendente da impostazioni cultura specifiche. In questo caso, vengono utilizzati i metodi <xref:System.Globalization.Calendar> per esprimere le date come valori che riflettono il calendario.

Si noti che come calendari autonomi è possibile utilizzare solo sei classi di calendario, ovvero <xref:System.Globalization.ChineseLunisolarCalendar>, <xref:System.Globalization.JapaneseLunisolarCalendar>, <xref:System.Globalization.JulianCalendar>, <xref:System.Globalization.KoreanLunisolarCalendar>, <xref:System.Globalization.PersianCalendar> e <xref:System.Globalization.TaiwanLunisolarCalendar>. Esse non vengono utilizzate dalle impostazioni cultura né come calendari predefiniti né come calendari facoltativi.

## <a name="calendars-and-cultures"></a>Calendari e impostazioni cultura

Le impostazioni cultura hanno un calendario predefinito, che viene definito dalla proprietà <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType>. La proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType> restituisce una matrice di oggetti <xref:System.Globalization.Calendar> che specifica tutti i calendari supportati dalle specifiche impostazioni cultura, incluso il calendario predefinito di tali impostazioni cultura.

Nell'esempio seguente vengono illustrate le proprietà <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType> e <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>. Vengono creati gli oggetti `CultureInfo` per le impostazioni cultura thailandesi (Thailandia) e giapponesi (Giappone) e vengono visualizzati i relativi calendari predefiniti e facoltativi. Si noti che in entrambi i casi il calendario predefinito delle impostazioni cultura è incluso anche nella raccolta <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>.

[!code-csharp[Conceptual.Calendars#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/calendarinfo1.cs#1)]
[!code-vb[Conceptual.Calendars#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/calendarinfo1.vb#1)]

Il calendario attualmente in uso da un oggetto <xref:System.Globalization.CultureInfo> specifico viene definito dalla proprietà <xref:System.Globalization.DateTimeFormatInfo.Calendar%2A?displayProperty=nameWithType> delle impostazioni cultura. L'oggetto <xref:System.Globalization.DateTimeFormatInfo> delle impostazioni cultura viene restituito dalla proprietà <xref:System.Globalization.CultureInfo.DateTimeFormat%2A?displayProperty=nameWithType>. Quando vengono create le impostazioni cultura, il relativo valore predefinito è uguale al valore della proprietà <xref:System.Globalization.CultureInfo.Calendar%2A?displayProperty=nameWithType>. È tuttavia possibile sostituire il calendario corrente delle impostazioni cultura con qualsiasi calendario contenuto nella matrice restituita dalla proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>. Se si tenta di impostare il calendario corrente su un calendario che non è incluso nel valore della proprietà <xref:System.Globalization.CultureInfo.OptionalCalendars%2A?displayProperty=nameWithType>, viene generato un oggetto <xref:System.ArgumentException>.

Nell'esempio seguente viene modificato il calendario utilizzato dalle impostazioni cultura arabe (Arabia Saudita). Viene innanzitutto creata un'istanza di un valore <xref:System.DateTime>, il quale viene quindi visualizzato utilizzando le impostazioni cultura correnti che, in questo caso, sono quelle inglesi (Stati Uniti) e il calendario corrente delle impostazioni cultura che, in questo caso, è il calendario gregoriano. A questo punto vengono impostate le impostazioni cultura arabe (Arabia Saudita) e la data viene visualizzata utilizzando il calendario Um Al-Qura predefinito. Viene quindi chiamato il metodo `CalendarExists` per determinare se il calendario Hijri è supportato dalle impostazioni cultura arabe (Arabia Saudita). Poiché il calendario è supportato, il calendario corrente viene sostituito con il calendario Hijri e viene visualizzata nuovamente la data. Si noti che in ogni caso la data viene visualizzata utilizzando il calendario corrente delle impostazioni cultura correnti.

[!code-csharp[Conceptual.Calendars#2](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/changecalendar2.cs#2)]
[!code-vb[Conceptual.Calendars#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/changecalendar2.vb#2)]

## <a name="dates-and-calendars"></a>Date e calendari

Ad eccezione dei costruttori che includono un parametro di tipo <xref:System.Globalization.Calendar> e consentono agli elementi di una data, ad esempio mese, giorno e anno, di riflettere i valori in un calendario designato, entrambi i valori <xref:System.DateTime> e <xref:System.DateTimeOffset> si basano sempre sul calendario gregoriano. Ciò significa, ad esempio, che la proprietà <xref:System.DateTime.Year%2A?displayProperty=nameWithType> restituisce l'anno nel calendario gregoriano e la proprietà <xref:System.DateTime.Day%2A?displayProperty=nameWithType> restituisce il giorno del mese nel calendario gregoriano.

> [!IMPORTANT]
> È importante tenere presente che esiste una differenza tra un valore di data e la relativa rappresentazione di stringa. Il primo si basa sul calendario gregoriano, mentre il secondo si basa sul calendario corrente delle impostazioni cultura specifiche.

Nell'esempio seguente viene illustrata la differenza tra le proprietà <xref:System.DateTime> e i relativi metodi <xref:System.Globalization.Calendar> corrispondenti. Nell'esempio le impostazioni cultura correnti sono quelle arabe (Egitto) e il calendario corrente è Um Al Qura. Il valore <xref:System.DateTime> viene impostato sul quindicesimo giorno del settimo mese del 2011. Risulta chiaro che tale valore viene interpretato come data del calendario gregoriano, poiché questi stessi valori vengono restituiti dal metodo <xref:System.DateTime.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType> quando vengono utilizzate le convenzioni delle impostazioni cultura inglesi. La rappresentazione di stringa della data formattata utilizzando le convenzioni delle impostazioni cultura correnti è 14/08/32, che è la data equivalente nel calendario Um Al Qura. Successivamente, vengono utilizzati i membri di `DateTime` e `Calendar` per restituire il giorno, il mese e l'anno del valore <xref:System.DateTime>. In ogni caso, i valori restituiti dai membri di <xref:System.DateTime> riflettono i valori del calendario gregoriano, mentre i valori restituiti dai membri di <xref:System.Globalization.UmAlQuraCalendar> riflettono i valori del calendario Um Al Qura.

[!code-csharp[Conceptual.Calendars#3](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/datesandcalendars2.cs#3)]
[!code-vb[Conceptual.Calendars#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/datesandcalendars2.vb#3)]

### <a name="instantiate-dates-based-on-a-calendar"></a>Creare un'istanza di date in base a un calendario

Poiché i valori <xref:System.DateTime> e <xref:System.DateTimeOffset> si basano sul calendario gregoriano, è necessario chiamare un costruttore di overload che include un parametro di tipo <xref:System.Globalization.Calendar> per creare un'istanza di un valore di data se si desidera utilizzare i valori di giorno, mese o anno da un calendario diverso. È inoltre possibile chiamare uno degli overload del metodo <xref:System.Globalization.Calendar.ToDateTime%2A?displayProperty=nameWithType> del calendario specifico per creare un'istanza di un oggetto <xref:System.DateTime> basato sui valori di un determinato calendario.

Nell'esempio seguente viene creata un'istanza di un valore <xref:System.DateTime> passando un oggetto <xref:System.Globalization.HebrewCalendar> a un costruttore <xref:System.DateTime> e viene creata un'istanza di un secondo valore <xref:System.DateTime> chiamando il metodo <xref:System.Globalization.HebrewCalendar.ToDateTime%28System.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%2CSystem.Int32%29?displayProperty=nameWithType>. Poiché i due valori vengono creati con valori identici dal calendario ebraico, la chiamata al metodo <xref:System.DateTime.Equals%2A?displayProperty=nameWithType> mostra che i due valori <xref:System.DateTime> sono uguali.

[!code-csharp[Conceptual.Calendars#4](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatehcdate1.cs#4)]
[!code-vb[Conceptual.Calendars#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatehcdate1.vb#4)]

### <a name="represent-dates-in-the-current-calendar"></a>Rappresenta le date nel calendario corrente

I metodi di formattazione di data e ora utilizzano sempre il calendario corrente quando si convertono le date in stringhe. Ciò significa che le rappresentazioni di stringa dell'anno, del mese e del giorno del mese riflettono il calendario corrente e non necessariamente il calendario gregoriano.

Nell'esempio seguente viene illustrato come il calendario corrente influisce sulla rappresentazione di stringa di una data. Vengono sostituite le impostazioni cultura correnti con quelle cinesi (tradizionale, Taiwan) e viene creata un'istanza di un valore di data. Viene quindi visualizzato il calendario corrente e la data, viene sostituito il calendario corrente con <xref:System.Globalization.TaiwanCalendar> e viene visualizzato il calendario corrente e di nuovo la data. La prima volta che viene visualizzata la data, essa viene rappresentata come data del calendario gregoriano. La seconda volta che viene visualizzata, essa viene rappresentata come data del calendario taiwanese.

[!code-csharp[Conceptual.Calendars#5](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/currentcalendar1.cs#5)]
[!code-vb[Conceptual.Calendars#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/currentcalendar1.vb#5)]

### <a name="represent-dates-in-a-non-current-calendar"></a>Rappresenta le date in un calendario non corrente

Per rappresentare una data utilizzando un calendario che non è il calendario corrente delle impostazioni cultura specifiche, è necessario chiamare i metodi dell'oggetto <xref:System.Globalization.Calendar>. Ad esempio, i metodi <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> e <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> convertono l'anno, il mese e il giorno in valori che riflettono un determinato calendario.

> [!WARNING]
> Poiché alcuni calendari non sono calendari facoltativi delle impostazioni cultura, per rappresentare le date in tali calendari è necessario chiamare sempre i metodi del calendario. Ciò vale per tutti i calendari che derivano dalle classi <xref:System.Globalization.EastAsianLunisolarCalendar>, <xref:System.Globalization.JulianCalendar> e <xref:System.Globalization.PersianCalendar>.

Nell'esempio seguente viene utilizzato un oggetto <xref:System.Globalization.JulianCalendar> per creare un'istanza di una data, il 9 gennaio 1905, nel calendario giuliano. Quando tale data viene visualizzata utilizzando il calendario predefinito (gregoriano), essa viene rappresentata come il 22 gennaio 1905. Le chiamate ai singoli metodi <xref:System.Globalization.JulianCalendar> consentono di rappresentare la data nel calendario giuliano.

[!code-csharp[Conceptual.Calendars#6](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/noncurrentcalendar1.cs#6)]
[!code-vb[Conceptual.Calendars#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/noncurrentcalendar1.vb#6)]

### <a name="calendars-and-date-ranges"></a>Calendari e intervalli di date

La data più vicina supportata da un calendario è indicata dalla proprietà <xref:System.Globalization.Calendar.MinSupportedDateTime%2A?displayProperty=nameWithType> del calendario. Per la classe <xref:System.Globalization.GregorianCalendar>, tale data è il 1° gennaio, 0001. d.C. La maggior parte degli altri calendari in .NET supporta una data successiva. Il tentativo di utilizzare un valore di data e ora che precede la data più vicina supportata da un calendario genera un'eccezione <xref:System.ArgumentOutOfRangeException>.

Tuttavia, esiste un'eccezione importante. Il valore (non inizializzato) predefinito di un oggetto <xref:System.DateTime> e un oggetto <xref:System.DateTimeOffset> è uguale al valore <xref:System.Globalization.GregorianCalendar.MinSupportedDateTime%2A?displayProperty=nameWithType>. Se si tenta di formattare questa data in un calendario che non supporta il 1 ° gennaio 0001 E.V. e non si specifica un identificatore di formato, il metodo di formattazione usa l'identificatore di formato "s" (modello di data/ora ordinabile) anziché l'identificatore di formato "G" (schema di data/ora generale). Di conseguenza, l'operazione di formattazione non genera un'eccezione <xref:System.ArgumentOutOfRangeException>. Al contrario, restituisce la data non supportata. Come illustrato nell'esempio, viene mostrato il valore <xref:System.DateTime.MinValue?displayProperty=nameWithType> quando le impostazioni cultura correnti sono impostate su giapponese (Giappone) con il calendario giapponese e su arabo (Egitto) con il calendario Um al Qura. Vengono inoltre impostate le impostazioni cultura correnti su inglese (Stati Uniti) e viene chiamato il metodo <xref:System.DateTime.ToString%28System.IFormatProvider%29?displayProperty=nameWithType> con ognuno di questi oggetti <xref:System.Globalization.CultureInfo>. In ogni caso, la data viene visualizzata usando lo schema di data/ora ordinabile.

[!code-csharp[Conceptual.Calendars#11](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/minsupporteddatetime1.cs#11)]
[!code-vb[Conceptual.Calendars#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/minsupporteddatetime1.vb#11)]

## <a name="work-with-eras"></a>Usare le ere

I calendari dividono in genere le date in ere. Tuttavia, le <xref:System.Globalization.Calendar> classi in .NET non supportano tutte le era definite da un calendario e la maggior parte delle <xref:System.Globalization.Calendar> classi supporta solo una singola era. Solo le classi <xref:System.Globalization.JapaneseCalendar> e <xref:System.Globalization.JapaneseLunisolarCalendar> supportano più ere.

> [!IMPORTANT]
> L'era REIWA, una nuova era in <xref:System.Globalization.JapaneseCalendar> e <xref:System.Globalization.JapaneseLunisolarCalendar> , inizia il 1 ° maggio 2019. Questo cambio interessa tutte le applicazioni che usano questi calendari. Per altre informazioni, vedere gli articoli seguenti:
>
> - [Gestione di una nuova era nel calendario giapponese in .NET](https://devblogs.microsoft.com/dotnet/handling-a-new-era-in-the-japanese-calendar-in-net/), che documenta le funzionalità aggiunte a .NET per supportare calendari con più ere e illustra le procedure consigliate da usare per la gestione dei calendari multi-era.
> - [Preparare l'applicazione per la modifica dell'era giapponese](/windows/uwp/design/globalizing/japanese-era-change), che fornisce informazioni sul test delle applicazioni in Windows per garantirne la conformità alla modifica dell'era.
> - [Riepilogo dei nuovi aggiornamenti dell'era giapponese per .NET Framework](https://support.microsoft.com/help/4477957/new-japanese-era-updates-for-net-framework), che elenca gli aggiornamenti .NET Framework per le singole versioni di Windows correlate alla nuova era del calendario giapponese, nota nuove funzionalità di .NET Framework per il supporto di più epoche e include elementi da cercare durante il test delle applicazioni.

Un'era nella maggior parte dei calendari denota un periodo di tempo estremamente lungo. Nel calendario gregoriano, ad esempio, l'era corrente si estende su più di due millenni. Per <xref:System.Globalization.JapaneseCalendar> e, i <xref:System.Globalization.JapaneseLunisolarCalendar> due calendari che supportano più ere, questo non è il caso. Un'era corrisponde al periodo di Regno di un imperatore. Il supporto per più ere, in particolare quando il limite superiore dell'era sconosciuta, pone particolari difficoltà.

### <a name="eras-and-era-names"></a>Ere e nomi dell'era

In .NET, i numeri interi che rappresentano le ere supportate da una particolare implementazione del calendario vengono archiviati in ordine inverso nella <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType> matrice. L'era corrente (ossia l'era con l'intervallo di tempo più recente) si trova in corrispondenza dell'indice zero e per le <xref:System.Globalization.Calendar> classi che supportano più ere, ogni indice successivo riflette l'era precedente. La proprietà <xref:System.Globalization.Calendar.CurrentEra?displayProperty=nameWithType> statica definisce l'indice dell'era corrente nella matrice <xref:System.Globalization.Calendar.Eras%2A?displayProperty=nameWithType>. Si tratta di una costante il cui valore è sempre zero. Le singole classi <xref:System.Globalization.Calendar> includono anche i campi statici che restituiscono il valore dell'era corrente. Tali valori vengono elencati nella tabella seguente.

| Classe di calendario                                        | Campo era corrente                                                 |
| ----------------------------------------------------- | ----------------------------------------------------------------- |
| <xref:System.Globalization.ChineseLunisolarCalendar>  | <xref:System.Globalization.ChineseLunisolarCalendar.ChineseEra>   |
| <xref:System.Globalization.GregorianCalendar>         | <xref:System.Globalization.GregorianCalendar.ADEra>               |
| <xref:System.Globalization.HebrewCalendar>            | <xref:System.Globalization.HebrewCalendar.HebrewEra>              |
| <xref:System.Globalization.HijriCalendar>             | <xref:System.Globalization.HijriCalendar.HijriEra>                |
| <xref:System.Globalization.JapaneseLunisolarCalendar> | <xref:System.Globalization.JapaneseLunisolarCalendar.JapaneseEra> |
| <xref:System.Globalization.JulianCalendar>            | <xref:System.Globalization.JulianCalendar.JulianEra>              |
| <xref:System.Globalization.KoreanCalendar>            | <xref:System.Globalization.KoreanCalendar.KoreanEra>              |
| <xref:System.Globalization.KoreanLunisolarCalendar>   | <xref:System.Globalization.KoreanLunisolarCalendar.GregorianEra>  |
| <xref:System.Globalization.PersianCalendar>           | <xref:System.Globalization.PersianCalendar.PersianEra>            |
| <xref:System.Globalization.ThaiBuddhistCalendar>      | <xref:System.Globalization.ThaiBuddhistCalendar.ThaiBuddhistEra>  |
| <xref:System.Globalization.UmAlQuraCalendar>          | <xref:System.Globalization.UmAlQuraCalendar.UmAlQuraEra>          |

Il nome corrispondente al numero dell'era specifico può essere recuperato passando il numero dell'era al metodo <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> o <xref:System.Globalization.DateTimeFormatInfo.GetAbbreviatedEraName%2A?displayProperty=nameWithType>. Nell'esempio seguente vengono chiamati questi metodi per recuperare le informazioni sul supporto dell'era nella classe <xref:System.Globalization.GregorianCalendar>. Viene visualizzata la data del calendario gregoriano corrispondente al 1 ° gennaio del secondo anno dell'era corrente, nonché la data del calendario gregoriano corrispondente al 1 ° gennaio del secondo anno di ciascuna era del calendario giapponese supportata.

[!code-csharp[Conceptual.Calendars#7](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/instantiatewithera1.cs)]
[!code-vb[Conceptual.Calendars#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/instantiatewithera1.vb)]

Inoltre, la stringa di formato di data e ora personalizzata "g" include il nome dell'era di un calendario nella rappresentazione di stringa di una data e ora. Per altre informazioni, vedere [stringhe di formato di data e ora personalizzate](../base-types/custom-date-and-time-format-strings.md).

### <a name="instantiatie-a-date-with-an-era"></a>Creare un'istanza di una data con un'era

Per le due <xref:System.Globalization.Calendar> classi che supportano più ere, una data costituita da un valore specifico di anno, mese e giorno del mese può essere ambigua. Ad esempio, tutte le ere supportate dal <xref:System.Globalization.JapaneseCalendar> hanno anni il cui numero è 1. In genere, se non viene specificata un'era, entrambi i metodi del calendario e di data e ora presuppongono che i valori appartengano all'era corrente. Questo vale <xref:System.DateTime.%23ctor%2A> per i costruttori e <xref:System.DateTimeOffset.%23ctor%2A> che includono parametri di tipo, nonché <xref:System.Globalization.Calendar> i metodi [JapaneseCalendar. ToDateTime](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) e [JapaneseLunisolarCalendar. ToDateTime](xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)) . Nell'esempio seguente viene creata un'istanza di una data che rappresenta l'1 gennaio del secondo anno di un'era non specificata. Se si esegue l'esempio quando REIWA era l'era corrente, la data viene interpretata come il secondo anno dell'era REIWA. L'era, 令和, precede l'anno nella stringa restituita dal <xref:System.DateTime.ToString(System.String,System.IFormatProvider)?displayProperty=nameWithType> metodo e corrisponde al 1 gennaio 2020 nel calendario gregoriano. L'era REIWA inizia nell'anno 2019 del calendario gregoriano.

[!code-csharp[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/cs/program.cs)]
[!code-vb[A date in the current era](~/samples/snippets/standard/datetime/calendars/current-era/vb/program.vb)]

Tuttavia, se l'era modificata, lo scopo di questo codice diventa ambiguo. La data è destinata a rappresentare il secondo anno dell'era corrente o è destinata a rappresentare il secondo anno dell'era Heisei? Esistono due modi per evitare questa ambiguità:

- Creare un'istanza del valore di data e ora utilizzando la <xref:System.Globalization.GregorianCalendar> classe predefinita. È quindi possibile usare il calendario giapponese o il calendario lunisolare giapponese per la rappresentazione di stringa delle date, come illustrato nell'esempio seguente.

  [!code-csharp[Insantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/cs/program.cs)]
  [!code-vb[Instantiating a Gregorian date](~/samples/snippets/standard/datetime/calendars/gregorian/vb/program.vb)]

- Chiamare un metodo di data e ora che specifichi in modo esplicito un'era. Sono inclusi i metodi seguenti:

  - <xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)>Metodo della <xref:System.Globalization.JapaneseCalendar> <xref:System.Globalization.JapaneseLunisolarCalendar> classe o.

  - <xref:System.DateTime> <xref:System.DateTimeOffset> Metodo di analisi o, ad esempio <xref:System.DateTime.Parse%2A> ,, <xref:System.DateTime.TryParse%2A> <xref:System.DateTime.ParseExact%2A> o <xref:System.DateTime.TryParseExact%2A> , che include la stringa da analizzare e, facoltativamente, un <xref:System.Globalization.DateTimeStyles> argomento se le impostazioni cultura correnti sono giapponesi (Giappone) e il calendario delle impostazioni cultura è <xref:System.Globalization.JapaneseCalendar> . La stringa da analizzare deve includere l'era.

  - <xref:System.DateTime> <xref:System.DateTimeOffset> Metodo di analisi o che include un `provider` parametro di tipo <xref:System.IFormatProvider> . `provider`deve essere un <xref:System.Globalization.CultureInfo> oggetto che rappresenta le impostazioni cultura giapponese-Giappone ("ja-JP") il cui calendario corrente è <xref:System.Globalization.JapaneseCalendar> o un <xref:System.Globalization.DateTimeFormatInfo> oggetto la cui <xref:System.Globalization.DateTimeFormatInfo.Calendar> proprietà è <xref:System.Globalization.JapaneseCalendar> . La stringa da analizzare deve includere l'era.

  Nell'esempio seguente vengono usati tre di questi metodi per creare un'istanza di data e ora nell'era Meiji, iniziata l'8 settembre 1868 e terminata il 29 luglio 1912.

  [!code-csharp[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/cs/program.cs)]
  [!code-vb[A date in a specified era](~/samples/snippets/standard/datetime/calendars/specify-era/vb/program.vb)]

> [!TIP]
> Quando si utilizzano calendari che supportano più ere, utilizzare *sempre* la data gregoriano per creare un'istanza di una data o specificare l'era quando si crea un'istanza di una data e un'ora in base al calendario.

Quando si specifica un'era per il <xref:System.Globalization.Calendar.ToDateTime(System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32,System.Int32)> metodo, è necessario fornire l'indice dell'era nella proprietà del calendario <xref:System.Globalization.Calendar.Eras> . Per i calendari le cui ere sono soggette a modifiche, tuttavia, questi indici non sono valori costanti; l'era corrente è in corrispondenza dell'indice 0 e l'era meno recente è l'indice `Eras.Length - 1` . Quando viene aggiunta una nuova era a un calendario, gli indici delle ere precedenti aumentano di uno. È possibile fornire l'indice di era appropriato come indicato di seguito:

- Per le date nell'era corrente, utilizzare sempre la proprietà del calendario <xref:System.Globalization.Calendar.CurrentEra> .

- Per le date in un'era specificata, utilizzare il <xref:System.Globalization.DateTimeFormatInfo.GetEraName%2A?displayProperty=nameWithType> metodo per recuperare l'indice che corrisponde al nome di un'era specificata. Questa operazione richiede che <xref:System.Globalization.JapaneseCalendar> sia il calendario corrente dell' <xref:System.Globalization.CultureInfo> oggetto che rappresenta le impostazioni cultura ja-JP.  Questa tecnica funziona anche per la <xref:System.Globalization.JapaneseLunisolarCalendar> , perché supporta le stesse ere di <xref:System.Globalization.JapaneseCalendar> . Nell'esempio precedente viene illustrato questo approccio.

### <a name="calendars-eras-and-date-ranges-relaxed-range-checks"></a>Calendari, ere e intervalli di date: controlli intervallo rilassato

Analogamente ai singoli calendari sono supportati intervalli di date, le ere <xref:System.Globalization.JapaneseCalendar> nelle <xref:System.Globalization.JapaneseLunisolarCalendar> classi e hanno anche intervalli supportati. In precedenza, .NET usava un intervallo di tempo rigoroso per assicurarsi che una data specifica era compresa nell'intervallo di quell'era. Ovvero, se una data non è compresa nell'intervallo dell'era specificata, il metodo genera un'eccezione <xref:System.ArgumentOutOfRangeException> . Attualmente .NET usa il controllo con intervallo rilassato per impostazione predefinita. Gli aggiornamenti a tutte le versioni di .NET hanno introdotto controlli di intervallo di era rilassato; il tentativo di creare un'istanza di una data specifica dell'era non compreso nell'intervallo dell'era specificata "overflow" nell'era seguente e non viene generata alcuna eccezione.

Nell'esempio seguente viene effettuato un tentativo di creare un'istanza di una data nell'anno 65 dell'era Showa, iniziata il 25 dicembre 1926 ed è terminata il 7 gennaio 1989. Questa data corrisponde al 9 gennaio 1990, che non rientra nell'intervallo dell'era di visualizzazione in <xref:System.Globalization.JapaneseCalendar> . Come illustrato nell'output dell'esempio, la data visualizzata nell'esempio è il 9 gennaio 1990 nel secondo anno dell'era Heisei.

  [!code-csharp[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/cs/program.cs)]
  [!code-vb[Relaxed range checks](~/samples/snippets/standard/datetime/calendars/relaxed-range/vb/program.vb)]

Se i controlli di intervallo rilassato sono indesiderati, è possibile ripristinare rigorosi controlli di intervallo in diversi modi, a seconda della versione di .NET in cui è in esecuzione l'applicazione:

- **.NET Core:** Aggiungere il codice seguente al file di configurazione *. Netcore. Runtime. JSON* :

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.EnforceJapaneseEraYearRanges": true
    }
  }
  ```

- **.NET Framework 4,6 o versione successiva:** Impostare l'opzione AppContext seguente nel file *app. config* :

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceJapaneseEraYearRanges=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 o versioni precedenti:** Impostare il valore del registro di sistema seguente:

   |  |  |
   |--|--|
   | **Codice** | **HKEY_LOCAL_MACHINE \Software\Microsoft \\ . NETFramework\AppContext** |
   | **Nome** | Switch. System. Globalization. EnforceJapaneseEraYearRanges |
   | **Type** | REG_SZ |
   | **Valore** | true |

Con i controlli di intervallo rigorosi abilitati, nell'esempio precedente viene generato un oggetto <xref:System.ArgumentOutOfRangeException> e viene visualizzato l'output seguente:

```console
Unhandled Exception: System.ArgumentOutOfRangeException: Valid values are between 1 and 64, inclusive.
Parameter name: year
   at System.Globalization.GregorianCalendarHelper.GetYearOffset(Int32 year, Int32 era, Boolean throwOnError)
   at System.Globalization.GregorianCalendarHelper.ToDateTime(Int32 year, Int32 month, Int32 day, Int32 hour, Int32 minute, Int32 second, Int32 millisecond, Int32 era)
   at Example.Main()
```

### <a name="represent-dates-in-calendars-with-multiple-eras"></a>Rappresenta le date nei calendari con più ere

Se un oggetto <xref:System.Globalization.Calendar> supporta le ere ed è il calendario corrente di un oggetto <xref:System.Globalization.CultureInfo>, l'era viene inclusa nella rappresentazione di stringa di un valore di data e ora per i modelli di data e ora completa, di data estesa e di data breve. Nell'esempio seguente vengono visualizzati questi modelli di data quando le impostazioni cultura correnti sono quelle giapponesi (Giappone) e il calendario corrente è il calendario giapponese.

[!code-csharp[Conceptual.Calendars#8](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings1.cs#8)]
[!code-vb[Conceptual.Calendars#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings1.vb#8)]

> [!WARNING]
> La <xref:System.Globalization.JapaneseCalendar> classe è l'unica classe Calendar in .NET che supporta entrambe le date in più di un'era e che può corrispondere al calendario corrente di un <xref:System.Globalization.CultureInfo> oggetto, in particolare, di un <xref:System.Globalization.CultureInfo> oggetto che rappresenta le impostazioni cultura giapponesi (Giappone).

Per tutti i calendari l'identificatore di formato personalizzato "g" include l'era nella stringa di risultato. Nell'esempio seguente viene utilizzata la stringa di formato personalizzata "MM-dd-yyyy g" per includere l'era nella stringa di risultato quando il calendario corrente è il calendario gregoriano.

[!code-csharp[Conceptual.Calendars#9](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings2.cs#9)]
[!code-vb[Conceptual.Calendars#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings2.vb#9)]

Nei casi in cui la rappresentazione di stringa di una data viene espressa in un calendario che non è il calendario corrente, la classe <xref:System.Globalization.Calendar> include un metodo <xref:System.Globalization.Calendar.GetEra%2A?displayProperty=nameWithType> che può essere utilizzato con i metodi <xref:System.Globalization.Calendar.GetYear%2A?displayProperty=nameWithType>, <xref:System.Globalization.Calendar.GetMonth%2A?displayProperty=nameWithType> e <xref:System.Globalization.Calendar.GetDayOfMonth%2A?displayProperty=nameWithType> per indicare in modo non ambiguo una data, nonché l'era a cui appartiene. Nell'esempio seguente viene utilizzata la classe <xref:System.Globalization.JapaneseLunisolarCalendar> per fornire un'illustrazione. Si noti, tuttavia, che se si include un nome significativo o un'abbreviazione anziché un intero per l'era nella stringa di risultato, è necessario creare un'istanza di un oggetto <xref:System.Globalization.DateTimeFormatInfo> e rendere <xref:System.Globalization.JapaneseCalendar> il calendario corrente. Il calendario <xref:System.Globalization.JapaneseLunisolarCalendar> non può essere il calendario corrente delle impostazioni cultura, ma in questo caso i due calendari condividono le stesse ere.

[!code-csharp[Conceptual.Calendars#10](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.calendars/cs/formatstrings3.cs#10)]
[!code-vb[Conceptual.Calendars#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.calendars/vb/formatstrings3.vb#10)]

Nei calendari giapponesi, il primo anno di un'era denominato Gannen (元年). Ad esempio, invece di Heisei 1, il primo anno dell'era Heisei può essere descritto come Heisei Gannen. .NET adotta questa convenzione nelle operazioni di formattazione per date e ore formattate con le stringhe di formato di data e ora standard o personalizzate seguenti quando vengono usate con un <xref:System.Globalization.CultureInfo> oggetto che rappresenta le impostazioni cultura giapponese-Giappone ("ja-JP") con la <xref:System.Globalization.JapaneseCalendar> classe:

- [Modello di data estesa](../base-types/standard-date-and-time-format-strings.md#LongDate), indicato dalla stringa di formato di data e ora standard "D".
- [Modello di ora estesa per la data completa](../base-types/standard-date-and-time-format-strings.md#FullDateLongTime), indicato dalla stringa di formato di data e ora standard "F".
- [Modello di ora breve e data completa](../base-types/standard-date-and-time-format-strings.md#FullDateShortTime), indicato dalla stringa di formato di data e ora standard "f".
- [Modello di anno/mese](../base-types/standard-date-and-time-format-strings.md#YearMonth), indicato dalla stringa di formato di data e ora standard y "o" y ".
- [La [stringa di formato di data e ora personalizzato](../base-types/custom-date-and-time-format-strings.md)"GGY" o "ggy年".

Ad esempio, nell'esempio seguente viene visualizzata una data nel primo anno dell'era Heisei in <xref:System.Globalization.JapaneseCalendar> .

  [!code-csharp[gannen](~/samples/snippets/standard/datetime/calendars/gannen/cs/program.cs)]
  [!code-vb[gannen](~/samples/snippets/standard/datetime/calendars/gannen/vb/gannen-fmt.vb)]

Se questo comportamento non è auspicabile nelle operazioni di formattazione, è possibile ripristinare il comportamento precedente, che rappresenta sempre il primo anno di un'era come "1" anziché "Gannen", seguendo questa procedura, a seconda della versione di .NET:

- **.NET Core:** Aggiungere il codice seguente al file di configurazione *. Netcore. Runtime. JSON* :

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.FormatJapaneseFirstYearAsANumber": true
    }
  }
  ```

- **.NET Framework 4,6 o versione successiva:** Impostare l'opzione AppContext seguente nel file *app. config* :

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.FormatJapaneseFirstYearAsANumber=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 o versioni precedenti:** Impostare il valore del registro di sistema seguente:

   |  |  |
   |--|--|
   | **Codice** | **HKEY_LOCAL_MACHINE \Software\Microsoft \\ . NETFramework\AppContext** |
   | **Nome** | Switch. System. Globalization. FormatJapaneseFirstYearAsANumber |
   | **Type** | REG_SZ |
   | **Valore** | true |

Con il supporto di Gannen nelle operazioni di formattazione disabilitate, nell'esempio precedente viene visualizzato l'output seguente:

```console
Japanese calendar date: 平成1年8月18日 (Gregorian: Friday, August 18, 1989)
```

.NET è stato inoltre aggiornato in modo che le operazioni di analisi di data e ora supportino stringhe contenenti l'anno rappresentato come "1" o Gannen. Sebbene non sia necessario eseguire questa operazione, è possibile ripristinare il comportamento precedente in modo che riconosca solo "1" come primo anno di un'era. Questa operazione può essere eseguita come indicato di seguito, a seconda della versione di .NET:

- **.NET Core:** Aggiungere il codice seguente al file di configurazione *. Netcore. Runtime. JSON* :

  ```json
  "runtimeOptions": {
    "configProperties": {
        "Switch.System.Globalization.EnforceLegacyJapaneseDateParsing": true
    }
  }
  ```

- **.NET Framework 4,6 o versione successiva:** Impostare l'opzione AppContext seguente nel file *app. config* :

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <configuration>
    <runtime>
      <AppContextSwitchOverrides value="Switch.System.Globalization.EnforceLegacyJapaneseDateParsing=true" />
    </runtime>
  </configuration>
  ```

- **.NET Framework 4.5.2 o versioni precedenti:** Impostare il valore del registro di sistema seguente:

   |  |  |
   |--|--|
   | **Codice** | **HKEY_LOCAL_MACHINE \Software\Microsoft \\ . NETFramework\AppContext** |
   | **Nome** | Switch. System. Globalization. EnforceLegacyJapaneseDateParsing |
   | **Type** | REG_SZ |
   | **Valore** | true |

## <a name="see-also"></a>Vedere anche

- [Procedura: visualizzare le date in calendari non gregoriani](../base-types/how-to-display-dates-in-non-gregorian-calendars.md)
- [Esempio: utilità di intervallo Calendar Week](https://code.msdn.microsoft.com/NET-Framework-4-Calendar-3360a84a)
- [Classe di calendario](xref:System.Globalization.Calendar)
