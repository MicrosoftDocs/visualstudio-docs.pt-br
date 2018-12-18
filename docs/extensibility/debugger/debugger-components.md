---
title: Componentes do depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d3f79b9f22c2eb26b456e5e45c049a8f8bc04fae
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49818972"
---
# <a name="debugger-components"></a>Componentes do depurador
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador é implementado como um VSPackage e gerencia a sessão de depuração inteira. A sessão de depuração inclui os seguintes elementos:  
  
- **Pacote de depuração:** o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador fornece a mesma interface de usuário, não importa o que está sendo depurado.  
  
- **Gerenciador de sessão de depuração (SDM):** fornece uma interface de programação consistente para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador para o gerenciamento de uma variedade de mecanismos de depuração. Ela é implementada por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
- **Gerenciador de depuração do processo (PDM):** gerencia para todas as instâncias em execução [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], uma lista de todos os programas que podem ser ou estão sendo depurados. Ela é implementada por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
- **(DES) do mecanismo de depuração:** é responsável por monitorar um programa que está sendo depurado, comunicando-se o estado do programa em execução para o SDM e o PDM e interagir com o avaliador de expressão e o provedor de símbolo para fornecer análise em tempo real das estado da memória e variáveis de um programa. Ela é implementada por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (para os idiomas oferece suporte a ele) e fornecedores de terceiros que desejam dar suporte a seu próprio tempo de execução. 
  
- **O avaliador de expressão (EE):** fornece suporte para a avaliação dinâmica de variáveis e expressões fornecidas pelo usuário quando um programa foi interrompido em um ponto específico. Ela é implementada por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (para os idiomas oferece suporte a ele) e fornecedores de terceiros que desejam oferecer suporte a seus próprios idiomas.  
  
- **Provedor de símbolos (SP):** também chamado de um manipulador de símbolo, mapeia os símbolos de depuração de um programa para uma instância em execução do programa para que informações significativas podem ser fornecidas (por exemplo, avaliação de depuração e a expressão de nível de código-fonte). Ela é implementada por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (para o CLR Common Language Runtime [] símbolos e o banco de dados do programa [PDB] símbolo de formato de arquivo) e por fornecedores de terceiros que possuem seu próprio método proprietário de armazenar informações de depuração.  
  
  O diagrama a seguir mostra a relação entre esses elementos do depurador do Visual Studio.  
  
  ![Visão geral dos componentes de depuração](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")  
  
## <a name="in-this-section"></a>Nesta seção  
 [Pacote de depuração](../../extensibility/debugger/debug-package.md)  
 Discute o pacote de depuração, que é executado no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] de shell e manipula toda a interface do usuário.  
  
 [O Gerenciador de depuração do processo](../../extensibility/debugger/process-debug-manager.md)  
 Fornece uma visão geral dos recursos do PDM, que é o Gerenciador de processos que podem ser depurados.  
  
 [Gerenciador de sessão de depuração](../../extensibility/debugger/session-debug-manager.md)  
 Define o SDM, que fornece uma exibição unificada da sessão de depuração para o IDE. O SDM gerencia a Alemanha.  
  
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)  
 Documenta os serviços de depuração que o DE fornece.  
  
 [Modos operacionais](../../extensibility/debugger/operational-modes.md)  
 Fornece uma visão geral dos três modos em que o IDE pode operar: modo de interrupção, modo de execução e modo de design. Também são abordados os mecanismos de transição.  
  
 [Avaliador de expressão](../../extensibility/debugger/expression-evaluator.md)  
 Explica a finalidade de EE em tempo de execução.  
  
 [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md)  
 Discute como fazer isso, na implementação, o provedor de símbolo avalia expressões e variáveis.  
  
 [Visualizador de tipo e visualizador personalizado](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)  
 Discute o que são um visualizador de tipo e o visualizador personalizado e qual função o avaliador de expressão desempenha no suporte a ambos.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)  
 Descreve os principais conceitos de arquiteturas de depuração.  
  
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)  
 Explica como o DE simultaneamente opera dentro do código, documentação e contextos de avaliação de expressão. Descreve, para cada um dos três contextos, a localização, posição ou avaliação relevante a ele.  
  
 [As tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)  
 Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)