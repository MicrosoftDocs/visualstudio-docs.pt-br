---
title: 'CA1304: especificar CultureInfo'
ms.date: 06/30/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyCultureInfo
- CA1304
helpviewer_keywords:
- SpecifyCultureInfo
- CA1304
ms.assetid: b912d76a-54fd-4c93-b25d-16491e0ae319
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: fe02dd66b523e6ee82c5e1a2051f3a68839957d4
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546177"
---
# <a name="ca1304-specify-cultureinfo"></a>CA1304: especificar CultureInfo

|||
|-|-|
|NomeDoTipo|SpecifyCultureInfo|
|CheckId|CA1304|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

Um método ou construtor chama um membro que tem uma sobrecarga que aceita uma <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> parâmetro e o método ou construtor não chama a sobrecarga que utiliza o <xref:System.Globalization.CultureInfo> parâmetro. Essa regra ignora as chamadas para os seguintes métodos:

- <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>

## <a name="rule-description"></a>Descrição da regra

Quando um <xref:System.Globalization.CultureInfo> ou <xref:System.IFormatProvider?displayProperty=nameWithType> objeto não for fornecido, o valor padrão fornecido pelo membro sobrecarregado pode não ter o efeito desejado em todas as localidades. Além disso, a cultura padrão de escolha de membros do .NET Framework e formatação com base em suposições que podem não estar corretas para seu código. Para garantir que o código funciona conforme o esperado para seus cenários, você deve fornecer informações específicas da cultura acordo com as diretrizes a seguir:

- Se o valor será exibido ao usuário, use a cultura atual. Consulte <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>.

- Se o valor será armazenado e acessado pelo software, ou seja, mantidos em um arquivo ou banco de dados, use a cultura invariável. Consulte <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>.

- Se você não souber o destino do valor, ter o consumidor de dados ou provedor de especificar a cultura.

Mesmo se o comportamento padrão do membro sobrecarregado é apropriado para suas necessidades, é melhor chamar explicitamente a sobrecarga de específicas da cultura para que seu código seja autodocumentados e mais fácil manutenção.

> [!NOTE]
> <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> é usado apenas para recuperar os recursos localizados por meio de uma instância da <xref:System.Resources.ResourceManager?displayProperty=nameWithType> classe.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, use a sobrecarga que utiliza um <xref:System.Globalization.CultureInfo> argumento.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra, quando você tiver certeza de que a cultura padrão é a escolha correta e manutenção de código não é uma prioridade de desenvolvimento importantes.

## <a name="example-showing-how-to-fix-violations"></a>Exemplo mostrando como corrigir violações

No exemplo a seguir, `BadMethod` faz com que as duas violações dessa regra. `GoodMethod` corrige a primeira violação, passando a cultura invariável para <xref:System.String.Compare%2A?displayProperty=nameWithType>e corrige a violação de segundo, passando a cultura atual como <xref:System.String.ToLower%2A?displayProperty=nameWithType> porque `string3` é exibida ao usuário.

[!code-csharp[FxCop.Globalization.CultureInfo#1](../code-quality/codesnippet/CSharp/ca1304-specify-cultureinfo_1.cs)]

## <a name="example-showing-formatted-output"></a>Saída formatada de mostrando exemplo

O exemplo a seguir mostra o efeito da cultura atual em padrão <xref:System.IFormatProvider> que é selecionada pelo <xref:System.DateTime> tipo.

[!code-csharp[FxCop.Globalization.IFormatProvider#1](../code-quality/codesnippet/CSharp/ca1304-specify-cultureinfo_2.cs)]

Este exemplo gera a seguinte saída:

```txt
6/4/1900 12:15:12 PM
06/04/1900 12:15:12
```

## <a name="related-rules"></a>Regras relacionadas

- [CA1305: especificar IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md)

## <a name="see-also"></a>Consulte também

- [Usando a classe CultureInfo](/dotnet/standard/globalization-localization/globalization#Cultures)