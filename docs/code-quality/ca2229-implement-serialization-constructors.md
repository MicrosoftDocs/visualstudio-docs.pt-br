---
title: 'CA2229: implementar construtores de serialização'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2229
- ImplementSerializationConstructors
helpviewer_keywords:
- CA2229
- ImplementSerializationConstructors
ms.assetid: 8e04d5fe-dfad-445a-972e-0648324fac45
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: c1c4dea2b6b3a7f64efa06a1600c63ad7a7d9d5c
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551971"
---
# <a name="ca2229-implement-serialization-constructors"></a>CA2229: implementar construtores de serialização

|||
|-|-|
|NomeDoTipo|ImplementSerializationConstructors|
|CheckId|CA2229|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 O tipo implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> da interface, não é um delegado ou interface e uma das seguintes condições for verdadeira:

- O tipo não tem um construtor que usa um <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> objeto e um <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> objeto (a assinatura do construtor de serialização).

- O tipo é sem lacre e o modificador de acesso para seu construtor de serialização não é protegida (família).

- O tipo está lacrado e o modificador de acesso para seu construtor de serialização não é privado.

## <a name="rule-description"></a>Descrição da regra
 Essa regra é relevante para tipos que oferecem suporte a serialização personalizada. Um tipo é compatível com a serialização personalizada se ele implementa o <xref:System.Runtime.Serialization.ISerializable> interface. O construtor de serialização é necessário para desserializar ou recriar objetos que foram serializados usando a <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> método.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, implemente o construtor de serialização. Para uma classe lacrada, torne o construtor particular; do contrário, deixe-o protegido.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima uma violação da regra. O tipo não serão desserializável e não funcionará em muitos cenários.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que satisfaça a regra.

 [!code-csharp[FxCop.Usage.ISerializableCtor#1](../code-quality/codesnippet/CSharp/ca2229-implement-serialization-constructors_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2237: marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>
- <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
- <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>