---
title: Usar expressões regulares no Visual Studio
ms.date: 03/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vsregularexpressionhelp
- vs.regularexpressionhelp
- vs.wildcardsbuilder
- vs.netregularexpressionhelp
- vs.wildcards
helpviewer_keywords:
- regular expressions [Visual Studio]
- regular expressions
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bef854fd04ce8ac2ddf6fe834b3bede0f371eefe
ms.sourcegitcommit: 12d6398c02e818de4fbcb4371bae9e5db6cf9509
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050294"
---
# <a name="use-regular-expressions-in-visual-studio"></a>Usar expressões regulares no Visual Studio

O Visual Studio usa [expressões regulares do .NET Framework](/dotnet/standard/base-types/regular-expressions) para localizar e substituir texto.

## <a name="replacement-patterns"></a>Padrões de substituição

Para usar um grupo de captura numerado, coloque o grupo entre parênteses no padrão de expressão regular. Use `$number`, em que `number` é um inteiro começando em 1, para especificar um grupo numerado específico em um padrão de substituição. Por exemplo, a expressão regular agrupada `(\d)([a-z])` define dois grupos: o primeiro grupo contém um único dígito decimal e o segundo grupo contém um único caractere entre **a** e **z**. A expressão localiza quatro correspondências na cadeia de caracteres a seguir: **1a 2b 3c 4d**. A cadeia de caracteres de substituição `z$1` referencia somente o primeiro grupo e converte a cadeia de caracteres em **z1 z2 z3 z4**.

Para obter informações sobre as expressões regulares usadas em padrões de substituição, consulte [Substituições em expressões regulares (guia do .NET)](/dotnet/standard/base-types/substitutions-in-regular-expressions).

## <a name="regular-expression-examples"></a>Exemplos de expressões regulares

Estes são alguns exemplos:

|Finalidade|Expressão|Exemplo|
|-------------|----------------|-------------|
|Encontrar a correspondência de um único caractere (exceto uma quebra de linha)|.|`a.o` corresponde a “aro” em “around” e “abo” em “about”, mas a não “acro” em “across”.|
|Encontrar a correspondência de zero ou mais ocorrências da expressão anterior (encontrar a correspondência do máximo de caracteres possíveis)|*|`a*r` corresponde a “r” em “rack”, “ar” em “ark” e “aar” em “aardvark”|
|Encontrar a correspondência de um caractere zero ou mais vezes (Curinga *)|.*|`c.*e` corresponde a "cke" em "racket", "comme" em "comment" e "code" em "code"|
|Encontrar a correspondência de uma ou mais ocorrências da expressão anterior (encontrar a correspondência do máximo de caracteres possíveis)|+|`e.+d` corresponde a "eed" em "feeder", mas não a "ed".|
|Encontrar a correspondência de um caractere uma ou mais vezes (Curinga ?)|.+|`e.+e` corresponde a “eede” em “feeder”, mas não a “ee”.|
|Encontrar a correspondência de zero ou mais ocorrências da expressão anterior (encontrar a correspondência do mínimo de caracteres possíveis)|*?|`e.*?e` corresponde a “ee” em “feeder”, mas não a “eede”.|
|Encontrar a correspondência de uma ou mais ocorrências da expressão anterior (encontrar a correspondência do mínimo de caracteres possíveis)|+?|`e.+?e` corresponde a “ente” e “erprise” em “enterprise”, mas não à palavra inteira “enterprise”.|
|Ancorar a cadeia de caracteres de correspondência ao início de uma linha ou uma cadeia de caracteres|^|`^car` corresponde à palavra “car” somente quando ela aparece no início de uma linha.|
|Ancorar a cadeia de caracteres de correspondência ao final de uma linha|\r?$|`end\r?$` corresponde a “end” somente quando aparece no final de uma linha.|
|Ancorar a cadeia de caracteres de correspondência ao final do arquivo|$|`end$` corresponde a "end" somente quando aparece no final do arquivo.|
|Encontrar a correspondência de um único caractere em um conjunto|[abc]|`b[abc]` corresponde a “ba”, “bb” e “bc”.|
|Encontrar a correspondência de um caractere em um intervalo de caracteres|[a-f]|`be[n-t]` corresponde a “bet” em “between”, “ben” em “beneath” e “bes” em “beside”, mas não a “below”.|
|Capturar e numerar implicitamente a expressão contida entre parênteses|()|`([a-z])X\1` corresponde a “aXa” e “bXb”, mas não a “aXb”. “\1” se refere ao primeiro grupo de expressão “[a-z]”.|
|Invalidar uma correspondência|(?!abc)|`real(?!ity)` corresponde a “real” em “realty” e “really”, mas não a “reality”. Também encontra o segundo “real” (mas não o primeiro “real”) em “realityreal”.|
|Encontrar a correspondência de um caractere que não está em um conjunto de caracteres específico|[^abc]|`be[^n-t]` corresponde a “bef” em “before”, “beh” em “behind” e “bel” em “below”, mas não a “beneath”.|
|Encontrar a correspondência da expressão antes ou depois do símbolo.|&#124;|`(sponge\|mud) bath` corresponde a “sponge bath” e a “mud bath”.|
|Escapa o caractere após a barra invertida| \\ |`\^` corresponde ao caractere ^.|
|Especificar o número de ocorrências do caractere ou do grupo anterior|{x}, em que x é o número de ocorrências|`x(ab){2}x` corresponde a “xababx”, e `x(ab){2,3}x` corresponde a “xababx” e “xabababx”, mas não a “xababababx”.|
|Corresponder ao texto em uma classe de caractere Unicode. Para obter mais informações sobre classes de caracteres Unicode, consulte<br /><br /> [Propriedades de caracteres Unicode Standard 5.2](http://www.unicode.org/versions/Unicode5.2.0/ch04.pdf).|\p{X}, em que "X" é o número Unicode.|`\p{Lu}` corresponde a “T” e “D” em “Thomas Doe”.|
|Encontrar a correspondência de um limite de palavra|\b (fora de uma classe de caractere, `\b` especifica um limite de palavra e, dentro de uma classe de caractere, `\b` especifica um backspace.)|`\bin` corresponde a “in” em “inside”, mas não em “pintor”.|
|Encontrar a correspondência de uma quebra de linha (isto é, um retorno de carro seguido por uma nova linha).|\r?\n|`End\r?\nBegin` corresponde a “End” e “Begin” somente quando “End” é a última cadeia de caracteres em uma linha e “Begin” é a primeira cadeia de caracteres na próxima linha.|
|Encontrar a correspondência de um caractere alfanumérico|\w|`a\wd` corresponde a “add” e “a1d”, mas não a “a d”.|
|Encontrar a correspondência de um caractere de espaço em branco.|(?([^\r\n])\s)|`Public\sInterface` corresponde à frase “Public Interface”.|
|Encontrar a correspondência de um caractere numérico|\d|`\d` corresponde a “3” em “3456”, “2” em “23” e “1” em “1”.|
|Encontrar a correspondência de um caractere Unicode|\uXXXX em que XXXX especifica o valor do caractere Unicode.|`\u0065` corresponde ao caractere “e”.|
|Encontrar a correspondência de um identificador|\b[\_\w-[0-9]][\_\w]*\b|Corresponde a "type1", mas não a "&type1" nem "#define".|
|Encontrar a correspondência de uma cadeia de caracteres entre aspas|((\\".+?\\")&#124;('.+?'))|Encontrar a correspondência de uma cadeia de caracteres entre aspas simples ou duplas.|
|Encontrar a correspondência de um número hexadecimal|\b0[xX]([0-9a-fA-F]\)\b|Corresponde a “0xc67f”, mas não a “0xc67fc67f”.|
|Encontrar a correspondência de inteiros e decimais|\b[0-9]*\\.\*[0-9]+\b|Encontrar a correspondência de “1.333”.|

> [!TIP]
> Em sistemas operacionais Windows, a maioria das linhas termina em “\r\n” (um retorno de carro seguido por uma nova linha). Esses caracteres não são visíveis, mas estão presentes no editor e são passados para o serviço de expressão regular do .NET.

## <a name="see-also"></a>Consulte também

- [Localizar e substituir texto](../ide/finding-and-replacing-text.md)
