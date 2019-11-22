---
title: Opções de depuração dos serviços de nuvem do Azure | Microsoft Docs
description: Depurando serviços de nuvem do Azure
author: mikejo5000
manager: jillfra
ms.assetid: 80755da7-8350-4f5c-97ce-2962beabb36d
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 03/18/2017
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.openlocfilehash: c64ef6d998143aa7e20cbacc9a811fbabc8f332c
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74294161"
---
# <a name="learn-the-various-ways-to-debug-an-azure-cloud-service"></a>Conheça as várias maneiras de depurar um serviço de nuvem do Azure
Este artigo fornece links para as várias maneiras de depurar um serviço de nuvem do Azure. 

## <a name="debugging-an-azure-cloud-service-in-visual-studio"></a>Depurando um serviço de nuvem do Azure no Visual Studio
Você pode economizar tempo e dinheiro usando o emulador de computação para depurar o serviço de nuvem em um computador local. Ao depurar um serviço localmente antes de implantá-lo, você pode aprimorar a confiabilidade e o desempenho sem pagar pelo tempo de computação. No entanto, alguns erros podem ocorrer somente quando um serviço de nuvem é executado no Azure. Os erros que ocorrem apenas quando um serviço de nuvem é executado no Azure podem ser depurados com a habilitação da depuração remota ao publicar o serviço e, em seguida, com a anexação do depurador a uma instância de função. Para saber mais, consulte [Depurar o serviço de nuvem no computador local](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-your-cloud-service-on-your-local-computer)

## <a name="using-intellitrace"></a>Usando o IntelliTrace 
Se você estiver usando o Visual Studio Enterprise para escrever funções destinadas ao .NET Framework 4.5, poderá habilitar o IntelliTrace durante a implantação de um serviço de nuvem do Azure por meio do Visual Studio. O IntelliTrace fornece um log que você pode usar com o Visual Studio para depurar seu aplicativo, como se ele estivesse em execução no Azure. Para saber mais, consulte [Depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=623016).

## <a name="remote-debugging"></a>Depuração remota 
Você pode habilitar a depuração remota nos serviços de nuvem no momento em que implanta o serviço de nuvem usando o Visual Studio. Se você optar por habilitar a depuração remota para uma implantação, os serviços de depuração remota serão instalados nas máquinas virtuais que executam cada instância de função. Esses serviços – como `msvsmon.exe` – não afetam o desempenho nem resultam em custos extras. Para saber mais, consulte [Depurar o serviço de nuvem no Azure](vs-azure-tools-debug-cloud-services-virtual-machines.md#debug-a-cloud-service-in-azure)

## <a name="next-steps"></a>Próximas etapas
- [Depurando um serviço de nuvem ou uma VM do Azure no Visual Studio](./vs-azure-tools-debug-cloud-services-virtual-machines.md) – conheça os detalhes de como depurar serviços de nuvem do Azure.