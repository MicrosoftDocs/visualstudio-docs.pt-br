---
title: Comentar o código
description: Este artigo descreve como usar comentários no editor de código-fonte do Visual Studio para Mac
author: conceptdev
ms.author: crdun
ms.date: 05/06/2018
ms.assetid: 0FE5E929-1846-4F48-B5E3-70990FAF9504
ms.openlocfilehash: 1f792e5ba670854e4a3a9ce703212d18c16e5512
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295651"
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

## <a name="see-also"></a>Consulte também

- [Comentar o código (Visual Studio no Windows)](/visualstudio/ide/quickstart-editor#comment-out-code)