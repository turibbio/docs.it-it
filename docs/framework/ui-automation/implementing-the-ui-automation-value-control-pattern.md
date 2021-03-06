---
title: Implementazione del pattern di controllo Value di automazione interfaccia utente
ms.date: 03/30/2017
helpviewer_keywords:
- control patterns, Value
- UI Automation, Value control pattern
- Value control pattern
ms.assetid: b0fcdd87-3add-4345-bca9-e891205e02ba
ms.openlocfilehash: eb77f26bbe3546a3f90804c3648f8547fb6abad0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/12/2020
ms.locfileid: "79180082"
---
# <a name="implementing-the-ui-automation-value-control-pattern"></a>Implementazione del pattern di controllo Value di automazione interfaccia utente
> [!NOTE]
> Questa documentazione è destinata agli sviluppatori di .NET Framework che vogliono usare le classi gestite di [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] definite nello spazio dei nomi <xref:System.Windows.Automation>. Per informazioni aggiornate su [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], vedere [Windows Automation API: automazione interfaccia utente](/windows/win32/winauto/entry-uiauto-win32).  
  
 In questo argomento vengono presentate le linee guida e le convenzioni per l'implementazione di <xref:System.Windows.Automation.Provider.IValueProvider>, incluse le informazioni relative a eventi e proprietà. Alla fine della panoramica sono elencati collegamenti ad altro materiale di riferimento.  
  
 Il pattern di controllo <xref:System.Windows.Automation.ValuePattern> viene usato per supportare i controlli con un valore intrinseco che non si estende su un intervallo e che può essere rappresentato come stringa. Questa stringa può essere modificabile, a seconda del controllo e delle impostazioni. Per esempi di controlli che implementano questo pattern, vedere [Control Pattern Mapping for UI Automation Clients](control-pattern-mapping-for-ui-automation-clients.md).  
  
<a name="Implementation_Guidelines_and_Conventions"></a>
## <a name="implementation-guidelines-and-conventions"></a>Linee guida e convenzioni di implementazione  
 Quando si implementa il pattern di controllo Value, tenere presenti le linee guida e le convenzioni seguenti:  
  
- I controlli come <xref:System.Windows.Automation.ControlType.ListItem> e <xref:System.Windows.Automation.ControlType.TreeItem> devono supportare <xref:System.Windows.Automation.ValuePattern> se il valore di uno qualsiasi degli elementi è modificabile, indipendentemente dalla modalità di modifica corrente del controllo. Il controllo padre deve supportare anche <xref:System.Windows.Automation.ValuePattern> se gli elementi figlio sono modificabili.  
  
 ![Elemento di elenco modificabile](./media/uia-valuepattern-editable-listitem.PNG "UIA_ValuePattern_Editable_ListItem")  
Esempio di elemento elenco modificabile  
  
- I controlli di modifica a riga singola supportano l'accesso a livello di codice ai contenuti implementando <xref:System.Windows.Automation.Provider.IValueProvider>. I controlli di modifica a più righe, tuttavia, non implementano <xref:System.Windows.Automation.Provider.IValueProvider>, ma forniscono l'accesso ai contenuti implementando <xref:System.Windows.Automation.Provider.ITextProvider>.  
  
- Per recuperare i contenuti testuali di un controllo di modifica a più righe, il controllo deve implementare <xref:System.Windows.Automation.Provider.ITextProvider>. <xref:System.Windows.Automation.Provider.ITextProvider> non supporta, tuttavia, l'impostazione del valore di un controllo.  
  
- <xref:System.Windows.Automation.Provider.IValueProvider> non supporta il recupero delle informazioni di formattazione o dei valori delle sottostringhe. Implementare <xref:System.Windows.Automation.Provider.ITextProvider> in questi scenari.  
  
- <xref:System.Windows.Automation.Provider.IValueProvider>deve essere implementato da controlli quali il controllo di selezione **Selezione colori** di Microsoft Word (illustrato di seguito), che supporta il mapping delle stringhe tra un valore di colore (ad esempio, "giallo") e una struttura RGB interna equivalente.  
  
 ![Selezione colori con il giallo evidenziato](./media/uia-valuepattern-colorpicker.png "UIA_ValuePattern_ColorPicker")  
Esempio di mapping delle stringhe dei campioni colore  
  
- Un controllo deve avere <xref:System.Windows.Automation.AutomationElement.IsEnabledProperty> impostato su `true` e <xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty> impostato su `false` prima di consentire una chiamata a <xref:System.Windows.Automation.Provider.IValueProvider.SetValue%2A>.  
  
<a name="Required_Members_for_the_IValueProvider_Interface"></a>
## <a name="required-members-for-ivalueprovider"></a>Membri obbligatori per IValueProvider  
 Le proprietà e i metodi seguenti sono obbligatori per l'implementazione di <xref:System.Windows.Automation.Provider.IValueProvider>.  
  
|Membri obbligatori|Tipo di membro|Note|  
|----------------------|-----------------|-----------|  
|<xref:System.Windows.Automation.ValuePattern.IsReadOnlyProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.ValuePattern.ValueProperty>|Proprietà|nessuno|  
|<xref:System.Windows.Automation.ValuePattern.SetValue%2A>|Metodo|nessuno|  
  
<a name="Exceptions"></a>
## <a name="exceptions"></a>Eccezioni  
 I provider devono generare le eccezioni seguenti.  
  
|Tipo di eccezione|Condizione|  
|--------------------|---------------|  
|<xref:System.InvalidOperationException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> - Se le informazioni specifiche delle impostazioni locali vengono passate a un controllo in un formato non corretto, ad esempio una data formattata in modo non corretto.|  
|<xref:System.ArgumentException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> - Se un nuovo valore non può essere convertito da una stringa in un formato riconosciuto dal controllo.- If a new value cannot be converted from a string to a format the control recognizes.|  
|<xref:System.Windows.Automation.ElementNotEnabledException>|<xref:System.Windows.Automation.ValuePattern.SetValue%2A><br /><br /> - Quando si tenta di modificare un controllo che non è abilitato.- When an attempt to manipulate a control that is not enabled.|  
  
## <a name="see-also"></a>Vedere anche

- [UI Automation Control Patterns Overview](ui-automation-control-patterns-overview.md)
- [Supportare pattern di controllo in un provider di automazione interfaccia utente](support-control-patterns-in-a-ui-automation-provider.md)
- [Pattern di controllo di automazione interfaccia utente per i client](ui-automation-control-patterns-for-clients.md)
- [Esempio di inserimento di testo di ValuePattern](https://github.com/Microsoft/WPF-Samples/tree/master/Accessibility/InsertText)
- [UI Automation Tree Overview](ui-automation-tree-overview.md)
- [Utilizzare la memorizzazione nella cache per l'automazione interfaccia utente](use-caching-in-ui-automation.md)
