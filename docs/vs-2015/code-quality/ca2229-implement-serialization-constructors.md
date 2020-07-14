---
title: 'CA2229: Implementar construtores de serialização | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2229
- ImplementSerializationConstructors
helpviewer_keywords:
- CA2229
- ImplementSerializationConstructors
ms.assetid: 8e04d5fe-dfad-445a-972e-0648324fac45
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: ba654496d80654f0d9790a01bbc41326f7a5f13e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540485"
---
# <a name="ca2229-implement-serialization-constructors"></a>CA2229: Implementar construtores de serialização
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ImplementSerializationConstructors|
|CheckId|CA2229|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 O tipo implementa a <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface, não é um delegado ou interface, e uma das seguintes condições é verdadeira:

- O tipo não tem um construtor que usa um <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> objeto e um <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> objeto (a assinatura do construtor de serialização).

- O tipo não é lacrado e o modificador de acesso para seu construtor de serialização não é protegido (família).

- O tipo é lacrado e o modificador de acesso para seu construtor de serialização não é privado.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra é relevante para tipos que dão suporte à serialização personalizada. Um tipo oferece suporte à serialização personalizada se ela implementar a <xref:System.Runtime.Serialization.ISerializable> interface. O construtor de serialização é necessário para desserializar ou recriar objetos que foram serializados usando o <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, implemente o construtor de serialização. Para uma classe lacrada, torne o construtor particular; do contrário, deixe-o protegido.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir uma violação da regra. O tipo não será desserializável e não funcionará em muitos cenários.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que satisfaz a regra.

 [!code-csharp[FxCop.Usage.ISerializableCtor#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.ISerializableCtor/cs/FxCop.Usage.ISerializableCtor.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2237: Marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>Consulte Também
 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>
