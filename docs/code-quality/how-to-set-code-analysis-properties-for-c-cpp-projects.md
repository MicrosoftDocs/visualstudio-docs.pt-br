---
title: Como definir propriedades de análise de código para projetos do C/C++
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.native
- VC.Project.VCCLCompilerTool.EnablePrefast
- VC.Project.VCFxCopTool.EnablePREfast
- VC.Project.VCFxCopTool.IgnoreGeneratedCode
helpviewer_keywords:
- properties, C/C++ Code Analysis
- properties, Code Analysis
- code analysis properties
- C/C++ code analysis properties
ms.assetid: 7af52097-6d44-4785-9b9f-43b7a7d447d7
author: mikeblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: f2800ce4784f5a8215dfe49b00194925c3cdb588
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31920671"
---
# <a name="how-to-set-code-analysis-properties-for-cc-projects"></a>Como definir propriedades de análise de código para projetos do C/C++
Você pode configurar quais regras usa a ferramenta de análise de código para analisar o código em cada configuração de seu projeto. Além disso, você pode direcionar a análise de código para suprimir avisos do código que foi gerado e adicionado ao seu projeto por uma ferramenta de terceiros.

## <a name="code-analysis-property-page"></a>Página de propriedades de análise de código
 O **análise de código** página de propriedades contém todas as definições de configuração de análise de código para um projeto. Para abrir a página de propriedades de análise de código para um projeto em **Solution Explorer**, clique com o botão direito e, em seguida, clique em **propriedades**. Em seguida, expanda **propriedades de configuração** e selecione o **análise de código** guia.

## <a name="project-configuration-and-platform"></a>Plataforma e a configuração de projeto
 O **configuração** lista e **plataforma** lista permite que você aplique as configurações de análise de código diferente para combinações de configuração e plataforma de projeto diferente. Por exemplo, você pode direcionar compilações de análise de código para aplicar um conjunto de regras ao seu projeto para depuração e cria um conjunto diferente de versão.

## <a name="enabling-code-analysis"></a>Habilitar análise de código
 Você pode decidir se deseja habilitar a análise de código para seu projeto selecionando **habilitar código análise para C/C++ na compilação**. Em combinação com o **configuração** lista, por exemplo, poderia optar por desabilitar análise de código para compilações de depuração e habilite-o para a versão cria.

 Se o seu projeto contém o código gerenciado, você pode decidir se deseja habilitar ou desabilitar análise de código selecionando **habilitar análise de código na compilação**.

 Análise de código foi projetada para ajudá-lo a melhorar a qualidade do seu código e evitar armadilhas comuns. Portanto, considere cuidadosamente se desativar a análise de código. Ele geralmente é melhor desabilitar conjuntos de regras ou regras individuais que você deseja não aplicadas ao seu projeto.

## <a name="generated-code"></a>Código gerado
 Os desenvolvedores usam frequentemente ferramentas para ajudar a desenvolver aplicativos rapidamente. Essas ferramentas podem gerar o código que é adicionado ao projeto. Deseja ver as violações de regra da análise de código descobre no código gerado. No entanto, não deseja vê-los se você não deseja manter o código.

 O **Suprimir resultados do código gerado** caixa de seleção de **geral** permite que você selecione se você deseja ver avisos da análise de código do código gerenciado que é gerado por uma ferramenta de terceiros de página de propriedades .

## <a name="rule-sets"></a>Conjuntos de regras
 Se o seu projeto contém o código gerenciado, você pode selecionar as regras a serem aplicadas em uma análise de código, selecionando uma conjunto de regras do **executar esse conjunto de regras** lista.

## <a name="see-also"></a>Consulte também
 [Analisando a qualidade do código gerenciado](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md) [de análise de código para avisos do C/C++](../code-quality/code-analysis-for-c-cpp-warnings.md)