---
title: Modifiche di rilievo-.NET Framework a .NET Core
titleSuffix: ''
description: Elenca le modifiche di rilievo da .NET Framework a .NET Core.
ms.date: 05/05/2020
ms.openlocfilehash: 613c4e41e12be57d5631b347055140a4418e7207
ms.sourcegitcommit: 488aced39b5f374bc0a139a4993616a54d15baf0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/12/2020
ms.locfileid: "83206453"
---
# <a name="breaking-changes-for-migration-from-net-framework-to-net-core"></a><span data-ttu-id="25426-103">Modifiche di rilievo per la migrazione da .NET Framework a .NET Core</span><span class="sxs-lookup"><span data-stu-id="25426-103">Breaking changes for migration from .NET Framework to .NET Core</span></span>

<span data-ttu-id="25426-104">Se si esegue la migrazione di un'app da .NET Framework a .NET Core, le modifiche di rilievo elencate in questo articolo potrebbero interessare l'utente.</span><span class="sxs-lookup"><span data-stu-id="25426-104">If you're migrating an app from .NET Framework to .NET Core, the breaking changes listed in this article may affect you.</span></span> <span data-ttu-id="25426-105">Le modifiche di rilievo sono raggruppate per categoria e all'interno di tali categorie dalla versione di .NET Core in cui sono state introdotte.</span><span class="sxs-lookup"><span data-stu-id="25426-105">Breaking changes are grouped by category, and within those categories, by the version of .NET Core in which they were introduced.</span></span>

> [!NOTE]
> <span data-ttu-id="25426-106">Questo articolo non è un elenco completo delle modifiche di rilievo tra .NET Framework e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="25426-106">This article is not a complete list of breaking changes between .NET Framework and .NET Core.</span></span> <span data-ttu-id="25426-107">Di seguito sono riportate le modifiche di rilievo più importanti che verranno acquisite.</span><span class="sxs-lookup"><span data-stu-id="25426-107">The most important breaking changes are added here as we become aware of them.</span></span>

## <a name="core-net-libraries"></a><span data-ttu-id="25426-108">Principali librerie .NET</span><span class="sxs-lookup"><span data-stu-id="25426-108">Core .NET libraries</span></span>

- [<span data-ttu-id="25426-109">Modificare il valore predefinito di UseShellExecute</span><span class="sxs-lookup"><span data-stu-id="25426-109">Change in default value of UseShellExecute</span></span>](#change-in-default-value-of-useshellexecute)
- [<span data-ttu-id="25426-110">UnauthorizedAccessException generata da FileSystemInfo. Attributes</span><span class="sxs-lookup"><span data-stu-id="25426-110">UnauthorizedAccessException thrown by FileSystemInfo.Attributes</span></span>](#unauthorizedaccessexception-thrown-by-filesysteminfoattributes)
- [<span data-ttu-id="25426-111">Gestione delle eccezioni di stato del processo danneggiato non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-111">Handling corrupted-process-state exceptions is not supported</span></span>](#handling-corrupted-state-exceptions-is-not-supported)
- [<span data-ttu-id="25426-112">Le Proprietà UriBuilder non precedono più caratteri iniziali</span><span class="sxs-lookup"><span data-stu-id="25426-112">UriBuilder properties no longer prepend leading characters</span></span>](#uribuilder-properties-no-longer-prepend-leading-characters)

### <a name="net-core-21"></a><span data-ttu-id="25426-113">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="25426-113">.NET Core 2.1</span></span>

[!INCLUDE[Process.Start changes](~/includes/core-changes/corefx/2.1/process-start-changes.md)]

***

### <a name="net-core-10"></a><span data-ttu-id="25426-114">.NET Core 1.0</span><span class="sxs-lookup"><span data-stu-id="25426-114">.NET Core 1.0</span></span>

[!INCLUDE [UnauthorizedAccessException thrown by FileSystemInfo.Attributes](~/includes/core-changes/corefx/1.0/filesysteminfo-attributes-exceptions.md)]

***

[!INCLUDE [corrupted-state-exceptions](~/includes/core-changes/corefx/1.0/corrupted-state-exceptions.md)]

***

[!INCLUDE [uribuilder-behavior-changes](../../../includes/core-changes/corefx/1.0/uribuilder-behavior-changes.md)]

***

## <a name="cryptography"></a><span data-ttu-id="25426-115">Crittografia</span><span class="sxs-lookup"><span data-stu-id="25426-115">Cryptography</span></span>

- [<span data-ttu-id="25426-116">Il parametro booleano di SignedCms. ComputeSignature è rispettato</span><span class="sxs-lookup"><span data-stu-id="25426-116">Boolean parameter of SignedCms.ComputeSignature is respected</span></span>](#boolean-parameter-of-signedcmscomputesignature-is-respected)

### <a name="net-core-21"></a><span data-ttu-id="25426-117">.NET Core 2.1</span><span class="sxs-lookup"><span data-stu-id="25426-117">.NET Core 2.1</span></span>

[!INCLUDE [Boolean parameter of SignedCms.ComputeSignature is respected](~/includes/core-changes/cryptography/2.1/compute-signature-silent-parameter.md)]

***

## <a name="msbuild"></a><span data-ttu-id="25426-118">MSBuild</span><span class="sxs-lookup"><span data-stu-id="25426-118">MSBuild</span></span>

- [<span data-ttu-id="25426-119">Modifica del nome del file manifesto della risorsa</span><span class="sxs-lookup"><span data-stu-id="25426-119">Resource manifest file name change</span></span>](#resource-manifest-file-name-change)

### <a name="net-core-30"></a><span data-ttu-id="25426-120">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="25426-120">.NET Core 3.0</span></span>

[!INCLUDE[Resource file names](~/includes/core-changes/msbuild/3.0/resource-manifest-name.md)]

***

## <a name="networking"></a><span data-ttu-id="25426-121">Rete</span><span class="sxs-lookup"><span data-stu-id="25426-121">Networking</span></span>

- [<span data-ttu-id="25426-122">WebClient. CancelAsync non viene sempre annullato immediatamente</span><span class="sxs-lookup"><span data-stu-id="25426-122">WebClient.CancelAsync doesn't always cancel immediately</span></span>](#webclientcancelasync-doesnt-always-cancel-immediately)

### <a name="net-core-20"></a><span data-ttu-id="25426-123">.NET Core 2.0</span><span class="sxs-lookup"><span data-stu-id="25426-123">.NET Core 2.0</span></span>

[!INCLUDE [behavior-change-webclient-cancelasync](../../../includes/core-changes/networking/2.0/behavior-change-webclient-cancelasync.md)]

***

## <a name="windows-forms"></a><span data-ttu-id="25426-124">Windows Forms</span><span class="sxs-lookup"><span data-stu-id="25426-124">Windows Forms</span></span>

<span data-ttu-id="25426-125">È stato aggiunto il supporto Windows Forms a .NET Core nella versione 3,0.</span><span class="sxs-lookup"><span data-stu-id="25426-125">Windows Forms support was added to .NET Core in version 3.0.</span></span> <span data-ttu-id="25426-126">Se si esegue la migrazione di un'app Windows Forms da .NET Framework a .NET Core, le modifiche di rilievo elencate qui potrebbero influire sull'app.</span><span class="sxs-lookup"><span data-stu-id="25426-126">If you're migrating a Windows Forms app from .NET Framework to .NET Core, the breaking changes listed here may affect your app.</span></span>

- [<span data-ttu-id="25426-127">Controlli rimossi</span><span class="sxs-lookup"><span data-stu-id="25426-127">Removed controls</span></span>](#removed-controls)
- [<span data-ttu-id="25426-128">Evento CellFormatting non generato se viene visualizzata la descrizione comando</span><span class="sxs-lookup"><span data-stu-id="25426-128">CellFormatting event not raised if tooltip is shown</span></span>](#cellformatting-event-not-raised-if-tooltip-is-shown)
- [<span data-ttu-id="25426-129">Control. DefaultFont modificato in Segoe UI 9 PT</span><span class="sxs-lookup"><span data-stu-id="25426-129">Control.DefaultFont changed to Segoe UI 9 pt</span></span>](#default-control-font-changed-to-segoe-ui-9-pt)
- [<span data-ttu-id="25426-130">Modernizzazione di FolderBrowserDialog</span><span class="sxs-lookup"><span data-stu-id="25426-130">Modernization of the FolderBrowserDialog</span></span>](#modernization-of-the-folderbrowserdialog)
- [<span data-ttu-id="25426-131">SerializableAttribute rimosso da alcuni tipi di Windows Forms</span><span class="sxs-lookup"><span data-stu-id="25426-131">SerializableAttribute removed from some Windows Forms types</span></span>](#serializableattribute-removed-from-some-windows-forms-types)
- [<span data-ttu-id="25426-132">Opzione di compatibilità AllowUpdateChildControlIndexForTabControls non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-132">AllowUpdateChildControlIndexForTabControls compatibility switch not supported</span></span>](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-133">Opzione di compatibilità DomainUpDown. UseLegacyScrolling non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-133">DomainUpDown.UseLegacyScrolling compatibility switch not supported</span></span>](#domainupdownuselegacyscrolling-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-134">Opzione di compatibilità DoNotLoadLatestRichEditControl non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-134">DoNotLoadLatestRichEditControl compatibility switch not supported</span></span>](#donotloadlatestricheditcontrol-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-135">Opzione di compatibilità DoNotSupportSelectAllShortcutInMultilineTextBox non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-135">DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported</span></span>](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-136">Opzione di compatibilità DontSupportReentrantFilterMessage non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-136">DontSupportReentrantFilterMessage compatibility switch not supported</span></span>](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-137">Opzione di compatibilità EnableVisualStyleValidation non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-137">EnableVisualStyleValidation compatibility switch not supported</span></span>](#enablevisualstylevalidation-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-138">Opzione di compatibilità UseLegacyContextMenuStripSourceControlValue non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-138">UseLegacyContextMenuStripSourceControlValue compatibility switch not supported</span></span>](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-139">Opzione di compatibilità UseLegacyImages non supportata</span><span class="sxs-lookup"><span data-stu-id="25426-139">UseLegacyImages compatibility switch not supported</span></span>](#uselegacyimages-compatibility-switch-not-supported)
- [<span data-ttu-id="25426-140">Modifica dell'accesso per AccessibleObject. RuntimeIDFirstItem</span><span class="sxs-lookup"><span data-stu-id="25426-140">Change of access for AccessibleObject.RuntimeIDFirstItem</span></span>](#change-of-access-for-accessibleobjectruntimeidfirstitem)
- [<span data-ttu-id="25426-141">API duplicate rimosse da Windows Forms</span><span class="sxs-lookup"><span data-stu-id="25426-141">Duplicated APIs removed from Windows Forms</span></span>](#duplicated-apis-removed-from-windows-forms)

### <a name="net-core-31"></a><span data-ttu-id="25426-142">.NET Core 3,1</span><span class="sxs-lookup"><span data-stu-id="25426-142">.NET Core 3.1</span></span>

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

***

### <a name="net-core-30"></a><span data-ttu-id="25426-143">.NET Core 3.0</span><span class="sxs-lookup"><span data-stu-id="25426-143">.NET Core 3.0</span></span>

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9 pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

***

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

***

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

***

[!INCLUDE[AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

***

[!INCLUDE[DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

***

[!INCLUDE[DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

***

[!INCLUDE[DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

***

[!INCLUDE[DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

***

[!INCLUDE[EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

***

[!INCLUDE[UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

***

[!INCLUDE[UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

***

[!INCLUDE[Change of access for AccessibleObject.RuntimeIDFirstItem](~/includes/core-changes/windowsforms/3.0/changed-access-for-runtimeidfirstitem.md)]

***

[!INCLUDE[Duplicated APIs removed from Windows Forms](~/includes/core-changes/windowsforms/3.0/remove-duplicated-apis.md)]

***

## <a name="see-also"></a><span data-ttu-id="25426-144">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="25426-144">See also</span></span>

- [<span data-ttu-id="25426-145">API che generano sempre eccezioni in .NET Core</span><span class="sxs-lookup"><span data-stu-id="25426-145">APIs that always throw exceptions on .NET Core</span></span>](unsupported-apis.md)
- [<span data-ttu-id="25426-146">Tecnologie di .NET Framework non disponibili in .NET Core</span><span class="sxs-lookup"><span data-stu-id="25426-146">.NET Framework technologies unavailable on .NET Core</span></span>](../porting/net-framework-tech-unavailable.md)
