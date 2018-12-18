---
title: 'CA2238: Implementar métodos de serialização corretamente | Microsoft Docs'
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
- ImplementSerializationMethodsCorrectly
- CA2238
helpviewer_keywords:
- ImplementSerializationMethodsCorrectly
- CA2238
ms.assetid: 00882cf9-e10d-4d40-9126-3e6753e3c934
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3222deaeac97df8b954853f21eaff40a8244d8ca
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49864270"
---
# <a name="ca2238-implement-serialization-methods-correctly"></a>CA2238: implementar métodos de serialização corretamente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para obter a documentação mais recente do Visual Studio 2017, consulte [CA2238: implementar métodos de serialização corretamente](https://docs.microsoft.com/visualstudio/code-quality/ca2238-implement-serialization-methods-correctly) em docs.microsoft.com.  
  
|||  
|-|-|  
|NomeDoTipo|ImplementSerializationMethodsCorrectly|  
|CheckId|CA2238|  
|Categoria|Microsoft.Usage|  
|Alteração Significativa|Quebrando - se o método é visível fora do assembly.<br /><br /> Não separável - se o método não é visível fora do assembly.|  
  
## <a name="cause"></a>Causa  
 Um método que trata um evento de serialização não tem a assinatura, o tipo de retorno ou a visibilidade corretos.  
  
## <a name="rule-description"></a>Descrição da Regra  
 Um método é designado um manipulador de eventos de serialização, aplicando um dos seguintes atributos de evento de serialização:  
  
- <xref:System.Runtime.Serialization.OnSerializingAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnSerializedAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnDeserializingAttribute?displayProperty=fullName>  
  
- <xref:System.Runtime.Serialization.OnDeserializedAttribute?displayProperty=fullName>  
  
  Manipuladores de eventos de serialização usam um único parâmetro do tipo <xref:System.Runtime.Serialization.StreamingContext?displayProperty=fullName>, return `void`e ter `private` visibilidade.  
  
## <a name="how-to-fix-violations"></a>Como Corrigir Violações  
 Para corrigir uma violação dessa regra, corrija a assinatura, o tipo de retorno ou a visibilidade do manipulador de eventos de serialização.  
  
## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos  
 Não suprima um aviso nessa regra.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra a serialização declarada corretamente manipuladores de eventos.  
  
 [!code-csharp[FxCop.Usage.SerializationEventHandlers#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.SerializationEventHandlers/cs/FxCop.Usage.SerializationEventHandlers.cs#1)]
 [!code-vb[FxCop.Usage.SerializationEventHandlers#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.SerializationEventHandlers/vb/FxCop.Usage.SerializationEventHandlers.vb#1)]  
  
## <a name="related-rules"></a>Regras relacionadas  
 [CA2236: chamar métodos de classe base em tipos ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)  
  
 [CA2240: implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md)  
  
 [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md)  
  
 [CA2235: marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md)  
  
 [CA2237: marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)  
  
 [CA2239: fornecer métodos de desserialização para campos opcionais](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)  
  
 [CA2120: proteger construtores de serialização](../code-quality/ca2120-secure-serialization-constructors.md)

