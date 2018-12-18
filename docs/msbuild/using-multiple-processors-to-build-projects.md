---
title: Uso de vários processadores para criar projetos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- multiple processors
- MSBuild, multiple processor systems
ms.assetid: 49fa36c9-8e14-44f5-8a2b-34146cf6807b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ae7ff885ea7707ebe2f60001b265913856cbd125
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39177744"
---
# <a name="use-multiple-processors-to-build-projects"></a>Usar vários processadores para criar projetos
MSBuild pode tirar proveito dos sistemas com vários processadores ou vários núcleos processadores. Um processo de compilação separado é criado para cada processador disponível. Por exemplo, se o sistema possui quatro processadores, então quatro processos de compilação são criados. [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode processar essas compilações simultaneamente e, portanto, em geral o tempo de compilação é reduzido. No entanto, a construção em paralelo apresenta algumas alterações em como os processos de compilação ocorrem. Este tópico aborda essas alterações.  
  
## <a name="project-to-project-references"></a>Referências projeto a projeto  
 Quando o [!INCLUDE[vstecmsbuildengine](../msbuild/includes/vstecmsbuildengine_md.md)] encontra uma referência de projeto para projeto (P2P) enquanto ela está usando paralelo compilações para compilar um projeto, ele cria a referência de apenas uma vez. Se dois projetos tiverem a mesma referência P2P, a referência não é reconstruída para cada projeto. Em vez disso, o mecanismo de compilação retorna a mesma referência P2P para ambos os projetos que dependem dele. As solicitações futuras na sessão para o mesmo destino recebem a mesma referência P2P.  
  
## <a name="cycle-detection"></a>Detecção do ciclo  
 Ciclo de detecção funciona da mesma maneira que no [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 2.0, exceto que agora [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode relatar a detecção de ciclo em um momento diferente ou na compilação.  
  
## <a name="errors-and-exceptions-during-parallel-builds"></a>Erros e exceções durante compilações paralelas  
 Em compilações paralelas, erros e exceções podem ocorrer em momentos diferentes que fazem em uma compilação não paralelos e quando um projeto não será compilado, continuam as compilações do projeto. [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] não irá parar qualquer compilação do projeto que está criando em paralelo com aqueles que falharam. Outros projetos continuam a ser criados até que tenham êxito ou falha. No entanto, se <xref:Microsoft.Build.Framework.IBuildEngine.ContinueOnError%2A> foi habilitado, então nenhum build será interrompido, mesmo que ocorra um erro.  
  
## <a name="visual-c-project-vcproj-and-solution-sln-files"></a>Arquivos de projeto do Visual C++ (.vcproj) e de solução (.sln)  
 Ambos os arquivos de projetos [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] (*.vcproj*) e de solução (*.sln*) que podem ser passados para a [tarefa do MSBuild](../msbuild/msbuild-task.md). Para projetos [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)], VCWrapperProject é chamado e então o projeto [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] interno é criado. Para [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] soluções, um SolutionWrapperProject é criado e, em seguida, interno [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] projeto é criado. Em ambos os casos, o projeto resultante será tratado o mesmo que qualquer outro projeto do [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)].  
  
## <a name="multi-process-execution"></a>Execução multiprocesso  
 Quase todas as atividades relacionadas à compilação exigem o diretório atual para permanecer constante ao longo do processo de compilação para evitar erros de caminho. Portanto, projetos não podem ser executado em threads diferentes em [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] porque eles causaria vários diretórios a serem criados.  
  
 Para evitar esse problema, mas ainda permitir compilações para vários processadores, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] usa "isolamento de processo." Usando o isolamento do processo, [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] pode criar no máximo `n` processos, onde `n` é igual ao número de processadores disponíveis no sistema. Por exemplo, se [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] compilações uma solução em um sistema com dois processadores, e somente dois processos de compilação são criados. Novamente, esses processos são usados para criar todos os projetos na solução.  
  
## <a name="see-also"></a>Consulte também  
 [Compilar vários projetos paralelamente](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)