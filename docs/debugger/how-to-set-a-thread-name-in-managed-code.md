---
title: Definir um nome de thread no código gerenciado | Microsoft Docs
description: Defina um nome de thread em código gerenciado durante a depuração de aplicativo multithread no Visual Studio. A nomenclatura de threads é usada para controlar threads na janela threads.
ms.custom: SEO-VS-2020
ms.date: 04/27/2017
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Thread.Name property
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c0c4d74a-0314-4b71-81c9-b0b019347ab8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 3defa5eaee2aafabcb4cf890516f7c78be47b1e7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915768"
---
# <a name="how-to-set-a-thread-name-in-managed-code"></a>Como definir um nome de thread no código gerenciado
A nomeação de thread é possível em qualquer edição do Visual Studio. A nomeação de thread é útil para manter o controle de threads na janela **Threads**.

 Para definir um nome do thread no código gerenciado, use a propriedade <xref:System.Threading.Thread.Name%2A>.

## <a name="example"></a>Exemplo

```csharp
public class Needle
{
    // This method will be called when the thread is started.
    public void Baz()
    {
        Console.WriteLine("Needle Baz is running on another thread");
    }
}

public void Main()
{
    Console.WriteLine("Thread Simple Sample");
    Needle oNeedle = new Needle();
    // Create a Thread object.
    System.Threading.Thread oThread = new System.Threading.Thread(oNeedle.Baz);
    // Set the Thread name to "MyThread".
    oThread.Name = "MyThread";
    // Starting the thread invokes the ThreadStart delegate
    oThread.Start();
}
```

```VB
Public Class Needle
    ' This method will be called when the thread is started.
    Sub Baz()
        Console.WriteLine("Needle Baz is running on another thread")
    End Sub
End Class

Sub Main()
    Console.WriteLine("Thread Simple Sample")
    Dim oNeedle As New Needle()
   ' Create a Thread object.
    Dim oThread As New System.Threading.Thread(AddressOf oNeedle.Baz)
    ' Set the Thread name to "MyThread".
    oThread.Name = "MyThread"
    ' Starting the thread invokes the ThreadStart delegate
    oThread.Start()
End Sub
```

## <a name="see-also"></a>Confira também
- [Depurar aplicativos multissegmentados](../debugger/debug-multithreaded-applications-in-visual-studio.md)
- [Como definir um nome de thread em código nativo](../debugger/how-to-set-a-thread-name-in-native-code.md)