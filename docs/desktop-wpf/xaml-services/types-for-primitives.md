---
title: Tipi incorporati per primitive del linguaggio XAML comuni
ms.date: 03/30/2017
helpviewer_keywords:
- XAML language primitives [XAML Services]
- XAML [XAML Services], built-in types
- x:String [XAML Services]
- x:TimeSpan [XAML Services]
- x:Byte [XAML Services]
- x:Double [XAML Services]
- XAML [XAML Services], types
- x:Uri [XAML Services]
- XAML built-in types [XAML Services]
- x:Int64 [XAML Services]
- x:Single [XAML Services]
- x:Int32 [XAML Services]
ms.assetid: 11de2f08-5b95-4989-b5ec-5178eb968184
ms.openlocfilehash: 3bd486ee66c5f9a32621416638bb7575025f7dee
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2020
ms.locfileid: "82071836"
---
# <a name="built-in-types-for-common-xaml-language-primitives"></a>Tipi predefiniti per primitive comuni del linguaggio XAMLBuilt-in types for common XAML language primitives

XAML 2009 introduce il supporto del livello di linguaggio XAML per diversi tipi di dati che sono primitive di uso frequente in Common Language Runtime (CLR) e in altri linguaggi di programmazione. XAML 2009 aggiunge il supporto per queste primitive: `x:Object`, `x:Boolean`, `x:Char`, `x:String`, `x:Decimal`, `x:Single`, `x:Double`, `x:Int16`, `x:Int32`, `x:Int64`, `x:TimeSpan`, `x:Uri`, `x:Byte`e `x:Array`

## <a name="previous-techniques-for-language-primitives-in-xaml-markup"></a>Tecniche precedenti per le primitive di linguaggio nel markup XAML

 In XAML per le versioni di WPF precedenti era possibile fare riferimento alle primitive del linguaggio CLR eseguendo il mapping dell'assembly e dello spazio dei nomi che contenevano una classe di definizione della primitiva CLR per .NET Framework. La maggior parte di queste si trovano nell'assembly mscorlib e nello spazio dei nomi <xref:System> . Ad esempio, per usare <xref:System.Int32>era possibile dichiarare il mapping seguente (con un esempio di utilizzo come illustrato di seguito):

```xaml
<Application xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
xmlns:sys="clr-namespace:System;assembly=mscorlib">
  <Application.Resources>
    <sys:Int32 x:Key="intMeaning">42</sys:Int32>
  </Application.Resources>
</Application>
```

## <a name="xaml-2009-language-primitives"></a>Primitive del linguaggio XAML 2009

Per convenzione, le primitive di linguaggio per XAML e tutti gli altri elementi del linguaggio XAML vengono mostrati con il prefisso `x:` . Questo è il modo in cui gli elementi del linguaggio XAML vengono in genere usati nel markup reale. Questa convenzione viene seguita nella documentazione concettuale per XAML in WPF e anche nelle specifiche XAML.

### <a name="xobject"></a>x:Object

Per il supporto CLR, la primitiva `x:Object` corrisponde a <xref:System.Object>.

Questa primitiva in genere non viene usata nel markup dell'applicazione, ma può essere utile per alcuni scenari, ad esempio la verifica dell'assegnabilità in un sistema di tipi XAML.

### <a name="xboolean"></a>x:Boolean

Per il supporto CLR, la primitiva `x:Boolean` corrisponde a <xref:System.Boolean>.

XAML analizza i valori per `x:Boolean` senza fare distinzione tra maiuscole e minuscole. Tenere presente che `x:Bool` non rappresenta un'alternativa valida. Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.17 e 5.4.11.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xchar"></a>x:Char

Per il supporto CLR, la primitiva `x:Char` corrisponde a <xref:System.Char>.

I tipi string e char interagiscono con la codifica globale del file a livello di XML. Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni 5.2.7 e 5.4.1 di MS-XAML.\] ](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xstring"></a>x:String

Per il supporto CLR, la primitiva `x:String` corrisponde a <xref:System.String>.

I tipi string e char interagiscono con la codifica globale del file a livello di XML. Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni 5.2.6 di MS-XAML.\] ](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xdecimal"></a>x:Decimal

Per il supporto CLR, la primitiva `x:Decimal` corrisponde a <xref:System.Decimal>.

L'analisi XAML viene eseguita intrinsecamente con `en-US` le impostazioni cultura. Con le impostazioni cultura `en-US` , il separatore corretto per i componenti di un numero decimale è sempre un punto (`.`) indipendentemente dalle impostazioni cultura dell'ambiente di sviluppo o dell'eventuale destinazione client in cui XAML viene caricato in fase di esecuzione.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.14 e 5.4.8.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xsingle"></a>x:Single

Per il supporto CLR, la primitiva `x:Single` corrisponde a <xref:System.Single>.

Oltre ai valori numerici, nella sintassi del testo per `x:Single` è consentito anche l'uso dei token `Infinity`, `-Infinity`e `NaN`. Per questi token viene rilevata la distinzione tra maiuscole e minuscole.

`x:Single` può supportare valori nel formato di notazione scientifico, se il primo carattere nella sintassi del testo è `e` o `E`.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni 5.2.8 e 5.4.2 di MS-XAML.\] ](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xdouble"></a>x:Double

Per il supporto CLR, la primitiva `x:Double` corrisponde a <xref:System.Double>.

Oltre ai valori numerici, nella sintassi del testo per `x:Double` è consentito l'uso dei token `Infinity`, `-Infinity`e `NaN`. Per questi token viene rilevata la distinzione tra maiuscole e minuscole.

`x:Double` può supportare valori nel formato di notazione scientifico. Utilizzare il carattere `e` o `E` per introdurre la parte dell'esponente.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni 5.2.9 e 5.4.3 di MS-XAML.\] ](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xint16"></a>x:Int16

Per il supporto CLR, la primitiva `x:Int16` corrisponde a <xref:System.Int16> e `x:Int16` viene considerato con segno. In XAML l'assenza di un segno più (`+`) nella sintassi del testo indica implicitamente un valore con segno positivo.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.11 e 5.4.5.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xint32"></a>x:Int32

Per il supporto CLR, la primitiva `x:Int32` corrisponde a <xref:System.Int32>. `x:Int32` viene considerato un valore con segno. In XAML l'assenza di un segno più (`+`) nella sintassi del testo indica implicitamente un valore con segno positivo.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.12 e 5.4.6.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xint64"></a>x:Int64

Per il supporto CLR, la primitiva `x:Int64` corrisponde a <xref:System.Int64>. `x:Int64` viene considerato un valore con segno. In XAML l'assenza di un segno più (`+`) nella sintassi del testo indica implicitamente un valore con segno positivo.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.13 e 5.4.7.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xtimespan"></a>x:TimeSpan

Per il supporto CLR, la primitiva `x:TimeSpan` corrisponde a <xref:System.TimeSpan>.

L'analisi XAML per il formato della `en-US` data e dell'ora viene eseguita intrinsecamente con le impostazioni cultura.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.16 e 5.4.10.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xuri"></a>x:Uri

Per il supporto CLR, la primitiva `x:Uri` corrisponde a <xref:System.Uri>.

La verifica dei protocolli non fa parte della definizione XAML per `x:Uri`.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni MS-XAML\] 5.2.15 e 5.4.9.](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xbyte"></a>x:Byte

Per il supporto CLR, la primitiva `x:Byte` corrisponde a <xref:System.Byte>. <xref:System.Byte>  /  A `x:Byte` viene considerato come unsigned.

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni 5.2.10 e 5.4.4. di MS-XAML.\] ](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

### <a name="xarray"></a>x:Array

Per il supporto CLR, la primitiva `x:Array` corrisponde a <xref:System.Array>.

In XAML 2006 è possibile definire una matrice utilizzando una sintassi dell'estensione di markup, mentre la sintassi di XAML 2009 è una primitiva definita dal linguaggio che non richiede l'accesso a un'estensione di markup. Per ulteriori informazioni sul supporto di XAML 2006, vedere [x:Array Markup Extension](xarray-markup-extension.md).

Per la definizione della specifica del linguaggio XAML, vedere [ \[Sezioni 5.2.18 di MS-XAML.\] ](https://docs.microsoft.com/previous-versions/msp-n-p/ff650760(v=pandp.10))

## <a name="wpf-support"></a>Supporto WPF

In WPF è possibile usare le funzionalità di XAML 2009, ma solo per il codice XAML non compilato dal markup. Il codice XAML compilato dal markup per WPF e il modulo BAML di XAML non supportano attualmente le parole chiave e le funzionalità di XAML 2009.

Un scenario in cui è possibile usare le funzionalità di XAML 2009 con WPF consiste nella creazione di XAML separato e nel successivo caricamento in un runtime di WPF e in un oggetto grafico con <xref:System.Windows.Markup.XamlReader.Load%2A?displayProperty=nameWithType>. L'oggetto <xref:System.Windows.Markup.XamlReader?displayProperty=nameWithType> di WPF e il relativo metodo <xref:System.Windows.Markup.XamlReader.Load%2A> possono elaborare parole chiave e funzionalità del linguaggio XAML 2009 in una rappresentazione dell'oggetto grafico valida.
