---
title: Comando Iniciar
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.start
helpviewer_keywords:
- Start command
- Debug.Start command
ms.assetid: dc4e4aa2-b0ab-4e00-92db-6dc3058ddc21
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bbd2d64d8103afe1e303052c9b27fc2cc85cab58
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33704688"
---
# <a name="start-command"></a>Comando Iniciar
Inicia a depuração do projeto de inicialização.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.Start [address]
```

## <a name="arguments"></a>Arguments
 `address`

 Opcional. O endereço no qual o programa suspende a execução, semelhante a um ponto de interrupção no código-fonte. Este argumento é válido apenas no modo de depuração.

## <a name="remarks"></a>Comentários
 O comando **Iniciar**, quando executado, executa uma operação RunToCursor para o endereço especificado.

## <a name="example"></a>Exemplo
 Este exemplo inicia o depurador e ignora todas as exceções que ocorrerem.

```cmd
>Debug.Start
```

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)