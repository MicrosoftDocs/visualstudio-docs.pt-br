---
title: Criando e Editando Configurações de Build
description: Este artigo descreve como criar configurações de build no Visual Studio para Mac
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.assetid: CC1B72D6-12FF-4CCC-A9D4-00F2DC14589F
ms.custom: video
ms.topic: how-to
ms.openlocfilehash: eb3ceed624e3bbba67564bb8f7c359841c0e496d
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939177"
---
# <a name="creating-and-editing-build-configurations"></a>Criando e editando configurações de build

As configurações de Build oferecem um controle preciso sobre uma compilação, permitindo que você crie configurações para atender a diferentes situações de teste e distribuição. Você pode criar configurações de compilação para projetos individuais ou em toda a solução.

Você pode criar novas configurações e editar as existentes para projetos e soluções usando a caixa de diálogo opções do projeto.

>[!NOTE]
>Este tópico se aplica ao Visual Studio para Mac. Para o Visual Studio no Windows, consulte [como: criar e editar configurações](/visualstudio/ide/how-to-create-and-edit-configurations).

## <a name="creating-a-project-build-configuration"></a>Criando uma configuração de compilação do projeto

Para criar uma configuração de compilação de projeto, siga estas etapas:

1. Clique com botão direito do mouse no nó do projeto e selecione **Opções**. Você também pode clicar duas vezes no nó do projeto para abrir a caixa de diálogo opções do projeto.

2. Na caixa de diálogo Opções do Projeto, selecione **Compilar > Configurações**:

    ![Gerenciador de configurações nas opções do projeto](media/create-and-edit-configurations-image2.png)

3. Selecione **Adicionar** para criar uma nova configuração. Você também pode copiar qualquer uma das configurações existentes.

Depois de criar a configuração, você pode usar a seção **Build** nas opções de projeto para adaptar as propriedades apropriadas à sua configuração:

![Configurar opções de build](media/create-and-edit-configurations-image3.png)

## <a name="creating-a-solution-build-configuration"></a>Criando uma configuração de build da solução

Para criar uma configuração de compilação de solução, siga estas etapas:

1. Clique com o botão direito do mouse no nó da solução e selecione **Opções**. Você também pode clicar duas vezes no nó da solução para abrir a caixa de diálogo opções de solução.

2. Na caixa de diálogo Opções da Solução, selecione **Compilar > Configurações**:

    ![Gerenciador de configurações nas opções da solução](media/create-and-edit-configurations-image1.png)

3. Selecione **Adicionar** para criar uma nova configuração. Você também pode copiar qualquer uma das configurações existentes.

Depois de criar a configuração, você pode usar a seção **Build** da caixa de diálogo de opções do projeto para cada um dos seus projetos para adaptar as propriedades apropriadas à sua configuração:

![Configurar opções de build](media/create-and-edit-configurations-image3.png)

## <a name="renaming-a-build-configuration"></a>Renomeando uma configuração de compilação

Para renomear uma configuração, selecione-a na lista de configuração navegando para **criar > configurações** nas opções de projeto ou solução:

![lista de configurações](media/create-and-edit-configurations-image4.png)

Selecione o botão **Renomear**.

![renomear caixa de diálogo](media/create-and-edit-configurations-image5.png)

Em seguida, clique em **OK** para confirmar.

## <a name="related-video"></a>Vídeo relacionados

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Launch-Multiple-Projects/player]

## <a name="see-also"></a>Confira também

- [Criar e editar configurações de build (Visual Studio no Windows)](/visualstudio/ide/how-to-create-and-edit-configurations)