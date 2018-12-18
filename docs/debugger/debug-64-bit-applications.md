---
title: Depurar aplicativos de 64 bits | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], 64-bit
- 64-bit debugging
ms.assetid: db648e5f-6375-4e2d-aa98-eb7261958927
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 28a7625729989252a29ab1d0f65feec010e9e65f
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44284075"
---
# <a name="debug-64-bit-applications"></a>Depurar aplicativos de 64 bits
Você pode depurar um aplicativo de 64 bits que está sendo executado no computador local ou em um computador remoto.  
  
 Para depurar um aplicativo de 64 bits que está em execução em um computador remoto, consulte [depuração remota](../debugger/remote-debugging.md).  
  
 Para depurar aplicativos de 64 bits localmente, Visual Studio usa um processo de trabalho de 64 bits (msvsmon.exe) para executar as operações de nível inferior não podem ser feitas dentro do processo do Visual Studio de 32 bits.  
  
 Não há suporte para a depuração de modo misto para processos de 64 bits que usam o .NET Framework versão 3.5 ou anterior.  
  
## <a name="debug-a-64-bit-application"></a>Depurar um aplicativo de 64 bits  
 Para tentar depurar um aplicativo de 64 bits:  
  
1.  Crie uma solução do Visual Studio, por exemplo um console aplicativo c#.  
  
2.  Defina a configuração para 64 bits usando o Configuration Manager. Para obter mais informações, consulte [como: configurar projetos para plataformas de destino](../ide/how-to-configure-projects-to-target-platforms.md).  
  
3.  Neste ponto, a versão de 64 bits do depurador remoto (msvsmon.exe) inicia. Ele é executado, desde que a solução com a configuração de 64 bits está aberta.  
  
4.  Inicie a depuração. Você deve ter a mesma experiência assim como acontece com uma configuração de 32 bits. Se você obtiver erros, consulte a seção de solução de problemas abaixo.  
  
## <a name="troubleshooting-64-bit-debugging"></a>Solucionando problemas de depuração de 64 bits  
 Você verá um erro: "uma operação de depuração de 64 bits está demorando mais do que o esperado." Nesse caso, o Visual Studio enviou uma solicitação para a versão de 64 bits do msvsmon.exe e levou muito tempo para o resultado da solicitação antes de voltar.  
  
 Há duas causas principais para este erro:  
  
-   Você tem o software de segurança de rede instalado no computador que fez a pilha de rede seja pouco confiável e ele descartado pacotes ultrapassou o localhost. Tente desabilitar todos os softwares de segurança de rede e veja se isso resolve. Nesse caso, de relatório para o seu fornecedor de software de segurança de rede que o software está interferindo com o tráfego de localhost.  
  
-   Você está executando em um problema de suspensão ou de desempenho com o Visual Studio. Se o problema ocorrer regularmente, você pode coletar despejos de memória do Visual Studio (devenv.exe) e o processo de trabalho (msvsmon.exe) e enviá-los à Microsoft. Para obter informações sobre como relatar um problema, consulte [como relatar um problema com o Visual Studio](../ide/How-to-Report-a-Problem-with-Visual-Studio-2017.md).
  
## <a name="see-also"></a>Consulte também  
 [Aplicativos de 64 bits](https://docs.microsoft.com/dotnet/framework/64-bit-apps)   
 [Configurando programas para 64 bits](/cpp/build/configuring-programs-for-64-bit-visual-cpp)   
 [Suporte de 64 bits do Visual Studio IDE](../ide/visual-studio-ide-64-bit-support.md)   
 [Usando arquivos de despejo](../debugger/using-dump-files.md)   
 [Depuração remota](../debugger/remote-debugging.md)