---
title: 'CA1306: definir localidade para tipos de dados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1306
- SetLocaleForDataTypes
helpviewer_keywords:
- CA1306
- SetLocaleForDataTypes
ms.assetid: 104297b2-5806-4de0-a8d9-c589380a796c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e60a788d94a6c0d594ee45505b8f4ad9f64dbdff
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45547176"
---
# <a name="ca1306-set-locale-for-data-types"></a>CA1306: definir localidade para tipos de dados

|||
|-|-|
|NomeDoTipo|SetLocaleForDataTypes|
|CheckId|CA1306|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método ou construtor criado um ou mais <xref:System.Data.DataTable?displayProperty=fullName> ou <xref:System.Data.DataSet?displayProperty=fullName> instâncias e não definir explicitamente a propriedade de localidade (<xref:System.Data.DataTable.Locale%2A?displayProperty=fullName> ou <xref:System.Data.DataSet.Locale%2A?displayProperty=fullName>).

## <a name="rule-description"></a>Descrição da regra
 A localidade determina os elementos de apresentação específicos da cultura para dados, como a formatação usada para valores numéricos, símbolos de moeda e ordem de classificação. Quando você cria um <xref:System.Data.DataTable> ou <xref:System.Data.DataSet>, você deve definir explicitamente a localidade. Por padrão, a localidade para esses tipos é a cultura atual. Para dados que são armazenados em um arquivo ou banco de dados e são compartilhados globalmente, a localidade normalmente deve ser definida para a cultura invariável (<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>). Quando dados são compartilhados entre culturas, usando a localidade padrão pode causar o conteúdo do <xref:System.Data.DataTable> ou <xref:System.Data.DataSet> ser apresentada ou interpretados incorretamente.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, definir explicitamente a localidade para o <xref:System.Data.DataTable> ou <xref:System.Data.DataSet>.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, quando o aplicativo ou biblioteca é para um público limitado de local, os dados não são compartilhados ou a configuração padrão produz o comportamento desejado em todos os cenários com suporte.

## <a name="example"></a>Exemplo
 O exemplo a seguir cria dois <xref:System.Data.DataTable> instâncias.

 [!code-csharp[FxCop.Globalization.DataTable#1](../code-quality/codesnippet/CSharp/ca1306-set-locale-for-data-types_1.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataTable?displayProperty=fullName>
- <xref:System.Data.DataSet?displayProperty=fullName>
- <xref:System.Globalization.CultureInfo?displayProperty=fullName>
- <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>
- <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>