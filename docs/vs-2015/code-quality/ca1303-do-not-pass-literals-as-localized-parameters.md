---
title: 'CA1303: não passe literais como parâmetros localizados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Do not pass literals as localized parameters
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
helpviewer_keywords:
- DoNotPassLiteralsAsLocalizedParameters
- CA1303
ms.assetid: 904d284e-76d0-4b8f-a4df-0094de8d7aac
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f3ad1f56215d002c03d346b38ce6155e8df7412b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539107"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303: Não passar literais como parâmetros localizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método passa um literal de cadeia de caracteres como um parâmetro para um construtor ou método na [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] biblioteca de classes e essa cadeia de caracteres deve ser localizável.

 Esse aviso é gerado quando uma cadeia de caracteres literal é passada como um valor para um parâmetro ou propriedade e um ou mais dos seguintes casos é verdadeiro:

- O <xref:System.ComponentModel.LocalizableAttribute> atributo do parâmetro ou da propriedade é definido como true.

- O nome do parâmetro ou da propriedade contém "texto", "mensagem" ou "legenda".

- O nome do parâmetro de cadeia de caracteres que é passado para um método Console. Write ou console. WriteLine é "value" ou "Format".

## <a name="rule-description"></a>Descrição da Regra
 Literais de cadeia de caracteres inseridos no código-fonte são difíceis de localizar.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, substitua o literal da cadeia de caracteres por uma cadeia de caracteres recuperada por meio de uma instância da <xref:System.Resources.ResourceManager> classe.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se a biblioteca de códigos não for localizada ou se a cadeia de caracteres não for exposta ao usuário final ou a um desenvolvedor usando a biblioteca de códigos.

 Os usuários podem eliminar ruídos em relação a métodos que não devem passar cadeias de caracteres localizadas renomeando o parâmetro ou a propriedade chamada ou marcando esses itens como condicionais.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que gera uma exceção quando qualquer um dos dois argumentos está fora do intervalo. Para o primeiro argumento, o construtor de exceção recebe uma cadeia de caracteres literal, que viola essa regra. Para o segundo argumento, o Construtor passa corretamente uma cadeia de caracteres recuperada por meio de um <xref:System.Resources.ResourceManager> .

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cpp/FxCop.Globalization.DoNotPassLiterals.cpp#1)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/cs/FxCop.Globalization.DoNotPassLiterals.cs#1)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.DoNotPassLiterals/vb/FxCop.Globalization.DoNotPassLiterals.vb#1)]

## <a name="see-also"></a>Consulte Também
 [Recursos em aplicativos da área de trabalho](https://msdn.microsoft.com/library/8ad495d4-2941-40cf-bf64-e82e85825890)
