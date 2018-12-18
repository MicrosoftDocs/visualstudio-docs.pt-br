---
title: 'CA2236: Chamar métodos de classe base em tipos ISerializable | Microsoft Docs'
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
- CA2236
- CallBaseClassMethodsOnISerializableTypes
helpviewer_keywords:
- CA2236
- CallBaseClassMethodsOnISerializableTypes
ms.assetid: 5a15b20d-769c-4640-b31a-36e07077daae
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: bcde222020ca18b918ad694abe42c2c76a4a613c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886676"
---
# <a name="ca2236-call-base-class-methods-on-iserializable-types"></a>CA2236: chamar métodos de classe base em tipos ISerializable
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|CallBaseClassMethodsOnISerializableTypes|
|CheckId|CA2236|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um tipo derivado de um tipo que implementa o <xref:System.Runtime.Serialization.ISerializable?displayProperty=fullName> interface e uma das seguintes condições é verdadeira:

-   O tipo implementa o construtor de serialização, ou seja, um construtor com o <xref:System.Runtime.Serialization.SerializationInfo?displayProperty=fullName>, <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName> a assinatura do parâmetro, mas não chama o construtor de serialização do tipo base.

-   O tipo implementa a <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A?displayProperty=fullName> método, mas não chama o <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> método do tipo base.

## <a name="rule-description"></a>Descrição da Regra
 Em um processo de serialização personalizada, um tipo implementa o <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> método para serializar seus campos e o construtor de serialização para desserializar os campos. Se o tipo é derivado de um tipo que implementa o <xref:System.Runtime.Serialization.ISerializable> da interface, o tipo base <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> construtor de serialização e o método deve ser chamado para/serializar desserializar os campos do tipo base. Caso contrário, o tipo de não ser serializado e desserializado corretamente. Observe que, se o tipo derivado não adiciona todos os novos campos, o tipo não precisa implementar o <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> método nem o construtor de serialização ou chamar os equivalentes do tipo base.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame o tipo base <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> construtor de serialização ou método de correspondente derivado de tipo de método ou construtor.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um tipo derivado que satisfaz a regra chamando o construtor de serialização e <xref:System.Runtime.Serialization.ISerializable.GetObjectData%2A> método da classe base.

 [!code-csharp[FxCop.Usage.CallBaseISerializable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/cs/FxCop.Usage.CallBaseISerializable.cs#1)]
 [!code-vb[FxCop.Usage.CallBaseISerializable#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.CallBaseISerializable/vb/FxCop.Usage.CallBaseISerializable.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA2240: implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md)

 [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)

 [CA2238: implementar métodos de serialização corretamente](../code-quality/ca2238-implement-serialization-methods-correctly.md)

 [CA2235: marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md)

 [CA2237: marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)

 [CA2239: fornecer métodos de desserialização para campos opcionais](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)

 [CA2120: proteger construtores de serialização](../code-quality/ca2120-secure-serialization-constructors.md)



