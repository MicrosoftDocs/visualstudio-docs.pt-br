---
title: 'CA1040: Evite interfaces vazias | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1040
- AvoidEmptyInterfaces
helpviewer_keywords:
- AvoidEmptyInterfaces
- CA1040
ms.assetid: 120a741b-5fd1-4836-8453-7857e0cd0380
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ef6dc666cbc3c26d58358c9b59264f93a7bf184
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548246"
---
# <a name="ca1040-avoid-empty-interfaces"></a>CA1040: Evitar interfaces vazias
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|AvoidEmptyInterfaces|
|CheckId|CA1040|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 A interface não declara nenhum membro ou implementa duas ou mais interfaces.

## <a name="rule-description"></a>Descrição da Regra
 As interfaces definem os membros que fornecem um contrato de comportamento ou de uso. A funcionalidade descrita pela interface pode ser adotada por qualquer tipo, independentemente de onde o tipo seja exibido na hierarquia de herança. Um tipo implementa uma interface fornecendo implementações para os membros da interface. Uma interface vazia não define nenhum membro. Portanto, ele não define um contrato que pode ser implementado.

 Se o design incluir interfaces vazias que devem ser implementadas pelos tipos, você provavelmente está usando uma interface como um marcador ou uma maneira de identificar um grupo de tipos. Se essa identificação ocorrer em tempo de execução, a maneira correta de fazer isso é usar um atributo personalizado. Use a presença ou a ausência do atributo, ou as propriedades do atributo, para identificar os tipos de destino. Se a identificação deve ocorrer no momento da compilação, é aceitável usar uma interface vazia.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Remova a interface ou adicione membros a ela. Se a interface vazia estiver sendo usada para rotular um conjunto de tipos, substitua a interface por um atributo personalizado.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando a interface é usada para identificar um conjunto de tipos no momento da compilação.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma interface vazia.

 [!code-cpp[FxCop.Design.InterfacesNotEmpty#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cpp/FxCop.Design.InterfacesNotEmpty.cpp#1)]
 [!code-csharp[FxCop.Design.InterfacesNotEmpty#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/cs/FxCop.Design.InterfacesNotEmpty.cs#1)]
 [!code-vb[FxCop.Design.InterfacesNotEmpty#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.InterfacesNotEmpty/vb/FxCop.Design.InterfacesNotEmpty.vb#1)]
