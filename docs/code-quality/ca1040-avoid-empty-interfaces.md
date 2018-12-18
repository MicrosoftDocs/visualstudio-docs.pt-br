---
title: 'CA1040: evitar interfaces vazias'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1040
- AvoidEmptyInterfaces
helpviewer_keywords:
- AvoidEmptyInterfaces
- CA1040
ms.assetid: 120a741b-5fd1-4836-8453-7857e0cd0380
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: d5c23a52e65d04b5cc8d147cc0ec3bd7c12bde3c
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548261"
---
# <a name="ca1040-avoid-empty-interfaces"></a>CA1040: evitar interfaces vazias

|||
|-|-|
|NomeDoTipo|AvoidEmptyInterfaces|
|CheckId|CA1040|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 A interface não declarar membros ou implementar duas ou mais interfaces.

## <a name="rule-description"></a>Descrição da regra
 As interfaces definem os membros que fornecem um contrato de comportamento ou de uso. A funcionalidade descrita pela interface pode ser adotada por qualquer tipo, independentemente de onde o tipo seja exibido na hierarquia de herança. Um tipo implementa uma interface fornecendo implementações para os membros da interface. Uma interface vazia não define nenhum membro. Portanto, ele não define um contrato que pode ser implementado.

 Se seu design incluir vazio devem implementar interfaces tipos, você provavelmente está usando uma interface como um marcador ou uma maneira de identificar um grupo de tipos. Se essa identificação ocorrerá em tempo de execução, a maneira correta de fazer isso é usar um atributo personalizado. Use a presença ou ausência do atributo, ou as propriedades do atributo, para identificar os tipos de destino. Se a identificação deve ocorrer no tempo de compilação, é aceitável usar uma interface vazia.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Remova a interface ou adicionar membros a ela. Se a interface vazia estiver sendo usado para rotular um conjunto de tipos, substitua a interface com um atributo personalizado.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, quando a interface é usada para identificar um conjunto de tipos em tempo de compilação.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma interface vazia.

 [!code-csharp[FxCop.Design.InterfacesNotEmpty#1](../code-quality/codesnippet/CSharp/ca1040-avoid-empty-interfaces_1.cs)]
 [!code-cpp[FxCop.Design.InterfacesNotEmpty#1](../code-quality/codesnippet/CPP/ca1040-avoid-empty-interfaces_1.cpp)]
 [!code-vb[FxCop.Design.InterfacesNotEmpty#1](../code-quality/codesnippet/VisualBasic/ca1040-avoid-empty-interfaces_1.vb)]