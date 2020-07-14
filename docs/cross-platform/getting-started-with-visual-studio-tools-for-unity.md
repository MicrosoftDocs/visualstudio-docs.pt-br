---
title: Introdução às Ferramentas do Visual Studio para Unity | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2020
ms.technology: vs-unity-tools
ms.topic: how-to
ms.assetid: 66b5b4eb-13b5-4071-98d2-87fafa4598a8
author: indiesaudi
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 32766fdf69136f3882186bbcad08aaf83d2e573e
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815740"
---
# <a name="get-started-with-visual-studio-tools-for-unity"></a>Introdução às Ferramentas do Visual Studio para Unity

## <a name="install-visual-studio"></a>Instalar o Visual Studio

### <a name="unity-bundled-installation"></a>Instalação em pacote do Unity

Começando pelo Unity 2018.1, o Visual Studio é o editor de script padrão de C# para Unity e está incluído no Assistente de Download do Unity, bem como na ferramenta de instalação do Unity Hub.

- Baixe o Unity de [store.unity.com](https://store.unity.com/).

Durante a instalação, verifique se o Visual Studio está marcado na lista de componentes a serem instalados com o Unity:

#### <a name="unity-hub"></a>Unity Hub

:::moniker range="vs-2017"
![instalação do Unity Hub](media/vs-2017/vstu-unity-hub.png)
:::moniker-end
:::moniker range=">=vs-2019"
![instalação do Unity Hub](media/vs-2019/vstu-unity-hub.png)
:::moniker-end

:::moniker range="vs-2017"

#### <a name="unity-download-assistant"></a>Assistente de Download do Unity

![instalação do Assistente de Download do Unity](media/vs-2017/vstu-download-assistant.png)

A versão do Visual Studio incluída na instalação do Unity pode não ser a mais recente. Se for solicitado que você instale o Visual Studio 2017, recomendamos a instalação manual de uma versão mais recente do Visual Studio.
:::moniker-end

### <a name="manual-installation"></a>Instalação manual

Se você já tiver o Visual Studio instalado ou preferir instalar manualmente, execute o instalador do Visual Studio.

1. [Baixe o instalador do Visual Studio](../install/install-visual-studio.md) ou abra-o, se já estiver instalado.

1. Clique em **Modificar** (se já estiver instalado) ou em **Instalar** (para novas instalações) para a versão desejada do Visual Studio.

1. Na guia **Cargas de trabalho**, role até a seção **Móvel e Jogos** e selecione a carga de trabalho **Desenvolvimento de jogos com Unity**.

   :::moniker range="vs-2017"
   ![Carga de trabalho do Unity](media/vs-2017/vstu-unity-workload.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![Carga de trabalho do Unity](media/vs-2019/vstu-unity-workload.png)
   :::moniker-end

1. Clique em **Modificar** (se já estiver instalado) ou em **Instalar** (para novas instalações) no canto inferior direito da janela do instalador.


#### <a name="check-for-updates-to-visual-studio"></a>Verificar se há atualizações para o Visual Studio

É recomendável verificar se há atualizações no Visual Studio para garantir que você tenha acesso às ferramentas e recursos mais recentes. Isso não interromperá seu projeto do Unity.

- [Atualizar o Visual Studio](../install/update-visual-studio.md)


## <a name="configure-unity-for-use-with-visual-studio"></a>Configurar o Unity para ser usado com o Visual Studio

Começando pelo Unity 2018.1, o Visual Studio deve ser o editor de scripts externo padrão no Unity. Confirme isso ou altere o editor de scripts externo para uma versão específica do Visual Studio:

1. Selecione **Preferências** no menu **Editar**.

   :::moniker range="vs-2017"
   ![Selecionar preferências](media/vs-2017/vstu-unity-preferences.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![Selecionar preferências](media/vs-2019/vstu-unity-preferences.png)
   :::moniker-end

2. Na caixa de diálogo Preferências, selecione a guia **Ferramentas Externas**.

3. Na lista suspensa **Editor de Script Externo**, escolha sua versão preferida do Visual Studio, se ela estiver listada, caso contrário, selecione **Procurar....**.

   :::moniker range="vs-2017"
   ![Selecionar o Visual Studio](media/vs-2017/vstu-unity-external-tools.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![Selecionar o Visual Studio](media/vs-2019/vstu-unity-external-tools.png)
   :::moniker-end


4. Se **Procurar... ** for selecionado, navegue até o diretório **Common7/IDE** dentro do seu diretório de instalação do Visual Studio e selecione **devenv.exe**. Em seguida, clique em **Abrir**.

   :::moniker range="vs-2017"
   ![Selecione Abrir](media/vs-2017/vstu-browse-for-application.png)
   :::moniker-end
   :::moniker range=">=vs-2019"
   ![Selecione Abrir](media/vs-2019/vstu-browse-for-application.png)
   :::moniker-end

5. Após a seleção do Visual Studio na lista **Editor de Script Externo**, confirme se a caixa de seleção **Anexo do Editor** está selecionada.

6. Feche a caixa de diálogo **Preferências** para concluir o processo de configuração.

## <a name="support-for-older-versions"></a>Suporte para versões mais antigas

Baixe e instale as Ferramentas do Visual Studio para Unity do Visual Studio Marketplace. Você precisará instalar o pacote correto para a sua versão do Visual Studio.

- Para o Visual Studio 2015 Community, Visual Studio 2015 Professional ou Visual Studio 2015 Enterprise:

   [Baixe as Ferramentas do Visual Studio 2015 para Unity](https://marketplace.visualstudio.com/items?itemName=SebastienLebreton.VisualStudio2015ToolsforUnity)

> [!NOTE]
> As Ferramentas do Visual Studio para Unity exigem o Unity 5.2 e superiores, além de uma versão do Visual Studio que dê suporte a extensões, como o Visual Studio Community, Professional, Premium ou Enterprise. Para verificar se as Ferramentas do Visual Studio para Unity estão habilitadas na sua instalação do Unity, selecione **Sobre o Unity** no menu do **Ajuda** e procure o texto “Ferramentas do Microsoft Visual Studio para Unity habilitadas” na parte inferior esquerda da caixa de diálogo.
> ![Sobre o Unity](media/vs-2019/vstu-about-unity.png)


## <a name="next-steps"></a>Próximas etapas

 Para saber como trabalhar com o projeto do Unity no Visual Studio e como depurá-lo, confira [Ferramentas do Visual Studio para Unity](../cross-platform/using-visual-studio-tools-for-unity.md).
