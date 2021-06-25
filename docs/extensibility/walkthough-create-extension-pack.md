---
title: Criar um pacote de extensões
description: Saiba como criar um pacote de extensões com o modelo de item do pacote de extensões
ms.custom: SEO-VS-2020
ms.date: 07/27/2018
ms.topic: tutorial
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: leslierichardson95
ms.author: lerich
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: 213e3e71503ebea8074594bbc88a06980e3e64b4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112905131"
---
# <a name="walkthrough-create-an-extension-pack"></a>Passo a passo: criar um pacote de extensão

Um Pacote de Extensões é um conjunto de extensões que podem ser instaladas juntas. Os Pacotes de Extensão permitem compartilhar facilmente suas extensões favoritas com outros usuários ou agrupar um conjunto de extensões para um cenário específico.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, o SDK do Visual Studio está incluído como um recurso opcional na Visual Studio configuração. Você também pode instalar o SDK do VS posteriormente. Para obter mais informações, [consulte Instalando o SDK Visual Studio .](../extensibility/installing-the-visual-studio-sdk.md)

O recurso Pacote de Extensões está disponível a partir do Visual Studio 15.8 Versão Prévia 2.

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>Criar uma extensão com um modelo de item do Pacote de Extensões

O modelo de item do Pacote de Extensões cria um Pacote de Extensões com um conjunto de extensões que podem ser instaladas juntas.

1. Na caixa **de diálogo Novo** Projeto, pesquise "vsix" e selecione Projeto **VSIX.** Em **Nome do projeto,** digite "Testar Pacote de Extensão". Selecione **Criar**.

2. No **Gerenciador de Soluções**, clique com o botão direito do mouse no nó do projeto e **selecione Adicionar**  >  **Novo Item**. Vá para o nó **Extensibilidade do** Visual C# e selecione **Pacote de Extensões**. Deixe o nome do arquivo padrão (ExtensionPack1.cs).

3. O arquivo ExtensionPack1.vsext é adicionado, que contém o código a seguir

   ```json
   {
    "id": "ExtensionPack1",
    "name": "ExtensionPack1",
    "description": "Read about creating extension packs at https://aka.ms/vsextpack",
    "version": "1.0.0.0",
    "extensions": [  // List of extensions that are included in the Extension Pack.
      {
        "vsixId": "41858b2d-ff0b-4a43-80b0-f1b2d6084935", // The vsix id of the extension you want to   include.
        "name": "AlignAssignments"
      },
      {
          "vsixId": "42374550-426a-400e-96f9-237682e8dea6",
        "name": "CopyAsHtml"
      }
    ]
   }
   ```

4. O vsixid da extensão a ser incluído no Pacote de Extensões pode ser encontrado no [Visual Studio Marketplace](https://marketplace.visualstudio.com/). Encontre a extensão que você deseja incluir e clique em **Copiar ID.** Você pode atualizar o **vsixId** existente no arquivo acima ou adicionar outra extensão à lista.

    ![Copiar VsixId do Marketplace](media/vsixid-marketplace.png)

5. Crie o projeto e carregue sua extensão no Marketplace. Consulte [Publicando uma extensão Visual Studio .](../extensibility/walkthrough-publishing-a-visual-studio-extension.md)

> [!NOTE]
> Um pacote de extensões só pode instalar extensões que estão disponíveis no [Visual Studio Marketplace](https://marketplace.visualstudio.com/) [ou na Galeria privada.](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md)

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>Instale o Pacote de Extensões do Visual Studio Marketplace

Agora que a extensão foi publicada, instale-a no Visual Studio e teste-a lá.

::: moniker range="vs-2017"

1. No Visual Studio, no menu **Ferramentas,** clique **em Extensões e Atualizações.**

::: moniker-end

::: moniker range=">=vs-2019"

1. No Visual Studio, no menu **Extensões,** clique em **Extensões Gerenciadas**.

::: moniker-end

2. Clique **em Online** e pesquise "Testar Pacote de Extensão".

3. Clique em **Download**. A extensão e sua lista de extensões incluídas no Pacote de Extensões serão agendadas para instalação.

4. Veja abaixo um exemplo de exibição de download do Pacote de Extensões da **caixa de diálogo Gerenciar Extensões.** Se preferir instalar apenas algumas das extensões incluídas no pacote de extensões, você poderá modificar a lista de extensões em **Agendado para Instalação**.

    ![Baixar o Pacote de Extensões do Marketplace](media/vside-extensionpack.png)

5. Para concluir a instalação, feche todas as instâncias do Visual Studio.

## <a name="remove-the-extension"></a>Remover a extensão

Para remover a extensão do computador:

::: moniker range="vs-2017"

1. No Visual Studio, no menu **Ferramentas,** clique **em Extensões e Atualizações.**

::: moniker-end

::: moniker range=">=vs-2019"

1. No Visual Studio, no menu **Extensões,** clique em **Extensões Gerenciadas**.

::: moniker-end

2. Selecione **Testar Pacote de Extensão** e clique em **Desinstalar**. A extensão e sua lista de extensões incluídas no Pacote de Extensões serão agendadas para desinstalação.

3. Para concluir a desinstalação, feche todas as instâncias do Visual Studio.
