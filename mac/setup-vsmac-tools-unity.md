---
title: Configurar as Ferramentas do Visual Studio para Mac para Unity
description: Configurando e instalando ferramentas do Unity para uso no Visual Studio para Mac
author: therealjohn
ms.author: johmil
ms.date: 06/18/2019
ms.assetid: 83FDD7A3-5D16-4B4B-9080-078E3FB5C623
ms.topic: how-to
ms.openlocfilehash: cc43dd74fb5427161cb3992394530328129c607c
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85949975"
---
# <a name="set-up-visual-studio-for-mac-tools-for-unity"></a>Configurar as Ferramentas do Visual Studio para Mac para Unity

Esta seção explica como começar a usar as Ferramentas do Visual Studio para Mac para Unity.

## <a name="install-visual-studio-for-mac"></a>Instalar o Visual Studio para Mac

### <a name="unity-bundled-installation"></a>Instalação de pacote do Unity

Começando pelo Unity 2018.1, o Visual Studio para Mac é o IDE (ambiente de desenvolvimento integrado) padrão do C# para o Unity e está incluído no Assistente de Download do Unity, bem como na ferramenta de instalação do Unity Hub. Baixe o Unity de [store.unity.com](https://store.unity.com/).

Durante a instalação, verifique se o Visual Studio para Mac está marcado na lista de componentes a serem instalados com o Unity:

#### <a name="unity-hub"></a>Unity Hub

![instalação do Unity Hub](media/setup-vsmac-tools-unity-image7.png)

#### <a name="unity-download-assistant"></a>Assistente de Download do Unity

![instalação do Assistente de Download do Unity](media/setup-vsmac-tools-unity-image8.png)

#### <a name="check-for-updates-to-visual-studio-for-mac"></a>Verificar se há atualizações para o Visual Studio para Mac

A versão do Visual Studio para Mac incluída na instalação do Unity pode não ser a última. É recomendável verificar se há atualizações para garantir que você tem acesso às últimas ferramentas e funcionalidades.

* [Atualizando o Visual Studio para Mac](update.md)

### <a name="manual-installation"></a>Instalação manual

Caso você já tenha o Unity 5.6.1 ou superior, mas não tenha o Visual Studio para Mac, instale o Visual Studio para Mac manualmente. Todas as edições do Visual Studio para Mac são fornecidas com as Ferramentas do Visual Studio para Mac para Unity, incluindo a edição Community gratuita:

* Baixe o Visual Studio para Mac de [visualstudio.microsoft.com](https://visualstudio.microsoft.com/).
* As Ferramentas do Visual Studio para Mac para Unity são instaladas automaticamente durante o processo de instalação.
* Siga as etapas no [guia de instalação](/visualstudio/mac/installation) para obter ajuda de instalação adicional.

> [!NOTE]
> As Ferramentas do Visual Studio para Mac para Unity requerem o Unity versão 5.6.1 ou superior. Para verificar se as Ferramentas do Visual Studio para Unity estão habilitadas na sua versão do Unity, selecione **Sobre o Unity** no menu do Unity e procure o texto “Ferramentas do Microsoft Visual Studio para Unity habilitadas” na parte inferior esquerda da caixa de diálogo.
>
> ![Sobre o Unity](media/setup-vsmac-tools-unity-image3.png)

## <a name="confirm-that-the-visual-studio-for-mac-tools-for-unity-extension-is-enabled"></a>Confirme se a extensão das Ferramentas do Visual Studio para Mac para Unity está habilitada

Embora a extensão das Ferramentas do Visual Studio para Mac para Unity devem ser habilitadas por padrão, você pode confirmar isso e verificar o número de versão instalada:

1. No menu do Visual Studio, escolha **Extensões...**.

   ![Selecionar Extensões](media/setup-vsmac-tools-unity-image1.png)

2. Expanda a seção de Desenvolvimento de Jogos e confirme a entrada das Ferramentas do Visual Studio para Mac para Unity.

   ![Exibir a Entrada do Unity](media/setup-vsmac-tools-unity-image2.png)

## <a name="configure-unity-for-use-with-visual-studio-for-mac"></a>Configurar o Unity para ser usado com o Visual Studio para Mac

Começando pelo Unity 2018.1, o Visual Studio deve ser o editor de scripts externo padrão no Unity. Confirme isso ou altere o editor de scripts externo para o Visual Studio:

1. Selecione **Preferências... ** no menu do Unity.

   ![Selecionar preferências](media/setup-vsmac-tools-unity-image4.png)

2. Na caixa de diálogo Preferências, selecione a guia **Ferramentas Externas**.

3. Na lista suspensa do Editor de script externo, escolha **Visual Studio** se ele estiver listado, caso contrário, selecione **Procurar...**.

   ![Selecionar o Visual Studio](media/setup-vsmac-tools-unity-image5.png)

4. Se **Procurar...** foi selecionado, navegue para o Diretório de aplicativos, selecione o Visual Studio e clique em **Abrir**.

   ![Selecione Abrir](media/setup-vsmac-tools-unity-image6.png)

5. Depois de selecionar o Visual Studio na lista **Editor de script externo**, feche a caixa de diálogo Preferências para concluir o processo de configuração.