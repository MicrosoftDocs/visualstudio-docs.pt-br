---
title: Como depurar o método OnStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- OnStart method
- debugging [Visual Studio], Windows services
- debugging managed code, OnStart method
- debugging Windows Services applications, OnStart method
- Windows Service applications, debugging
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7392b4185def34f38f0e183f2626bd648bb4b4ea
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350011"
---
# <a name="how-to-debug-the-onstart-method"></a>Como depurar o método OnStart
Você pode depurar um serviço do Windows iniciando o serviço e anexando o depurador ao processo do serviço. Para obter mais informações, confira [Como depurar aplicativos de Serviço Windows](/dotnet/framework/windows-services/how-to-debug-windows-service-applications). No entanto, para depurar o <xref:System.ServiceProcess.ServiceBase.OnStart%2A?displayProperty=fullName> método de um serviço do Windows, você deve iniciar o depurador de dentro do método.

1. Adicione uma chamada para <xref:System.Diagnostics.Debugger.Launch%2A> no início do `OnStart()` método.

    ```csharp
    protected override void OnStart(string[] args)
    {
        System.Diagnostics.Debugger.Launch();
    }
    ```

2. Inicie o serviço (você pode usá `net start` -lo ou iniciá-lo na janela **Serviços** ).

    Você deverá ver uma caixa de diálogo semelhante à seguinte:

    ![OnStartDebug](../debugger/media/onstartdebug.png "OnStartDebug")

3. Selecione **Sim, depurar \<service name> .**

4. Na janela do depurador just-in-time, selecione a versão do Visual Studio que você deseja usar para depuração.

    ![JustInTimeDebugger](../debugger/media/justintimedebugger.png "JustInTimeDebugger")

5. Uma nova instância do Visual Studio é iniciada e a execução é interrompida no `Debugger.Launch()` método.

## <a name="see-also"></a>Veja também
- [Segurança do depurador](../debugger/debugger-security.md)
- [Depurando código gerenciado](../debugger/debugging-managed-code.md)
