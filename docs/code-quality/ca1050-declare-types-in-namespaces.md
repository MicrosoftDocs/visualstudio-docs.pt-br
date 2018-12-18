---
title: 'CA1050: declarar tipos em namespaces'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1050
- DeclareTypesInNamespaces
helpviewer_keywords:
- DeclareTypesInNamespaces
- CA1050
ms.assetid: 1002748d-ac8d-404f-85dd-7a12d1ad3e05
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 5bff984d9ea11ba8fd7f2e42deb5898f04da7d44
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45548472"
---
# <a name="ca1050-declare-types-in-namespaces"></a>CA1050: declarar tipos em namespaces

|||
|-|-|
|NomeDoTipo|DeclareTypesInNamespaces|
|CheckId|CA1050|
|Categoria|Microsoft.Design|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido é definido fora do escopo de um namespace nomeado.

## <a name="rule-description"></a>Descrição da regra
 Tipos são declarados em namespaces para evitar colisões de nome e como uma forma de organizar tipos relacionados em uma hierarquia de objetos. Tipos que estão fora de qualquer namespace nomeado estão em um namespace global que não pode ser referenciado no código.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, coloque o tipo em um namespace.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Embora você nunca precisará suprimir um aviso nessa regra, é seguro fazer isso quando o assembly nunca será usado em conjunto com outros assemblies.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma biblioteca que tenha um tipo declarado incorretamente fora de um namespace e um tipo que tem o mesmo nome declarado em um namespace.

 [!code-csharp[FxCop.Design.TypesLiveInNamespaces#1](../code-quality/codesnippet/CSharp/ca1050-declare-types-in-namespaces_1.cs)]
 [!code-vb[FxCop.Design.TypesLiveInNamespaces#1](../code-quality/codesnippet/VisualBasic/ca1050-declare-types-in-namespaces_1.vb)]

## <a name="example"></a>Exemplo
 O aplicativo a seguir usa a biblioteca que foi definida anteriormente. Observe que o tipo que é declarado fora de um namespace é criado quando o nome `Test` não são qualificados por um namespace. Observe também que, para acessar o `Test` digitar `Goodspace`, o nome do namespace é necessário.

 [!code-csharp[FxCop.Design.TestTypesLive#1](../code-quality/codesnippet/CSharp/ca1050-declare-types-in-namespaces_2.cs)]
 [!code-vb[FxCop.Design.TestTypesLive#1](../code-quality/codesnippet/VisualBasic/ca1050-declare-types-in-namespaces_2.vb)]