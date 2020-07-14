---
title: 'CA2211: campos não constantes não devem ser visíveis | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2211
- NonConstantFieldsShouldNotBeVisible
helpviewer_keywords:
- NonConstantFieldsShouldNotBeVisible
- CA2211
ms.assetid: e1e42c40-0acd-4312-af29-70133739a304
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: aa67c33eac5d618c0a080323720775beea7b68c3
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548207"
---
# <a name="ca2211-non-constant-fields-should-not-be-visible"></a>CA2211: Campos não constantes não devem ser visíveis
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|NonConstantFieldsShouldNotBeVisible|
|CheckId|CA2211|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um campo estático ou público protegido não é constante nem é somente leitura.

## <a name="rule-description"></a>Descrição da Regra
 Os campos estáticos que não são constantes nem somente leitura não são thread-safe. O acesso a esse campo deve ser cuidadosamente controlado e requer técnicas de programação avançadas para sincronizar o acesso ao objeto de classe. Como essas são habilidades difíceis de aprender e dominar e testar tal objeto representa seus próprios desafios, os campos estáticos são mais bem usados para armazenar dados que não são alterados. Esta regra se aplica a bibliotecas; os aplicativos não devem expor nenhum campo.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, torne a constante de campo estático ou somente leitura. Se isso não for possível, recrie o tipo para usar um mecanismo alternativo, como uma propriedade thread-safe, que gerencia o acesso seguro ao thread para o campo subjacente. Perceba que problemas como contenção de bloqueio e deadlocks podem afetar o desempenho e o comportamento da biblioteca.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se você estiver desenvolvendo um aplicativo e, portanto, tiver controle total sobre o acesso ao tipo que contém o campo estático. Os designers de biblioteca não devem suprimir um aviso dessa regra; o uso de campos estáticos não constantes pode tornar o uso da biblioteca difícil para os desenvolvedores usarem corretamente.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola essa regra.

 [!code-csharp[FxCop.Usage.AvoidStaticNonConstants#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.AvoidStaticNonConstants/cs/FxCop.Usage.AvoidStaticNonConstants.cs#1)]
 [!code-vb[FxCop.Usage.AvoidStaticNonConstants#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.AvoidStaticNonConstants/vb/FxCop.Usage.AvoidStaticNonConstants.vb#1)]
