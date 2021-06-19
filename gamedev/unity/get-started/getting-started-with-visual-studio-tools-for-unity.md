---
title: Introdução às Ferramentas do Visual Studio para Unity | Microsoft Docs
description: Saiba como instalar e configurar o Visual Studio desenvolvimento do Unity.
ms.custom: acquisition
ms.date: 01/27/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
zone_pivot_groups: platform
ms.openlocfilehash: 8eea998731c4d29e533d1e6bf21d4a2870a81ff5
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386690"
---
# <a name="get-started-with-visual-studio-and-unity"></a>Começar a trabalhar com Visual Studio e Unity

> [!NOTE]
> Este guia pressu que você já instalou o Unity usando o programa hub do Unity. Se você for novo no Unity, recomendamos visitar o Unity Learn e concluir o caminho de aprendizagem do [Unity Essentials](https://learn.unity.com/pathway/unity-essentials) primeiro.

## <a name="install-unity-support-for-visual-studio"></a>Instalar o suporte do Unity para Visual Studio

Ferramentas do Visual Studio para Unity é uma extensão gratuita que fornece suporte para escrever e depurar C# e muito mais. Visite a [visão geral das Ferramentas para Unity](./visual-studio-tools-for-unity.md) para ver uma lista completa do que as extensões incluem.

:::zone pivot="windows"

> [!NOTE]
> Este guia de instalação é para Visual Studio. Se você estiver usando o Visual Studio Code, visite a documentação Desenvolvimento [do Unity com VS Code .](https://code.visualstudio.com/docs/other/unity)

1. [Baixe o Visual Studio ou](/visualstudio/install/install-visual-studio.md)execute-o se já estiver instalado.
2. Clique em **Modificar** (se já estiver instalado) ou em **Instalar** (para novas instalações) para a versão desejada do Visual Studio.
3. Na guia **Cargas de** trabalho, role até **a seção Jogos** e selecione a carga de trabalho Desenvolvimento de jogos com **Unity.**

    ![Caixa de trabalho Desenvolvimento de jogos com Unity no instalador](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> Este guia de instalação é para Visual Studio para Mac. Se você estiver usando o Visual Studio Code, visite a documentação Desenvolvimento [do Unity com VS Code .](https://code.visualstudio.com/docs/other/unity)

As ferramentas para Unity estão incluídas na instalação do Visual Studio para Mac e nenhuma etapa de instalação separada é necessária. Você pode verificar isso no menu **Visual Studio para Mac > Extensões > Game Development.** **Visual Studio para Mac Ferramentas para Unity** devem ser habilitadas.

![Exibição do Gerenciador de Extensões mostrando Visual Studio para Mac ferramentas para Unity habilitadas](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>Verificar atualizações

É recomendável manter o Visual Studio e Visual Studio para Mac para que você tenha as correções de bug, os recursos e o suporte ao Unity mais recentes. Isso não requer uma atualização das versões do Unity.

:::zone pivot="windows"

1. Clique no menu **Ajuda > Verificar Atualizações.**

    ![O menu Verificar Atualizações no Visual Studio 2019](../media/vs/check-for-updates.png)

2. Se houver uma atualização disponível, o Instalador do Visual Studio mostrará uma nova versão. Clique no botão **Atualizar**.

:::zone-end
:::zone pivot="macos"

1. Clique no **menu Visual Studio para Mac > Verificar Atualizações...** para abrir a caixa **de Visual Studio Atualizar.**
2. Se houver uma atualização disponível, clique no **botão** Instalar.

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>Configurar o Unity para usar Visual Studio

Por padrão, o Unity já deve estar configurado para usar Visual Studio ou Visual Studio para Mac como um editor de scripts. Você pode confirmar isso ou alterar o editor de script externo para uma versão específica do Visual Studio do Editor do Unity.

:::zone pivot="windows"

1. No Editor do Unity, selecione o menu **Editar > Preferências..**
2. Selecione a **guia Ferramentas** Externas à esquerda.
3. A **lista suspenso Editor** de Script Externo fornece uma maneira de escolher diferentes instalações de Visual Studio. Você também pode clicar **em Procurar...** na lista suspenso para adicionar uma versão não listada.

    ![O menu de preferência Ferramentas Externas no Editor do Unity no Windows](../media/vs/preferences-external-tools.png)

4. Se **Procurar...** for selecionado, navegue até o diretório **Common7/IDE** dentro do seu diretório de instalação do Visual Studio e selecione **devenv.exe**. Em seguida, clique **em Abrir.**
5. Após a seleção do Visual Studio na lista **Editor de Script Externo**, confirme se a caixa de seleção **Anexo do Editor** está selecionada.
6. Feche a caixa de diálogo **Preferências** para concluir o processo de configuração.

:::zone-end
:::zone pivot="macos"

1. No Editor do Unity, selecione o menu **> Unity..**
2. Selecione a **guia Ferramentas** Externas à esquerda.
3. A **lista suspenso Editor** de Script Externo fornece uma maneira de escolher diferentes instalações de Visual Studio. Você também pode clicar **em Procurar...** na lista suspenso para adicionar uma versão não listada.

    ![O menu de preferência Ferramentas Externas no Editor do Unity no macOS](../media/vsm/preferences-external-tools.png)

4. Feche a caixa de diálogo **Preferências** para concluir o processo de configuração.

:::zone-end

## <a name="next-steps"></a>Próximas etapas

 Para saber como trabalhar e depurar seu projeto do Unity no Visual Studio, visite [Usando Ferramentas do Visual Studio para Unity](using-visual-studio-tools-for-unity.md).
