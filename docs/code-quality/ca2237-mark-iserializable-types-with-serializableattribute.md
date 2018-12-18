---
title: 'CA2237: marcar tipos ISerializable com SerializableAttribute'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2237
- MarkISerializableTypesWithSerializable
helpviewer_keywords:
- MarkISerializableTypesWithSerializable
- CA2237
ms.assetid: 9bd6bb24-a527-43dd-9952-043c0c694f46
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8629262da35b9897b789b2fae853bff4eea1aa8f
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551721"
---
# <a name="ca2237-mark-iserializable-types-with-serializableattribute"></a>CA2237: marcar tipos ISerializable com SerializableAttribute

|||
|-|-|
|NomeDoTipo|MarkISerializableTypesWithSerializable|
|CheckId|CA2237|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um tipo visível externamente implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface e o tipo não está marcado com o <xref:System.SerializableAttribute?displayProperty=fullName> atributo. A regra ignora os tipos derivados cujo tipo base não é serializável.

## <a name="rule-description"></a>Descrição da regra
 Para serem reconhecidos pelo common language runtime como serializáveis, os tipos devem ser marcados com o <xref:System.SerializableAttribute> mesmo se o tipo usa uma rotina de serialização personalizada por meio da implementação do atributo a <xref:System.Runtime.Serialization.ISerializable> interface.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, aplicar o <xref:System.SerializableAttribute> para o tipo de atributo.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra para classes de exceção, porque eles devem ser serializáveis para funcionar corretamente entre domínios de aplicativo.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra. Remova o <xref:System.SerializableAttribute> linha satisfazer a regra de atributo.

 [!code-vb[FxCop.Usage.MarkSerializable#1](../code-quality/codesnippet/VisualBasic/ca2237-mark-iserializable-types-with-serializableattribute_1.vb)]
 [!code-csharp[FxCop.Usage.MarkSerializable#1](../code-quality/codesnippet/CSharp/ca2237-mark-iserializable-types-with-serializableattribute_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2236: chamar métodos de classe base em tipos ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240: implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238: implementar métodos de serialização corretamente](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235: marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2239: fornecer métodos de desserialização para campos opcionais](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120: proteger construtores de serialização](../code-quality/ca2120-secure-serialization-constructors.md)