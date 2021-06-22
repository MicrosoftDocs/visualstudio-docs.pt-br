---
title: Introdução às Ferramentas do Visual Studio para Unity | Microsoft Docs
description: Saiba como instalar e configurar o Visual Studio para desenvolvimento do Unity.
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
ms.openlocfilehash: 706700c8343d934f7a9a5ce32f98bf96e67d4259
ms.sourcegitcommit: 07e6db4bf2966863093e3974c60c3b46e6953416
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2021
ms.locfileid: "112488839"
---
# <a name="get-started-with-visual-studio-and-unity"></a>Introdução ao Visual Studio e ao Unity

> [!NOTE]
> Este guia pressupõe que você já instalou o Unity usando o programa do Hub do Unity. Se você for novo no Unity, é recomendável visitar o Unity Learn e concluir primeiro o [roteiro de aprendizagem do Unity Essentials](https://learn.unity.com/pathway/unity-essentials) .

## <a name="install-unity-support-for-visual-studio"></a>Instalar o suporte do Unity para o Visual Studio

Ferramentas do Visual Studio para Unity é uma extensão gratuita que fornece suporte para escrever e depurar C# e muito mais. Visite a [visão geral do Tools for Unity](./visual-studio-tools-for-unity.md) para obter uma lista completa do que as extensões incluem.

:::zone pivot="windows"

> [!NOTE]
> Este guia de instalação é para o Visual Studio. Se você estiver usando Visual Studio Code, visite a [documentação de desenvolvimento do Unity com vs Code](https://code.visualstudio.com/docs/other/unity).

1. [Baixe o instalador do Visual Studio](/visualstudio/install/install-visual-studio.md)ou execute-o se já estiver instalado.
2. Clique em **Modificar** (se já estiver instalado) ou em **Instalar** (para novas instalações) para a versão desejada do Visual Studio.
3. Na guia **cargas de trabalho** , role até a seção **jogos** e selecione o **desenvolvimento de jogos com** carga de trabalho do Unity.

    ![Desenvolvimento de jogos com a caixa carga de trabalho do Unity no instalador](../media/vs/unity-workload.png)

:::zone-end
:::zone pivot="macos"

> [!NOTE]
> Este guia de instalação é para Visual Studio para Mac. Se você estiver usando Visual Studio Code, visite a [documentação de desenvolvimento do Unity com vs Code](https://code.visualstudio.com/docs/other/unity).

As ferramentas para o Unity estão incluídas na instalação do Visual Studio para Mac e não são necessárias etapas de instalação separadas. Você pode verificar isso no menu **Visual Studio para Mac > Extensions > desenvolvimento de jogos** . As **ferramentas de Visual Studio para Mac para Unity** devem ser habilitadas.

![Exibição do Gerenciador de extensões mostrando as ferramentas de Visual Studio para Mac para o Unity habilitado](../media/vsm/unity-workload.png)

:::zone-end

## <a name="check-for-updates"></a>Verificar atualizações

É recomendável manter o Visual Studio e Visual Studio para Mac atualizado para que você tenha as mais recentes correções de bugs, recursos e suporte do Unity. Isso não requer uma atualização das versões do Unity.

:::zone pivot="windows"

1. Clique no menu **ajuda > verificar atualizações** .

    ![O menu verificar atualizações no Visual Studio 2019](../media/vs/check-for-updates.png)

2. Se houver uma atualização disponível, o Instalador do Visual Studio mostrará uma nova versão. Clique no botão **Atualizar**.

:::zone-end
:::zone pivot="macos"

1. Clique no menu **Visual Studio para Mac > verificar se há atualizações...** para abrir a caixa de diálogo **atualização do Visual Studio** .
2. Se houver uma atualização disponível, clique no botão **instalar** .

:::zone-end

## <a name="configure-unity-to-use-visual-studio"></a>Configurar o Unity para usar o Visual Studio

Por padrão, o Unity já deve estar configurado para usar o Visual Studio ou Visual Studio para Mac como um editor de scripts. Você pode confirmar isso ou alterar o editor de script externo para uma versão específica do Visual Studio do editor do Unity.

:::zone pivot="windows"

1. No editor do Unity, selecione o menu **Editar preferências de >** ..
2. Selecione a guia **Ferramentas externas** à esquerda.
3. A lista suspensa **Editor de scripts externos** fornece uma maneira de escolher diferentes instalações do Visual Studio. Você também pode clicar em **procurar...** na lista suspensa para adicionar uma versão não listada.

    ![O menu de preferências de ferramentas externas no editor do Unity no Windows](../media/vs/preferences-external-tools.png)

4. Se **Procurar...** for selecionado, navegue até o diretório **Common7/IDE** dentro do seu diretório de instalação do Visual Studio e selecione **devenv.exe**. Em seguida, clique em **abrir**.
5. Após a seleção do Visual Studio na lista **Editor de Script Externo**, confirme se a caixa de seleção **Anexo do Editor** está selecionada.
6. Feche a caixa de diálogo **Preferências** para concluir o processo de configuração.

:::zone-end
:::zone pivot="macos"

1. No editor do Unity, selecione o menu de **preferências do > do Unity** .
2. Selecione a guia **Ferramentas externas** à esquerda.
3. A lista suspensa **Editor de scripts externos** fornece uma maneira de escolher diferentes instalações do Visual Studio. Você também pode clicar em **procurar...** na lista suspensa para adicionar uma versão não listada.

    ![O menu de preferências de ferramentas externas no editor do Unity no macOS](../media/vsm/preferences-external-tools.png)

4. Feche a caixa de diálogo **Preferências** para concluir o processo de configuração.

:::zone-end

## <a name="next-steps"></a>Próximas etapas

 Para saber como trabalhar com e depurar seu projeto do Unity no Visual Studio, visite [usando ferramentas do Visual Studio para Unity](using-visual-studio-tools-for-unity.md).
