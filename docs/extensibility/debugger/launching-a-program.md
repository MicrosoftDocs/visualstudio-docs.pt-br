---
title: Iniciar um programa | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, launching
- programs, launching
ms.assetid: 6857e9c6-e44a-468a-afa4-f7c4a0b77844
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4ab4432eed95fd042bd35d34b6a42d3cd036fcf2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49858362"
---
# <a name="launch-a-program"></a>Iniciar um programa
Os usuários que desejam depurar um programa podem pressionar **F5** para executar o depurador do IDE. Isso inicia uma série de eventos que resultam, por fim, o IDE com a conexão com um mecanismo de depuração (DE), que por sua vez conectado, ou anexado, o programa da seguinte maneira:  
  
1. O IDE primeiro chama o pacote do projeto para obter as configurações de depuração de projeto de ativo da solução. As configurações incluem o diretório inicial, as variáveis de ambiente, a porta na qual o programa será executado e o DE ser usado para criar o programa, se especificado. Essas configurações são passadas para o pacote de depuração.  
  
2. Se a DE for especificada, o DE chama o sistema operacional para iniciar o programa. Como consequência de iniciar o programa, o ambiente de tempo de execução do programa carrega. Por exemplo, se um programa é escrito em MSIL, o common language runtime será invocado para executar o programa.  
  
    -ou-  
  
    Se a DE não for especificada, a porta chama o sistema operacional para iniciar o programa, o que faz com que o ambiente de tempo de execução do programa carregar.  
  
   > [!NOTE]
   >  Se a DE é usada para iniciar um programa, é provável que o mesmo DE será anexado ao programa.  
  
3. Dependendo se a porta ou o DE iniciado o programa, o DE ou no ambiente de tempo de execução, em seguida, cria uma descrição do programa ou nó e notifica a porta que o programa está em execução.  
  
   > [!NOTE]
   >  É recomendável que o ambiente de tempo de execução criar o nó de programa, porque o nó do programa é uma representação leve de um programa que pode ser depurado. Não é necessário para carregar um inteiro DE apenas para criar e registrar um nó de programa. Se a Alemanha é projetada ser executado no processo do IDE, mas nenhum IDE está realmente em execução, é preciso haver um componente que pode adicionar um nó de programa para a porta.  
  
   O programa criado recentemente, juntamente com outros programas, relacionados ou não relacionados, iniciado ou anexados a partir do mesmo IDE, compor uma sessão de depuração.  
  
   Programaticamente, quando o usuário primeiro pressiona **F5**, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]do pacote de depuração chama o pacote do projeto (que é associado com o tipo de programa que está sendo iniciado) por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.DebugLaunch%2A> método, que por sua vez preenche um <xref:Microsoft.VisualStudio.Shell.Interop.VsDebugTargetInfo2> estrutura com configurações de depuração do projeto ativo da solução. Essa estrutura é passada de volta para o pacote de depuração por meio de uma chamada para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger2.LaunchDebugTargets2%2A> método. O pacote de depuração, em seguida, instancia o Gerenciador de depuração de sessão (SDM), que inicia o programa que está sendo mecanismos de depuração de qualquer associado e depurado.  
  
   Um dos argumentos passados para o SDM é o GUID da a ser usado para iniciar o programa.  
  
   Se o GUID DE não for `GUID_NULL`, o SDM cria conjunta DE e, em seguida, chama seus [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) método para iniciar o programa. Por exemplo, se um programa é escrito em código nativo, `IDebugEngineLaunch2::LaunchSuspended` provavelmente chamará `CreateProcess` e `ResumeThread` (funções do Win32) para executar o programa.  
  
   Como consequência de iniciar o programa, o ambiente de tempo de execução do programa é carregado. O DE ou o ambiente de tempo de execução, em seguida, cria uma [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) para descrever o programa de interface e passa essa interface para [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) para notificar a porta que o programa é em execução.  
  
   Se `GUID_NULL` for passado, a porta inicia o programa. Quando o programa estiver em execução, o ambiente de tempo de execução cria um `IDebugProgramNode2` para descrever o programa de interface e passa-o para `IDebugPortNotify2::AddProgramNode`. Isso notifica a porta que o programa está em execução. Em seguida, o SDM anexa o mecanismo de depuração para o programa em execução.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Notificar a porta](../../extensibility/debugger/notifying-the-port.md)  
 Explica o que acontece depois que um programa é iniciado e a porta é notificada.  
  
 [Anexar após uma inicialização](../../extensibility/debugger/attaching-after-a-launch.md)  
 Documentos quando a sessão de depuração estiver pronta para anexar o DE para o programa.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)  
 Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.