---
title: Comando Listar Registros
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.listregisters
helpviewer_keywords:
- list registers command
- Debug.ListRegisters command
- ListRegisters command
ms.assetid: 19a9d789-f6c9-46b3-b1f6-4934fc33e055
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ce91abde91edf989b33c476b042abaf16c685df0
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33704896"
---
# <a name="list-registers-command"></a>Comando Listar Registros
Exibe o valor dos registros selecionados e permite modificar a lista de registros a mostrar.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.ListRegisters [/Display [{register|registerGroup}...]] [/List]
[/Watch [{register|registerGroup}...]]
[/Unwatch [{register|registerGroup}...]]
```

## <a name="switches"></a>Opções
 /Display [{`register`&#124;`registerGroup`}...]

 Exibe os valores do `register` ou `registerGroup` especificado. Se nenhum `register` ou `registerGroup` for especificado, a lista padrão de registros será exibida. Se nenhuma opção for especificada, o comportamento será o mesmo. Por exemplo:

 `Debug.ListRegisters /Display eax`

 equivale a

 `Debug.ListRegisters eax`

 /List

 Exibe todos os grupos de registros na lista.

 /Watch [{`register`&#124;`registerGroup`}...]

 Adiciona um ou mais valores `register` ou `registerGroup` à lista.

 /Unwatch [{`register`&#124;`registerGroup`}...]

 Remove um ou mais valores `register` ou `registerGroup` da lista.

## <a name="remarks"></a>Comentários
 O alias `r` pode ser usado no lugar de `Debug.ListRegisters`.

## <a name="example"></a>Exemplo
 Este exemplo usa o alias `Debug.ListRegisters` `r` para exibir os valores do registro de grupo `Flags`.

```cmd
r /Display Flags
```

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Noções básicas sobre depuração: janela Registros](../../debugger/debugging-basics-registers-window.md)
- [Como usar a janela Registros](../../debugger/how-to-use-the-registers-window.md)