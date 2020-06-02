---
title: Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle raccolte
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- CaseInsensitiveComparer class, using
- CollectionsUtil.CreateCaseInsensitiveHashtable method
- culture-insensitive string operations, collections
- collections [.NET Framework], culture-insensitive string operations
- CaseInsensitiveHashCodeProvider class, using
- ArrayList.Sort method
- SortedList class, culture-insensitive string operations
- culture parameter
ms.assetid: 5cdc9396-a64b-4615-a1cd-b605db4c5983
ms.openlocfilehash: 377fa58e052e8f8e35a546c21fe2b4fb00cb103d
ms.sourcegitcommit: 33deec3e814238fb18a49b2a7e89278e27888291
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/02/2020
ms.locfileid: "84288264"
---
# <a name="performing-culture-insensitive-string-operations-in-collections"></a>Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura nelle raccolte

Nello spazio dei nomi <xref:System.Collections> sono disponibili classi e membri che per impostazione predefinita forniscono un comportamento dipendente dalle impostazioni cultura. I costruttori senza parametri per le classi <xref:System.Collections.CaseInsensitiveComparer> e <xref:System.Collections.CaseInsensitiveHashCodeProvider> inizializzano una nuova istanza tramite la proprietà <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=nameWithType>. Per impostazione predefinita, tutti gli overload del metodo <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType> creano una nuova istanza della classe <xref:System.Collections.Hashtable> tramite la proprietà `Thread.CurrentCulture`. Per impostazione predefinita, gli overload del metodo <xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType> consentono di eseguire ordinamenti dipendenti dalle impostazioni cultura tramite `Thread.CurrentCulture`. Ordinamento e ricerca in un <xref:System.Collections.SortedList> possono essere influenzati dal `Thread.CurrentCulture` quando vengono usate stringhe come chiavi. Per ottenere risultati indipendenti dalle impostazioni cultura da queste classi e da questi metodi dello spazio dei nomi `Collections`, attenersi ai consigli sull'utilizzo forniti in questa sezione.

> [!NOTE]
> Il passaggio <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType> a un metodo di confronto comporta l'esecuzione di un confronto senza distinzione tra le impostazioni cultura. Non viene tuttavia eseguito un confronto non linguistico, ad esempio per percorsi di file, chiavi del Registro di sistema e variabili di ambiente e non sono supportate le decisioni relative alla sicurezza basate sul risultato del confronto. Per un confronto non linguistico o per il supporto delle decisioni relative alla sicurezza basate sul risultato, l'applicazione deve utilizzare un metodo di confronto che accetti un valore <xref:System.StringComparison>. L'applicazione deve quindi passare <xref:System.StringComparison>.

## <a name="using-the-caseinsensitivecomparer-and-caseinsensitivehashcodeprovider-classes"></a>Uso delle classi CaseInsensitiveComparer e CaseInsensitiveHashCodeProvider

I costruttori senza parametri per `CaseInsensitiveHashCodeProvider` e `CaseInsensitiveComparer` inizializzano una nuova istanza della classe tramite `Thread.CurrentCulture`, determinando così un comportamento dipendente dalle impostazioni cultura. Nell'esempio di codice seguente viene illustrato il costruttore per un oggetto `Hashtable` dipendente dalle impostazioni cultura in quanto usa i costruttori senza parametri per `CaseInsensitiveHashCodeProvider` e `CaseInsensitiveComparer`.

```vb
internalHashtable = New Hashtable(CaseInsensitiveHashCodeProvider.Default, CaseInsensitiveComparer.Default)
```

```csharp
internalHashtable = new Hashtable(CaseInsensitiveHashCodeProvider.Default, CaseInsensitiveComparer.Default);
```

Per creare un oggetto `Hashtable` non basato sulle impostazioni di cultura usando le classi `CaseInsensitiveComparer` e `CaseInsensitiveHashCodeProvider`, inizializzare nuove istanze di queste classi utilizzando costruttori che accettano un parametro `culture`. Per il parametro `culture` specificare <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>. Nell'esempio di codice seguente viene illustrato il costruttore per un oggetto `Hashtable` indipendente dalle impostazioni cultura.

```vb
internalHashtable = New Hashtable(New
    CaseInsensitiveHashCodeProvider(CultureInfo.InvariantCulture),
    New CaseInsensitiveComparer(CultureInfo.InvariantCulture))
```

```csharp
internalHashtable = new Hashtable(new CaseInsensitiveHashCodeProvider
    (CultureInfo.InvariantCulture),
    new CaseInsensitiveComparer(CultureInfo.InvariantCulture));
```

## <a name="using-the-collectionsutilcreatecaseinsensitivehashtable-method"></a>Utilizzo del metodo CollectionsUtil.CreateCaseInsensitiveHashtable

Il metodo `CollectionsUtil.CreateCaseInsensitiveHashTable` rappresenta un rapido meccanismo per creare una nuova istanza della classe `Hashtable` in cui viene ignorato l'uso di maiuscole e minuscole nelle stringhe. Tutti gli overload del metodo `CollectionsUtil.CreateCaseInsensitiveHashTable` sono tuttavia dipendenti dalle impostazioni cultura in quanto utilizzano la proprietà `Thread.CurrentCulture`. Con questo metodo non è possibile creare un oggetto `Hashtable` indipendente dalle impostazioni cultura. Per creare un oggetto `Hashtable` indipendente dalle impostazioni cultura, usare il costruttore di `Hashtable`che accetta un parametro `culture`. Per il parametro `culture` specificare `CultureInfo.InvariantCulture`. Nell'esempio di codice seguente viene illustrato il costruttore per un oggetto `Hashtable` indipendente dalle impostazioni cultura.

```vb
internalHashtable = New Hashtable(New
    CaseInsensitiveHashCodeProvider(CultureInfo.InvariantCulture),
    New CaseInsensitiveComparer(CultureInfo.InvariantCulture))
```

```csharp
internalHashtable = new Hashtable(new CaseInsensitiveHashCodeProvider
    (CultureInfo.InvariantCulture),
    new CaseInsensitiveComparer(CultureInfo.InvariantCulture));
```

<a name="cpconperformingculture-insensitivestringoperationsincollectionsanchor1"></a>

## <a name="using-the-sortedlist-class"></a>Utilizzo della classe SortedList

Un oggetto `SortedList` rappresenta una raccolta di coppie chiave-valore ordinate in base alle chiavi e a cui è possibile accedere in base alla chiave e all'indice. Quando si utilizza un oggetto `SortedList` in cui le chiavi sono costituite da stringhe, è possibile che la proprietà `Thread.CurrentCulture` influisca sull'ordinamento e sulla ricerca. Per ottenere un comportamento indipendente dalle impostazioni cultura da un oggetto `SortedList`, creare un oggetto `SortedList` con uno dei costruttori che accetta un parametro `comparer`. Il parametro `comparer` specifica l'implementazione di <xref:System.Collections.IComparer> da usare quando si confrontano le chiavi. Per il parametro, specificare una classe di operatori di confronto personalizzata che usi `CultureInfo.InvariantCulture` per il confronto delle chiavi. Nell'esempio seguente viene illustrata una classe personalizzata di operatori di confronto indipendenti dalle impostazioni cultura che è possibile specificare come parametro `comparer` per un costruttore di `SortedList`.

```vb
Imports System.Collections
Imports System.Globalization

Friend Class InvariantComparer
    Implements IComparer
    Private m_compareInfo As CompareInfo
    Friend Shared [Default] As New InvariantComparer()

    Friend Sub New()
        m_compareInfo = CultureInfo.InvariantCulture.CompareInfo
    End Sub

    Public Function Compare(a As Object, b As Object) As Integer _
            Implements IComparer.Compare
        Dim sa As String = CType(a, String)
        Dim sb As String = CType(b, String)
        If Not (sa Is Nothing) And Not (sb Is Nothing) Then
            Return m_compareInfo.Compare(sa, sb)
        Else
            Return Comparer.Default.Compare(a, b)
        End If
    End Function
End Class
```

```csharp
using System;
using System.Collections;
using System.Globalization;

internal class InvariantComparer : IComparer
{
    private CompareInfo m_compareInfo;
    internal static readonly InvariantComparer Default = new
        InvariantComparer();

    internal InvariantComparer()
    {
        m_compareInfo = CultureInfo.InvariantCulture.CompareInfo;
    }

    public int Compare(Object a, Object b)
    {
        String sa = a as String;
        String sb = b as String;
        if (sa != null && sb != null)
            return m_compareInfo.Compare(sa, sb);
        else
            return Comparer.Default.Compare(a,b);
    }
}
```

In generale, se si utilizza un oggetto `SortedList` nelle stringhe senza specificare un operatore di confronto invariabile personalizzato, è possibile che l'elenco venga invalidato da una modifica apportata a `Thread.CurrentCulture` dopo che vi sono state inserite voci.

## <a name="using-the-arraylistsort-method"></a>Utilizzo del metodo ArrayList.Sort

Per impostazione predefinita, gli overload del metodo `ArrayList.Sort` consentono di eseguire ordinamenti dipendenti dalle impostazioni cultura tramite la proprietà `Thread.CurrentCulture`. I risultati possono variare in base alle impostazioni cultura, a causa di diversi criteri di ordinamento. Per eliminare il comportamento dipendente dalle impostazioni cultura, utilizzare gli overload del metodo che accettano un'implementazione di `IComparer`. Per il parametro `comparer`, specificare una classe di operatori di confronto invariabili personalizzati che usi `CultureInfo.InvariantCulture`. Per un esempio di classe di questo tipo, vedere l'argomento [Utilizzo della classe SortedList](#cpconperformingculture-insensitivestringoperationsincollectionsanchor1).

## <a name="see-also"></a>Vedere anche

- <xref:System.Collections.CaseInsensitiveComparer>
- <xref:System.Collections.CaseInsensitiveHashCodeProvider>
- <xref:System.Collections.ArrayList.Sort%2A?displayProperty=nameWithType>
- <xref:System.Collections.SortedList>
- <xref:System.Collections.Hashtable>
- <xref:System.Collections.IComparer>
- [Esecuzione di operazioni sulle stringhe indipendenti dalle impostazioni cultura](performing-culture-insensitive-string-operations.md)
- <xref:System.Collections.Specialized.CollectionsUtil.CreateCaseInsensitiveHashtable%2A?displayProperty=nameWithType>
