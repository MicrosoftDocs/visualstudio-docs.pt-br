---
title: Comando Listar Desmontagem
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.listdisassembly
helpviewer_keywords:
- Debug.ListDisassembly command
- list disassembly command
ms.assetid: eb363e35-e86a-4121-966f-991210c27e2a
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91319a8d25aaec6bdd676ed6d709dffc47100195
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770650"
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

## <a name="see-also"></a>Confira também

- [Comando listar pilha de chamadas](../../ide/reference/list-call-stack-command.md)
- [Comando listar threads](../../ide/reference/list-threads-command.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela de comando](../../ide/reference/command-window.md)
- [Caixa Localizar/comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)