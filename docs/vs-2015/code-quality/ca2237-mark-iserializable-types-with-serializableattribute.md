---
title: 'CA2237: marcar tipos ISerializable com SerializableAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2237
- MarkISerializableTypesWithSerializable
helpviewer_keywords:
- MarkISerializableTypesWithSerializable
- CA2237
ms.assetid: 9bd6bb24-a527-43dd-9952-043c0c694f46
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d8778b0bfa035c782cf35d205fc59d463112196c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545152"
---
# <a name="ca2237-mark-iserializable-types-with-serializableattribute"></a>CA2237: Marcar tipos ISerializable com SerializableAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkISerializableTypesWithSerializable|
|CheckId|CA2237|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo visível externamente implementa a <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface e o tipo não é marcado com o <xref:System.SerializableAttribute?displayProperty=fullName> atributo. A regra ignora tipos derivados cujo tipo base não é serializável.

## <a name="rule-description"></a>Descrição da Regra
 Para ser reconhecido pelo Common Language Runtime como serializável, os tipos devem ser marcados com o <xref:System.SerializableAttribute> atributo, mesmo que o tipo use uma rotina de serialização personalizada por meio da implementação da <xref:System.Runtime.Serialization.ISerializable> interface.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, aplique o <xref:System.SerializableAttribute> atributo ao tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso desta regra para classes de exceção porque elas devem ser serializáveis para funcionar corretamente entre domínios de aplicativo.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra. Remova a marca de comentário da <xref:System.SerializableAttribute> linha de atributo para atender à regra.

 [!code-csharp[FxCop.Usage.MarkSerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/cs/FxCop.Usage.MarkSerializable.cs#1)]
 [!code-vb[FxCop.Usage.MarkSerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.MarkSerializable/vb/FxCop.Usage.MarkSerializable.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2236: Chamar métodos da classe base em tipos ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240: Implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: Implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238: Implementar métodos de serialização corretamente](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235: Marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2239: Fornecer métodos de desserialização para campos opcionais](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120: Construtores de serialização seguros](../code-quality/ca2120-secure-serialization-constructors.md)
