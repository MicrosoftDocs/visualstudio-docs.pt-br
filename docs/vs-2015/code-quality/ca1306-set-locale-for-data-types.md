---
title: 'CA1306: Definir localidade para tipos de dados | Microsoft Docs'
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
- CA1306
- SetLocaleForDataTypes
helpviewer_keywords:
- CA1306
- SetLocaleForDataTypes
ms.assetid: 104297b2-5806-4de0-a8d9-c589380a796c
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a089a26d4dfb10fc6017efbc422a8284fbfaf66d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825589"
---
# <a name="ca1306-set-locale-for-data-types"></a>CA1306: definir localidade para tipos de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SetLocaleForDataTypes|
|CheckId|CA1306|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método ou construtor criado um ou mais <xref:System.Data.DataTable?displayProperty=fullName> ou <xref:System.Data.DataSet?displayProperty=fullName> instâncias e não definir explicitamente a propriedade de localidade (<xref:System.Data.DataTable.Locale%2A?displayProperty=fullName> ou <xref:System.Data.DataSet.Locale%2A?displayProperty=fullName>).

## <a name="rule-description"></a>Descrição da Regra
 A localidade determina os elementos de apresentação específicos da cultura para dados, como a formatação usada para valores numéricos, símbolos de moeda e ordem de classificação. Quando você cria um <xref:System.Data.DataTable> ou <xref:System.Data.DataSet>, você deve definir explicitamente a localidade. Por padrão, a localidade para esses tipos é a cultura atual. Para dados que são armazenados em um arquivo ou banco de dados e são compartilhados globalmente, a localidade normalmente deve ser definida para a cultura invariável (<xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>). Quando dados são compartilhados entre culturas, usando a localidade padrão pode causar o conteúdo do <xref:System.Data.DataTable> ou <xref:System.Data.DataSet> ser apresentada ou interpretados incorretamente.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, definir explicitamente a localidade para o <xref:System.Data.DataTable> ou <xref:System.Data.DataSet>.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, quando o aplicativo ou biblioteca é para um público limitado de local, os dados não são compartilhados ou a configuração padrão produz o comportamento desejado em todos os cenários com suporte.

## <a name="example"></a>Exemplo
 O exemplo a seguir cria dois <xref:System.Data.DataTable> instâncias.

 [!code-csharp[FxCop.Globalization.DataTable#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.DataTable/cs/FxCop.Globalization.DataTable.cs#1)]

## <a name="see-also"></a>Consulte também
 <xref:System.Data.DataTable?displayProperty=fullName> <xref:System.Data.DataSet?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName>
 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>



