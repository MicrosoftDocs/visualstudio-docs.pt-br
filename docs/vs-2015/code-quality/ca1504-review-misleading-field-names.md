---
title: 'CA1504: revisar nomes de campo enganosos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- ReviewMisleadingFieldNames
- CA1504
helpviewer_keywords:
- CA1504
- ReviewMisleadingFieldNames
ms.assetid: 94136ff1-4aaf-4dc2-9170-48c171ab7499
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d375b64bbc877cb377157f13b3e4cfa7c7cf1592
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547869"
---
# <a name="ca1504-review-misleading-field-names"></a>CA1504: Examinar nomes de campo confusos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReviewMisleadingFieldNames|
|CheckId|CA1504|
|Categoria|Microsoft. Maintainabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 O nome de um campo de instância começa com "s_" ou o nome de `static` um `Shared` campo (in [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ) começa com "M_".

## <a name="rule-description"></a>Descrição da Regra
 Os nomes de campo que começam com "s_" são associados a dados estáticos por muitos usuários. Da mesma forma, os nomes de campo que começam com "m_" são associados a dados de instância (membro). Para um código mais fácil de ser mantido, os nomes devem seguir as convenções geralmente usadas.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, renomeie o campo usando o prefixo apropriado. Como alternativa, faça com que o campo concorde com o sufixo atual adicionando ou removendo o `static` modificador.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.
