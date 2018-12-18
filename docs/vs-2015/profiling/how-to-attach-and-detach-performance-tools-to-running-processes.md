---
title: Como anexar e desanexar ferramentas de desempenho de processos em execução | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.performance.attach
helpviewer_keywords:
- performance tools, attach process
- profiling tools, detach process
- profiling tools, attach process
- performance tools, detach process
- profiler
ms.assetid: 56a99c39-e7f6-4f48-ae56-04ab8e022bf7
caps.latest.revision: 35
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 931608decb44f0e49cb4ae2984b9cbf724a63d56
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51778235"
---
# <a name="how-to-attach-and-detach-performance-tools-to-running-processes"></a>Como anexar e desanexar ferramentas de desempenho de processos em execução
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O criador de perfil pode ser usado para anexar ou desanexar de um processo em execução para facilitar a amostragem e a coleta de dados de desempenho. É possível usar esse método para criar o perfil de um processo quando você deseja evitar a coleta de dados sobre o tempo de carregamento do aplicativo ou para monitorar o desempenho de um processo após ele atingir um estado específico.  
  
> [!NOTE]
>  As etapas a seguir se aplicam aos processos de anexar e desanexar de dentro do IDE (ambiente de desenvolvimento integrado) do [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]. Para obter informações sobre como usar ferramentas de linha de comando, consulte [Criação de perfil da linha de comando](../profiling/using-the-profiling-tools-from-the-command-line.md). Para obter informações sobre como criar o perfil de serviços, consulte [Criando o perfil de serviços](../profiling/command-line-profiling-of-services.md).  
  
 Os processos que estão disponíveis para criação de perfil dependem das Permissões de acesso do usuário definidas por um administrador do computador. Uma conta de usuário pode, por exemplo, ter permissão para qualquer um dos seguintes:  
  
- Recursos avançados de criação de perfil, quando o administrador tiver configurado o início do driver e do serviço.  
  
- Criação de perfil de amostra apenas (usuários de domínio).  
  
- Acesso negado à criação de perfil para todos.  
  
  Para obter mais informações, consulte [Criação de perfil e segurança do Windows Vista](../profiling/profiling-and-windows-vista-security.md) e as opções de administração em [VSPerfCmd](../profiling/vsperfcmd.md).  
  
### <a name="to-attach-to-a-running-process"></a>Para anexar a um processo em execução  
  
1.  No menu **Analisar**, aponte para **Criador de Perfil** e clique em **Anexar/Desanexar**.  
  
     \- ou -  
  
     No **Gerenciador de Desempenho**, clique com o botão direito do mouse na sessão de desempenho e, em seguida, clique em **Anexar/Desanexar**.  
  
     É exibida a caixa de diálogo **Anexar Criador de Perfil a Processo**.  
  
2.  Clique no nome do processo ao qual deseja anexar.  
  
3.  Clique em **Anexar**.  
  
### <a name="to-detach-from-a-running-process"></a>Para desanexar de um processo em execução  
  
1.  No menu **Analisar**, aponte para **Criador de Perfil** e clique em **Anexar/Desanexar**.  
  
     \- ou -  
  
     No **Gerenciador de Desempenho**, clique com o botão direito do mouse na sessão de desempenho e, em seguida, clique em **Anexar/Desanexar**.  
  
     É exibida a caixa de diálogo **Anexar Criador de Perfil a Processo**.  
  
2.  Clique no nome da imagem da qual deseja desanexar.  
  
3.  Clique em **Desanexar**.  
  
## <a name="see-also"></a>Consulte também  
 [Controlling Data Collection](../profiling/controlling-data-collection.md)  (Controlando a coleta de dados)  
 [Visão geral da sessão de desempenho](../profiling/performance-session-overview.md)   
 [Como iniciar e encerrar a coleta de dados de desempenho](../profiling/how-to-start-and-end-performance-data-collection.md)   
 [Criação de perfil e segurança do Windows Vista](../profiling/profiling-and-windows-vista-security.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)



