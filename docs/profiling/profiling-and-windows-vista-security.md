---
title: Criação de perfil e segurança do Windows Vista | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,security
- performance tools, security
ms.assetid: 842112fc-b886-4801-8cd7-a25b314b0393
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ac83bc523b830c3e3adff258511d2785db0ddb62
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924792"
---
# <a name="profiling-and-windows-vista-security"></a>Criação de perfil e segurança do Windows Vista
Dependendo das configurações de Permissões de Acesso do Usuário do [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)] que um administrador de computador disponibilizou, um usuário individual pode ter a permissão de segurança para analisar um processo no computador. Os exemplos a seguir ilustram possíveis diferenças entre os usuários:  
  
- Alguns usuários podem acessar recursos de criação de perfil avançados quando o administrador tiver configurado o início do driver e do serviço.  
  
- Os usuários do domínio podem acessar apenas as amostras de criação de perfil.  
  
- Alguns usuários podem negar acesso à criação de perfil para todos os outros usuários.  
  
  Para obter mais informações, consulte as opções de ADMIN em [VSPerfCmd](../profiling/vsperfcmd.md).  
  
## <a name="cross-session-profiling"></a>Criação de perfil de sessão cruzada  
 *Criação de perfil de sessão cruzada* é a capacidade de analisar um processo que é executado em uma sessão de logon diferente. Por exemplo, a maioria dos serviços executados na sessão 0, os usuários não podem ser executados diretamente na sessão 0. Usando o botão **Anexar ao Processo** na barra de ferramentas do Gerenciador de Desempenho ou a opção /attach da ferramenta de linha de comando VSPerfCmd, você pode analisar a maioria dos processos em sessões de logon diferentes.  
  
 Você pode ver uma lista dos processos que estão disponíveis, definindo as opções de visibilidade de criação de perfil de processo cruzado. Essas opções estão disponíveis na janela **Anexar ao processo** que é exibida quando você clica em **Anexar ao Processo**:  
  
-   **Mostrar processos de todos os usuários**  
  
     Quando essa opção não estiver selecionada, a lista exibe apenas os processos pertencentes ao usuário atual. Quando **Mostrar processos de todos os usuários** é selecionado, a lista exibe os processos de todos os usuários.  
  
-   **Exibir processos em todas as sessões**  
  
     Quando essa opção não está selecionada, a lista exibe os processos na sessão atual. Quando essa opção está selecionada, a lista exibe os processos em todas as sessões.  
  
## <a name="see-also"></a>Consulte também  
 [Visões gerais](../profiling/overviews-performance-tools.md)   
 [VSPerfCmd](../profiling/vsperfcmd.md)   
 [Como anexar a um processo em execução](http://msdn.microsoft.com/en-us/636d0a52-4bfd-48d2-89ad-d7b9ca4dc4f4)