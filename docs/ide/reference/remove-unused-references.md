---
title: Remover referências não utilizadas
description: Saiba como limpar as referências do projeto e os pacotes do NuGet que não têm uso com o novo comando remover referências não utilizadas.
ms.custom: SEO-VS-2021
ms.date: 06/01/2021
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 707769229ad7bc1864a135bade1df918d4b27847
ms.sourcegitcommit: f50bbdb15c4f9fca0fa245ca765183c378960cc5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/03/2021
ms.locfileid: "111352080"
---
# <a name="remove-unused-references"></a>Remover referências não utilizadas

Esta refatoração aplica-se a:

- C#
- Visual Basic

**O que:** Permite remover referências não utilizadas.

**Quando:** Você deseja limpar as referências do projeto e os pacotes do NuGet que não têm uso. 

**Por que:** A remoção de referências de projeto que não têm uso pode ajudar a economizar espaço e reduzir o tempo de inicialização do seu aplicativo, pois leva tempo para carregar cada módulo e evita que o compilador carregue os metadados que nunca serão usados.

## <a name="how-to"></a>Como fazer

1. Clique com o botão direito do mouse no nó nome ou dependências do projeto em Gerenciador de Soluções.

2. Selecione **remover referências não usadas**.

    ![Comando remover referências não utilizadas](media/remove-unused-references-command.png)

3. A caixa de diálogo **remover referências não utilizadas** abrirá exibindo referências que não têm uso no código-fonte. As referências não utilizadas serão previamente selecionadas para remoção com uma opção para preservar referências, selecionando `Keep` na lista suspensa ação.

    ![Caixa de diálogo remover referências não utilizadas](media/remove-unused-references-dialog.png)

5. Clique `Apply` para remover as referências selecionadas. 

## <a name="see-also"></a>Confira também

- [Refatoração](../refactoring-in-visual-studio.md)