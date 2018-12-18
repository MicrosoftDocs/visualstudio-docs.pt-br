---
title: Avisos de globalização
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- vs.codeanalysis.globalizationrules
helpviewer_keywords:
- warnings, globalization
- globalization warnings
- globalization [Visual Studio], warnings
- managed code analysis warnings, globalization warnings
ms.assetid: a8d12d41-14bf-4b43-af24-168312d7c390
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a5728116d6153b3397e4caf5b949b440772b8d3e
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47860298"
---
# <a name="globalization-warnings"></a>Avisos de globalização
Avisos de globalização dão suporte a aplicativos e bibliotecas do mundo.

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA1300: especificar MessageBoxOptions](../code-quality/ca1300-specify-messageboxoptions.md)|Para exibir corretamente uma caixa de mensagem para as culturas que usam uma ordem de leitura da direita para a esquerda, os membros RightAlign e RtlReading da enumeração MessageBoxOptions devem ser passados para o método Show.|
|[CA1301: evitar aceleradores duplicados](../code-quality/ca1301-avoid-duplicate-accelerators.md)|Uma tecla de acesso, também conhecida como acelerador, dá ao teclado acesso a um controle usando-se a tecla ALT. Quando vários controles têm teclas de acesso duplicadas, o comportamento da tecla de acesso não é bem definido.|
|[CA1302: não codificar cadeias de caracteres específicas da localidade](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md)|A enumeração System.Environment.SpecialFolder contém membros que fazem referência às pastas especiais do sistema. Os locais dessas pastas podem ter valores diferentes em diferentes sistemas operacionais; o usuário pode alterar alguns dos locais; e os locais são diferentes para cada linguagem. O método getfolderpath retorna os locais que estão associados com a enumeração SpecialFolder, localizada e apropriada para o computador em execução no momento.|
|[CA1303: não passar literais como parâmetros localizados](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|Um método visível externamente passa uma cadeia de caracteres literal como um parâmetro para um construtor ou método na biblioteca de classes do .NET Framework, e essa cadeia de caracteres deve ser localizável.|
|[CA1304: especificar CultureInfo](../code-quality/ca1304-specify-cultureinfo.md)|Um método ou um construtor chama um membro que tem uma sobrecarga que aceita um parâmetro System.Globalization.CultureInfo, e o método ou o construtor não chama a sobrecarga que utiliza o parâmetro CultureInfo. Quando um objeto CultureInfo ou System.IFormatProvider não for fornecido, o valor padrão fornecido pelo membro sobrecarregado poderá não ter o efeito desejado em todas as localidades.|
|[CA1305: especificar IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md)|Um método ou um construtor chama um ou mais membros que têm sobrecargas que aceitam um parâmetro System.IFormatProvider, e o método ou o construtor não chama a sobrecarga que utiliza o parâmetro IFormatProvider. Quando um objeto System.Globalization.CultureInfo ou System.IFormatProvider não for fornecido, o valor padrão fornecido pelo membro sobrecarregado poderá não ter o efeito desejado em todas as localidades.|
|[CA1306: definir localidade para tipos de dados](../code-quality/ca1306-set-locale-for-data-types.md)|A localidade determina os elementos de apresentação específicos da cultura para dados, como a formatação usada para valores numéricos, símbolos de moeda e ordem de classificação. Ao criar um DataTable ou um DataSet, você deve definir explicitamente a localidade.|
|[CA1307: especificar StringComparison](../code-quality/ca1307-specify-stringcomparison.md)|Uma operação de comparação de cadeia de caracteres usa uma sobrecarga de método que não define um parâmetro StringComparison.|
|[CA1308: normalizar cadeias de caracteres para maiúsculas](../code-quality/ca1308-normalize-strings-to-uppercase.md)|As cadeias de caracteres devem ser normalizadas em maiúsculas. Um pequeno grupo de caracteres não pode fazer uma viagem de ida e volta quando são convertidos em minúsculas.|
|[CA1309: usar StringComparison ordinal](../code-quality/ca1309-use-ordinal-stringcomparison.md)|Uma operação de comparação de cadeia de caracteres não linguística não define o parâmetro StringComparison como Ordinal ou OrdinalIgnoreCase. Definindo-se explicitamente o parâmetro como StringComparison.Ordinal ou StringComparison.OrdinalIgnoreCase, o código normalmente ganha velocidade, fica mais correto e se torna mais confiável.|
|[CA2101: especificar marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|Uma invocação de plataforma permite chamadores parcialmente confiáveis, o membro tem um parâmetro de cadeia de caracteres e não realizar marshaling explicitamente a cadeia de caracteres. Isso pode causar uma vulnerabilidade de segurança em potencial.|