---
title: 'CA1300: especifique MessageBoxoptions | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyMessageBoxOptions
- CA1300
helpviewer_keywords:
- SpecifyMessageBoxOptions
- CA1300
ms.assetid: 9357a724-026e-4a3d-a03a-f14635064ec6
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: af0017a7ee6918a80a93ca90c7cf3de78885d61f
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539185"
---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300: Especificar MessageBoxOptions
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|SpecifyMessageBoxOptions|
|CheckId|CA1300|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método chama uma sobrecarga do <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> método que não assume um <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName> argumento.

## <a name="rule-description"></a>Descrição da Regra
 Para exibir uma caixa de mensagem corretamente para culturas que usam uma ordem de leitura da direita para a esquerda, os <xref:System.Windows.Forms.MessageBoxOptions> <xref:System.Windows.Forms.MessageBoxOptions> Membros e da <xref:System.Windows.Forms.MessageBoxOptions> Enumeração devem ser passados para o <xref:System.Windows.Forms.MessageBox.Show%2A> método. Examine a <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName> Propriedade do controle recipiente para determinar se deve usar uma ordem de leitura da direita para a esquerda.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame uma sobrecarga do <xref:System.Windows.Forms.MessageBox.Show%2A> método que usa um <xref:System.Windows.Forms.MessageBoxOptions> argumento.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando a biblioteca de códigos não for localizada para uma cultura que usa uma ordem de leitura da direita para a esquerda.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que exibe uma caixa de mensagem que tem opções apropriadas para a ordem de leitura da cultura. Um arquivo de recurso, que não é mostrado, é necessário para criar o exemplo. Siga os comentários no exemplo para criar o exemplo sem um arquivo de recurso e para testar o recurso da direita para a esquerda.

 [!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/cs/FxCop.Globalization.SpecifyMBOptions.cs#1)]
 [!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/vb/FxCop.Globalization.SpecifyMBOptions.vb#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Resources.ResourceManager?displayProperty=fullName>[Recursos em aplicativos da área de trabalho](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
