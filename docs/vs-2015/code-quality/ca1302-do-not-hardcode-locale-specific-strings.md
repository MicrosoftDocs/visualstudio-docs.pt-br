---
title: 'CA1302: não codificar Cadeias de caracteres específicas de localidade | Microsoft Docs'
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 18da0471b1ac62f0e61b303c60b46c15cdc2e428
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85539003"
---
# <a name="ca1302-do-not-hardcode-locale-specific-strings"></a>CA1302: Não embutir no código cadeias de caracteres específicas da localidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotHardcodeLocaleSpecificStrings|
|CheckId|CA1302|
|Categoria|Microsoft. Globalization|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método usa um literal de cadeia de caracteres que representa parte do caminho de determinadas pastas do sistema.

## <a name="rule-description"></a>Descrição da Regra
 A <xref:System.Environment.SpecialFolder?displayProperty=fullName> enumeração contém membros que se referem a pastas especiais do sistema. Os locais dessas pastas podem ter valores diferentes em sistemas operacionais diferentes, o usuário pode alterar alguns dos locais e os locais são localizados. Um exemplo de uma pasta especial é a pasta do sistema, que é "C:\WINDOWS\system32" em [!INCLUDE[winxp](../includes/winxp-md.md)] , mas "C:\winnt\system32" em [!INCLUDE[win2kfamily](../includes/win2kfamily-md.md)] . O <xref:System.Environment.GetFolderPath%2A?displayProperty=fullName> método retorna os locais associados à <xref:System.Environment.SpecialFolder> enumeração. Os locais retornados pelo <xref:System.Environment.GetFolderPath%2A> são localizados e apropriados para o computador em execução no momento.

 Essa regra cria tokens os caminhos de pasta que são recuperados usando o <xref:System.Environment.GetFolderPath%2A> método em níveis de diretório separados. Cada literal de cadeia de caracteres é comparado aos tokens. Se uma correspondência for encontrada, supõe-se que o método está criando uma cadeia de caracteres que se refere ao local do sistema que está associado ao token. Para portabilidade e possibilidade de localização, use o <xref:System.Environment.GetFolderPath%2A> método para recuperar os locais das pastas especiais do sistema em vez de usar literais de cadeia de caracteres.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, recupere o local usando o <xref:System.Environment.GetFolderPath%2A> método.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o literal da cadeia de caracteres não for usado para fazer referência a um dos locais do sistema que está associado à <xref:System.Environment.SpecialFolder> enumeração.

## <a name="example"></a>Exemplo
 O exemplo a seguir cria o caminho da pasta Common Application Data, que gera três avisos dessa regra. Em seguida, o exemplo recupera o caminho usando o <xref:System.Environment.GetFolderPath%2A> método.

 [!code-csharp[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/cs/FxCop.Globalization.HardcodedLocaleStrings.cs#1)]
 [!code-vb[FxCop.Globalization.HardcodedLocaleStrings#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Globalization.HardcodedLocaleStrings/vb/FxCop.Globalization.HardcodedLocaleStrings.vb#1)]

## <a name="related-rules"></a>Regras relacionadas
 [CA1303: Não passar literais como parâmetros localizados](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)
