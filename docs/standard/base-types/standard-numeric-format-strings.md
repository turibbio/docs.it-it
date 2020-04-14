---
title: Stringhe di formato numerico standard
ms.date: 06/10/2018
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- numeric format strings [.NET Framework]
- formatting [.NET Framework], numbers
- standard format strings, numeric
- format strings
- numbers [.NET Framework], formatting
- format specifiers, numeric
- standard numeric format strings
- formatting numbers [.NET Framework]
- format specifiers, standard numeric format strings
ms.openlocfilehash: 9b0c784a1c7b6b428636a1a4c99ec8e2bb76a9e0
ms.sourcegitcommit: 7980a91f90ae5eca859db7e6bfa03e23e76a1a50
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/13/2020
ms.locfileid: "81242712"
---
# <a name="standard-numeric-format-strings"></a>Stringhe di formato numerico standard

Le stringhe di formato numerico standard vengono usate per formattare tipi numerici comuni. Una stringa di formato numerico standard usa il formato `Axx`, dove:

- `A` è un carattere alfabetico denominato *identificatore di formato*. Le stringhe di formato numerico contenenti più caratteri alfabetici, inclusi gli spazi, vengono interpretate come stringhe di formato numerico personalizzate. Per altre informazioni, vedere [Stringhe di formato numerico personalizzato](../../../docs/standard/base-types/custom-numeric-format-strings.md).

- `xx` è un numero intero facoltativo denominato *identificatore di precisione*. L'identificatore di precisione, compreso tra 0 e 99, controlla il numero di cifre nel risultato. L'identificatore di precisione controlla il numero di cifre nella rappresentazione di stringa di un numero. Non arrotonda il numero stesso. Per eseguire un'operazione di arrotondamento, usare il metodo <xref:System.Math.Ceiling%2A?displayProperty=nameWithType>, <xref:System.Math.Floor%2A?displayProperty=nameWithType> o <xref:System.Math.Round%2A?displayProperty=nameWithType>.

  Quando l'*identificatore di precisione* controlla il numero di cifre frazionali nella stringa del risultato, quest'ultima riflette un numero arrotondato al risultato rappresentabile più vicino al risultato con precisione all'infinito. In presenza di due risultati rappresentabili equivalenti:
  - **In .NET Framework e .NET Core fino alla versione .NET Core 2.0** il runtime seleziona il risultato con la cifra meno significativa maggiore, ovvero usando <xref:System.MidpointRounding.AwayFromZero?displayProperty=nameWithType>.
  - **In .NET Core 2.1 e versioni successive** il runtime seleziona il risultato con una cifra meno significativa pari, ovvero usando <xref:System.MidpointRounding.ToEven?displayProperty=nameWithType>.

  > [!NOTE]
  > L'identificatore di precisione determina il numero di cifre nella stringa risultato. Per riempire una stringa risultato con spazi iniziali o finali, usare la funzionalità di [formattazione composita](../../../docs/standard/base-types/composite-formatting.md) e definire un *componente allineamento* nell'elemento di formato.

Le stringhe di formato numerico standard sono supportate:

- Da alcuni overload del metodo `ToString` di tutti i tipi numerici. È ad esempio possibile fornire una stringa di formato numerico ai metodi <xref:System.Int32.ToString%28System.String%29?displayProperty=nameWithType> e <xref:System.Int32.ToString%28System.String%2CSystem.IFormatProvider%29?displayProperty=nameWithType>.

- Dalla [funzionalità di formattazione composita](../../../docs/standard/base-types/composite-formatting.md) di .NET usata da alcuni metodi `Write` e `WriteLine` delle classi <xref:System.Console> e <xref:System.IO.StreamWriter>, dal metodo <xref:System.String.Format%2A?displayProperty=nameWithType> e dal metodo <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType>. La funzionalità di formattazione composta consente di includere la rappresentazione di stringa di più elementi dati in un'unica stringa per specificare la larghezza di un campo e per allinearvi i numeri all'interno. Per altre informazioni, vedere [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md).

- Dalle [stringhe interpolate](../../csharp/language-reference/tokens/interpolated.md) in c# e Visual Basic, che forniscono una sintassi semplificata rispetto alle stringhe di formato composito.

> [!TIP]
> È possibile scaricare l'**utilità di formattazione**, un'applicazione .NET Core Windows Forms che consente di applicare stringhe di formato a valori numerici o di data e ora e di visualizzare la stringa di risultato. Il codice sorgente è disponibile per [C#](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs) e [Visual Basic](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-vb).

<a name="table"></a>Nella tabella seguente vengono descritti gli identificatori di formato numerico standard e viene visualizzato l'output di esempio prodotto da ogni identificatore di formato. Vedere la sezione [Note](#NotesStandardFormatting) per informazioni aggiuntive sull'uso di stringhe di formato numerico standard e la sezione [Esempio](#example) per un'illustrazione completa dell'uso.

|Identificatore di formato|Nome|Descrizione|Esempi|
|----------------------|----------|-----------------|--------------|
|"C" o "c"|Valuta|Risultato: un valore di valuta.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre decimali.<br /><br /> Identificatore di precisione predefinito: definito da <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A?displayProperty=nameWithType>.<br /><br /> Altre informazioni: [Identificatore di formato di valuta ("C")](#CFormatString).|123.456 ("C", en-US) \\-> 123,46 USD<br /><br /> 123.456 ("C", fr-FR) -> 123,46 €<br /><br /> 123.456 ("C", ja-JP) -> ¥123<br /><br /> -123.456 ("C3", en-US)\\-> ( 123.456 USD)<br /><br /> -123.456 ("C3", fr-FR) -> -123,456 €<br /><br /> -123.456 ("C3", ja-JP) -> -¥123.456|
|"D" o "d"|Decimal|Risultato: cifre intere con segno negativo facoltativo.<br /><br /> Supportato da: solo tipi integrali.<br /><br /> Identificatore di precisione: numero minimo di cifre.<br /><br /> Identificatore di precisione predefinito: numero minimo di cifre richieste.<br /><br /> Altre informazioni: [Identificatore di formato decimale ("D")](#DFormatString).|1234 ("D") -> 1234<br /><br /> -1234 ("D6") -> -001234|
|"E" o "e"|Esponenziale (scientifico)|Risultato: notazione esponenziale.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre decimali.<br /><br /> Identificatore di precisione predefinito: 6.<br /><br /> Altre informazioni: [Identificatore di formato esponenziale ("E")](#EFormatString).|1052.0329112756 ("E", en-US) -> 1.052033E+003<br /><br /> 1052.0329112756 ("e", fr-FR) -> 1,052033e+003<br /><br /> -1052.0329112756 ("e2", en-US) -> -1.05e+003<br /><br /> -1052.0329112756 ("E2", fr-FR) -> -1,05E+003|
|"F" o "f"|A virgola fissa|Risultato: cifre integrali e decimali con segno negativo facoltativo.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre decimali.<br /><br /> Identificatore di precisione predefinito: definito da <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType>.<br /><br /> Altre informazioni: [Identificatore di formato a virgola fissa ("F")](#FFormatString).|1234.567 ("F", en-US) -> 1234.57<br /><br /> 1234.567 ("F", de-DE) -> 1234,57<br /><br /> 1234 ("F1", en-US) -> 1234.0<br /><br /> 1234 ("F1", de-DE) -> 1234,0<br /><br /> -1234.56 ("F4", en-US) -> -1234.5600<br /><br /> -1234.56 ("F4", de-DE) -> -1234,5600|
|"G" o "g"|Generale|Risultato: la più compatta tra la notazione a virgola fissa e quella scientifica.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero di cifre significative.<br /><br /> Identificatore di precisione predefinito: dipende dal tipo numerico.<br /><br /> Altre informazioni: [Identificatore di formato generale ("G")](#GFormatString).|-123.456 ("G", en-US) -> -123.456<br /><br /> -123.456 ("G", sv-SE) -> -123,456<br /><br /> 123.4546 ("G4", en-US) -> 123.5<br /><br /> 123.4546 ("G4", sv-SE) -> 123,5<br /><br /> -1.234567890e-25 ("G", en-US) -> -1.23456789E-25<br /><br /> -1.234567890e-25 ("G", sv-SE) -> -1,23456789E-25|
|"N" o "n"|Number|Risultato: cifre integrali e decimali, separatori di gruppi e un separatore decimale con segno negativo facoltativo.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero desiderato di posizioni decimali.<br /><br /> Identificatore di precisione predefinito: definito da <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType>.<br /><br /> Altre informazioni: [Identificatore di formato numerico ("N")](#NFormatString).|1234.567 ("N", en-US) -> 1,234.57<br /><br /> 1234.567 ("N", ru-RU) -> 1 234,57<br /><br /> 1234 ("N1", en-US) -> 1,234.0<br /><br /> 1234 ("N1", ru-RU) -> 1 234,0<br /><br /> -1234.56 ("N3", en-US) -> -1,234.560<br /><br /> -1234.56 ("N3", ru-RU) -> -1 234,560|
|"P" o "p"|Percentuale|Risultato: numero moltiplicato per 100 e visualizzato con un simbolo di percentuale.<br /><br /> Supportato da: tutti i tipi numerici.<br /><br /> Identificatore di precisione: numero desiderato di posizioni decimali.<br /><br /> Identificatore di precisione predefinito: definito da <xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A?displayProperty=nameWithType>.<br /><br /> Altre informazioni: [Identificatore di formato percentuale ("P")](#PFormatString).|1 ("P", en-US) -> 100.00 %<br /><br /> 1 ("P", fr-FR) -> 100,00 %<br /><br /> -0.39678 ("P1", en-US) -> -39.7 %<br /><br /> -0.39678 ("P1", fr-FR) -> -39,7 %|
|"R" o "r"|Round trip|Risultato: stringa che può eseguire il round trip a un numero identico.<br /><br /> Supportato da: <xref:System.Single>, <xref:System.Double> e <xref:System.Numerics.BigInteger>.<br /><br /> Nota: consigliato solo per il tipo <xref:System.Numerics.BigInteger>. Per i tipi <xref:System.Double>, usare "G17"; per i tipi <xref:System.Single>, usare "G9". <br> Identificatore di precisione: ignorato.<br /><br /> Altre informazioni: [Identificatore di formato di round trip ("R")](#RFormatString).|123456789.12345678 ("R") -> 123456789.12345678<br /><br /> -1234567890.12345678 ("R") -> -1234567890.1234567|
|"X" o "x"|Valore esadecimale|Risultato: stringa esadecimale.<br /><br /> Supportato da: solo tipi integrali.<br /><br /> Identificatore di precisione: numero di cifre nella stringa di risultato.<br /><br /> Altre informazioni: [Identificatore di formato esadecimale ("X")](#XFormatString).|255 ("X") -> FF<br /><br /> -1 ("x") -> ff<br /><br /> 255 ("x4") -> 00ff<br /><br /> -1 ("X4") -> 00FF|
|Qualsiasi altro carattere singolo|Identificatore sconosciuto|Risultato: genera un evento <xref:System.FormatException> in fase di esecuzione.||

<a name="Using"></a>

## <a name="using-standard-numeric-format-strings"></a>uso di stringhe di formato numerico standard

[!INCLUDE[interactive-note](~/includes/csharp-interactive-note.md)]

È possibile usare una stringa di formato numerico standard per definire la formattazione di un valore numerico in uno dei due modi seguenti:

- È possibile passare la stringa a un overload del metodo `ToString` che ha un parametro `format`. Nell'esempio seguente un valore numerico viene formattato come stringa di valuta nelle impostazioni cultura correnti (in questo caso, en-US).

  [!code-cpp[Formatting.Numeric.Standard#10](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#10)]
  [!code-csharp-interactive[Formatting.Numeric.Standard#10](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#10)]
  [!code-vb[Formatting.Numeric.Standard#10](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#10)]

- È possibile fornire la stringa come argomento `formatString` in un elemento di formato usato con metodi come <xref:System.String.Format%2A?displayProperty=nameWithType>, <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> e <xref:System.Text.StringBuilder.AppendFormat%2A?displayProperty=nameWithType>. Per altre informazioni, vedere [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md). Nell'esempio seguente viene usato un elemento di formato per inserire un valore di valuta in una stringa.

  [!code-cpp[Formatting.Numeric.Standard#11](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#11)]
  [!code-csharp-interactive[Formatting.Numeric.Standard#11](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#11)]
  [!code-vb[Formatting.Numeric.Standard#11](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#11)]

  Facoltativamente, fornire un argomento `alignment` per specificare la lunghezza del campo numerico e se il relativo valore è allineato a destra o a sinistra. L'esempio seguente allinea a sinistra un valore corrente in un campo a 28 caratteri e allinea a destra un valore di valuta in un campo a 14 caratteri.

  [!code-cpp[Formatting.Numeric.Standard#12](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/standardusage1.cpp#12)]
  [!code-csharp-interactive[Formatting.Numeric.Standard#12](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/standardusage1.cs#12)]
  [!code-vb[Formatting.Numeric.Standard#12](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/standardusage1.vb#12)]

- Può essere passato come argomento `formatString` in un elemento espressione interpolata di una stringa interpolata. Per altre informazioni, vedere l'argomento [Interpolazione di stringhe](../../csharp/language-reference/tokens/interpolated.md) nelle informazioni di riferimento di C# o l'argomento [Stringhe interpolate](../../visual-basic/programming-guide/language-features/strings/interpolated-strings.md) nelle informazioni di riferimento di Visual Basic.

Nelle sezioni seguenti vengono fornite informazioni dettagliate su ognuna delle stringhe di formato numerico standard.

<a name="CFormatString"></a>

## <a name="the-currency-c-format-specifier"></a>Identificatore di formato di valuta ("C")

L'identificatore di formato di valuta ("C") consente di convertire un numero in una stringa che rappresenta un importo di valuta. L'identificatore di precisione indica il numero desiderato di posizioni decimali nella stringa di risultato. Se l'identificatore di precisione viene omesso, viene usata la precisione predefinita definita dalla proprietà <xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A?displayProperty=nameWithType>.

Se il valore da formattare contiene un numero di posizioni decimali maggiore del numero specificato o predefinito, il valore frazionario viene arrotondato nella stringa di risultato. Se il valore a destra del numero di posizioni decimali specificate è maggiore o uguale a 5, l'ultima cifra nella stringa di risultato viene arrotondata per eccesso.

La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Nella tabella seguente sono elencate le proprietà di <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa restituita.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.CurrencyPositivePattern%2A>|Definisce la posizione del simbolo di valuta per i valori positivi.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A>|Definisce la posizione del simbolo di valuta per i valori negativi e specifica se il segno negativo è rappresentato da parentesi o dalla proprietà <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>.|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce il segno negativo usato se <xref:System.Globalization.NumberFormatInfo.CurrencyNegativePattern%2A> indica che non vengono usate le parentesi.|
|<xref:System.Globalization.NumberFormatInfo.CurrencySymbol%2A>|Definisce il simbolo di valuta.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalDigits%2A>|Definisce il numero predefinito di cifre decimali in un valore di valuta. È possibile eseguire l'override di questo valore usando l'identificatore di precisione.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyDecimalSeparator%2A>|Definisce la stringa che separa le cifre integrali da quelle decimali.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyGroupSeparator%2A>|Definisce la stringa che separa i gruppi di numeri integrali.|
|<xref:System.Globalization.NumberFormatInfo.CurrencyGroupSizes%2A>|Definisce il numero di cifre intere visualizzate in un gruppo.|

Nell'esempio seguente <xref:System.Double> viene formattato un valore con l'identificatore di formato della valuta:

[!code-cpp[Formatting.Numeric.Standard#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#1)]
[!code-csharp[Formatting.Numeric.Standard#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#1)]
[!code-vb[Formatting.Numeric.Standard#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#1)]

[Torna alla tabella](#table)

<a name="DFormatString"></a>

## <a name="the-decimal-d-format-specifier"></a>Identificatore di formato decimale ("D")

L'identificatore di formato decimale ("D") consente di convertire un numero in una stringa di cifre decimali, da 0 a 9, preceduta da un segno meno se il numero è negativo. Questo formato è supportato solo per i tipi integrali.

L'identificatore di precisione indica il numero minimo di cifre che si vogliono visualizzare nella stringa risultante. Se necessario, alla sinistra del numero verranno aggiunti degli zeri in modo da raggiungere il numero di cifre specificato dall'identificatore di precisione. Se non viene specificato alcun identificatore di precisione, il valore predefinito corrisponde al valore minimo richiesto per rappresentare il numero intero senza zeri iniziali.

La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Come illustrato nella tabella seguente, una singola proprietà influisce sulla formattazione della stringa di risultato.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo.|

Nell'esempio seguente viene formattato un valore <xref:System.Int32> con l'identificatore di formato decimale.

[!code-cpp[Formatting.Numeric.Standard#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#2)]
[!code-csharp-interactive[Formatting.Numeric.Standard#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#2)]
[!code-vb[Formatting.Numeric.Standard#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#2)]

[Torna alla tabella](#table)

<a name="EFormatString"></a>

## <a name="the-exponential-e-format-specifier"></a>Identificatore di formato esponenziale ("E")

L'identificatore di formato esponenziale ("E") consente di convertire un numero in una stringa nel formato "-d.ddd…E+ddd" o "-d.ddd…e+ddd", dove ciascuna "d" indica una cifra da 0 a 9. Se il numero è negativo, la stringa inizierà con un segno meno. Il separatore decimale è sempre preceduto esattamente da una cifra.

L'identificatore di precisione indica il numero di cifre desiderato dopo il separatore decimale. Se l'identificatore di precisione viene omesso, verrà usato il numero predefinito di sei cifre dopo il separatore decimale.

Il fatto che per l'identificatore di formato venga usata una lettera maiuscola o minuscola indica, rispettivamente, se l'esponente debba essere preceduto dal prefisso "E" o "e". L'esponente consiste sempre in un segno più o meno e in un minimo di tre cifre. Se necessario, vengono aggiunti all'esponente degli zeri in modo da raggiungere tale numero di cifre.

La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Nella tabella seguente sono elencate le proprietà di <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa restituita.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo sia per il coefficiente che per l'esponente.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|Definisce la stringa che separa la cifra integrale dalle cifre decimali nel coefficiente.|
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|Definisce la stringa che indica che un esponente è positivo.|

L'esempio seguente <xref:System.Double> formatta un valore con l'identificatore di formato esponenziale:The following example formats a value with the exponential format specifier:

[!code-cpp[Formatting.Numeric.Standard#3](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#3)]
[!code-csharp[Formatting.Numeric.Standard#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#3)]
[!code-vb[Formatting.Numeric.Standard#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#3)]

[Torna alla tabella](#table)

<a name="FFormatString"></a>

## <a name="the-fixed-point-f-format-specifier"></a>Identificatore di formato a virgola fissa ("F")

L'identificatore di formato a virgola fissa ("F") consente di convertire un numero in una stringa nel formato "-ddd.ddd…", dove ogni "d" indica una cifra da 0 a 9. Se il numero è negativo, la stringa inizierà con un segno meno.

L'identificatore di precisione indica il numero di posizioni decimali desiderato. Se l'identificatore di precisione viene omesso, la precisione numerica viene fornita dalla proprietà <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType> corrente.

La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Nella tabella seguente sono elencate le proprietà dell'oggetto <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa di risultato.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|Definisce la stringa che separa le cifre integrali da quelle decimali.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A>|Definisce il numero predefinito di cifre decimali. È possibile eseguire l'override di questo valore usando l'identificatore di precisione.|

L'esempio seguente <xref:System.Double> formatta a e un <xref:System.Int32> valore con l'identificatore di formato a virgola fissa:

[!code-cpp[Formatting.Numeric.Standard#4](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#4)]
[!code-csharp[Formatting.Numeric.Standard#4](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#4)]
[!code-vb[Formatting.Numeric.Standard#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#4)]

[Torna alla tabella](#table)

<a name="GFormatString"></a>

## <a name="the-general-g-format-specifier"></a>Identificatore di formato generale ("G")

L'identificatore di formato generale ("G") consente di convertire un numero nel formato più compatto tra la notazione scientifica e quella a virgola fissa, a seconda del tipo di numero e della presenza di un identificatore di precisione. L'identificatore di precisione definisce il numero massimo di cifre significative che possono essere visualizzate nella stringa di risultato. Se l'identificatore di precisione viene omesso o è uguale a zero, il tipo di numero determina la precisione predefinita, come indicato nella tabella seguente.

|Tipo numerico|Precisione predefinita|
|------------------|-----------------------|
|<xref:System.Byte> o <xref:System.SByte>|3 cifre|
|<xref:System.Int16> o <xref:System.UInt16>|5 cifre|
|<xref:System.Int32> o <xref:System.UInt32>|10 cifre|
|<xref:System.Int64>|19 cifre|
|<xref:System.UInt64>|20 cifre|
|<xref:System.Numerics.BigInteger>|Illimitato (uguale [a "R")](#RFormatString)|
|<xref:System.Single>|7 cifre|
|<xref:System.Double>|15 cifre|
|<xref:System.Decimal>|29 cifre|

La notazione a virgola fissa verrà usata se l'esponente ottenuto esprimendo il numero con la notazione scientifica risulta maggiore di -5 e minore dell'identificatore di precisione. In caso contrario, verrà usata la notazione scientifica. Il risultato contiene un separatore decimale, se richiesto, e gli zeri finali dopo la virgola decimale vengono omessi. Se l'identificatore di precisione è presente e il numero di cifre significative nel risultato è superiore alla precisione specificata, le cifre finali in eccesso vengono rimosse mediante arrotondamento.

Se, tuttavia, il numero è di tipo <xref:System.Decimal> e l'identificatore di precisione viene omesso, viene usata sempre la notazione a virgola fissa e gli zeri finali vengono mantenuti.

Se viene usata la notazione scientifica, l'esponente nel risultato sarà preceduto da un prefisso "E" se l'identificatore di formato è "G" o da un prefisso "e" se l'identificatore di formato è "g". L'esponente contiene un minimo di due cifre. Questo aspetto è diverso rispetto al formato per la notazione scientifica, prodotto dall'identificatore di formato esponenziale, che include un minimo di tre cifre nell'esponente.

Si noti che, se usato con un valore <xref:System.Double>, l'identificatore di formato "G17" assicura che il valore <xref:System.Double> originale esegua correttamente il round trip. Ciò è dovuto al fatto che <xref:System.Double> è un numero in formato a virgola mobile a doppia precisione (`binary64`) conforme allo standard IEEE 754-2008, caratterizzato da una precisione con fino a 17 cifre significative. Se ne consiglia l'uso al posto dell'[identificatore di formato "R"](#RFormatString), dal momento che in alcuni casi "R" non esegue correttamente il round trip dei valori a virgola mobile e precisione doppia. Nell'esempio riportato di seguito viene illustrato un caso di questo tipo.

[!code-csharp-interactive[Round-tripping a Double](../../../samples/snippets/standard/base-types/format-strings/csharp/g17.cs#GeneralFormatSpecifier)]
[!code-vb[Round-tripping a Double](../../../samples/snippets/standard/base-types/format-strings/vb/g17.vb)]

Se usato con un valore <xref:System.Single>, l'identificatore di formato "G9" assicura che il valore <xref:System.Single> originale esegua correttamente il round trip. Ciò è dovuto al fatto che <xref:System.Single> è un numero in formato a virgola mobile a precisione singola (`binary32`) conforme allo standard IEEE 754-2008, caratterizzato da una precisione con fino a nove cifre significative. Per motivi di prestazioni, è consigliabile usare questo anziché l'[identificatore di formato "R"](#RFormatString).

La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Nella tabella seguente sono elencate le proprietà di <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa di risultato.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|Definisce la stringa che separa le cifre integrali da quelle decimali.|
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|Definisce la stringa che indica che un esponente è positivo.|

Nell'esempio seguente vengono formattati i valori a virgola mobile assortiti con l'identificatore di formato generale:

[!code-cpp[Formatting.Numeric.Standard#5](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#5)]
[!code-csharp[Formatting.Numeric.Standard#5](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#5)]
[!code-vb[Formatting.Numeric.Standard#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#5)]

[Torna alla tabella](#table)

<a name="NFormatString"></a>

## <a name="the-numeric-n-format-specifier"></a>Identificatore di formato numerico ("N")

L'identificatore di formato numerico ("N") converte un numero in una stringa in formato "-c.ccc.ccc,ccc…", dove "-" indica un simbolo di numero negativo, se richiesto, "c" indica una cifra (0-9), "." indica il separatore delle migliaia tra gruppi numerici e "," indica il simbolo di separatore decimale. L'identificatore di precisione indica il numero di cifre desiderato dopo il separatore decimale. Se l'identificatore di precisione viene omesso, il numero di cifre decimali viene definito dalla proprietà <xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A?displayProperty=nameWithType> corrente.

La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Nella tabella seguente sono elencate le proprietà di <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa di risultato.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo.|
|<xref:System.Globalization.NumberFormatInfo.NumberNegativePattern%2A>|Definisce il formato dei valori negativi e specifica se il segno negativo è rappresentato da parentesi o dalla proprietà <xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>.|
|<xref:System.Globalization.NumberFormatInfo.NumberGroupSizes%2A>|Definisce il numero di cifre integrali visualizzate tra i separatori di gruppi.|
|<xref:System.Globalization.NumberFormatInfo.NumberGroupSeparator%2A>|Definisce la stringa che separa i gruppi di numeri integrali.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|Definisce la stringa che separa le cifre integrali da quelle decimali.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalDigits%2A>|Definisce il numero predefinito di cifre decimali. È possibile eseguire l'override di questo valore usando un identificatore di precisione.|

Nell'esempio seguente vengono formattati i valori a virgola mobile assortiti con l'identificatore di formato numerico:

[!code-cpp[Formatting.Numeric.Standard#6](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#6)]
[!code-csharp[Formatting.Numeric.Standard#6](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#6)]
[!code-vb[Formatting.Numeric.Standard#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#6)]

[Torna alla tabella](#table)

<a name="PFormatString"></a>

## <a name="the-percent-p-format-specifier"></a>Identificatore di formato percentuale ("P")

L'identificatore di formato percentuale ("P") moltiplica un numero per 100 e lo converte in una stringa che rappresenta una percentuale. L'identificatore di precisione indica il numero di posizioni decimali desiderato. Se l'identificatore di precisione viene omesso, viene usata la precisione numerica predefinita fornita dalla proprietà <xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A> corrente.

Nella tabella seguente sono elencate le proprietà di <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa restituita.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.PercentPositivePattern%2A>|Definisce la posizione del simbolo di percentuale per i valori positivi.|
|<xref:System.Globalization.NumberFormatInfo.PercentNegativePattern%2A>|Definisce la posizione del simbolo di percentuale e del simbolo negativo per i valori negativi.|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo.|
|<xref:System.Globalization.NumberFormatInfo.PercentSymbol%2A>|Definisce il simbolo di percentuale.|
|<xref:System.Globalization.NumberFormatInfo.PercentDecimalDigits%2A>|Definisce il numero predefinito di cifre decimali in un valore percentuale. È possibile eseguire l'override di questo valore usando l'identificatore di precisione.|
|<xref:System.Globalization.NumberFormatInfo.PercentDecimalSeparator%2A>|Definisce la stringa che separa le cifre integrali da quelle decimali.|
|<xref:System.Globalization.NumberFormatInfo.PercentGroupSeparator%2A>|Definisce la stringa che separa i gruppi di numeri integrali.|
|<xref:System.Globalization.NumberFormatInfo.PercentGroupSizes%2A>|Definisce il numero di cifre intere visualizzate in un gruppo.|

L'esempio seguente formatta i valori a virgola mobile con l'identificatore di formato percentuale:The following example formats floating-point values with the percent format specifier:

[!code-cpp[Formatting.Numeric.Standard#7](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#7)]
[!code-csharp[Formatting.Numeric.Standard#7](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#7)]
[!code-vb[Formatting.Numeric.Standard#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#7)]

[Torna alla tabella](#table)

<a name="RFormatString"></a>

## <a name="the-round-trip-r-format-specifier"></a>Identificatore di formato di round trip ("R")

L'identificatore di formato di round trip ("R") cerca di garantire che un valore numerico convertito in una stringa venga riportato al medesimo valore numerico. Questo formato è supportato solo per i tipi <xref:System.Single>, <xref:System.Double> e <xref:System.Numerics.BigInteger>.

Per i valori <xref:System.Double> l'identificatore di formato "R" in alcuni casi non esegue correttamente il round trip del valore originale. Per entrambi i valori <xref:System.Double> e <xref:System.Single>, garantisce poi prestazioni relativamente scarse. È invece consigliabile usare l'identificatore di formato ["G17"](#GFormatString) per i valori <xref:System.Double> e l'identificatore di formato ["G9"](#GFormatString) per eseguire correttamente il round trip dei valori <xref:System.Single>.

Quando un valore <xref:System.Numerics.BigInteger> viene formattato usando questo identificatore, la relativa rappresentazione di stringa contiene tutte le cifre significative nel valore <xref:System.Numerics.BigInteger>.

Sebbene sia possibile includere un identificatore di precisione, questo viene ignorato. Quando si usa questo identificatore, infatti, il formato della riconversione ha la precedenza sulla precisione.
La stringa di risultato è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente. Nella tabella seguente sono elencate le proprietà di <xref:System.Globalization.NumberFormatInfo> che consentono di controllare la formattazione della stringa di risultato.

|Proprietà di NumberFormatInfo|Descrizione|
|-------------------------------|-----------------|
|<xref:System.Globalization.NumberFormatInfo.NegativeSign%2A>|Definisce la stringa che indica che un numero è negativo.|
|<xref:System.Globalization.NumberFormatInfo.NumberDecimalSeparator%2A>|Definisce la stringa che separa le cifre integrali da quelle decimali.|
|<xref:System.Globalization.NumberFormatInfo.PositiveSign%2A>|Definisce la stringa che indica che un esponente è positivo.|

Nell'esempio seguente viene formattato un valore <xref:System.Numerics.BigInteger> con l'identificatore di formato round trip.

[!code-cpp[R format specifier with a BigInteger](../../../samples/snippets/standard/base-types/format-strings/biginteger-r.cpp)]
[!code-csharp[R format specifier with a BigInteger](../../../samples/snippets/standard/base-types/format-strings/biginteger-r.cs)]
[!code-vb[R format specifier with a BigInteger](../../../samples/snippets/standard/base-types/format-strings/biginteger-r.vb)]

> [!IMPORTANT]
> In alcuni casi, i valori <xref:System.Double> formattati con la stringa di formato numerico standard "R" non completano il round trip se compilati usando le opzioni `/platform:x64` o `/platform:anycpu` e in esecuzione su sistemi a 64 bit. Per altre informazioni, vedere il paragrafo seguente.

Per ovviare al problema dei valori <xref:System.Double> formattati con la stringa di formato numerico standard "R" che non completano correttamente il round trip se compilati usando l'opzione `/platform:x64` o `/platform:anycpu` e in esecuzione in sistemi a 64 bit, è possibile formattare i valori <xref:System.Double> usando la stringa di formato numerico standard "G17". Nell'esempio seguente viene utilizzata la <xref:System.Double> stringa di formato "R" con un valore che non esegue correttamente il round trip e viene utilizzata anche la stringa di formato "G17" per eseguire correttamente il round trip del valore originale:

[!code-csharp[System.Double.ToString#5](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Double.ToString/cs/roundtripex1.cs#RoundTrip)]
[!code-vb[System.Double.ToString#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Double.ToString/vb/roundtripex1.vb#5)]

[Torna alla tabella](#table)

<a name="XFormatString"></a>

## <a name="the-hexadecimal-x-format-specifier"></a>Identificatore di formato esadecimale ("X")

L'identificatore di formato esadecimale ("X") consente di convertire un numero in una stringa di cifre esadecimali. Il fatto che per l'identificatore di formato venga usata una lettera maiuscola o minuscola indica, rispettivamente, se usare caratteri maiuscoli o minuscoli per le cifre esadecimali maggiori di 9. usare ad esempio "X" per produrre la stringa "ABCDEF" e "x" per produrre "abcdef". Questo formato è supportato solo per i tipi integrali.

L'identificatore di precisione indica il numero minimo di cifre che si vogliono visualizzare nella stringa risultante. Se necessario, alla sinistra del numero verranno aggiunti degli zeri in modo da raggiungere il numero di cifre specificato dall'identificatore di precisione.

La stringa di risultato non è influenzata dalle informazioni sulla formattazione dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente.

Nell'esempio seguente vengono formattati valori <xref:System.Int32> con l'identificatore di formato esadecimale.

[!code-cpp[Formatting.Numeric.Standard#9](../../../samples/snippets/cpp/VS_Snippets_CLR/Formatting.Numeric.Standard/cpp/Standard.cpp#9)]
[!code-csharp-interactive[Formatting.Numeric.Standard#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.Numeric.Standard/cs/Standard.cs#9)]
[!code-vb[Formatting.Numeric.Standard#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.Numeric.Standard/vb/Standard.vb#9)]

[Torna alla tabella](#table)

<a name="NotesStandardFormatting"></a>

## <a name="notes"></a>Note

### <a name="control-panel-settings"></a>Impostazioni del Pannello di controllo

Le impostazioni di **Opzioni internazionali e della lingua** nel Pannello di controllo influiscono sulla stringa risultato prodotta da un'operazione di formattazione. Queste impostazioni vengono usate per inizializzare l'oggetto <xref:System.Globalization.NumberFormatInfo> associato alle impostazioni cultura del thread corrente, che fornisce i valori usati per definire la formattazione. Computer con impostazioni diverse generano stringhe di risultato diverse.

Inoltre, se viene usato il costruttore <xref:System.Globalization.CultureInfo.%23ctor%28System.String%29> per creare un'istanza di un nuovo oggetto <xref:System.Globalization.CultureInfo> che rappresenta le stesse impostazioni cultura delle impostazioni cultura del sistema correnti, le eventuali personalizzazioni definite dall'elemento **Opzioni internazionali e della lingua** nel Pannello Controllo verranno applicate al nuovo oggetto <xref:System.Globalization.CultureInfo>. È possibile usare il costruttore di <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29> per creare un oggetto <xref:System.Globalization.CultureInfo> che non rifletta le personalizzazioni di un sistema.

### <a name="numberformatinfo-properties"></a>Proprietà NumberFormatInfo

La formattazione è influenzata dalle proprietà dell'oggetto <xref:System.Globalization.NumberFormatInfo> corrente, che viene fornito in modo implicito dalle impostazioni cultura del thread corrente o in modo esplicito dal parametro <xref:System.IFormatProvider> del metodo che richiama la formattazione. Specificare un oggetto <xref:System.Globalization.NumberFormatInfo> o <xref:System.Globalization.CultureInfo> per questo parametro.

> [!NOTE]
> Per informazioni sulla personalizzazione delle stringhe o dei modelli usati nella formattazione di valori numerici, vedere l'argomento relativo alla classe <xref:System.Globalization.NumberFormatInfo>.

### <a name="integral-and-floating-point-numeric-types"></a>Tipi numerici integrali e a virgola mobile

Alcune descrizioni di identificatori di formato numerico standard fanno riferimento a tipi numerici integrali o a virgola mobile. I tipi numerici integrali sono <xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64> e <xref:System.Numerics.BigInteger>. I tipi numerici a virgola mobile sono <xref:System.Decimal>, <xref:System.Single> e <xref:System.Double>.

### <a name="floating-point-infinities-and-nan"></a>Valori infiniti a virgola mobile e NaN

Indipendentemente dalla stringa di formato, se il valore di un tipo a virgola mobile <xref:System.Single> o <xref:System.Double> è un numero infinito positivo, un numero infinito negativo o un valore NaN (Not a Number, non un numero), la stringa formattata corrisponde al valore della proprietà <xref:System.Globalization.NumberFormatInfo.PositiveInfinitySymbol%2A>, <xref:System.Globalization.NumberFormatInfo.NegativeInfinitySymbol%2A> o <xref:System.Globalization.NumberFormatInfo.NaNSymbol%2A> corrispondente specificata dall'oggetto <xref:System.Globalization.NumberFormatInfo> attualmente applicabile.

## <a name="example"></a>Esempio

[!INCLUDE[interactive-note](~/includes/csharp-interactive-partial-note.md)]

Nell'esempio seguente vengono formattati un valore numerico a virgola mobile e uno integrale usando le impostazioni cultura en-US e tutti gli identificatori di formato numerico standard. Nell'esempio vengono usati due tipi numerici particolari (<xref:System.Double> e <xref:System.Int32>), tuttavia i risultati sarebbero simili con qualsiasi altro tipo numerico di base (<xref:System.Byte>, <xref:System.SByte>, <xref:System.Int16>, <xref:System.Int32>, <xref:System.Int64>, <xref:System.UInt16>, <xref:System.UInt32>, <xref:System.UInt64>, <xref:System.Numerics.BigInteger>, <xref:System.Decimal> e <xref:System.Single>).

[!code-csharp[system.x.tostring-and-culture#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.X.ToString-and-Culture/cs/xts.cs#FinalExample)]
[!code-vb[system.x.tostring-and-culture#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.X.ToString-and-Culture/vb/xts.vb#1)]

## <a name="see-also"></a>Vedere anche

- <xref:System.Globalization.NumberFormatInfo>
- [Stringhe di formato numerico personalizzatoCustom Numeric Format Strings](../../../docs/standard/base-types/custom-numeric-format-strings.md)
- [Formattazione di tipi](../../../docs/standard/base-types/formatting-types.md)
- [Procedura: Aggiungere zeri iniziali a un numero](../../../docs/standard/base-types/how-to-pad-a-number-with-leading-zeros.md)
- [Formattazione composita](../../../docs/standard/base-types/composite-formatting.md)
- [Esempio: Utilità di formattazione di .NET Core WinForms (C#)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-cs)
- [Esempio: Utilità di formattazione di .NET Core WinForms (Visual Basic)](https://docs.microsoft.com/samples/dotnet/samples/winforms-formatting-utility-vb)
