---
title: Comando Ativar/Desativar Ponto de Interrupção
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.togglebreakpoint
helpviewer_keywords:
- ToggleBreakpoint command
- Debug.ToggleBreakPoint command
- Toggle Breakpoint command
ms.assetid: d50dfadb-ce79-4d5e-9c09-1cfddd57876d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 14f4d60bcbf7c7f394d62cc881c78ef9aa51e545
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31946800"
---
# <a name="toggle-breakpoint-command"></a>Comando Ativar/Desativar Ponto de Interrupção
Ativa ou desativa o ponto de interrupção dependendo de seu estado atual, no local atual do arquivo.

## <a name="syntax"></a>Sintaxe

```
Debug.ToggleBreakpoint [text]
```

## <a name="arguments"></a>Arguments
 `text` Opcional. Se o texto for especificado, a linha será marcada como um ponto de interrupção nomeado. Caso contrário, a linha será marcada como um ponto de interrupção sem nome, semelhante ao que acontece quando você pressiona F9.

## <a name="example"></a>Exemplo
 O exemplo a seguir ativa/desativa o ponto de interrupção atual.

```
>Debug.ToggleBreakpoint
```

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)