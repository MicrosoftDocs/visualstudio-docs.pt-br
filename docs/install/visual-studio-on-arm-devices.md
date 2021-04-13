---
title: Visual Studio em dispositivos equipados com ARM
description: Recomendações para usar o Visual Studio em dispositivos com processadores baseados em ARM.
ms.date: 09/10/2020
ms.topic: conceptual
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 31fb209a3f19c052c19e98691b8643bb098887ee
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107295800"
---
# <a name="visual-studio-on-arm-powered-devices"></a>Visual Studio em dispositivos com tecnologia ARM

> [!IMPORTANT]
> Só há suporte para o Visual Studio em dispositivos que usam um processador baseado em x86 ou AMD64/x64.

O Visual Studio foi criado para direcionar processadores com base na arquitetura x86 e não há versões do Visual Studio para processadores baseados em ARM. No entanto, o Windows fornece [emulação x86 no ARM](https://www.docs.microsoft.com/windows/uwp/porting/apps-on-arm-x86-emulation), que pode ser executado pelo Visual Studio. Executar o Visual Studio em um processador ARM por meio da emulação x86 prejudica seriamente o desempenho do Visual Studio, e vários recursos do Visual Studio não são projetados para funcionar nesse cenário. Como tal, não recomendamos a execução do Visual Studio em dispositivos que usam processadores baseados em ARM e, em vez disso, recomendam dispositivos ARM de destino remoto.

## <a name="remote-targeting-arm-devices"></a>Dispositivos ARM de direcionamento remoto
Para obter a melhor experiência, recomendamos que você use o Visual Studio em um computador com x86 e separado, e use os recursos de implantação remota e depuração no Visual Studio para direcionar o dispositivo baseado em ARM. Para depurar aplicativos Windows universal já instalados no dispositivo, consulte a documentação [depurar pacote do aplicativo instalado](../debugger/debug-installed-app-package.md) . Para implantar um novo aplicativo, consulte [executando um aplicativo da Windows Store remotley](../debugger/run-windows-store-apps-on-a-remote-machine.md). Para todos os outros tipos de aplicativos, consulte a documentação de [depuração remota](../debugger/remote-debugging.md) .

## <a name="tips-for-running-visual-studio-on-arm-devices"></a>Dicas para executar o Visual Studio em dispositivos ARM

### <a name="use-only-when-needed"></a>Usar somente quando necessário
Otimize seu tempo usando o Visual Studio somente quando necessário para o trabalho específico do ARM. O desempenho em qualquer dispositivo com tecnologia ARM será ruim, e você provavelmente achará inaceitável para uso regular.

### <a name="install-time"></a>Hora da instalação
Planeje o Visual Studio para que demore mais para instalar e espere que ele seja pausado por períodos de tempo ou exija a reinicialização.
 
### <a name="remote-tools"></a>Ferramentas remotas
Para depurar um aplicativo em execução em um dispositivo remoto, você precisará [baixar e instalar as ferramentas remotas para o](../debugger/remote-debugging.md#download-and-install-the-remote-tools) ARM.

### <a name="start-debugging-f5"></a>{1&gt;Iniciar a depuração (F5)&lt;1}
Nem todos os projetos do Visual Studio estão configurados para iniciar projetos localmente quando você inicia a depuração (**F5**) de um dispositivo ARM. Talvez seja necessário configurar o Visual Studio para depuração remota, embora seu aplicativo esteja sendo executado localmente. Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).

## <a name="we-need-your-help"></a>Precisamos de sua ajuda!
Se você quiser que o Visual Studio seja executado nativamente em dispositivos ARM, adoraríamos saber mais sobre os cenários e o suporte necessário. Você pode contatá-los postando na [comunidade de desenvolvedores](https://developercommunity.visualstudio.com/idea/1161018/native-arm-support-for-visual-studio.html).
