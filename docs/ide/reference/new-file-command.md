---
title: Comando Novo Arquivo
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- file.newfile
helpviewer_keywords:
- File.NewFile command
- New File command
ms.assetid: 767868d6-a525-425b-a43b-2198f636ab6b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8b4d68f53343b2523347f89977fe2bd602d64742
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39179951"
---
# <a name="new-file-command"></a>Comando Novo Arquivo
Cria um novo arquivo e abre-o. O arquivo aparece na pasta Arquivos Diversos.

## <a name="syntax"></a>Sintaxe

```cmd
File.NewFile [filename] [/t:templatename] [/editor:editorname]
```

## <a name="arguments"></a>Arguments
 `filename`

 Opcional. Nome para o arquivo. Se nenhum nome for fornecido, será fornecido um nome padrão. Se nenhum nome de modelo for listado, será criado um arquivo de texto.

## <a name="switches"></a>Opções
 /t:`templatename`

 Opcional. Especifica o tipo de arquivo a ser criado.

 A sintaxe do argumento /t:`templatename` espelha as informações encontradas na Caixa de Diálogo Novo Arquivo. Insira o nome da categoria seguido por uma barra invertida (`\`) e o nome do modelo e coloque toda a cadeia de caracteres entre aspas.

 Por exemplo, para criar um novo arquivo de origem [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)], você inseriria o seguinte para o argumento /t:`templatename`.

```cmd
/t:"Visual C++\C++ File (.cpp)"
```

 O exemplo acima indica que o modelo de Arquivo C++ está localizado na categoria no Visual C++ na caixa de diálogo **Novo Arquivo**.

 /e:`editorname`

 Opcional. Nome do editor no qual o arquivo será aberto. Se o argumento for especificado, mas nenhum nome de editor for fornecido, a caixa de diálogo **Abrir com** será exibida.

 A sintaxe do argumento /e:`editorname` usa os nomes de editor como eles são exibidos na Caixa de Diálogo Abrir com, entre aspas.

 Por exemplo, para abrir um arquivo no editor de código-fonte, insira o seguinte para o argumento /e:`editorname`.

```cmd
/e:"Source Code (text) Editor"
```

## <a name="example"></a>Exemplo
 Este exemplo cria uma nova página da Web "test1.htm" e abre-a no editor de código-fonte.

```cmd
>File.NewFile test1 /t:"General\HTML Page" /e:"Source Code (text) Editor"
```

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Janela Imediata](../../ide/reference/immediate-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)