---
title: Comando Listar Desmontagem
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- debug.listdisassembly
helpviewer_keywords:
- Debug.ListDisassembly command
- list disassembly command
ms.assetid: eb363e35-e86a-4121-966f-991210c27e2a
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6b175c6b7e0fcd145d58318d89707cfd907acb2c
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53913358"
---
# <a name="list-disassembly-command"></a>Comando Listar Desmontagem
Inicia o processo de depuração e permite que você especifique como os erros são tratados.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.ListDisassembly [/count:number] [/endaddress:expression]
[/codebytes:yes|no] [/source:yes|no] [/symbolnames:yes|no]
[/linenumbers:yes|no]
```

## <a name="switches"></a>Opções
 Cada opção pode ser invocada usando sua forma completa ou abreviada.

 /count: `number` [ou] /c: `number` [ou] /length: `number` [ou] /l: `number`

 Opcional. Número de instruções a serem exibidas. O valor padrão é 8.

 /endaddress: `expression` [ou] /e: `expression`

 Opcional. Endereço no qual interromper a desmontagem.

 /codebytes:`yes`&#124;`no` [ou] /bytes:`yes`&#124;`no` [ou] /b:`yes`&#124;`no`

 Opcional. Indica se deve você deseja exibir bytes de código. O valor padrão é `no`.

 /source:`yes`&#124;`no` [ou] /s:`yes`&#124;`no`

 Opcional. Indica se deve você deseja exibir o código-fonte. O valor padrão é `no`.

 /symbolnames:`yes`&#124;`no` [ou] /names:`yes`&#124;`no` [ou] /n:`yes`&#124;`no`

 Opcional. Indica se deve você deseja exibir os nomes de símbolos. O valor padrão é `yes`.

 [/linenumbers:`yes`&#124;`no`]

 Opcional. Habilita a exibição de números de linha associados ao código-fonte. A opção /source deve ter um valor de `yes` para usar a opção /linenumbers.

## <a name="example"></a>Exemplo

```cmd
>Debug.ListDisassembly
```

## <a name="see-also"></a>Consulte também

- [Comando List Call Stack](../../ide/reference/list-call-stack-command.md)
- [Comando List Threads](../../ide/reference/list-threads-command.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)