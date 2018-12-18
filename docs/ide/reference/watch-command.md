---
title: Comando Inspecionar
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.watch
helpviewer_keywords:
- Watch command
- Debug.Watch command
ms.assetid: aa02e647-d9f5-4905-a651-52a8df595795
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f3226a81e748581cc96b62cb40600864fb9ac805
ms.sourcegitcommit: fe5a72bc4c291500f0bf4d6e0778107eb8c905f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2018
ms.locfileid: "33704454"
---
# <a name="watch-command"></a>Comando Inspecionar
Cria e abre uma instância especificada de uma janela **Inspeção**. Você pode usar uma janela **Inspeção** para calcular os valores de variáveis, expressões e registros, para editar esses valores e para salvar os resultados.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.Watch[index]
```

## <a name="arguments"></a>Arguments
 `index`

 Necessário. O número de instância da janela Inspeção.

## <a name="remarks"></a>Comentários
 O `index` deve ser um inteiro. Os valores válidos são 1, 2, 3 ou 4.

## <a name="example"></a>Exemplo

```cmd
>Debug.Watch1
```

## <a name="see-also"></a>Consulte também

- [Janelas Autos e Locais](../../debugger/autos-and-locals-windows.md)
- [Definir uma inspeção nas variáveis usando as janelas Inspeção e QuickWatch no Visual Studio](../../debugger/watch-and-quickwatch-windows.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)