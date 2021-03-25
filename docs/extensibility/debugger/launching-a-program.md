---
title: Iniciando um programa | Microsoft Docs
description: Saiba mais sobre a série de eventos que ocorrem quando você depura um programa usando F5 para executar o depurador a partir do IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- programs, launching
ms.assetid: 6857e9c6-e44a-468a-afa4-f7c4a0b77844
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a21036d3a9661306d1efff5a66ae47f8f7404209
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094712"
---
# <a name="launch-a-program"></a>Iniciar um programa
Os usuários que desejam depurar um programa podem pressionar **F5** para executar o depurador do IDE. Isso inicia uma série de eventos que, por fim, resultam na conexão do IDE com um mecanismo DE depuração (DE), que, por sua vez, está conectado, ou anexado, ao programa da seguinte maneira:

1. O IDE primeiro chama o pacote de projeto para obter as configurações de depuração de projeto ativo da solução. As configurações incluem o diretório inicial, as variáveis de ambiente, a porta na qual o programa será executado e o DE usar para criar o programa, se especificado. Essas configurações são passadas para o pacote de depuração.

2. Se um DE for especificado, o DE chamará o sistema operacional para iniciar o programa. Como consequência de iniciar o programa, o ambiente de tempo de execução do programa é carregado. Por exemplo, se um programa for escrito em MSIL, o Common Language Runtime será invocado para executar o programa.

    – ou –

    Se um DE não for especificado, a porta chamará o sistema operacional para iniciar o programa, o que faz com que o ambiente de tempo de execução do programa seja carregado.

   > [!NOTE]
   > Se um DE for usado para iniciar um programa, é provável que o mesmo DE será anexado ao programa.

3. Dependendo se a porta DE ou a que iniciou o programa, o DE ou o ambiente de tempo DE execução cria uma descrição do programa, ou nó, e notifica a porta que o programa está em execução.

   > [!NOTE]
   > É recomendável que o ambiente de tempo de execução crie o nó do programa, pois o nó do programa é uma representação leve de um programa que pode ser depurado. Não há necessidade de carregar um inteiro DE apenas para criar e registrar um nó de programa. Se o DE for projetado para ser executado no processo do IDE, mas nenhum IDE estiver realmente em execução, precisará ser um componente que pode adicionar um nó de programa à porta.

   O programa recém-criado, junto com quaisquer outros programas, relacionados ou não relacionados, iniciados ou anexados a partir do mesmo IDE, compõem uma sessão de depuração.

   Programaticamente, quando o usuário pressiona primeiro **F5**, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] pacote de depuração do chama o pacote do projeto (que está associado ao tipo de programa que está sendo iniciado) por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> método, que, por sua vez, preenche uma <xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2> estrutura com as configurações de depuração de projeto ativo da solução. Essa estrutura é passada de volta para o pacote de depuração por meio de uma chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A> método. Em seguida, o pacote de depuração instancia o SDM (Gerenciador de depuração de sessão), que inicia o programa que está sendo depurado e todos os mecanismos de depuração associados.

   Um dos argumentos passados para o SDM é o GUID do DE a ser usado para iniciar o programa.

   Se o DE GUID não for `GUID_NULL` , o SDM cocriará o de e, em seguida, chamará seu método [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) para iniciar o programa. Por exemplo, se um programa for escrito em código nativo, `IDebugEngineLaunch2::LaunchSuspended` provavelmente ele chamará `CreateProcess` e `ResumeThread` (funções do Win32) para executar o programa.

   Como consequência de iniciar o programa, o ambiente de tempo de execução do programa é carregado. O ou o ambiente DE tempo DE execução cria uma interface [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) para descrever o programa e passa essa interface para [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) para notificar a porta que o programa está em execução.

   Se `GUID_NULL` for passado, a porta iniciará o programa. Depois que o programa estiver em execução, o ambiente de tempo de execução criará uma `IDebugProgramNode2` interface para descrever o programa e passá-lo para `IDebugPortNotify2::AddProgramNode` . Isso notifica a porta de que o programa está em execução. Em seguida, o SDM anexa o mecanismo de depuração ao programa em execução.

## <a name="in-this-section"></a>Nesta seção
 [Notificando a porta](../../extensibility/debugger/notifying-the-port.md) Explica o que acontece depois que um programa é iniciado e a porta é notificada.

 [Anexando após uma inicialização](../../extensibility/debugger/attaching-after-a-launch.md) Documentos quando a sessão de depuração estiver pronta para anexar o DE ao programa.

## <a name="related-sections"></a>Seções relacionadas
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md) Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.
