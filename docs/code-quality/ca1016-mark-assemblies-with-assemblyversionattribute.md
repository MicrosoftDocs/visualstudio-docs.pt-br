---
title: 'CA1016: marcar assemblies com AssemblyVersionAttribute'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkAssembliesWithAssemblyVersion
- CA1016
helpviewer_keywords:
- CA1016
- MarkAssembliesWithAssemblyVersion
ms.assetid: 4340aed8-d92b-4cde-a398-cb6963c6da5a
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7fbc3fa747171892066705ddc32a114cb34e1b02
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47858169"
---
# <a name="ca1016-mark-assemblies-with-assemblyversionattribute"></a>CA1016: marcar assemblies com AssemblyVersionAttribute

|||
|-|-|
|NomeDoTipo|MarkAssembliesWithAssemblyVersion|
|CheckId|CA1016|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

O assembly não tem um número de versão.

## <a name="rule-description"></a>Descrição da regra

A identidade de um assembly é composta das seguintes informações:

- Nome do assembly

- Número de versão

- Cultura

- Chave pública (para assemblies fortemente nomeados).

O .NET Framework usa o número de versão para identificar exclusivamente um assembly e associar a tipos em assemblies fortemente nomeados. O número de versão é usado com a versão e a política do publicador. Por padrão, os aplicativos só são executados com a versão do assembly com que foram criados.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, adicionar um número de versão ao assembly usando o <xref:System.Reflection.AssemblyVersionAttribute?displayProperty=fullName> atributo. Consulte o exemplo a seguir.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra para assemblies que são usados por terceiros ou em um ambiente de produção.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um assembly que tem o <xref:System.Reflection.AssemblyVersionAttribute> atributo aplicado.

 [!code-csharp[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/CSharp/ca1016-mark-assemblies-with-assemblyversionattribute_1.cs)]
 [!code-vb[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/VisualBasic/ca1016-mark-assemblies-with-assemblyversionattribute_1.vb)]
 [!code-cpp[FxCop.Design.AssembliesVersion#1](../code-quality/codesnippet/CPP/ca1016-mark-assemblies-with-assemblyversionattribute_1.cpp)]

## <a name="see-also"></a>Consulte também

- [Controle de versão do assembly](/dotnet/framework/app-domains/assembly-versioning)
- [Como criar uma política de editor](/dotnet/framework/configure-apps/how-to-create-a-publisher-policy)