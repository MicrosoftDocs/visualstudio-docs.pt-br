---
title: Introdução com o modelo de projeto VSIX | Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
helpviewer_keywords:
- Visual Studio SDK, VSIX project template
ms.assetid: 89fac33e-9380-4723-9b45-048a6e16f0ed
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 18ca9672b22120718f63638d8668812d0e42e41f
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905884"
---
# <a name="get-started-with-the-vsix-project-template"></a>Introdução ao modelo de projeto VSIX

Você pode usar o modelo de projeto VSIX para criar uma extensão ou para empacotar uma extensão existente para implantação. O modelo de projeto VSIX tem as versões Visual Basic e do Visual C# e é instalado como parte do SDK do Visual Studio.

 O modelo de projeto VSIX consiste apenas em um arquivo *Source. Extension. vsixmanifest* , que contém informações sobre a extensão e os ativos que ele envia.

 Para localizar o modelo de projeto VSIX, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="deploy-a-custom-project-template-using-the-vsix-project-template"></a>Implantar um modelo de projeto personalizado usando o modelo de projeto VSIX

 As etapas a seguir mostram como usar o projeto VSIX para empacotar um modelo de projeto que você pode compartilhar com outros desenvolvedores ou carregar na galeria do Visual Studio.

1. Crie um modelo de projeto.

    1. Abra o projeto do qual criar um modelo. Este projeto pode ser de qualquer tipo de projeto.

    2. No menu **Projeto**, clique em **Exportar Modelo**. Conclua as etapas do assistente.

         Um arquivo *. zip* é criado nos *modelos \\ exportados do%USERPROFILE%\My Documentos\Visual Studio {Version} \Meus*.

2. Crie um projeto VSIX vazio.

     Selecione **Arquivo** > **Novo** > **Projeto**. Na caixa de pesquisa, digite "VSIX" e selecione a versão em **C#** ou **Visual Basic** do **projeto VSIX**.

3. Adicione o arquivo *. zip* ao projeto. Defina sua propriedade **copiar para diretório de saída** como `Copy Always` .

4. Em **Gerenciador de soluções**, clique duas vezes no arquivo *Source. Extension. vsixmanifest* para abri-lo no **Designer de manifesto do VSIX**e faça as seguintes alterações:

    - Defina o campo **nome do produto** como **meu modelo de projeto**.

    - Defina o campo **ID do produto** como **MyProjectTemplate-1**.

    - Defina o campo **autor** como **Fabrikam**.

    - Defina o campo **Descrição** como **meu modelo de projeto**.

    - Na seção **ativos** , adicione um tipo **Microsoft. VisualStudio. ProjectTemplate** e defina seu caminho para o nome do arquivo *. zip* .

5. Salve e feche o arquivo *Source. Extension. vsixmanifest* .

6. Compile o projeto.

7. No diretório de saída, clique duas vezes no arquivo *. vsix* .

8. Uma caixa de mensagem de **instalador VSIX** é exibida. Siga as instruções para instalar a extensão.

9. Feche o Visual Studio e, em seguida, o reabra.

::: moniker range="vs-2017"

10. Selecione **extensões e atualizações** (no menu **ferramentas** ) e selecione a categoria **modelos** . Uma das extensões disponíveis deve ser **meu modelo de projeto**.

::: moniker-end

::: moniker range=">=vs-2019"

10. Selecione **gerenciar extensões** (no menu **extensões** ) e selecione a categoria **modelos** . Uma das extensões disponíveis deve ser **meu modelo de projeto**.

::: moniker-end

11. O novo modelo de projeto é exibido na caixa de diálogo **novo projeto** no mesmo local que o modelo de projeto original. Por exemplo, se você criou um modelo chamado **VB console** a partir de um aplicativo de console Visual Basic, o **console do VB** aparecerá no mesmo painel que o modelo de **aplicativo Visual Basic console** .

### <a name="to-specify-the-location-of-the-template-in-the-new-project-dialog-box"></a>Para especificar o local do modelo na caixa de diálogo novo projeto

1. As pastas de modelo estão localizadas nos diretórios *{caminho de instalação do Visual Studio} \Common7\IDE\ProjectTemplates* e *{caminho de instalação do Visual Studio} \Common7\IDE\ItemTemplates* . Os nomes das seções de nível superior na caixa de diálogo **novo projeto** não correspondem exatamente aos nomes das pastas de modelo. Quando forem diferentes, use o nome da pasta de modelos.

    Altere a extensão de arquivo *. vsix* para *. zip*e, em seguida, abra o arquivo.

2. Crie uma nova pasta com o mesmo nome que a seção da caixa de diálogo **novo projeto** em que o modelo deve aparecer.

3. Se o modelo for exibido em uma subseção, crie uma subpasta com o mesmo nome.

4. Mova o arquivo template *. zip* para a nova pasta.

5. Altere a extensão *. zip* para *. vsix*.

6. Abra o manifesto do VSIX.

7. No manifesto do VSIX, atualize o caminho do **ativo** do modelo para que ele aponte para a raiz da árvore de diretório que contém o arquivo de modelo. Por exemplo, se o modelo estiver em *\CSharp\Windows*, a referência deverá apontar para *\CSharp*.
