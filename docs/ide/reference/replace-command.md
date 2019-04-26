---
title: Comando Substituir
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.replace
helpviewer_keywords:
- Edit.Replace command
- Replace command
ms.assetid: a15767f1-5a3d-44f5-8c77-7b0f1157f340
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3de5b1b5add1337451d7b6a463c89951754e3581
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62956406"
---
# <a name="replace-command"></a>Comando Substituir
Substitui texto em arquivos usando um subconjunto das opções disponíveis na guia **Substituir nos Arquivos** da janela **Localizar e Substituir**.

## <a name="syntax"></a>Sintaxe

```
Edit.Replace findwhat replacewith [/all] [/case]
[/doc|/proc|/open|/sel] [/hidden] [/options] [/reset] [/up]
[/wild|/regex] [/word]
```

## <a name="arguments"></a>Arguments
 `findwhat`

 Necessário. O texto a ser correspondido.

 `replacewith`

 Necessário. O texto a ser substituído pelo texto correspondido.

## <a name="switches"></a>Opções
 /all ou /a

 Opcional. Substitui todas as ocorrências do texto da pesquisa pelo texto de substituição.

 /case ou /c

 Opcional. As correspondências ocorrerão somente se os caracteres maiúsculos e minúsculos corresponderem exatamente aos especificados no argumento `findwhat`.

 /doc ou /d

 Opcional. Pesquisa apenas o documento atual. Especifique apenas um dos escopos de pesquisa disponíveis, `/doc`, `/proc`, `/open` ou `/sel`.

 /hidden ou /h

 Opcional. Pesquisa texto oculto e recolhido, como os metadados de um controle DTC, uma região oculta de um documento com estrutura de tópicos ou uma classe ou método recolhido.

 /open ou /o

 Opcional. Pesquisa todos os documentos abertos como se fossem um documento. Especifique apenas um dos escopos de pesquisa disponíveis, `/doc`, `/proc`, `/open` ou `/sel`.

 /options ou /t

 Opcional. Exibe uma lista das configurações atuais da opção de localização e não realiza uma pesquisa.

 /proc ou /p

 Opcional. Pesquisa apenas o procedimento atual. Especifique apenas um dos escopos de pesquisa disponíveis, `/doc`, `/proc`, `/open` ou `/sel`.

 /regex ou /r

 Opcional. Usa caracteres especiais predefinidos no argumento `findwhat` como notações que representam padrões de texto, em vez de caracteres literais. Para obter uma lista completa de caracteres de expressão regular, consulte [Expressões Regulares](../../ide/using-regular-expressions-in-visual-studio.md).

 /reset ou /e

 Opcional. Retorna as opções de localização para suas configurações padrão e não realiza uma pesquisa.

 /sel ou /s

 Opcional. Pesquisa apenas a seleção atual. Especifique apenas um dos escopos de pesquisa disponíveis, `/doc`, `/proc`, `/open` ou `/sel`.

 /up ou /u

 Opcional. Pesquisa desde o local atual em um arquivo até o topo do arquivo. Por padrão, as pesquisas têm início no local atual no arquivo e vão até a parte inferior do arquivo.

 /wild ou /l

 Opcional. Usa caracteres especiais predefinidos no argumento `findwhat` como notações para representar um caractere ou uma sequência de caracteres.

 /word ou /w

 Opcional. Pesquisa somente palavras inteiras.

## <a name="example"></a>Exemplo
 Este exemplo substitui `btnSend` por `btnSubmit` em todos os documentos abertos.

```
>Edit.Replace btnSend btnSubmit /open
```

## <a name="see-also"></a>Consulte também

- [Localizando e substituindo texto](../../ide/finding-and-replacing-text.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)