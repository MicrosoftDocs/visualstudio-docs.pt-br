---
title: 'CA1305: especificar IFormatProvider | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- SpecifyIFormatProvider
- CA1305
helpviewer_keywords:
- CA1305
- SpecifyIFormatProvider
ms.assetid: fb34ed9a-4eab-47cc-8eef-3068a4a1397e
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 025d76f8e946dd3021141d6736c6b4bd40d57170
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539080"
---
# <a name="ca1305-specify-iformatprovider"></a>CA1305: Especificar IFormatProvider
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|SpecifyIFormatProvider|
|CheckId|CA1305|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método ou construtor chama um ou mais membros que têm sobrecargas que aceitam um <xref:System.IFormatProvider?displayProperty=fullName> parâmetro e o método ou construtor não chama a sobrecarga que usa o <xref:System.IFormatProvider> parâmetro. Essa regra ignora as chamadas para [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] métodos documentados como ignorar o <xref:System.IFormatProvider> parâmetro e, além disso, os seguintes métodos:

- <xref:System.Activator.CreateInstance%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetObject%2A?displayProperty=fullName>

- <xref:System.Resources.ResourceManager.GetString%2A?displayProperty=fullName>

## <a name="rule-description"></a>Descrição da Regra
 Quando um <xref:System.Globalization.CultureInfo?displayProperty=fullName> <xref:System.IFormatProvider> objeto ou não é fornecido, o valor padrão fornecido pelo membro sobrecarregado pode não ter o efeito desejado em todas as localidades. Além disso, [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] os membros escolhem a cultura e a formatação padrão com base nas suposições que podem não estar corretas para o seu código. Para garantir que o código funcione conforme o esperado para seus cenários, você deve fornecer informações específicas de cultura de acordo com as seguintes diretrizes:

- Se o valor for exibido para o usuário, use a cultura atual. Consulte <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName>.

- Se o valor for armazenado e acessado pelo software (persistido em um arquivo ou banco de dados), use a cultura invariável. Consulte <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>.

- Se você não souber o destino do valor, faça com que o consumidor ou o provedor de dados especifique a cultura.

  Observe que <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> é usado somente para recuperar recursos localizados usando uma instância da <xref:System.Resources.ResourceManager?displayProperty=fullName> classe.

  Mesmo que o comportamento padrão do membro sobrecarregado seja apropriado para suas necessidades, é melhor chamar explicitamente a sobrecarga específica da cultura para que seu código seja autodocumentado e mais facilmente mantido.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, use a sobrecarga que usa um <xref:System.Globalization.CultureInfo> ou <xref:System.IFormatProvider> e especifique o argumento de acordo com as diretrizes listadas anteriormente.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra quando tiver certeza de que o provedor padrão de cultura/formato é a opção correta e onde a manutenção do código não é uma prioridade de desenvolvimento importante.

## <a name="example"></a>Exemplo
 No exemplo a seguir, `BadMethod` causa duas violações dessa regra. `GoodMethod`corrige a primeira violação passando a cultura invariável para <xref:System.String.Compare%2A> e corrige a segunda violação passando a cultura atual para <xref:System.String.ToLower%2A> porque `string3` é exibido para o usuário.

 [!code-csharp[FxCop.Globalization.CultureInfo#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.CultureInfo/cs/FxCop.Globalization.CultureInfo.cs#1)]

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra o efeito da cultura atual no padrão <xref:System.IFormatProvider> selecionado pelo <xref:System.DateTime> tipo.

 [!code-csharp[FxCop.Globalization.IFormatProvider#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.IFormatProvider/cs/FxCop.Globalization.IFormatProvider.cs#1)]

 Este exemplo gerencia a seguinte saída.

 **6/4/1900 12:15:12 PM** 
 **06/04/1900 12:15:12**
## <a name="related-rules"></a>Regras relacionadas
 [CA1304: Especificar CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)

## <a name="see-also"></a>Consulte Também
 [NIB: usando a classe CultureInfo](https://msdn.microsoft.com/d4329e34-64c3-4d1e-8c73-5b0ee626ba7a)
