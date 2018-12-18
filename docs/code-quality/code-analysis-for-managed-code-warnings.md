---
title: Avisos da análise de código para código gerenciado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- vc.project.vcfxcoptool.enablefxcop
helpviewer_keywords:
- managed code analyis, warnings
- warnings, managed code analysis
- managed code analysis warnings
- code analysis,managed code
ms.assetid: 3c2741ff-0d3a-42e6-acd5-d42310bd03c4
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 600b5c7822232581cd01bd9bbf7616f4d1e9bb7c
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859062"
---
# <a name="code-analysis-for-managed-code-warnings"></a>Avisos da análise de código para código gerenciado
A ferramenta de análise de código gerenciado fornece avisos que indicam a violações de regra em bibliotecas de código gerenciado. Os avisos são organizados em áreas de regra, como design, localização, desempenho e segurança. Cada aviso significa que uma violação de uma regra de análise de código gerenciado. Esta seção fornece discussões detalhadas e exemplos de cada aviso de análise de código gerenciado.

 A tabela a seguir mostra o tipo de informação que é fornecido para cada aviso.

|Item|Descrição|
|----------|-----------------|
|Tipo|O TypeName para a regra.|
|CheckId|O identificador exclusivo para a regra. CheckId e categoria são usadas para supressão na origem de um aviso.|
|Categoria|A categoria do aviso.|
|Alteração Significativa|Se a correção para uma violação da regra é uma alteração significativa. Interrupção de alteração significa que um assembly que tem uma dependência no destino que causou a violação não irá recompilar com o novo fixa versão ou pode falhar em tempo de execução devido à alteração. Quando várias correções estão disponíveis e pelo menos uma correção é uma alteração significativa e uma correção não for, tanto 'Divisão' e 'Divisão não' são especificados.|
|Causa|O código gerenciado específico que faz com que a regra gerar um aviso.|
|Descrição|Discute os problemas que estão atrás de aviso.|
|Como Corrigir Violações|Explica como alterar o código-fonte para satisfazer a regra e impedir que ele gera um aviso.|
|Quando Suprimir Avisos|Descreve quando é seguro suprimir um aviso de regra.|
|Exemplo de código|Exemplos que violam a regra e corrigido exemplos que atendem à regra.|
|Avisos relacionados|Avisos relacionados.|

## <a name="in-this-section"></a>Nesta seção

|||
|-|-|
|[Avisos por CheckId](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)|Lista todos os avisos por CheckId|
|[Avisos de criptografia](../code-quality/cryptography-warnings.md)|Avisos que dão suporte a mais segura de bibliotecas e aplicativos por meio do uso correto da criptografia.|
|[Avisos de design](../code-quality/design-warnings.md)|Avisos que dão suporte ao design da biblioteca correta conforme especificado pelas diretrizes de Design do .NET Framework.|
|[Avisos de globalização](../code-quality/globalization-warnings.md)|Avisos que dão suporte a aplicativos e bibliotecas do mundo.|
|[Avisos de interoperabilidade](../code-quality/interoperability-warnings.md)|Avisos que dão suporte à interação com clientes COM.|
|[Avisos de facilidade de manutenção](../code-quality/maintainability-warnings.md)|Avisos que dão suporte à manutenção de biblioteca e o aplicativo.|
|[Avisos de mobilidade](../code-quality/mobility-warnings.md)|Avisos que dão suporte ao consumo de energia eficiente.|
|[Avisos de Nomenclatura](../code-quality/naming-warnings.md)|Avisos que dão suporte a conformidade com as convenções de nomenclatura de diretrizes de Design do .NET Framework.|
|[Avisos de desempenho](../code-quality/performance-warnings.md)|Avisos que dão suporte a aplicativos e bibliotecas de alto desempenho.|
|[Avisos de portabilidade](../code-quality/portability-warnings.md)|Avisos que dão suporte à portabilidade entre diferentes plataformas.|
|[Avisos de confiabilidade](../code-quality/reliability-warnings.md)|Avisos que dão suporte a confiabilidade de biblioteca e o aplicativo, como o uso de memória e thread corretos.|
|[Avisos de segurança](../code-quality/security-warnings.md)|Avisos que dão suporte a mais segura de bibliotecas e aplicativos.|
|[Avisos de Uso](../code-quality/usage-warnings.md)|Avisos que oferecem suporte ao uso apropriado do .NET Framework.|
|[Erros da política de análise de código](../code-quality/code-analysis-policy-errors.md)|Erros que ocorrem se a política de análise de código não for atendida no check-in.|