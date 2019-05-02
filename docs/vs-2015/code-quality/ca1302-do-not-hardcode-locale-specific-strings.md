---
title: 'CA1302: Não codificar cadeias de caracteres específicas de localidade | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
helpviewer_keywords:
- DoNotHardcodeLocaleSpecificStrings
- CA1302
ms.assetid: 05ed134a-837d-43d7-bf97-906edeac44ce
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d52489ba25fe2c541d2d0329fcad61aef75350e9
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58921949"
---
# <a name="ca1302-do-not-hardcode-locale-specific-strings"></a>CA1302: Não embutir no código cadeias de caracteres específicas da localidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|DoNotHardcodeLocaleSpecificStrings|
|CheckId|CA1302|
|Categoria|Microsoft.Globalization|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Um método usa uma cadeia de caracteres literal que representa a parte do caminho de determinadas pastas do sistema.

## <a name="rule-description"></a>Descrição da Regra
 O <xref:System.Environment.SpecialFolder?displayProperty=fullName> enumeração contém membros que se referem a pastas especiais do sistema. Os locais dessas pastas podem ter valores diferentes em diferentes sistemas operacionais, o usuário pode alterar alguns dos locais e os locais são localizados. Um exemplo de uma pasta especial é a pasta do sistema, que é "C:\WINDOWS\system32" em [!INCLUDE[winxp](../includes/winxp-md.md)] mas "C:\WINNT\system32" em [!INCLUDE[win2kfamily](../includes/win2kfamily-md.md)]. O <xref:System.Environment.GetFolderPath%2A?displayProperty=fullName> método retorna os locais que estão associados a <xref:System.Environment.SpecialFolder> enumeração. Os locais que são retornados pelo <xref:System.Environment.GetFolderPath%2A> são localizados e apropriado para o computador em execução no momento.

 Essa regra cria tokens os caminhos de pasta são recuperados por meio de <xref:System.Environment.GetFolderPath%2A> método nos níveis de diretório separado. Cada literal de cadeia de caracteres é comparadas com os tokens. Se uma correspondência for encontrada, supõe-se que o método é criando uma cadeia de caracteres que aponta para o local do sistema que está associado com o token. Para portabilidade e a possibilidade de localização, use o <xref:System.Environment.GetFolderPath%2A> método para recuperar os locais das pastas especiais do sistema em vez de usar literais de cadeia de caracteres.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, recupere o local usando o <xref:System.Environment.GetFolderPath%2A> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o literal de cadeia de caracteres não é usado para se referir a um dos locais de sistema que está associado com o <xref:System.Environment.SpecialFolder> enumeração.

## <a name="example"></a>Exemplo
 O exemplo a seguir cria o caminho de pasta de dados de aplicativo comuns, que gera três avisos dessa regra. Em seguida, o exemplo recupera o caminho usando o <xref:System.Environment.GetFolderPath%2A> método.

 [!code-csharp[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/cs/FxCop.Globalization.HardcodedLocaleStrings.cs#1)]
 [!code-vb[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/vb/FxCop.Globalization.HardcodedLocaleStrings.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1303: Não passar literais como parâmetros localizados](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)
