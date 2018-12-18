---
title: 'CA2120: Proteger construtores de serialização | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA2120
- SecureSerializationConstructors
helpviewer_keywords:
- SecureSerializationConstructors
- CA2120
ms.assetid: e9989da1-55a0-43f8-9aa9-da86afae3b41
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3bc919d8ea9186a5b0fff6bdd23efa7da1bd8b17
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49834175"
---
# <a name="ca2120-secure-serialization-constructors"></a>CA2120: proteger construtores de serialização
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SecureSerializationConstructors|
|CheckId|CA2120|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 O tipo implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface, não é um delegado ou interface e é declarado em um assembly que permite que os chamadores parcialmente confiáveis. O tipo tem um construtor que usa um <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName> objeto e um <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> objeto (a assinatura do construtor de serialização). Este construtor não é protegido por uma verificação de segurança, mas um ou mais dos construtores regulares no tipo é protegida.

## <a name="rule-description"></a>Descrição da Regra
 Essa regra é relevante para tipos que oferecem suporte a serialização personalizada. Um tipo é compatível com a serialização personalizada se ele implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface. O construtor de serialização é necessário e é usado para desserializar ou recriar objetos que foram serializados usando a <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> método. Como o construtor de serialização aloca e inicializa os objetos, as verificações de segurança que estão presentes nos construtores regulares também devem estar presentes no construtor de serialização. Se você violar essa regra, os chamadores que, caso contrário, não foi possível criar uma instância poderia usar o construtor de serialização para fazer isso.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, proteja o construtor de serialização com demandas de segurança que são idênticas àquelas Protegendo outros construtores.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima uma violação da regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo que viola a regra.

 [!code-csharp[FxCop.Security.SerialCtors#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.SerialCtors/cs/FxCop.Security.SerialCtors.cs#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2237: marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

## <a name="see-also"></a>Consulte também
 <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>
 <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>



