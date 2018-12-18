---
title: 'CA1300: Especificar MessageBoxOptions | Microsoft Docs'
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
- SpecifyMessageBoxOptions
- CA1300
helpviewer_keywords:
- SpecifyMessageBoxOptions
- CA1300
ms.assetid: 9357a724-026e-4a3d-a03a-f14635064ec6
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5d1b5e94ab05a5aca551cf0979aa475824a2e8fe
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825472"
---
# <a name="ca1300-specify-messageboxoptions"></a>CA1300: especificar MessageBoxOptions
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SpecifyMessageBoxOptions|
|CheckId|CA1300|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método chama uma sobrecarga da <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName> método que não utilize um <xref:System.Windows.Forms.MessageBoxOptions?displayProperty=fullName> argumento.

## <a name="rule-description"></a>Descrição da Regra
 Para exibir uma caixa de mensagem corretamente para as culturas que usam uma ordem de leitura da direita para esquerda, o <xref:System.Windows.Forms.MessageBoxOptions> e <xref:System.Windows.Forms.MessageBoxOptions> os membros a <xref:System.Windows.Forms.MessageBoxOptions> enumeração deve ser passada para o <xref:System.Windows.Forms.MessageBox.Show%2A> método. Examinar o <xref:System.Windows.Forms.Control.RightToLeft%2A?displayProperty=fullName> propriedade do controle recipiente para determinar se deve usar uma ordem de leitura da direita para esquerda.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, chame uma sobrecarga da <xref:System.Windows.Forms.MessageBox.Show%2A> método que usa um <xref:System.Windows.Forms.MessageBoxOptions> argumento.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, quando a biblioteca de código não será localizada para uma cultura que usa uma ordem de leitura da direita para esquerda.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que exibe uma caixa de mensagem que tem opções que são apropriadas para a ordem de leitura da cultura. Um arquivo de recurso, que não é exibido, é necessário para compilar o exemplo. Siga os comentários no exemplo, para compilar o exemplo sem um arquivo de recurso e testar o recurso da direita para esquerda.

 [!code-csharp[FxCop.Globalization.SpecifyMBOptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/cs/FxCop.Globalization.SpecifyMBOptions.cs#1)]
 [!code-vb[FxCop.Globalization.SpecifyMBOptions#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.SpecifyMBOptions/vb/FxCop.Globalization.SpecifyMBOptions.vb#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Resources.ResourceManager?displayProperty=fullName> [Recursos em aplicativos da área de trabalho](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)



