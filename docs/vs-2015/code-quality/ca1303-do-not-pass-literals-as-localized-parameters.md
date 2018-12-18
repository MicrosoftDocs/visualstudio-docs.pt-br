---
title: 'CA1303: Não passar literais como localizados parâmetros | Microsoft Docs'
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
- Do not pass literals as localized parameters
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
helpviewer_keywords:
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
ms.assetid: 904d284e-76d0-4b8f-a4df-0094de8d7aac
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d900abe23dab4d950b5790798916fe728a44af4a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886549"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303: não passar literais como parâmetros localizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um método passa uma cadeia de caracteres literal como um parâmetro para um construtor ou método no [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] biblioteca de classes e que a cadeia de caracteres deve ser localizável.

 Esse aviso é acionado quando uma cadeia de caracteres literal é passada como um valor para um parâmetro ou uma propriedade e um ou mais dos casos a seguir forem verdadeira:

-   O <xref:System.ComponentModel.LocalizableAttribute> atributo do parâmetro ou da propriedade é definido como true.

-   O nome de parâmetro ou a propriedade contém "Text", "Mensagem" ou "Legenda".

-   O nome do parâmetro de cadeia de caracteres que é passado para um método console. Write ou console. WriteLine é "valor" ou "formato".

## <a name="rule-description"></a>Descrição da Regra
 Literais de cadeia de caracteres que são inseridos no código-fonte são difíceis de localizar.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua a cadeia de caracteres literal com uma cadeia de caracteres recuperada por meio de uma instância da <xref:System.Resources.ResourceManager> classe.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se a biblioteca de código não será localizada ou se a cadeia de caracteres não é exposta ao usuário final ou um desenvolvedor que usa a biblioteca de código.

 Os usuários podem eliminar o ruído em relação a métodos que não deve ser passado cadeias de caracteres localizadas, renomeando o parâmetro ou uma propriedade chamada ou marcando esses itens como condicional.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que lança uma exceção quando qualquer um dos dois argumentos estão fora do intervalo. Para o primeiro argumento, o construtor de exceção é passado uma cadeia de caracteres literal, o que viola essa regra. Para o segundo argumento, o construtor corretamente é passado uma cadeia de caracteres recuperada por meio de um <xref:System.Resources.ResourceManager>.

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cpp/FxCop.Globalization.DoNotPassLiterals.cpp#1)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cs/FxCop.Globalization.DoNotPassLiterals.cs#1)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/vb/FxCop.Globalization.DoNotPassLiterals.vb#1)]

## <a name="see-also"></a>Consulte também
 [Recursos em aplicativos de área de trabalho](http://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)



