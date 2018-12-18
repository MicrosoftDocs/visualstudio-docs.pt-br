---
title: 'CA1305: especificar IFormatProvider'
ms.date: 06/30/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyIFormatProvider
- CA1305
helpviewer_keywords:
- CA1305
- SpecifyIFormatProvider
ms.assetid: fb34ed9a-4eab-47cc-8eef-3068a4a1397e
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 05e2efde1be3430f95b00edbe8da8f952efad758
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174300"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305: especificar IFormatProvider

|||
|-|-|
|NomeDoTipo|SpecifyIFormatProvider|
|CheckId|CA1305|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

Um método ou construtor chama um ou mais membros que têm sobrecargas que aceitam um <xref:System.IFormatProvider?displayProperty=fullName> parâmetro e o método ou construtor não chama a sobrecarga que utiliza o <xref:System.IFormatProvider> parâmetro.

Essa regra ignora chamadas para métodos do .NET Framework que são documentados como ignorando o <xref:System.IFormatProvider> parâmetro. A regra também ignora os seguintes métodos:

- <xref:System.Activator.CreateInstance%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=nameWithType>
- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=nameWithType>

## <a name="rule-description"></a>Descrição da regra

Quando um <xref:System.Globalization.CultureInfo?displayProperty=nameWithType> ou <xref:System.IFormatProvider> objeto não for fornecido, o valor padrão fornecido pelo membro sobrecarregado pode não ter o efeito desejado em todas as localidades. Além disso, a cultura padrão de escolha de membros do .NET Framework e formatação com base em suposições que podem não estar corretas para seu código. Para certificar-se de que o código funciona conforme o esperado para seus cenários, você deve fornecer informações específicas da cultura acordo com as diretrizes a seguir:

- Se o valor será exibido ao usuário, use a cultura atual. Consulte <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>.

- Se o valor será armazenado e acessado pelo software (persistida em um arquivo ou banco de dados), use a cultura invariável. Consulte <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=nameWithType>.

- Se você não souber o destino do valor, ter o consumidor de dados ou provedor de especificar a cultura.

Mesmo se o comportamento padrão do membro sobrecarregado é apropriado para suas necessidades, é melhor chamar explicitamente a sobrecarga de específicas da cultura para que seu código seja autodocumentados e mais fácil manutenção.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, use a sobrecarga que utiliza um <xref:System.IFormatProvider> argumento. Ou use uma [c# cadeia de caracteres interpolada](/dotnet/csharp/tutorials/string-interpolation) e passá-lo para o <xref:System.FormattableString.Invariant%2A?displayProperty=nameWithType> método.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

É seguro suprimir um aviso nessa regra, quando você tiver certeza de que o formato padrão é a escolha correta e manutenção de código não é uma prioridade de desenvolvimento importantes.

## <a name="example"></a>Exemplo

No código a seguir, o `example1` regra CA1305 viola a cadeia de caracteres. O `example2` cadeia de caracteres satisfaz a regra CA1305 passando <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=nameWithType>, que implementa <xref:System.IFormatProvider>, para <xref:System.String.Format(System.IFormatProvider,System.String,System.Object)?displayProperty=nameWithType>. O `example3` cadeia de caracteres satisfaz a regra CA1305, passando uma cadeia de caracteres interpolada <xref:System.FormattableString.Invariant%2A?displayProperty=fullName]>.

```csharp
string name = "Georgette";

// Violates CA1305
string example1 = String.Format("Hello {0}", name);

// Satisfies CA1305
string example2 = String.Format(CultureInfo.CurrentCulture, "Hello {0}", name);

// Satisfies CA1305
string example3 = FormattableString.Invariant($"Hello {name}");
```

## <a name="related-rules"></a>Regras relacionadas

- [CA1304: especificar CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>Consulte também

- [Usando a classe CultureInfo](/dotnet/standard/globalization-localization/globalization#Cultures)