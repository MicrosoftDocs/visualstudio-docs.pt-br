---
title: Problemas de segurança | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6807ea81d1898bfaf9c766e25e3c84c021c3aae5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799633"
---
# <a name="security-issues"></a>Problemas de segurança
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para depurar um programa usando o Visual Studio, as únicas permissões necessárias são as mesmas um desenvolvedor precisa para executar o programa. Isso inclui a depuração remota para a maioria das situações (algumas situações que envolvem a outros serviços, como o serviço de informações da Internet, podem exigir um nível mais alto de permissões).  
  
 Durante a execução do Visual Studio, o Gerenciador de depuração do processo (PDM) controla os processos de depuração no computador local. Remotamente, um programa chamado msvsmon.exe é iniciado pelo desenvolvedor para lidar com a depuração remota e disponibilize o PDM. (Observe que msvsmon.exe não é um serviço e deve ser iniciado manualmente para habilitar a depuração remota nesse computador). Quando o Visual Studio (ou msvsmon.exe) não está em execução, nenhum processo é rastreado para depuração.  
  
 Isso significa que um desenvolvedor pode depurar programas que ele ou ela iniciados com nenhuma permissão especial. O desenvolvedor pode até mesmo depurar processos iniciados por outra pessoa se outra pessoa que é um membro do mesmo grupo de segurança. E para habilitar a depuração remota, é necessário apenas a necessidade de copiar arquivos para o computador remoto de máquina em Iniciar msvsmon.exe (consulte [definir configurar as ferramentas remotas no dispositivo](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c) para obter mais detalhes).  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)   
 [O Gerenciador de depuração do processo](../../extensibility/debugger/process-debug-manager.md)   
 [Configurar as ferramentas remotas no dispositivo](http://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c)

