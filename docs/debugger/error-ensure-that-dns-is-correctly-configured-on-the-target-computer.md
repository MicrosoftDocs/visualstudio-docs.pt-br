---
title: Verifique se o DNS está configurado corretamente no computador de destino | Microsoft Docs
description: Esse erro ocorre quando o computador de destino não pode resolver o nome do computador host do depurador do Visual Studio.
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.callback_dns_failed
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cf61e50cc1a6a831625d9cb7c0b12a286e20239f
ms.sourcegitcommit: 8590cf6b3351e82827fd21159beefef0c02bf162
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2021
ms.locfileid: "102466245"
---
# <a name="error-ensure-that-dns-is-correctly-configured-on-the-target-computer"></a>Erro: verifique se o DNS está configurado corretamente no computador de destino
Ao tentar fazer a depuração remota, você pode receber a seguinte mensagem de erro:

```cmd
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Ensure that DNS is correctly configured on the target computer.
```

 Esse erro ocorre quando o computador de destino não pode resolver o nome do computador host do depurador do Visual Studio. Verifique as configurações DNS no computador de destino.

- Para obter informações sobre como exibir sua configuração de DNS em Windows 8.1, vista, Windows 7, Windows Server 2012, Windows Server 2008 ou Windows Server 2008 R2, faça o seguinte: no menu **Iniciar** , escolha **ajuda e suporte** e, em seguida, procure **alterar configurações TCP/IP**.

- Para obter mais informações, vá para o [site do Microsoft Windows](https://www.microsoft.com/windows/) e pesquise **Alterar configurações de TCP/IP**.

  Se você não conseguir resolver o problema de DNS, tente executar o Depurador Remoto em uma conta diferente. Esse erro ocorre somente quando você está executando o Depurador Remoto sob a conta Serviço de Rede ou Sistema Local. Se você executar o Depurador Remoto em outra conta, ele poderá usar a autenticação NTLM, que não exige DNS. . Para o procedimento, consulte [erro: o serviço de depurador remoto do Visual Studio no computador de destino não pode se conectar de volta a este computador](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md).
