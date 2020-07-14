---
title: 'CA1016: Marcar assemblies com AssemblyVersionAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkAssembliesWithAssemblyVersion
- CA1016
helpviewer_keywords:
- CA1016
- MarkAssembliesWithAssemblyVersion
ms.assetid: 4340aed8-d92b-4cde-a398-cb6963c6da5a
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 97bd41e51c8d6b5415ffb91c5696c7055f46cf7c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545399"
---
# <a name="ca1016-mark-assemblies-with-assemblyversionattribute"></a>CA1016: Marcar assemblies com AssemblyVersionAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|MarkAssembliesWithAssemblyVersion|
|CheckId|CA1016|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 O assembly não tem um número de versão.

## <a name="rule-description"></a>Descrição da Regra
 A identidade de um assembly é composta pelas seguintes informações:

- Nome do assembly

- Número de versão

- Cultura

- Chave pública (para assemblies com nome forte).

  O [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] usa o número de versão para identificar com exclusividade um assembly e associar a tipos em assemblies altamente nomeados. O número de versão é usado com a versão e a política do publicador. Por padrão, os aplicativos só são executados com a versão do assembly com que foram criados.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, adicione um número de versão ao assembly usando o <xref:System.Reflection.AssemblyVersionAttribute?displayProperty=fullName> atributo. Veja os exemplos a seguir.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso desta regra para assemblies que são usados por terceiros ou em um ambiente de produção.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um assembly que tem o <xref:System.Reflection.AssemblyVersionAttribute> atributo aplicado.

 [!code-cpp[FxCop.Design.AssembliesVersion#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesVersion/cpp/FxCop.Design.AssembliesVersion.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesVersion#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesVersion/cs/FxCop.Design.AssembliesVersion.cs#1)]
 [!code-vb[FxCop.Design.AssembliesVersion#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesVersion/vb/FxCop.Design.AssembliesVersion.vb#1)]

## <a name="see-also"></a>Consulte Também
 [Controle de versão do assembly](https://msdn.microsoft.com/library/775ad4fb-914f-453c-98ef-ce1089b6f903) [como criar uma política de Publicador](https://msdn.microsoft.com/library/8046bc5d-2fa9-4277-8a5e-6dcc96c281d9)
