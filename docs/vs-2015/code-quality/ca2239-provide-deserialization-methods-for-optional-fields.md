---
title: 'CA2239: fornecer métodos de desserialização para campos opcionais | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2239
- ProvideDeserializationMethodsForOptionalFields
helpviewer_keywords:
- ProvideDeserializationMethodsForOptionalFields
- CA2239
ms.assetid: 6480ff5e-0caa-4707-814e-2f927cdafef5
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dfbb9082d557c8e67ddebf0237293364d54a65cf
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545126"
---
# <a name="ca2239-provide-deserialization-methods-for-optional-fields"></a>CA2239: Fornecer métodos de desserialização para campos opcionais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ProvideDeserializationMethodsForOptionalFields|
|CheckId|CA2239|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um tipo tem um campo marcado com o <xref:System.Runtime.Serialization.OptionalFieldAttribute?displayProperty=fullName> atributo e o tipo não fornece métodos de manipulação de eventos de eliminação de serialização.

## <a name="rule-description"></a>Descrição da Regra
 O <xref:System.Runtime.Serialization.OptionalFieldAttribute> atributo não tem nenhum efeito na serialização; um campo marcado com o atributo é serializado. No entanto, o campo é ignorado na desserialização e retém o valor padrão associado ao seu tipo. Manipuladores de eventos de serialização devem ser declarados para definir o campo durante o processo de desserialização.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione métodos de manipulação de eventos de desserialização ao tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o campo deve ser ignorado durante o processo de desserialização.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo com um campo opcional e métodos de manipulação de eventos de desserialização.

 [!code-csharp[FxCop.Usage.OptionalFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OptionalFields/cs/FxCop.Usage.OptionalFields.cs#1)]
 [!code-vb[FxCop.Usage.OptionalFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OptionalFields/vb/FxCop.Usage.OptionalFields.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2236: Chamar métodos da classe base em tipos ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240: Implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: Implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238: Implementar métodos de serialização corretamente](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235: Marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237: Marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2120: Construtores de serialização seguros](../code-quality/ca2120-secure-serialization-constructors.md)
