---
title: Uso di un socket server sincrono
description: Questo esempio mostra un socket server sincrono in .NET Framework, che sospende un'applicazione fino a quando non viene ricevuta una richiesta di connessione sul socket.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- application protocols, sockets
- synchronous server sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- server sockets
- receiving data, sockets
- Socket class, synchronous server sockets
- protocols, sockets
- sockets, synchronous server sockets
- Internet, sockets
ms.assetid: d1ce882e-653e-41f5-9289-844ec855b804
ms.openlocfilehash: 9e7d32595f554b32ecc72bbb1f1a469ad5935467
ms.sourcegitcommit: da21fc5a8cce1e028575acf31974681a1bc5aeed
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84502054"
---
# <a name="using-a-synchronous-server-socket"></a><span data-ttu-id="bec04-103">Uso di un socket server sincrono</span><span class="sxs-lookup"><span data-stu-id="bec04-103">Using a Synchronous Server Socket</span></span>
<span data-ttu-id="bec04-104">I socket server sincroni sospendono l'esecuzione dell'applicazione fino a quando non viene ricevuta una richiesta di connessione sul socket.</span><span class="sxs-lookup"><span data-stu-id="bec04-104">Synchronous server sockets suspend the execution of the application until a connection request is received on the socket.</span></span> <span data-ttu-id="bec04-105">I socket server sincroni non sono adatti per le applicazioni che fanno un uso massiccio della rete per le loro operazioni, ma possono essere appropriati per applicazioni di rete semplici.</span><span class="sxs-lookup"><span data-stu-id="bec04-105">Synchronous server sockets are not suitable for applications that make heavy use of the network in their operation, but they can be suitable for simple network applications.</span></span>  
  
 <span data-ttu-id="bec04-106">Dopo aver impostato un <xref:System.Net.Sockets.Socket> per l'ascolto su un endpoint tramite i metodi <xref:System.Net.Sockets.Socket.Bind%2A> e <xref:System.Net.Sockets.Socket.Listen%2A>, il socket è pronto per accettare le richieste di connessione in ingresso tramite il metodo <xref:System.Net.Sockets.Socket.Accept%2A>.</span><span class="sxs-lookup"><span data-stu-id="bec04-106">After a <xref:System.Net.Sockets.Socket> is set to listen on an endpoint using the <xref:System.Net.Sockets.Socket.Bind%2A> and <xref:System.Net.Sockets.Socket.Listen%2A> methods, it is ready to accept incoming connection requests using the <xref:System.Net.Sockets.Socket.Accept%2A> method.</span></span> <span data-ttu-id="bec04-107">L'applicazione viene sospesa fino a quando non viene ricevuta una richiesta di connessione quando viene chiamato il metodo **Accept**.</span><span class="sxs-lookup"><span data-stu-id="bec04-107">The application is suspended until a connection request is received when the **Accept** method is called.</span></span>  
  
 <span data-ttu-id="bec04-108">Quando viene ricevuta una richiesta di connessione, **Accept** restituisce una nuova istanza di **Socket** associata al client che si connette.</span><span class="sxs-lookup"><span data-stu-id="bec04-108">When a connection request is received, **Accept** returns a new **Socket** instance that is associated with the connecting client.</span></span> <span data-ttu-id="bec04-109">L'esempio seguente legge i dati dal client, li visualizza nella console e li restituisce al client.</span><span class="sxs-lookup"><span data-stu-id="bec04-109">The following example reads data from the client, displays it on the console, and echoes the data back to the client.</span></span> <span data-ttu-id="bec04-110">Il **socket** non specifica alcun protocollo di messaggistica, quindi la stringa " \<EOF> " contrassegna la fine dei dati del messaggio.</span><span class="sxs-lookup"><span data-stu-id="bec04-110">The **Socket** does not specify any messaging protocol, so the string "\<EOF>" marks the end of the message data.</span></span> <span data-ttu-id="bec04-111">Si presuppone che un **Socket** denominato `listener` sia stato inizializzato e associato a un endpoint.</span><span class="sxs-lookup"><span data-stu-id="bec04-111">It assumes that a **Socket** named `listener` has been initialized and bound to an endpoint.</span></span>  
  
```vb  
Console.WriteLine("Waiting for a connection...")  
Dim handler As Socket = listener.Accept()  
Dim data As String = Nothing  
  
While True  
    bytes = New Byte(1024) {}  
    Dim bytesRec As Integer = handler.Receive(bytes)  
    data += Encoding.ASCII.GetString(bytes, 0, bytesRec)  
    If data.IndexOf("<EOF>") > - 1 Then  
        Exit While  
    End If  
End While  
  
Console.WriteLine("Text received : {0}", data)  
  
Dim msg As Byte() = Encoding.ASCII.GetBytes(data)  
handler.Send(msg)  
handler.Shutdown(SocketShutdown.Both)  
handler.Close()  
```  
  
```csharp  
Console.WriteLine("Waiting for a connection...");  
Socket handler = listener.Accept();  
String data = null;  
  
while (true) {  
    bytes = new byte[1024];  
    int bytesRec = handler.Receive(bytes);  
    data += Encoding.ASCII.GetString(bytes,0,bytesRec);  
    if (data.IndexOf("<EOF>") > -1) {  
        break;  
    }  
}  
  
Console.WriteLine( "Text received : {0}", data);  
  
byte[] msg = Encoding.ASCII.GetBytes(data);  
handler.Send(msg);  
handler.Shutdown(SocketShutdown.Both);  
handler.Close();  
```  
  
## <a name="see-also"></a><span data-ttu-id="bec04-112">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="bec04-112">See also</span></span>

- [<span data-ttu-id="bec04-113">Uso di un socket server asincrono</span><span class="sxs-lookup"><span data-stu-id="bec04-113">Using an Asynchronous Server Socket</span></span>](using-an-asynchronous-server-socket.md)
- [<span data-ttu-id="bec04-114">Esempio di socket server sincrono</span><span class="sxs-lookup"><span data-stu-id="bec04-114">Synchronous Server Socket Example</span></span>](synchronous-server-socket-example.md)
- [<span data-ttu-id="bec04-115">Attesa con socket</span><span class="sxs-lookup"><span data-stu-id="bec04-115">Listening with Sockets</span></span>](listening-with-sockets.md)
