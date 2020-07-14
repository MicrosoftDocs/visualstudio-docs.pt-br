---
title: 'CA1823: evitar campos particulares não utilizados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidUnusedPrivateFields
- CA1823
helpviewer_keywords:
- AvoidUnusedPrivateFields
- CA1823
ms.assetid: 614f94f6-0dc7-430f-8124-cb889a4a720f
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 01f2ef59ceb6d10cc33276fdd3e5388f39175f8b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545295"
---
# <a name="ca1823-avoid-unused-private-fields"></a>CA1823: Evitar campos particulares não utilizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidUnusedPrivateFields|
|CheckId|CA1823|
|Categoria|Microsoft. performance|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Essa regra é relatada quando um campo privado em seu código existe, mas não é usado por nenhum caminho de código.

## <a name="rule-description"></a>Descrição da Regra
 Foram detectados campos particulares que aparentemente não são acessados no assembly.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, remova o campo ou adicione o código que o utiliza.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra.

## <a name="related-rules"></a>Regras relacionadas
 [CA1812: Evitar classes internas sem instâncias](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

 [CA1801: Examinar parâmetros não utilizados](../code-quality/ca1801-review-unused-parameters.md)

 [CA1804: Remover locais não utilizados](../code-quality/ca1804-remove-unused-locals.md)

 [CA1811: Evitar código particular não chamado](../code-quality/ca1811-avoid-uncalled-private-code.md)
