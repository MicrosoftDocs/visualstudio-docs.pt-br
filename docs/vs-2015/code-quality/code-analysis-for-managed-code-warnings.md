---
title: Análise de código para avisos de código gerenciado | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vc.project.vcfxcoptool.enablefxcop
helpviewer_keywords:
- managed code analyis, warnings
- warnings, managed code analysis
- managed code analysis warnings
- code analysis,managed code
ms.assetid: 3c2741ff-0d3a-42e6-acd5-d42310bd03c4
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 5294840e4669f28f4e8a04978274ad130d1397ee
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85535727"
---
# <a name="code-analysis-for-managed-code-warnings"></a>Avisos da análise de código para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta de análise de código gerenciado fornece avisos que indicam violações de regra em bibliotecas de código gerenciado. Os avisos são organizados em áreas de regras, como design, localização, desempenho e segurança. Cada aviso significa uma violação de uma regra de análise de código gerenciado. Esta seção fornece discussões detalhadas e exemplos para cada aviso de análise de código gerenciado.

 A tabela a seguir mostra o tipo de informações que são fornecidas para cada aviso.

|Item|Descrição|
|----------|-----------------|
|Type|O TypeName da regra.|
|CheckId|O identificador exclusivo da regra. O CheckId e a categoria são usados para a supressão na origem de um aviso.|
|Categoria|A categoria do aviso.|
|Alteração Significativa|Se a correção de uma violação da regra é uma alteração significativa. Alteração significativa significa que um assembly que tem uma dependência no destino que causou a violação não será recompilado com a nova versão fixa ou pode falhar em tempo de execução devido à alteração. Quando há várias correções disponíveis e pelo menos uma correção é uma alteração significativa e uma correção não é especificada, ' quebra ' e ' não separável ' são especificados.|
|Causa|O código gerenciado específico que faz com que a regra gere um aviso.|
|Descrição|Discute os problemas que estão por trás do aviso.|
|Como Corrigir Violações|Explica como alterar o código-fonte para satisfazer a regra e impedir que ela gere um aviso.|
|Quando Suprimir Avisos|Descreve quando é seguro suprimir um aviso da regra.|
|Código de exemplo|Exemplos que violam a regra e exemplos corrigidos que satisfazem a regra.|
|Avisos relacionados|Avisos relacionados.|

## <a name="in-this-section"></a>Nesta seção

|Item|Valor|
|-|-|
|[Avisos por CheckId](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)|Lista todos os avisos por CheckId|
|[Avisos de criptografia](../code-quality/cryptography-warnings.md)|Avisos que dão suporte a bibliotecas e aplicativos mais seguros por meio do uso correto de criptografia.|
|[Avisos de design](../code-quality/design-warnings.md)|Avisos que dão suporte ao design de biblioteca correto conforme especificado pelas [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] diretrizes de design.|
|[Avisos de globalização](../code-quality/globalization-warnings.md)|Avisos que dão suporte a bibliotecas e aplicativos preparados para o mundo.|
|[Avisos de interoperabilidade](../code-quality/interoperability-warnings.md)|Avisos que dão suporte à interação com clientes COM.|
|[Avisos de manutenção](../code-quality/maintainability-warnings.md)|Avisos que dão suporte à manutenção da biblioteca e do aplicativo.|
|[Avisos de mobilidade](../code-quality/mobility-warnings.md)|Avisos que dão suporte ao uso de energia eficiente.|
|[Avisos de nomenclatura](../code-quality/naming-warnings.md)|Avisos que dão suporte à adesão às convenções de nomenclatura das [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] diretrizes de design.|
|[Avisos de desempenho](../code-quality/performance-warnings.md)|Avisos que dão suporte a bibliotecas e aplicativos de alto desempenho.|
|[Avisos de portabilidade](../code-quality/portability-warnings.md)|Avisos que dão suporte à portabilidade em diferentes plataformas.|
|[Avisos de confiabilidade](../code-quality/reliability-warnings.md)|Avisos que dão suporte à confiabilidade de biblioteca e aplicativo, como a memória correta e o uso de thread.|
|[Avisos de segurança](../code-quality/security-warnings.md)|Avisos que dão suporte a bibliotecas e aplicativos mais seguros.|
|[Avisos de uso](../code-quality/usage-warnings.md)|Avisos que dão suporte ao uso apropriado do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] .|
|[Erros de política de análise de código](../code-quality/code-analysis-policy-errors.md)|Erros que ocorrem se a política de análise de código não for satisfeita no check-in.|
