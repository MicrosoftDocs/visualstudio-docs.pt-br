---
title: Mover o tipo para refatoração de arquivo correspondente no Visual Studio
ms.date: 01/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 73e1d9d67d905fed5eb37e29c1be1ba7677da3e8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49884141"
---
# <a name="move-a-type-to-a-matching-file-refactoring"></a>Refatoração Mover um tipo para um arquivo correspondente

Esta refatoração aplica-se a:

- C#

- Visual Basic

**O quê:** permite mover o tipo selecionado para um arquivo separado com o mesmo nome.

**Quando:** você tem várias classes, structs, interfaces, etc. no mesmo arquivo que deseja separar.

**Por quê:** colocar vários tipos no mesmo arquivo pode dificultar a localização desses tipos. Ao mover os tipos de arquivos com o mesmo nome, o código torna-se mais legível e mais fácil de navegar.

## <a name="how-to"></a>Como fazer

1. Coloque o cursor dentro do nome do tipo de onde ele está definido. Por exemplo:

   ```csharp
   class Person
   ```

   ```vb
   Class Person
   ```

2. Depois, siga um destes procedimentos:

   - Pressione **Ctrl**+**.**
   - Clique com o botão direito do mouse sobre o nome do tipo e selecione **Ação Rápidas e Refatorações**

1. Selecione **Mover tipo para *NomeDoTipo*.cs** no menu, em que *NomeDoTipo* é o nome do tipo selecionado.

   O tipo é movido para um novo arquivo no projeto que possui o mesmo nome do tipo.

   - C#:

      ![Resultado embutido – C#](media/movetype-result-cs.png)

   - Visual Basic:

      ![Resultado embutido – Visual Basic](media/movetype-result-vb.png)

## <a name="see-also"></a>Consulte também

- [Refatoração](../refactoring-in-visual-studio.md)
