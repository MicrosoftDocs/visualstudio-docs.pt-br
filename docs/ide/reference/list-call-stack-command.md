---
title: Comando Listar Pilha de Chamadas
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listcallstack
helpviewer_keywords:
- list call stack command
- Debug.ListCallStack command
ms.assetid: a8b20bf2-81d2-4069-aea8-23e6b15b4347
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 34de768f41079311505ae7948502bb4356814ec7
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770688"
---
# <a name="list-call-stack-command"></a>Comando Listar Pilha de Chamadas
Exibe a pilha de chamadas atual.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.ListCallStack [/Count:number] [/ShowTypes:yes|no]
[/ShowNames:yes|no] [/ShowValues:yes|no] [/ShowModule:yes|no]
[/ShowLineOffset:yes|no] [/ShowByteOffset:yes|no]
[/ShowLanguage:yes|no] [/IncludeCallsAcrossThreads:yes|no]
[/ShowExternalCode:yes|no] [Thread:n] [index]
```

## <a name="arguments"></a>Argumentos

`index`\
Opcional. Define o registro de ativação atual e não exibe nenhuma saída.

## <a name="switches"></a>Opções
Cada opção pode ser invocada usando sua forma completa ou abreviada.

/Count:`number` [ou] /C:`number`

Opcional. Número máximo de pilhas de chamadas a exibir. O valor padrão é ilimitado.

/ShowTypes:`yes`&#124;`no` [ou] /T:`yes`&#124;`no`

Opcional. Especifica se deve tipos de parâmetro devem ser exibidos. O valor padrão é `yes`.

/ShowNames:`yes`&#124;`no` [ou] /N:`yes`&#124;`no`

Opcional. Especifica se nomes de parâmetro devem ser exibidos. O valor padrão é `yes`.

/ShowValues:`yes`&#124;`no` [ou] /V:`yes`&#124;`no`

Opcional. Especifica se valores de parâmetro devem ser exibidos. O valor padrão é `yes`.

/ShowModule:`yes`&#124;`no` [ou] /M:`yes`&#124;`no`

Opcional. Especifica se deve o nome do módulo deve ser exibido. O valor padrão é `yes`.

/ShowLineOffset:`yes`&#124;`no` [ou] /#:`yes`&#124;`no`

Opcional. Especifica se o deslocamento de linha deve ser exibido. O valor padrão é `no`.

/ShowByteOffset:`yes`&#124;`no` [ou] /B:`yes`&#124;`no`

Opcional. Especifica se o deslocamento de byte deve ser exibido. O valor padrão é `no`.

/ShowLanguage:`yes`&#124;`no` [ou] /L:`yes`&#124;`no`

Opcional. Especifica se o idioma deve ser exibido. O valor padrão é `no`.

/IncludeCallsAcrossThreads:`yes`&#124;`no` [ou] /I:`yes`&#124;`no`

Opcional. Especifica se chamadas de ou para outros threads devem ser incluídas. O valor padrão é `no`.

/ShowExternalCode:`yes`&#124;`no`

Opcional. Especifica se Apenas Meu Código deve ser exibido para a pilha de chamadas. Quando Apenas Meu Código está desativado, todo o código não do usuário é exibido. Quando Apenas Meu Código está ativado, o código não do usuário é exibido como `[external]` na saída da pilha de chamadas.

Thread:`n`

Opcional. exibe a pilha de chamadas para o thread `n`. Se nenhum thread for especificado, exibirá a pilha de chamadas do thread atual.

## <a name="remarks"></a>Comentários
As alterações feitas a argumentos ou opções aplicam-se a invocações futuras desse comando. Se você emitir Debug.ListCallStackby em si, toda a pilha de chamadas será exibida. Se você especificar um índice, por exemplo,

```cmd
Debug.ListCallStack 2
```

o registro de ativação atual será definido como aquele quadro (neste caso, o segundo quadro).

Você também pode escrever esse comando usando seu alias predefinido, kb. Por exemplo, você pode inserir

```cmd
kb 2
```

para definir o registro de ativação atual para o segundo quadro.

## <a name="example"></a>Exemplo

```cmd
>Debug.CallStack /Count:4 /ShowTypes:yes
```

## <a name="see-also"></a>Confira também

- [Comando listar desmontagem](../../ide/reference/list-disassembly-command.md)
- [Comando listar threads](../../ide/reference/list-threads-command.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela de comando](../../ide/reference/command-window.md)
- [Caixa Localizar/comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)