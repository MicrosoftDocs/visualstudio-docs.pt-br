---
title: Análise de código para visão geral do C/C++
ms.date: 04/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- annotations, code analysis
- build integration, code analysis
- C/C++ code analysis
- IDE, code analysis
- pragma directive, code analysis
- code analysis, C/C++
- code analysis tool
- command line, code analysis
- C++, code analysis
- check-in policies, code analysis
- '#pragma directives, code analysis'
- C, code analysis
ms.assetid: 81f0c9e8-f471-4de5-aac4-99db336a8809
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: 35f694d9cc397800249dd9b4acd86bf63d22ad93
ms.sourcegitcommit: 28909340cd0a0d7cb5e1fd29cbd37e726d832631
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44320703"
---
# <a name="code-analysis-for-cc-overview"></a>Análise de código para visão geral do C/C++

A ferramenta de análise de código C/C++ fornece informações sobre possíveis defeitos no seu código-fonte C/C++. Entre os erros de codificação comuns reportados pela ferramenta estão estouros de buffer, memória não inicializada, desreferências de ponteiro nulo, memória e perdas de recurso. A ferramenta também pode executar verificações em relação a [diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md).

## <a name="ide-integrated-development-environment-integration"></a>Integração de IDE (ambiente de desenvolvimento integrado)

A ferramenta de análise de código é totalmente integrada dentro do IDE do Visual Studio.

Durante o processo de compilação, todos os avisos gerados para o código-fonte aparecem na lista de erros. Você pode navegar para o código-fonte que causou o aviso, e você pode exibir informações adicionais sobre a causa e possíveis soluções do problema.

## <a name="command-line-support"></a>Suporte de linha de comando

Você também pode usar a ferramenta de análise da linha de comando, conforme mostrado no exemplo a seguir:

```cmd
C:\>cl /analyze Sample.cpp
```

**Visual Studio 2017 versão 15.7 e posterior** você pode executar a ferramenta da linha de comando com qualquer sistema de compilação, incluindo o CMake.

## <a name="pragma-support"></a>suporte de #pragma

Você pode usar o `#pragma` diretiva para tratar avisos como erros; ativar ou desativar avisos e suprimir avisos para linhas individuais de código. Para obter mais informações, consulte [como: definir propriedades de análise de código para projetos C/C++](how-to-set-code-analysis-properties-for-c-cpp-projects.md).

## <a name="annotation-support"></a>Suporte de anotação

Anotações de melhorar a precisão da análise de código. Anotações fornecem informações adicionais sobre condições pré e pós-nos parâmetros de função e tipos de retorno. Para obter mais informações, consulte [como: especificar informações de código adicionais usando analysis_assume](../code-quality/how-to-specify-additional-code-information-by-using-analysis-assume.md)

## <a name="run-analysis-tool-as-part-of-check-in-policy"></a>Execute a ferramenta de análise como parte da política de check-in

Talvez você queira exigem que o código de origem todos os check-ins satisfaçam determinadas políticas. Em particular, convém certificar-se de que a análise foi executada como uma etapa de compilação local mais recente. Para obter mais informações sobre como habilitar uma política de check-in do análise código, consulte [criando e usando análise de código de Check-In políticas](../code-quality/creating-and-using-code-analysis-check-in-policies.md)

## <a name="team-build-integration"></a>Integração do Team Build

Você pode usar os recursos integrados do sistema de compilação para executar a ferramenta de análise de código como uma etapa do [!INCLUDE[esprtfs](../code-quality/includes/esprtfs_md.md)] processo de compilação. Para obter mais informações, consulte [Pipelines do Azure](/azure/devops/pipelines/index?view=vsts).

## <a name="see-also"></a>Consulte também

- [Guia de início rápido: Análise de código para C/C++](quick-start-code-analysis-for-c-cpp.md)
- [Passo a passo: Analisar o código C/C++ em busca de defeitos](walkthrough-analyzing-c-cpp-code-for-defects.md)
- [Análise de código para avisos do C/C++](code-analysis-for-c-cpp-warnings.md)
- [Usar os verificadores de diretrizes de núcleo do C++](using-the-cpp-core-guidelines-checkers.md)
- [Referência de verificador das diretrizes principais do C++](code-analysis-for-cpp-corecheck.md)
- [Usar conjuntos de regras para especificar as regras do C++ para execução](using-rule-sets-to-specify-the-cpp-rules-to-run.md)
- [Analisar a qualidade do Driver usando as ferramentas de análise de código](/windows-hardware/drivers/develop/analyzing-driver-quality-by-using-code-analysis-tools)
- [Análise de código para avisos de Drivers](/windows-hardware/drivers/devtest/prefast-for-drivers-warnings)
