---
title: Depurar aplicativos de 64 bits | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], 64-bit
- 64-bit debugging
ms.assetid: db648e5f-6375-4e2d-aa98-eb7261958927
caps.latest.revision: 38
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2f67acff26d346b915f6b457fc0887f1d5f2ec3b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695909"
---
# <a name="debug-64-bit-applications"></a>Depurar aplicativos de 64 bits
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A versão mais recente deste tópico pode ser encontrada em [depurar 64-Bit Applications](https://docs.microsoft.com/visualstudio/debugger/debug-64-bit-applications) .  
  
Você pode depurar um aplicativo de 64 bits que está sendo executado no computador local ou em um computador remoto.  
  
 Para depurar um aplicativo de 64 bits que está em execução em um computador remoto, consulte [depuração remota](../debugger/remote-debugging.md).  
  
 Para depurar aplicativos de 64 bits localmente, Visual Studio usa um processo de trabalho de 64 bits (msvsmon.exe) para executar as operações de nível inferior não podem ser feitas dentro do processo do Visual Studio de 32 bits.  
  
 Não há suporte para a depuração de modo misto para processos de 64 bits que usam o .NET Framework versão 3.5 ou anterior.  
  
## <a name="debug-a-64-bit-application"></a>Depurar um aplicativo de 64 bits  
 Para tentar depurar um aplicativo de 64 bits:  
  
1. Crie uma solução do Visual Studio, por exemplo um console aplicativo c#.  
  
2. Defina a configuração para 64 bits usando o Configuration Manager. Para obter mais informações, confira [Como: Configurar projetos para plataformas de destino](../ide/how-to-configure-projects-to-target-platforms.md).  
  
3. Neste ponto, a versão de 64 bits do depurador remoto (msvsmon.exe) inicia. Ele é executado, desde que a solução com a configuração de 64 bits está aberta.  
  
4. Inicie a depuração. Você deve ter a mesma experiência assim como acontece com uma configuração de 32 bits. Se você obtiver erros, consulte a seção de solução de problemas abaixo.  
  
## <a name="troubleshooting-64-bit-debugging"></a>Solucionando problemas de depuração de 64 bits  
 Você verá um erro: "Uma operação de depuração de 64 bits está demorando mais do que o esperado." Nesse caso, o Visual Studio enviou uma solicitação para a versão de 64 bits do msvsmon.exe e levou muito tempo para o resultado da solicitação antes de voltar.  
  
 Há duas causas principais para este erro:  
  
- Você tem o software de segurança de rede instalado no computador que fez a pilha de rede seja pouco confiável e ele descartado pacotes ultrapassou o localhost. Tente desabilitar todos os softwares de segurança de rede e veja se isso resolve. Nesse caso, de relatório para o seu fornecedor de software de segurança de rede que o software está interferindo com o tráfego de localhost.  
  
- Você está executando em um problema de suspensão ou de desempenho com o Visual Studio. Se o problema ocorrer regularmente, você pode coletar despejos de memória do Visual Studio (devenv.exe) e o processo de trabalho (msvsmon.exe) e enviá-los à Microsoft. 
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos de 64 bits](https://msdn.microsoft.com/library/fd4026bc-2c3d-4b27-86dc-ec5e96018181)   
 [Configurando programas para 64 bits](https://msdn.microsoft.com/library/cb99f72b-8c74-48f4-846a-8921b37b97e9)   
 [Suporte ao IDE do Visual Studio de 64 bits](../ide/visual-studio-ide-64-bit-support.md)   
 [Usando arquivos de despejo](../debugger/using-dump-files.md)   
 [Depuração remota](../debugger/remote-debugging.md)
