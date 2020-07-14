---
title: 'Como: Compilar várias configurações'
ms.date: 05/13/2020
ms.technology: vs-ide-compile
ms.topic: how-to
ms.assetid: ba830937-3317-4674-8cc2-c0cd565603c5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d7820d56bcb266e8361f36cb5350475f31445800
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284756"
---
# <a name="how-to-build-multiple-configurations-in-a-single-build-request"></a>Como: Compilar várias configurações em uma única solicitação de compilação

Você pode criar a maioria dos tipos de projetos com várias ou até mesmo todas as suas configurações de compilação com uma ação do IDE usando a caixa de diálogo **Build do lote** . No entanto, não é possível compilar os seguintes tipos de projetos em várias configurações de build ao mesmo tempo:

1. Aplicativos [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] criados para Windows usando JavaScript.

2. Todos os projetos do Visual Basic.

3. Projetos de CMake.

Se uma solução contiver qualquer projeto desses dois tipos de projeto, a **compilação em lote** não estará disponível para essa solução. Nesse caso, o comando não aparece no menu **Compilar** .

   Para obter mais informações sobre configurações de build, consulte [Noções básicas sobre configurações de build](../ide/understanding-build-configurations.md).

## <a name="to-build-a-project-in-multiple-build-configurations"></a>Para compilar um projeto em várias configurações de build

1. Na barra de menus, escolha **criar**  >  **Build do lote**. Ou pressione **Ctrl** + **Q** para abrir a caixa de pesquisa e pesquise `Batch Build` .

2. Na coluna **Build**, marque as caixas de seleção para as configurações com as quais você deseja compilar um projeto.

    > [!TIP]
    > Para editar ou criar uma configuração de compilação para uma solução, escolha **criar**  >  **Configuration Manager** na barra de menus para abrir a caixa de diálogo **Configuration Manager** . Depois de editar uma configuração de build para uma solução, escolha o botão **Recompilar** na caixa de diálogo **Build em Lotes** para atualizar todas as configurações de build dos projetos na solução.

3. Escolha os botões **Build** ou **Recompilar** para compilar o projeto com as configurações especificadas.

## <a name="see-also"></a>Veja também

- [Como criar e editar configurações](../ide/how-to-create-and-edit-configurations.md)
- [Noções sobre configurações de build](../ide/understanding-build-configurations.md)
- [Crie vários projetos em paralelo](../msbuild/building-multiple-projects-in-parallel-with-msbuild.md)