---
title: Compilando e Limpando Projetos e Soluções
description: Este artigo descreve como criar um projeto no Visual Studio para Mac
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/19/2019
ms.assetid: E4B6CB42-9FE2-43B9-93B7-BD4BD50518B1
ms.topic: how-to
ms.openlocfilehash: a33b590290880a7e20e7c0ec44c0b12942b1240e
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939109"
---
# <a name="building-and-cleaning-projects-and-solutions"></a>Compilando e limpando Projetos e Soluções

Siga as etapas neste artigo para aprender a criar, recriar ou limpar todos ou alguns dos projetos em uma solução.

> [!NOTE]
> Este tópico se aplica ao Visual Studio para Mac. Para o Visual Studio no Windows, consulte [Compilar e limpar projetos e soluções no Visual Studio](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio).

## <a name="to-build-rebuild-or-clean-an-entire-solution"></a>Para criar, recriar ou limpar uma solução inteira

1. Selecione o nó da solução no **painel de soluções**:

    ![Selecionando o nó da solução](media/compiling-and-building-image1.png)

2. Selecione o menu **Compilar** na barra de menus e escolha uma das seguintes opções:

    ![selecionando o item de menu criar todos](media/compiling-and-building-image2.png)

    * Escolha **compilar tudo** para compilar os arquivos e componentes dentro do projeto que foram alterados desde a compilação mais recente.

    * Escolha **Recompilar tudo** para "limpar" a solução e, em seguida, compilar todos os arquivos e componentes do projeto.

    * Escolha **limpar tudo** para excluir todos os arquivos intermediários e de saída. Com apenas os arquivos de projeto e de componente restantes, novas instâncias dos arquivos de saída e intermediários podem ser criadas.

## <a name="to-build-or-rebuild-a-single-project"></a>Para compilar ou recompilar um único projeto

1. Selecione o projeto no **painel de soluções**.

2. Selecione o menu **Compilar** na barra de menus.

3. Escolha Compilar [ProjectName], recompilar [ProjectName] ou limpar [ProjectName].

## <a name="to-stop-a-build"></a>Para interromper um build

Para interromper uma compilação, use uma das seguintes opções:

* Pressione o quadrado vermelho na área de status:

    ![Pressione quadrado vermelho para parar o build](media/compiling-and-building-image3.png)

* Use o item **parar** no menu **Compilar** .

* Pressione **cmd + Shift + Return**.

## <a name="see-also"></a>Confira também

- [Criar e limpar projetos e soluções (Visual Studio no Windows)](/visualstudio/ide/building-and-cleaning-projects-and-solutions-in-visual-studio)