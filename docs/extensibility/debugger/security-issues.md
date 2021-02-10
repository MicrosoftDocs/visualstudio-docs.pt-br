---
title: Problemas de segurança | Microsoft Docs
description: Saiba mais sobre as permissões necessárias para depurar um programa usando o Visual Studio, incluindo depuração remota e situações que envolvem outros serviços.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- security [Debugging SDK]
- debugging [Debugging SDK], security
ms.assetid: d6ffff0a-afb4-4f38-86d8-476c881c4e4b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7e7b834dc41fb019e70aa40bca995770985d4c05
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99960917"
---
# <a name="security-issues"></a>Problemas de segurança
Para depurar um programa usando o Visual Studio, as únicas permissões necessárias são as mesmas que um desenvolvedor requer para executar o programa. Isso inclui a depuração remota na maioria das situações. Algumas situações, envolvendo outros serviços, como o serviço de informações da Internet, podem exigir um nível mais alto de permissões.

 Enquanto o Visual Studio está em execução, o Gerenciador de depuração de processos (PDM) rastreia os processos de depuração no computador local. Remotamente, um programa chamado *msvsmon.exe* é iniciado pelo desenvolvedor para manipular a depuração remota e tornar o PDM disponível. (*msvsmon.exe* não é um serviço e deve ser iniciado manualmente para habilitar a depuração remota nesse computador.) Quando o Visual Studio (ou *msvsmon.exe*) não está em execução, nenhum processo é acompanhado para depuração.

 Um desenvolvedor pode depurar programas iniciados sem permissões especiais. O desenvolvedor pode até mesmo depurar processos iniciados por outra pessoa se esse outro for membro do mesmo grupo de segurança. E, para habilitar a depuração remota, é necessário apenas copiar os arquivos necessários para o computador remoto e iniciar o *msvsmon.exe*. Para obter mais informações, consulte [depuração remota](../../debugger/remote-debugging.md).

## <a name="see-also"></a>Confira também
- [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)
- [Gerenciador de depuração de processo](../../extensibility/debugger/process-debug-manager.md)
- [Depuração remota](../../debugger/remote-debugging.md)
