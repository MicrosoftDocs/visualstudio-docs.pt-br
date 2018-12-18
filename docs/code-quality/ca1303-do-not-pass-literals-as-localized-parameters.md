---
title: 'CA1303: não passar literais como parâmetros localizados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
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
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8716a16ea3b141e7c5053e526d92531d0a77bc1e
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859400"
---
# <a name="ca1303-do-not-pass-literals-as-localized-parameters"></a>CA1303: não passar literais como parâmetros localizados

|||
|-|-|
|NomeDoTipo|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um método passa uma cadeia de caracteres literal como um parâmetro para um construtor ou método na biblioteca de classes do .NET Framework, e essa cadeia de caracteres deve ser localizável.

 Esse aviso é acionado quando uma cadeia de caracteres literal é passada como um valor para um parâmetro ou uma propriedade e um ou mais dos casos a seguir forem verdadeira:

- O <xref:System.ComponentModel.LocalizableAttribute> atributo do parâmetro ou da propriedade é definido como true.

- O nome de parâmetro ou a propriedade contém "Text", "Mensagem" ou "Legenda".

- O nome do parâmetro de cadeia de caracteres que é passado para um método console. Write ou console. WriteLine é "valor" ou "formato".

## <a name="rule-description"></a>Descrição da regra
 Literais de cadeia de caracteres que são inseridos no código-fonte são difíceis de localizar.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, substitua a cadeia de caracteres literal com uma cadeia de caracteres recuperada por meio de uma instância da <xref:System.Resources.ResourceManager> classe.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se a biblioteca de código não será localizada ou se a cadeia de caracteres não é exposta ao usuário final ou um desenvolvedor que usa a biblioteca de código.

 Os usuários podem eliminar o ruído em relação a métodos que não devem ser passados cadeias de caracteres localizadas, renomeando o parâmetro ou uma propriedade chamada ou marcando esses itens como condicional.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que lança uma exceção quando qualquer um dos dois argumentos estão fora do intervalo. Para o primeiro argumento, o construtor de exceção é passado uma cadeia de caracteres literal, o que viola essa regra. Para o segundo argumento, o construtor corretamente é passado uma cadeia de caracteres recuperada por meio de um <xref:System.Resources.ResourceManager>.

 [!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../code-quality/codesnippet/CPP/ca1303-do-not-pass-literals-as-localized-parameters_1.cpp)]
 [!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../code-quality/codesnippet/VisualBasic/ca1303-do-not-pass-literals-as-localized-parameters_1.vb)]
 [!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../code-quality/codesnippet/CSharp/ca1303-do-not-pass-literals-as-localized-parameters_1.cs)]

## <a name="see-also"></a>Consulte também
 [Recursos em aplicativos de área de trabalho](/dotnet/framework/resources/index)