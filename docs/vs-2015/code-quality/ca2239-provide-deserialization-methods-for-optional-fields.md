---
title: 'CA2239: Fornecer métodos de desserialização para campos opcionais | Microsoft Docs'
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5bfb682e3b2220a6eb68e7f225e147b8106c3e7c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201522"
---
# <a name="ca2239-provide-deserialization-methods-for-optional-fields"></a>CA2239: Fornecer métodos de desserialização para campos opcionais
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ProvideDeserializationMethodsForOptionalFields|
|CheckId|CA2239|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um tipo tem um campo que é marcado com o <xref:System.Runtime.Serialization.OptionalFieldAttribute?displayProperty=fullName> atributo e o tipo não fornece métodos de manipulação de eventos de desserialização.

## <a name="rule-description"></a>Descrição da Regra
 O <xref:System.Runtime.Serialization.OptionalFieldAttribute> atributo não tem nenhum efeito na serialização; um campo marcado com o atributo é serializado. No entanto, o campo é ignorado na desserialização e retém o valor padrão associado com seu tipo. Manipuladores de eventos de desserialização devem ser declarados para definir o campo durante o processo de desserialização.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione métodos para o tipo de manipulação de evento de desserialização.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o campo deve ser ignorado durante o processo de desserialização.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra métodos de manipulação de um tipo com um campo opcional e o evento de desserialização.

 [!code-csharp[FxCop.Usage.OptionalFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OptionalFields/cs/FxCop.Usage.OptionalFields.cs#1)]
 [!code-vb[FxCop.Usage.OptionalFields#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OptionalFields/vb/FxCop.Usage.OptionalFields.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2236: Chamar métodos da classe base em tipos ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)

 [CA2240: Implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238: Implementar métodos de serialização corretamente](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235: Marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237: Marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2120: Construtores de serialização segura](../code-quality/ca2120-secure-serialization-constructors.md)
