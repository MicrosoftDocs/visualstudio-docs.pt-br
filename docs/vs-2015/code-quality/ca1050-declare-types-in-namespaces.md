---
title: 'CA1050: declarar tipos em namespaces | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1050
- DeclareTypesInNamespaces
helpviewer_keywords:
- DeclareTypesInNamespaces
- CA1050
ms.assetid: 1002748d-ac8d-404f-85dd-7a12d1ad3e05
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0a4dcc53fac7dc9b7e189686a3b32e2fb4fd030
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539588"
---
# <a name="ca1050-declare-types-in-namespaces"></a>CA1050: Declarar tipos em namespaces
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DeclareTypesInNamespaces|
|CheckId|CA1050|
|Categoria|Microsoft. Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido é definido fora do escopo de um namespace nomeado.

## <a name="rule-description"></a>Descrição da Regra
 Os tipos são declarados em namespaces para evitar colisões de nomes e como uma maneira de organizar os tipos relacionados em uma hierarquia de objetos. Tipos que estão fora de qualquer namespace nomeado estão em um namespace global que não pode ser referenciado no código.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, coloque o tipo em um namespace.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Embora você nunca precise suprimir um aviso dessa regra, é seguro fazer isso quando o assembly nunca será usado junto com outros assemblies.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma biblioteca que tem um tipo incorretamente declarado fora de um namespace e um tipo que tem o mesmo nome declarado em um namespace.

 [!code-csharp[FxCop.Design.TypesLiveInNamespaces#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/cs/FxCop.Design.TypesLiveInNamespaces.cs#1)]
 [!code-vb[FxCop.Design.TypesLiveInNamespaces#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TypesLiveInNamespaces/vb/FxCop.Design.TypesLiveInNamespaces.vb#1)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir usa a biblioteca que foi definida anteriormente. Observe que o tipo declarado fora de um namespace é criado quando o nome `Test` não é qualificado por um namespace. Observe também que, para acessar o `Test` tipo `Goodspace` , o nome do namespace é necessário.

 [!code-csharp[FxCop.Design.TestTypesLive#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/cs/FxCop.Design.TestTypesLive.cs#1)]
 [!code-vb[FxCop.Design.TestTypesLive#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.TestTypesLive/vb/FxCop.Design.TestTypesLive.vb#1)]
