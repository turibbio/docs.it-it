---
title: Operazioni sulle porte in .NET Framework
ms.date: 07/20/2015
helpviewer_keywords:
- ports, Visual Basic
ms.assetid: 1eba223b-7bd3-401a-b097-982bce96df1b
ms.openlocfilehash: 0ef0b8a7aec40603185d227d972cea655fd238c1
ms.sourcegitcommit: f8c270376ed905f6a8896ce0fe25b4f4b38ff498
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/04/2020
ms.locfileid: "84360137"
---
# <a name="port-operations-in-the-net-framework-with-visual-basic"></a><span data-ttu-id="32137-102">Operazioni sulle porte in .NET Framework con Visual Basic</span><span class="sxs-lookup"><span data-stu-id="32137-102">Port Operations in the .NET Framework with Visual Basic</span></span>

<span data-ttu-id="32137-103">È possibile accedere alle porte seriali del computer attraverso le classi .NET Framework nello spazio nomi <xref:System.IO.Ports?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="32137-103">You can access your computer's serial ports through the .NET Framework classes in the <xref:System.IO.Ports?displayProperty=nameWithType> namespace.</span></span> <span data-ttu-id="32137-104">La classe più importante, <xref:System.IO.Ports.SerialPort>, fornisce un framework per l'I/O sincrono e basato su eventi, l'accesso agli stati di blocco e interruzione, l'accesso alle proprietà del driver seriale.</span><span class="sxs-lookup"><span data-stu-id="32137-104">The most important class, <xref:System.IO.Ports.SerialPort>, provides a framework for synchronous and event-driven I/O, access to pin and break states, and access to serial driver properties.</span></span> <span data-ttu-id="32137-105">È possibile eseguire il wrapping della classe in un oggetto <xref:System.IO.Stream>, accessibile attraverso la proprietà <xref:System.IO.Ports.SerialPort.BaseStream>.</span><span class="sxs-lookup"><span data-stu-id="32137-105">It can be wrapped in a <xref:System.IO.Stream> object, accessible through the <xref:System.IO.Ports.SerialPort.BaseStream> property.</span></span> <span data-ttu-id="32137-106">Il wrapping di <xref:System.IO.Ports.SerialPort> in un oggetto <xref:System.IO.Stream> consente di accedere alla porta seriale attraverso le classi che usano i flussi.</span><span class="sxs-lookup"><span data-stu-id="32137-106">Wrapping <xref:System.IO.Ports.SerialPort> in a <xref:System.IO.Stream> object allows the serial port to be accessed by classes that use streams.</span></span> <span data-ttu-id="32137-107">Lo spazio dei nomi include le enumerazioni che semplificano il controllo delle porte seriali.</span><span class="sxs-lookup"><span data-stu-id="32137-107">The namespace includes enumerations that simplify the control of serial ports.</span></span>

<span data-ttu-id="32137-108">Il modo più semplice per creare un oggetto <xref:System.IO.Ports.SerialPort> consiste nell'usare il metodo <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A>.</span><span class="sxs-lookup"><span data-stu-id="32137-108">The simplest way to create a <xref:System.IO.Ports.SerialPort> object is through the <xref:Microsoft.VisualBasic.Devices.Ports.OpenSerialPort%2A> method.</span></span>

> [!NOTE]
> <span data-ttu-id="32137-109">Non è possibile usare le classi .NET Framework per accedere direttamente ad altri tipi di porte, quali le porte parallele, le porte USB e così via.</span><span class="sxs-lookup"><span data-stu-id="32137-109">You cannot use .NET Framework classes to directly access other types of ports, such as parallel ports, USB ports, and so on.</span></span>

## <a name="enumerations"></a><span data-ttu-id="32137-110">Enumerazioni</span><span class="sxs-lookup"><span data-stu-id="32137-110">Enumerations</span></span>

<span data-ttu-id="32137-111">In questa tabella sono elencate e descritte le enumerazioni principali usate per l'accesso alla porta seriale:</span><span class="sxs-lookup"><span data-stu-id="32137-111">This table lists and describes the main enumerations used for accessing a serial port:</span></span>

|<span data-ttu-id="32137-112">Enumerazione</span><span class="sxs-lookup"><span data-stu-id="32137-112">Enumeration</span></span>|<span data-ttu-id="32137-113">Descrizione</span><span class="sxs-lookup"><span data-stu-id="32137-113">Description</span></span>|
|---|---|
|<xref:System.IO.Ports.Handshake>|<span data-ttu-id="32137-114">Specifica il protocollo di controllo usato per stabilire la comunicazione della porta seriale per un oggetto <xref:System.IO.Ports.SerialPort>.</span><span class="sxs-lookup"><span data-stu-id="32137-114">Specifies the control protocol used in establishing a serial port communication for a <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.Parity>|<span data-ttu-id="32137-115">Specifica il bit di parità per un oggetto <xref:System.IO.Ports.SerialPort>.</span><span class="sxs-lookup"><span data-stu-id="32137-115">Specifies the parity bit for a <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.SerialData>|<span data-ttu-id="32137-116">Specifica il tipo di carattere ricevuto sulla porta seriale dell'oggetto <xref:System.IO.Ports.SerialPort>.</span><span class="sxs-lookup"><span data-stu-id="32137-116">Specifies the type of character that was received on the serial port of the <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.SerialError>|<span data-ttu-id="32137-117">Specifica gli errori che si verificano nell'oggetto <xref:System.IO.Ports.SerialPort>.</span><span class="sxs-lookup"><span data-stu-id="32137-117">Specifies errors that occur on the <xref:System.IO.Ports.SerialPort> object</span></span>|
|<xref:System.IO.Ports.SerialPinChange>|<span data-ttu-id="32137-118">Specifica il tipo di modifica eseguita nell'oggetto <xref:System.IO.Ports.SerialPort>.</span><span class="sxs-lookup"><span data-stu-id="32137-118">Specifies the type of change that occurred on the <xref:System.IO.Ports.SerialPort> object.</span></span>|
|<xref:System.IO.Ports.StopBits>|<span data-ttu-id="32137-119">Specifica il numero di bit di interruzione usati nell'oggetto <xref:System.IO.Ports.SerialPort>.</span><span class="sxs-lookup"><span data-stu-id="32137-119">Specifies the number of stop bits used on the <xref:System.IO.Ports.SerialPort> object.</span></span>|

## <a name="see-also"></a><span data-ttu-id="32137-120">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="32137-120">See also</span></span>

- <xref:Microsoft.VisualBasic.Devices.Ports>
- [<span data-ttu-id="32137-121">Accesso alle porte del computer</span><span class="sxs-lookup"><span data-stu-id="32137-121">Accessing the Computer's Ports</span></span>](accessing-the-computer-s-ports.md)
