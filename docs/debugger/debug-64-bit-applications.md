---
title: Depurar aplicativos de 64 bits | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ca7feade173db9ccf8c86daaeb1399ef3e10a08b
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350765"
---
# <a name="debug-64-bit-applications"></a>Depurar aplicativos de 64 bits
Você pode depurar um aplicativo de 64 bits que está sendo executado no computador local ou em um computador remoto.

 Para depurar um aplicativo de 64 bits que está sendo executado em um computador remoto, consulte [depuração remota](../debugger/remote-debugging.md).

 Para depurar aplicativos de 64 bits localmente, o Visual Studio usa um processo de trabalho de 64 bits (msvsmon.exe) para executar as operações de nível baixo que não podem ser feitas dentro do processo do Visual Studio de 32 bits.

 Não há suporte para a depuração de modo misto em processos de 64 bits que usam .NET Framework versão 3,5 ou anterior.

## <a name="debug-a-64-bit-application"></a>Depurar um aplicativo de 64 bits
 Para tentar depurar um aplicativo de 64 bits:

1. Crie uma solução do Visual Studio, por exemplo, um aplicativo de console em C#.

2. Defina a configuração como 64 bits usando o Configuration Manager. Para obter mais informações, consulte [como: configurar projetos para plataformas de destino](../ide/how-to-configure-projects-to-target-platforms.md).

3. Neste ponto, a versão de 64 bits do depurador remoto (msvsmon.exe) é iniciada. Ele é executado contanto que a solução com a configuração de 64 bits esteja aberta.

4. Inicie a depuração. Você deve ter a mesma experiência que com uma configuração de 32 bits. Se você receber erros, consulte a seção solução de problemas abaixo.

## <a name="troubleshooting-64-bit-debugging"></a>Solução de problemas de depuração de 64 bits
 Você pode ver um erro: "uma operação de depuração de 64 bits está demorando mais do que o esperado". Nesse caso, o Visual Studio enviou uma solicitação para a versão de 64 bits do msvsmon.exe e levou muito tempo para que o resultado dessa solicitação volte.

 Há duas causas principais para esse erro:

- Você tem um software de segurança de rede instalado no seu computador que fez com que a pilha de rede não seja confiável e tenha descartado pacotes passando por localhost. Tente desabilitar todos os softwares de segurança de rede e ver se isso o resolve. Nesse caso, relate ao fornecedor do software de segurança de rede que o software está interferindo com o tráfego de localhost.

- Você está ficando com um problema de interrupção ou desempenho com o Visual Studio. Se o problema ocorrer regularmente, você poderá coletar despejos do Visual Studio (devenv.exe) e do processo de trabalho (msvsmon.exe) e enviá-los à Microsoft. Para obter informações sobre como relatar um problema, consulte [como relatar um problema com o Visual Studio](../ide/how-to-report-a-problem-with-visual-studio.md).

## <a name="see-also"></a>Veja também

- [Aplicativos de 64 bits](/dotnet/framework/64-bit-apps)
- [Configurando programas para 64 bits](/cpp/build/configuring-programs-for-64-bit-visual-cpp)
- [Visual Studio IDE 64-suporte de bit](../ide/visual-studio-ide-64-bit-support.md)
- [Usando arquivos de despejo](../debugger/using-dump-files.md)
- [Depuração remota](../debugger/remote-debugging.md)