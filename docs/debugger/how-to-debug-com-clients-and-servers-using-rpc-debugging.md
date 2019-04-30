---
title: Depurar clientes e servidores usando a depuração RPC COM | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- RPC (Remote Procedure Call), debugging COM clients and servers
- COM, debugging
- RPC (Remote Procedure Call)
- RPC (Remote Procedure Call), debugging
- COM clients, debugging
- COM servers, debugging
- out-of-process remote procedure call debugging
- remote debugging, RPC (Remote Procedure Call)
- in-process remote procedure call debugging
ms.assetid: 3e8526c8-43b5-4b87-8e0d-b22c24f0a3ea
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f5c98405b424dd5402a903a236b1c5549a43616d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387513"
---
# <a name="how-to-debug-com-clients-and-servers-using-rpc-debugging"></a>Como: Depurar clientes e servidores COM usando a depuração RPC
Você pode usar a depuração de chamada de procedimento remoto (RPC) para depurar aplicativos cliente/servidor COM. Você deve habilitar a depuração de RPC para usá-lo. Com a depuração de RPC habilitada, quando você entrar na chamada do servidor do cliente, o depurador anexará ao servidor e permitirá depurar o código. Quando o depurador for anexado, você poderá usar todos os recursos do depurador com o cliente e os processos do servidor.

### <a name="to-enable-rpc-debugging"></a>Para habilitar a depuração de RPC

1. No menu **Ferramentas**, clique em **Opções**.

2. Na caixa de diálogo **Opções**, clique na pasta **Depuração**.

3. Clique na página **Nativa**.

4. Marque a caixa de seleção **Depuração RPC**.

    > [!NOTE]
    > Para depurar chamadas de RPC, você deve ter privilégios de Administrador ou Usuário avançado.

    > [!NOTE]
    > A entrada de RPC em um servidor remoto que executa o Microsoft Windows Vista só funcionará se um depurador nativo for anexado ao servidor remoto. Caso contrário, a chamada de RPC apresentará falha sem uma mensagem de erro. De outro modo, a chamada de RPC será concluída, mas a depuração da chamada de RPC não funcionará.

## <a name="see-also"></a>Consulte também
- [Depuração de servidor COM e contêiner](../debugger/com-server-and-container-debugging.md)
- [Depurando no Visual Studio](../debugger/index.md)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)