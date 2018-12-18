---
title: 'CA1041: fornecer mensagem ObsoleteAttribute'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1041
- ProvideObsoleteAttributeMessage
helpviewer_keywords:
- ProvideObsoleteAttributeMessage
- CA1041
ms.assetid: be5bee69-d2d2-44e1-be2e-3ea451969003
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d8e8a4be147a786da06f3fdb7f961a7b36aa85a4
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546924"
---
# <a name="ca1041-provide-obsoleteattribute-message"></a>CA1041: fornecer mensagem ObsoleteAttribute

|||
|-|-|
|NomeDoTipo|ProvideObsoleteAttributeMessage|
|CheckId|CA1041|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um tipo ou membro marcado usando um <xref:System.ObsoleteAttribute?displayProperty=fullName> atributo que não tem seu <xref:System.ObsoleteAttribute.Message%2A?displayProperty=fullName> propriedade especificada.

## <a name="rule-description"></a>Descrição da regra
 <xref:System.ObsoleteAttribute> é usado para marcar membros e tipos de biblioteca preterido. Os clientes de biblioteca devem evitar o uso de qualquer tipo ou membro que está marcado como obsoleto. Isso ocorre porque ele não poderá ter suporte e eventualmente será removido de versões posteriores da biblioteca. Quando um tipo ou membro marcado usando <xref:System.ObsoleteAttribute> é compilado, o <xref:System.ObsoleteAttribute.Message%2A> propriedade do atributo é exibida. Isso dá ao usuário informações sobre o tipo ou o membro obsoleto. Essas informações geralmente incluem quanto o tipo obsoleto ou membro será compatível com os designers de biblioteca e da substituição de preferência para usar.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, adicione a `message` parâmetro para o <xref:System.ObsoleteAttribute> construtor.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprimir um aviso nessa regra porque o <xref:System.ObsoleteAttribute.Message%2A> propriedade fornece informações essenciais sobre o tipo ou membro obsoleto.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um membro obsoleto que tenha declarado corretamente <xref:System.ObsoleteAttribute>.

 [!code-cpp[FxCop.Design.ObsoleteAttributeOnMember#1](../code-quality/codesnippet/CPP/ca1041-provide-obsoleteattribute-message_1.cpp)]
 [!code-csharp[FxCop.Design.ObsoleteAttributeOnMember#1](../code-quality/codesnippet/CSharp/ca1041-provide-obsoleteattribute-message_1.cs)]
 [!code-vb[FxCop.Design.ObsoleteAttributeOnMember#1](../code-quality/codesnippet/VisualBasic/ca1041-provide-obsoleteattribute-message_1.vb)]

## <a name="see-also"></a>Consulte também
 <xref:System.ObsoleteAttribute?displayProperty=fullName>