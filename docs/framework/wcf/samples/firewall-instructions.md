---
title: Istruzioni del firewall
description: Informazioni su come abilitare porte o programmi nel firewall per gli esempi di WCF. Usare una di queste procedure, a seconda dei requisiti e dell'ambiente di sicurezza.
ms.date: 03/30/2017
ms.assetid: a7dc429f-65ac-4faf-974a-77d5fb977fe1
ms.openlocfilehash: de55d067960b8f2096c129f6feaf037219e06a96
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246141"
---
# <a name="firewall-instructions"></a><span data-ttu-id="d3a56-104">Istruzioni del firewall</span><span class="sxs-lookup"><span data-stu-id="d3a56-104">Firewall instructions</span></span>

<span data-ttu-id="d3a56-105">È necessario abilitare più porte o programmi nel firewall in modo che gli esempi di Windows Communication Foundation (WCF) possano funzionare.</span><span class="sxs-lookup"><span data-stu-id="d3a56-105">You must enable several ports or programs in the firewall so that the Windows Communication Foundation (WCF) samples can function.</span></span> <span data-ttu-id="d3a56-106">In molti degli esempi la comunicano avviene tramite le porte comprese nell'intervallo 8000-8003 e la porta 9000.</span><span class="sxs-lookup"><span data-stu-id="d3a56-106">Many of the samples communicate by using ports in the range 8000-8003, and port 9000.</span></span> <span data-ttu-id="d3a56-107">Il firewall viene attivato per impostazione predefinita e impedisce l'accesso a queste porte.</span><span class="sxs-lookup"><span data-stu-id="d3a56-107">The firewall is turned on by default and prevents access to these ports.</span></span> <span data-ttu-id="d3a56-108">Per abilitare il firewall per gli esempi, completare una delle procedure descritte di seguito, a seconda dei requisiti e dell’ambiente di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="d3a56-108">To enable the firewall for the samples, complete one of the following procedures, depending on your requirements and security environment:</span></span>

- <span data-ttu-id="d3a56-109">Opzione 1: abilitazione degli esempi in modo interattivo durante l’esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d3a56-109">Option 1: Interactively enable samples while running.</span></span> <span data-ttu-id="d3a56-110">Non apportare nessuna modifica alla configurazione del firewall in anticipo e procedere con l’avvio e l’esecuzione degli esempi.</span><span class="sxs-lookup"><span data-stu-id="d3a56-110">Make no advance changes to your firewall configuration and proceed to start building and running the samples.</span></span> <span data-ttu-id="d3a56-111">Quando viene eseguito un esempio, viene visualizzata una finestra di dialogo **avviso di sicurezza di Windows** .</span><span class="sxs-lookup"><span data-stu-id="d3a56-111">When a sample is run, a **Windows Security Alert** dialog box appears.</span></span> <span data-ttu-id="d3a56-112">Il programma di esempio in questione può essere quindi aggiunto, in modo interattivo, a un elenco sbloccato.</span><span class="sxs-lookup"><span data-stu-id="d3a56-112">The sample program in question can then be added interactively to an unblocked list.</span></span> <span data-ttu-id="d3a56-113">Questa procedura può richiedere il riavvio dell'esempio.</span><span class="sxs-lookup"><span data-stu-id="d3a56-113">With this procedure, you may have to then restart the sample.</span></span>

- <span data-ttu-id="d3a56-114">Opzione 2: abilitazione dei programmi di esempio in anticipo.</span><span class="sxs-lookup"><span data-stu-id="d3a56-114">Option 2: Enable sample programs in advance.</span></span> <span data-ttu-id="d3a56-115">Avviare l'applet del **Pannello di controllo Windows Firewall** e abilitare i programmi di esempio che si intende eseguire.</span><span class="sxs-lookup"><span data-stu-id="d3a56-115">Start the **Windows Firewall Control Panel** applet and enable the sample programs you plan to run.</span></span> <span data-ttu-id="d3a56-116">Per creare file eseguibili, è necessario prima compilare i programmi.</span><span class="sxs-lookup"><span data-stu-id="d3a56-116">You must build the programs first so the executable files exist.</span></span> <span data-ttu-id="d3a56-117">Informazioni più dettagliate sono descritte nella procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="d3a56-117">You can find more detailed instructions in the following procedure.</span></span>

- <span data-ttu-id="d3a56-118">Opzione 3: abilitazione dell’intervallo delle porte in anticipo.</span><span class="sxs-lookup"><span data-stu-id="d3a56-118">Option 3: Enable a port range in advance.</span></span> <span data-ttu-id="d3a56-119">Avviare l' **Windows Firewall** applet del pannello di controllo e abilitare le porte 80, 443, 8000-8003 e 9000, utilizzate dagli esempi.</span><span class="sxs-lookup"><span data-stu-id="d3a56-119">Start the **Windows Firewall Control Panel** applet and enable ports 80, 443, 8000-8003 and 9000, which are used by the samples.</span></span> <span data-ttu-id="d3a56-120">Informazioni più dettagliate sono descritte nella procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="d3a56-120">You can find more detailed instructions in the following procedure.</span></span> <span data-ttu-id="d3a56-121">Questa opzione è meno sicura rispetto alle altre in quanto consente a qualsiasi programma di utilizzare queste porte, non solo agli esempi.</span><span class="sxs-lookup"><span data-stu-id="d3a56-121">This option is less secure than the others because it allows any program to use these ports, not just the samples.</span></span>

<span data-ttu-id="d3a56-122">In caso di dubbi su quale procedura utilizzare, scegliere la prima opzione.</span><span class="sxs-lookup"><span data-stu-id="d3a56-122">If you are unsure of which procedure to use, choose the first option.</span></span> <span data-ttu-id="d3a56-123">Se si sta eseguendo un firewall di un altro fornitore, potrebbe essere necessario apportare modifiche simili.</span><span class="sxs-lookup"><span data-stu-id="d3a56-123">If you are running a firewall from another vendor, you might need to make similar changes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3a56-124">La modifica della configurazione del firewall influisce sulla sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d3a56-124">Changing your firewall configuration affects your security.</span></span> <span data-ttu-id="d3a56-125">È consigliabile registrare le modifiche apportate e rimuoverle una volta completate le operazioni con gli esempi.</span><span class="sxs-lookup"><span data-stu-id="d3a56-125">It is recommended that you record the changes you make and remove them when you are finished working with the samples.</span></span>

## <a name="enable-samples-programs-in-advance"></a><span data-ttu-id="d3a56-126">Abilitare i programmi di esempio in anticipo</span><span class="sxs-lookup"><span data-stu-id="d3a56-126">Enable samples programs in advance</span></span>

1. <span data-ttu-id="d3a56-127">Compilare l'esempio.</span><span class="sxs-lookup"><span data-stu-id="d3a56-127">Build the sample.</span></span>

2. <span data-ttu-id="d3a56-128">Scegliere **Avvia**  >  **esecuzione**, quindi immettere `firewall.cpl` .</span><span class="sxs-lookup"><span data-stu-id="d3a56-128">Choose **Start** > **Run**, and enter `firewall.cpl`.</span></span> <span data-ttu-id="d3a56-129">Verrà visualizzata l'applet del **Pannello di controllo Windows Firewall** .</span><span class="sxs-lookup"><span data-stu-id="d3a56-129">This opens the **Windows Firewall Control Panel** applet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d3a56-130">Per modificare le impostazioni del firewall ed eseguire gli esempi che richiedono la possibilità di comunicare con Windows Firewall, è necessario disporre delle autorizzazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="d3a56-130">You must have permission to change the Firewall settings to run samples that require the ability to communicate through the Windows Firewall.</span></span> <span data-ttu-id="d3a56-131">Se alcune impostazioni del firewall non sono disponibili e il computer è connesso a un dominio, è possibile che queste impostazioni vengano controllate dall'amministratore di sistema tramite Criteri di gruppo.</span><span class="sxs-lookup"><span data-stu-id="d3a56-131">If some firewall settings are unavailable and your computer is connected to a domain, your system administrator might be controlling these settings through Group Policy.</span></span>

3. <span data-ttu-id="d3a56-132">Completare uno dei seguenti passaggi specifici del sistema operativo per consentire a un programma di eseguire l'Windows Firewall:</span><span class="sxs-lookup"><span data-stu-id="d3a56-132">Complete one of the following operating-specific steps to allow a program through the Windows Firewall:</span></span>

    - <span data-ttu-id="d3a56-133">In Windows 7 o Windows Server 2008 R2 fare clic su **Consenti programma o funzionalità tramite Windows Firewall**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-133">On Windows 7 or Windows Server 2008 R2, click **Allow a program or feature through Windows Firewall**.</span></span> <span data-ttu-id="d3a56-134">Fare clic su **Modifica impostazioni**  >  **Consenti un altro programma**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-134">Click **Change Settings** > **Allow Another Program**.</span></span>

    - <span data-ttu-id="d3a56-135">In Windows Vista o Windows Server 2008, fare clic su **Consenti programma tramite Windows Firewall**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-135">On Windows Vista or Windows Server 2008, click **Allow a program through Windows Firewall**.</span></span>

4. <span data-ttu-id="d3a56-136">Nella scheda **eccezioni** fare clic su **Aggiungi programma**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-136">On the **Exceptions** tab, click **Add Program**.</span></span>

5. <span data-ttu-id="d3a56-137">Fare clic sul pulsante **Sfoglia** e selezionare il file eseguibile dell'esempio che si intende eseguire.</span><span class="sxs-lookup"><span data-stu-id="d3a56-137">Click the **Browse** button and select the executable file of the sample you plan to run.</span></span>

6. <span data-ttu-id="d3a56-138">Ripetere i passaggi 4 e 5 fino a quando non sono stati aggiunti i file eseguibili di tutti gli esempi che si prevede di eseguire.</span><span class="sxs-lookup"><span data-stu-id="d3a56-138">Repeat steps 4 and 5 until you have added the executable files of all the samples you plan to run.</span></span>

7. <span data-ttu-id="d3a56-139">Fare clic su **OK** per chiudere l'applet del firewall.</span><span class="sxs-lookup"><span data-stu-id="d3a56-139">Click **OK** to close the firewall applet.</span></span>

## <a name="enable-a-port-range-in-advance"></a><span data-ttu-id="d3a56-140">Abilita un intervallo di porte in anticipo</span><span class="sxs-lookup"><span data-stu-id="d3a56-140">Enable a port range in advance</span></span>

1. <span data-ttu-id="d3a56-141">Scegliere **Avvia**  >  **esecuzione**, quindi immettere `firewall.cpl` .</span><span class="sxs-lookup"><span data-stu-id="d3a56-141">Choose **Start** > **Run**, and enter `firewall.cpl`.</span></span> <span data-ttu-id="d3a56-142">Verrà visualizzata l'applet del **Pannello di controllo Windows Firewall** .</span><span class="sxs-lookup"><span data-stu-id="d3a56-142">This opens the **Windows Firewall Control Panel** applet.</span></span>

2. <span data-ttu-id="d3a56-143">In Windows 7 o Windows Server 2008 R2 attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d3a56-143">On Windows 7 or Windows Server 2008 R2, follow these steps.</span></span>

    1. <span data-ttu-id="d3a56-144">Fare clic su **Impostazioni avanzate** nella colonna a sinistra della finestra di Windows Firewall.</span><span class="sxs-lookup"><span data-stu-id="d3a56-144">Click **Advanced settings** in the left column of the Windows Firewall window.</span></span>

    2. <span data-ttu-id="d3a56-145">Fare clic su **regole in ingresso** nella colonna a sinistra.</span><span class="sxs-lookup"><span data-stu-id="d3a56-145">Click **Inbound Rules** in the left column.</span></span>

    3. <span data-ttu-id="d3a56-146">Fare clic su **nuove regole** nella colonna a destra.</span><span class="sxs-lookup"><span data-stu-id="d3a56-146">Click **New Rules** in the right column.</span></span>

    4. <span data-ttu-id="d3a56-147">Selezionare **porta** e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-147">Select **Port** and click **next**.</span></span>

    5. <span data-ttu-id="d3a56-148">Selezionare **TCP** e immettere `8000, 8001, 8002, 8003, 9000, 80, 443` nel campo **porte locali specifiche** .</span><span class="sxs-lookup"><span data-stu-id="d3a56-148">Select **TCP** and enter `8000, 8001, 8002, 8003, 9000, 80, 443` in the **Specific local ports** field.</span></span>

    6. <span data-ttu-id="d3a56-149">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-149">Click **Next**.</span></span>

    7. <span data-ttu-id="d3a56-150">Selezionare **Consenti la connessione**e fare clic su **Avanti** .</span><span class="sxs-lookup"><span data-stu-id="d3a56-150">Select **Allow the connection**, and click **Next** .</span></span>

    8. <span data-ttu-id="d3a56-151">Selezionare **dominio** e **privato**e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-151">Select **Domain** and **Private**, and click **Next**.</span></span>

    9. <span data-ttu-id="d3a56-152">Denominare questa regola `WCF-WF 4.0 Samples` e fare clic su **fine**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-152">Name this rule `WCF-WF 4.0 Samples`, and click **Finish**.</span></span>

    10. <span data-ttu-id="d3a56-153">Fare clic su **regole in uscita** e ripetere i passaggi da c a h.</span><span class="sxs-lookup"><span data-stu-id="d3a56-153">Click **Outbound Rules** and repeat steps c to h.</span></span>

3. <span data-ttu-id="d3a56-154">In Windows Vista o Windows Server 2008, attenersi alla seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="d3a56-154">On Windows Vista or Windows Server 2008, follow these steps.</span></span>

    1. <span data-ttu-id="d3a56-155">Fare clic su **Consenti programma con Windows Firewall**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-155">Click **Allow a program through Windows Firewall**.</span></span>

    2. <span data-ttu-id="d3a56-156">Nella scheda **eccezioni** fare clic su **Aggiungi porta**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-156">On the **Exceptions** tab, click **Add Port**.</span></span>

    3. <span data-ttu-id="d3a56-157">Immettere un nome, immettere 8000 come numero di porta e selezionare l'opzione **TCP** .</span><span class="sxs-lookup"><span data-stu-id="d3a56-157">Enter a name, enter 8000 as the port number, and select the **TCP** option.</span></span>

    4. <span data-ttu-id="d3a56-158">Fare clic sul pulsante **Cambia ambito** , selezionare l'opzione solo **rete** (subnet) e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3a56-158">Click the **Change Scope** button, select the **My Network** (subnet) only option, and click **OK**.</span></span>

    5. <span data-ttu-id="d3a56-159">Ripetere i passaggi da B a D per le porte 8001, 8002, 8003, 9000, 80 e 443.</span><span class="sxs-lookup"><span data-stu-id="d3a56-159">Repeat steps b to d for ports 8001, 8002, 8003, 9000, 80, and 443.</span></span>

4. <span data-ttu-id="d3a56-160">Fare clic su **OK** per chiudere l'applet del firewall.</span><span class="sxs-lookup"><span data-stu-id="d3a56-160">Click **OK** to close the firewall applet.</span></span>

> [!NOTE]
> <span data-ttu-id="d3a56-161">Rimuovere qualsiasi eccezione del firewall una volta completate le operazioni con gli esempi.</span><span class="sxs-lookup"><span data-stu-id="d3a56-161">Remove any firewall exceptions when you are finished working with the samples.</span></span> <span data-ttu-id="d3a56-162">A tale scopo, aprire l' **Windows Firewall** applet del pannello di controllo e rimuovere tutti i programmi o le voci di porta aggiunti dalle procedure precedenti.</span><span class="sxs-lookup"><span data-stu-id="d3a56-162">To do so, open the **Windows Firewall Control Panel** applet and remove any programs or port entries that were added by the previous procedures.</span></span>
