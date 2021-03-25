---
title: Criar um pacote de extensões
description: Saiba como criar um pacote de extensão com o modelo de item do pacote de extensão
ms.custom: SEO-VS-2020
ms.date: 07/27/2018
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], new - extensions
ms.assetid: 5388EEBA-211D-4114-8CD9-70C899919F7E
author: leslierichardson95
ms.author: lerich
manager: Meng
ms.workload:
- vssdk
ms.openlocfilehash: 57b447be3ee411b737c1aea5b0a4be5ef966c8c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062142"
---
# <a name="walkthrough-create-an-extension-pack"></a>Passo a passo: criar um pacote de extensão

Um pacote de extensão é um conjunto de extensões que podem ser instaladas juntas. Os pacotes de extensão permitem que você compartilhe facilmente suas extensões favoritas com outros usuários ou agrupe um conjunto de extensões para um cenário em particular.

## <a name="prerequisites"></a>Pré-requisitos

A partir do Visual Studio 2015, o SDK do Visual Studio está incluído como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalando o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

O recurso de pacote de extensão está disponível a partir do Visual Studio 15,8 Preview 2.

## <a name="create-an-extension-with-an-extension-pack-item-template"></a>Criar uma extensão com um modelo de item de pacote de extensão

O modelo de item do pacote de extensão cria um pacote de extensão com um conjunto de extensões que podem ser instaladas juntas.

1. Na caixa de diálogo **novo projeto** , procure "VSIX" e selecione **projeto VSIX**. Para **nome do projeto**, digite "Test Extension Pack". Selecione **Criar**.

2. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **Adicionar**  >  **novo item**. Vá para o nó **extensibilidade** do Visual C# e selecione **pacote de extensão**. Deixe o nome de arquivo padrão (ExtensionPack1. cs).

3. O arquivo ExtensionPack1. vsext é adicionado, que contém o código a seguir

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

4. O vsixid da extensão a ser incluída no pacote de extensão pode ser encontrado no [Visual Studio Marketplace](https://marketplace.visualstudio.com/). Localize a extensão que você deseja incluir e clique em **ID da cópia**. Você pode atualizar o **vsixid** existente no arquivo acima ou adicionar outra extensão à lista.

    ![Copiar Vsixid do Marketplace](media/vsixid-marketplace.png)

5. Compile o projeto e carregue sua extensão para o Marketplace. Consulte [publicando uma extensão do Visual Studio](../extensibility/walkthrough-publishing-a-visual-studio-extension.md).

> [!NOTE]
> Um pacote de extensão só pode instalar extensões que estão disponíveis no [Visual Studio Marketplace](https://marketplace.visualstudio.com/) ou na [galeria privada](../extensibility/how-to-create-an-atom-feed-for-a-private-gallery.md).

## <a name="install-the-extension-pack-from-the-visual-studio-marketplace"></a>Instalar o pacote de extensão do Visual Studio Marketplace

Agora que a extensão foi publicada, instale-a no Visual Studio e teste-a lá.

::: moniker range="vs-2017"

1. No Visual Studio, no menu **ferramentas** , clique em **extensões e atualizações**.

::: moniker-end

::: moniker range=">=vs-2019"

1. No Visual Studio, no menu **extensões** , clique em **extensões gerenciadas**.

::: moniker-end

2. Clique em **online** e procure "Test Extension Pack".

3. Clique em **Download**. A extensão e sua lista de extensões incluídas no pacote de extensão serão agendadas para instalação.

4. Veja abaixo uma exibição de download do pacote de extensão de exemplo da caixa de diálogo **gerenciar extensões** . Se você preferir instalar apenas algumas das extensões incluídas no pacote de extensão, poderá modificar a lista de extensões em **agendada para instalação**.

    ![Baixar o pacote de extensão do Marketplace](media/vside-extensionpack.png)

5. Para concluir a instalação, feche todas as instâncias do Visual Studio.

## <a name="remove-the-extension"></a>Remover a extensão

Para remover a extensão do seu computador:

::: moniker range="vs-2017"

1. No Visual Studio, no menu **ferramentas** , clique em **extensões e atualizações**.

::: moniker-end

::: moniker range=">=vs-2019"

1. No Visual Studio, no menu **extensões** , clique em **extensões gerenciadas**.

::: moniker-end

2. Selecione **pacote de extensão de teste** e clique em **desinstalar**. A extensão e sua lista de extensões incluídas no pacote de extensão serão agendadas para desinstalação.

3. Para concluir a desinstalação, feche todas as instâncias do Visual Studio.
