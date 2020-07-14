---
title: 'CA1306: definir a localidade para tipos de dados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1306
- SetLocaleForDataTypes
helpviewer_keywords:
- CA1306
- SetLocaleForDataTypes
ms.assetid: 104297b2-5806-4de0-a8d9-c589380a796c
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: edd1d6a7623f96f03403883ee2585d245414bb3b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539016"
---
# <a name="ca1306-set-locale-for-data-types"></a>CA1306: Definir localidade para tipos de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|SetLocaleForDataTypes|
|CheckId|CA1306|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método ou Construtor criou uma ou mais <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName> instâncias ou e não definiu explicitamente a propriedade locale ( <xref:System.Data.DataTable.Locale%2A?displayProperty=fullName> ou <xref:System.Data.DataSet.Locale%2A?displayProperty=fullName> ).

## <a name="rule-description"></a>Descrição da Regra
 A localidade determina elementos de apresentação específicos da cultura para dados, como formatação usada para valores numéricos, símbolos de moeda e ordem de classificação. Ao criar um <xref:System.Data.DataTable> ou <xref:System.Data.DataSet> , você deve definir a localidade explicitamente. Por padrão, a localidade para esses tipos é a cultura atual. Para dados que são armazenados em um arquivo ou banco de dado e são compartilhados globalmente, a localidade normalmente deve ser definida como a cultura invariável ( <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> ). Quando os dados são compartilhados entre culturas, o uso da localidade padrão pode fazer com que o conteúdo do <xref:System.Data.DataTable> ou <xref:System.Data.DataSet> seja apresentado ou interpretado incorretamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, defina explicitamente a localidade para o <xref:System.Data.DataTable> ou <xref:System.Data.DataSet> .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando a biblioteca ou o aplicativo é para um público local limitado, os dados não são compartilhados ou a configuração padrão gera o comportamento desejado em todos os cenários com suporte.

## <a name="example"></a>Exemplo
 O exemplo a seguir cria duas <xref:System.Data.DataTable> instâncias.

 [!code-csharp[FxCop.Globalization.DataTable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DataTable/cs/FxCop.Globalization.DataTable.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>
