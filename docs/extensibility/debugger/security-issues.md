---
title: Problemas de segurança | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6cd4d07721f202169ca0689882ac1a41045a4d61
ms.sourcegitcommit: 71b307ce86c4079cc7ad686d8d5f96a6a123aadd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2018
ms.locfileid: "39252317"
---
# <a name="security-issues"></a>Problemas de segurança
Para depurar um programa usando o Visual Studio, as únicas permissões necessárias são as mesmas exige que um desenvolvedor para executar o programa. Isso inclui a depuração remota para a maioria das situações. Algumas situações que envolvem a outros serviços, como o serviço de informações da Internet, podem exigir um nível mais alto de permissões.  
  
 Durante a execução do Visual Studio, o Gerenciador de depuração do processo (PDM) controla os processos de depuração no computador local. Remotamente, um programa chamado *msvsmon.exe* é iniciado pelo desenvolvedor para lidar com a depuração remota e disponibilize o PDM. (*msvsmon.exe* não é um serviço e deve ser iniciado manualmente para habilitar a depuração remota nesse computador.) Quando o Visual Studio (ou *msvsmon.exe*) é não em execução, não há processos são rastreados para depuração.  
  
 Um desenvolvedor pode depurar programas que eles começaram com nenhuma permissão especial. O desenvolvedor pode até mesmo depurar processos iniciados por outra pessoa se outra pessoa que é um membro do mesmo grupo de segurança. E, para habilitar a depuração remota, é necessário apenas copiar os arquivos necessários para o computador remoto e iniciar *msvsmon.exe*. Para obter mais informações, consulte [depuração remota](../../debugger/remote-debugging.md).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)   
 [O Gerenciador de depuração do processo](../../extensibility/debugger/process-debug-manager.md)   
 [Depuração remota](../../debugger/remote-debugging.md)
