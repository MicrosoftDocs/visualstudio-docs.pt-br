---
title: Comentar o código
description: Este artigo descreve como usar comentários no editor de código-fonte do Visual Studio para Mac
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.topic: how-to
ms.openlocfilehash: 44eee75b4803b4317bb7d3cd02cb19b55f41a067
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85949993"
---
# <a name="comments"></a>Comentários

Ao depurar ou fazer experimentos no código, pode ser útil comentar blocos de código temporariamente ou a longo prazo.

Para comentar um bloco inteiro de código:

* Selecione o código e escolha **Ativar/desativar comentários da linha** no menu de contexto

OU

* Use a associação de tela `cmd + /` no código selecionado.

Esses métodos podem ser usados para comentar ou remover a marca de comentário de partes do código. Em arquivos de C#, níveis adicionais de comentários de linha podem ser adicionados, permitindo que regiões de códigos sejam comentadas e a marca de comentário seja removida, preservando ainda os comentários reais:

![comentários de vários níveis](media/source-editor-image8.png)

Comentários também são úteis para documentar código para futuros desenvolvedores poderão vir a interagir com ele. Isso geralmente é feito na forma de comentário de várias linhas, que são adicionados da seguinte maneira em cada linguagem:

**C#**

```csharp
/*
 This is a multi-line
 comment in C#
*/
```

**F#**

```fsharp
(*
 This is a multi-line
  comment in F#
*)
```

## <a name="see-also"></a>Veja também

- [Comentar o código (Visual Studio no Windows)](/visualstudio/ide/quickstart-editor#comment-out-code)