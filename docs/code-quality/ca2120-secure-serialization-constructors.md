---
title: 'CA2120: proteger construtores de serialização'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2120
- SecureSerializationConstructors
helpviewer_keywords:
- SecureSerializationConstructors
- CA2120
ms.assetid: e9989da1-55a0-43f8-9aa9-da86afae3b41
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 123bff32b847342f4081a73abb1d8b899cc0efec
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548498"
---
# <a name="ca2120-secure-serialization-constructors"></a>CA2120: proteger construtores de serialização

|||
|-|-|
|NomeDoTipo|SecureSerializationConstructors|
|CheckId|CA2120|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O tipo implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface, não é um delegado ou interface e é declarado em um assembly que permite que os chamadores parcialmente confiáveis. O tipo tem um construtor que usa um <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> objeto e um <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> objeto (a assinatura do construtor de serialização). Este construtor não é protegido por uma verificação de segurança, mas um ou mais dos construtores regulares no tipo é protegida.

## <a name="rule-description"></a>Descrição da regra
 Essa regra é relevante para tipos que oferecem suporte a serialização personalizada. Um tipo é compatível com a serialização personalizada se ele implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface. O construtor de serialização é necessário e é usado para desserializar ou recriar objetos que foram serializados usando a <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> método. Como o construtor de serialização aloca e inicializa os objetos, as verificações de segurança que estão presentes nos construtores regulares também devem estar presentes no construtor de serialização. Se você violar essa regra, os chamadores que, caso contrário, não foi possível criar uma instância poderia usar o construtor de serialização para fazer isso.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, proteja o construtor de serialização com demandas de segurança que são idênticas àquelas Protegendo outros construtores.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima uma violação da regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Security.SerialCtors#1](../code-quality/codesnippet/CSharp/ca2120-secure-serialization-constructors_1.cs)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2237: marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName>
- <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
- <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>