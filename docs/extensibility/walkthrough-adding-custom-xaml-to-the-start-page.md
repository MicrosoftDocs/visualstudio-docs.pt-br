---
title: 'Walkthrough: adicionando XAML personalizado à página inicial | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: a13aada6cca9b54d8469885ab4c314a89cd06d6c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905963"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>Walkthrough: Adicionar XAML personalizado à página inicial

Este tutorial mostra como criar uma página inicial personalizada do Visual Studio que contém um navegador da Web.

## <a name="add-custom-xaml"></a>Adicionar XAML personalizado

1. Crie uma página inicial seguindo as instruções em [criar uma página inicial personalizada](../extensibility/creating-a-custom-start-page.md).

2. No arquivo *MainWindow. XAML* , localize a \<Grid> seção.

3. Adicione um \<TabControl> elemento e um \<TabItem> dentro do \< Grid> elemento, conforme mostrado no exemplo a seguir.

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. Adicione um segundo \<TabItem> , com um \<Button> elemento que abre um novo projeto:

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="MyButton" Height="Auto">
                <Button Name="btnNewProj" Content="New Project"
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
                    CommandParameter="File.NewProject" >
                </Button>
            </TabItem>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

## <a name="test-the-custom-start-page"></a>Testar a página inicial personalizada

1. Pressione **F5**.

     A instância experimental do Visual Studio é aberta, com a página inicial personalizada instalada, mas não selecionada.

2. Na instância experimental do Visual Studio, abra a página **ferramentas/opts/Environment** .

3. Selecione **inicialização**. Na lista **Personalizar página inicial** , selecione o arquivo *. XAML* e clique em **OK**.

4. No menu **Exibir** , clique em **página inicial**.

5. Clique na guia **Bing** .

     Você deve ver uma página da Web do Bing.

6. Clique na guia **MyButton** .

     Você deve ver um botão **MyProject** , que abre a caixa de diálogo **novo projeto** .

7. Feche a instância experimental.

Para aplicar a página inicial personalizada, em **ferramentas**  >  **Opções**  >  **ambiente**, selecione **inicialização**. Na lista **Personalizar página inicial** , selecione o arquivo *. XAML* e clique em **OK**.

## <a name="next-steps"></a>Próximas etapas

A página inicial do Visual Studio agora contém uma guia que exibe uma guia de navegador da Web e uma guia MyButton. Você pode criar páginas iniciais personalizadas que têm outras funcionalidades usando o modelo *code-behind* para adicionar um. dll personalizado, conforme mostrado em [adicionando controle de usuário à página inicial](../extensibility/adding-user-control-to-the-start-page.md). Você pode compartilhar páginas iniciais personalizadas com outros usuários publicando o arquivo. vsix resultante no site da [Visual Studio Marketplace](https://marketplace.visualstudio.com/) ou em outro compartilhamento de rede ou site da Web. Para obter mais informações, consulte [implantando páginas iniciais personalizadas](../extensibility/deploying-custom-start-pages.md).

## <a name="see-also"></a>Confira também

- [Personalizar a página inicial](../ide/customizing-the-start-page-for-visual-studio.md)
- [Controles de contêiner do WPF](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
