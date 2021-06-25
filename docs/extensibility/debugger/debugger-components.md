---
title: Componentes do depurador | Microsoft Docs
description: Saiba mais sobre os elementos que compõem uma sessão de depuração, que é gerenciada pelo depurador do Visual Studio, implementada como um VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debugging [Visual Studio], components
- components [Visual Studio SDK], debugging
- debugging [Debugging SDK], components
ms.assetid: 8b8ab77f-a134-495c-be42-3bc51aa62dfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8c246bc00ee4f6fcead8404b3174da39f7b5ca2d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903977"
---
# <a name="debugger-components"></a>Componentes do depurador
O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador é implementado como um VSPackage e gerencia toda a sessão de depuração. A sessão de depuração compreende os seguintes elementos:

- **Pacote de depuração:** O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador fornece a mesma interface do usuário, independentemente do que está sendo depurado.

- **SDM (Gerenciador de depuração de sessão):** Fornece uma interface programática consistente para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador para o gerenciamento de uma variedade de mecanismos de depuração. Ele é implementado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- **Gerenciador de depuração de processos (PDM):** Gerencia, para todas as instâncias em execução do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , uma lista de todos os programas que podem ser ou estão sendo depurados. Ele é implementado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

- **Mecanismo de depuração (de):** É responsável por monitorar um programa que está sendo depurado, comunicar o estado do programa em execução ao SDM e ao PDM e interagir com o avaliador de expressão e o provedor de símbolos para fornecer análise em tempo real do estado da memória e das variáveis de um programa. Ele é implementado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (para os idiomas com suporte) e por fornecedores de terceiros que desejam dar suporte ao seu próprio tempo de execução.

- **Avaliador de expressão (EE):** Fornece suporte para a avaliação dinâmica de variáveis e expressões fornecidas pelo usuário quando um programa é interrompido em um determinado ponto. Ele é implementado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (para os idiomas com suporte) e por fornecedores de terceiros que desejam oferecer suporte a seus próprios idiomas.

- **Provedor de símbolos (SP):** Também chamado de manipulador de símbolo, mapeia os símbolos de depuração de um programa para uma instância em execução do programa para que informações significativas possam ser fornecidas (como a depuração no nível de código-fonte e a avaliação de expressão). Ele é implementado pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] (para os símbolos CLR] e o formato de arquivo de símbolo do banco de dados do programa [PDB]) e por fornecedores de terceiros que têm seu próprio método proprietário de armazenar informações de depuração.

  O diagrama a seguir mostra a relação entre esses elementos do depurador do Visual Studio.

  ![Visão geral dos componentes de depuração](../../extensibility/debugger/media/dbugcompovrview.gif "DBugCompOvrview")

## <a name="in-this-section"></a>Nesta seção
 [Pacote de depuração](../../extensibility/debugger/debug-package.md) Discute o pacote de depuração, que é executado no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] shell e manipula toda a interface do usuário.

 [Gerenciador de depuração de processo](../../extensibility/debugger/process-debug-manager.md) Fornece uma visão geral dos recursos do PDM, que é o gerente dos processos que podem ser depurados.

 [Gerenciador de depuração de sessão](../../extensibility/debugger/session-debug-manager.md) Define o SDM, que fornece uma exibição unificada da sessão de depuração para o IDE. O SDM gerencia o DE.

 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md) Documenta os serviços de depuração que o DE fornece.

 [Modos operacionais](../../extensibility/debugger/operational-modes.md) Fornece uma visão geral dos três modos nos quais o IDE pode operar: modo de design, modo de execução e modo de interrupção. Mecanismos de transição também são discutidos.

 [Avaliador de expressão](../../extensibility/debugger/expression-evaluator.md) Explica a finalidade do EE em tempo de execução.

 [Provedor de símbolos](../../extensibility/debugger/symbol-provider.md) Discute como, na implementação, o provedor de símbolos avalia variáveis e expressões.

 [Visualizer de tipo e visualizador personalizado](../../extensibility/debugger/type-visualizer-and-custom-viewer.md) Discute o que é um visualizador de tipo e um visualizador personalizado e qual função o avaliador de expressão reproduz no suporte a ambos.

## <a name="related-sections"></a>Seções relacionadas
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md) Descreve os principais conceitos de arquitetura da depuração.

 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md) Explica como o DE Opera simultaneamente em código, documentação e contextos de avaliação de expressão. Descreve, para cada um dos três contextos, o local, a posição ou a avaliação relevante para ele.

 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md) Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.

## <a name="see-also"></a>Confira também
- [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)
