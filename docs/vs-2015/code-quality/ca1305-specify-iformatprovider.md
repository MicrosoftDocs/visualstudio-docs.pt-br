---
title: 'CA1305: Especificar IFormatProvider | Microsoft Docs'
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
- SpecifyIFormatProvider
- CA1305
helpviewer_keywords:
- CA1305
- SpecifyIFormatProvider
ms.assetid: fb34ed9a-4eab-47cc-8eef-3068a4a1397e
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 084fd28106a3ac5af9a40d46cf687d4982f53690
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49834281"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305: especificar IFormatProvider
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|SpecifyIFormatProvider|
|CheckId|CA1305|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método ou construtor chama um ou mais membros que têm sobrecargas que aceitam um <xref:System.IFormatProvider?displayProperty=fullName> parâmetro e o método ou construtor não chama a sobrecarga que utiliza o <xref:System.IFormatProvider> parâmetro. Essa regra ignora chamadas para [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] métodos que são documentados como ignorando o <xref:System.IFormatProvider> parâmetro e, além disso, os seguintes métodos:

-   <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

-   <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

-   <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da Regra
 Quando um <xref:System.Globalization.CultureInfo?displayProperty=fullName> ou <xref:System.IFormatProvider> objeto não for fornecido, o valor padrão fornecido pelo membro sobrecarregado pode não ter o efeito desejado em todas as localidades. Além disso, [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] membros escolhem a cultura padrão e a formatação com base em suposições que podem não estar corretas para seu código. Para certificar-se de que o código funciona conforme o esperado para seus cenários, você deve fornecer informações específicas da cultura acordo com as diretrizes a seguir:

- Se o valor será exibido ao usuário, use a cultura atual. Consulte <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>.

- Se o valor será armazenado e acessado pelo software (persistida em um arquivo ou banco de dados), use a cultura invariável. Consulte <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.

- Se você não souber o destino do valor, ter o consumidor de dados ou provedor de especificar a cultura.

  Observe que <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> é usado apenas para recuperar os recursos localizados por meio de uma instância da <xref:System.Resources.ResourceManager?displayProperty=fullName> classe.

  Mesmo se o comportamento padrão do membro sobrecarregado é apropriado para suas necessidades, é melhor chamar explicitamente a sobrecarga de específicas da cultura para que seu código seja autodocumentados e mais fácil manutenção.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, use a sobrecarga que utiliza um <xref:System.Globalization.CultureInfo> ou <xref:System.IFormatProvider> e especifique o argumento de acordo com as diretrizes que foram listados anteriormente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, quando você tiver certeza de que o provedor de formato de cultura/padrão é a escolha correta e em que a manutenção de código não é uma prioridade de desenvolvimento importantes.

## <a name="example"></a>Exemplo
 No exemplo a seguir, `BadMethod` faz com que as duas violações dessa regra. `GoodMethod` corrige a primeira violação, passando a cultura invariável para <xref:System.String.Compare%2A>e corrige a violação de segundo, passando a cultura atual como <xref:System.String.ToLower%2A> porque `string3` é exibida ao usuário.

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra o efeito da cultura atual em padrão <xref:System.IFormatProvider> que é selecionada pelo <xref:System.DateTime> tipo.

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **4/6/1900:12 12H15**
**04/06/1900 12:15:12**
## <a name="related-rules"></a>Regras relacionadas
 [CA1304: especificar CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>Consulte também
 [NIB: Usando a classe CultureInfo](http://msdn.microsoft.com/en-us/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)



