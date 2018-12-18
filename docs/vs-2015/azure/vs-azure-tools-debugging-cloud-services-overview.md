---
title: Serviços de nuvem de opções de depuração do Azure | Microsoft Docs
description: Depurando serviços de nuvem do Azure
author: mikejo5000
manager: douge
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/18/2017
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.openlocfilehash: bd2608371871b7adc925fc11927fe061b00a1ec6
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001301"
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a>Conheça as várias maneiras de depurar um serviço de nuvem do Azure
Este artigo fornece links para as várias maneiras para depurar um serviço de nuvem do Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Depuração de um serviço de nuvem do Azure no Visual Studio
Você pode economizar tempo e dinheiro usando o Azure compute emulator para depurar seu serviço de nuvem em um computador local. Ao depurar um serviço localmente antes de implantá-lo, você pode melhorar a confiabilidade e desempenho sem pagar pelo tempo de computação. No entanto, alguns erros podem ocorrer somente quando você executar um serviço de nuvem no Azure. Erros que ocorrem apenas quando você executa um serviço de nuvem no Azure podem ser depurados, habilitando a depuração remota quando você publica seu serviço e, em seguida, anexar o depurador a uma instância de função. Para obter mais informações, consulte [depurar seu serviço de nuvem em seu computador local](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer).

## <a name="using-intellitrace"></a>Usando o IntelliTrace 
Se você estiver usando o Visual Studio Enterprise para escrever funções destinadas ao .NET Framework 4.5, você pode habilitar o IntelliTrace no momento em que você implante um serviço de nuvem do Azure do Visual Studio. O IntelliTrace fornece um log que você pode usar com o Visual Studio para depurar seu aplicativo como se ele estivesse em execução no Azure. Para obter mais informações, consulte [depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Depuração remota 
Você pode habilitar a depuração remota em seus serviços de nuvem no momento, quando você implanta o serviço de nuvem do Visual Studio. Se você optar por habilitar a depuração remota para uma implantação, serviços de depuração remota serão instalados nas máquinas virtuais que executam cada instância de função. Esses serviços – como `msvsmon.exe` – não afetam o desempenho nem resultam em custos extras. Para obter mais informações, consulte [depurar um serviço de nuvem no Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure).

## <a name="next-steps"></a>Próximas etapas
- [Depurando um serviço de nuvem do Azure ou a VM no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) -Conheça os detalhes de como depurar serviços de nuvem do Azure.