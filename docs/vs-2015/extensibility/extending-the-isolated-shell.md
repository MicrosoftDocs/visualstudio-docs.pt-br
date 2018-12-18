---
title: Estender o Shell isolado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: 9a641d8f-211e-4486-a1b1-4a89fafe7ee8
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: dc700e0a1b8753a26067eff90df9ff58765de8d1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792015"
---
# <a name="extending-the-isolated-shell"></a>Estender o Shell isolado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode estender o shell isolado do Visual Studio com a adição de um VSPackage, uma parte do componente de Managed Extensibility Framework (MEF) ou um projeto VSIX genérico para seu aplicativo de shell isolado.  
  
> [!NOTE]
>  As etapas a seguir pressupõem que você tenha criado um aplicativo básico de shell isolado usando o modelo de projeto do Visual Studio Shell isolado. Para obter mais informações sobre este modelo de projeto, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
## <a name="locations-for-the-visual-studio-package-project-template"></a>Locais para o modelo de projeto de pacote do Visual Studio  
 O modelo de projeto de pacote do Visual Studio pode ser encontrado em três locais diferentes nos **novo projeto** caixa de diálogo:  
  
1.  Sob **Visual Basic**, **extensibilidade**. O idioma padrão do projeto é o Visual Basic.  
  
2.  Sob **Visual c#**, **extensibilidade**. O idioma padrão do projeto é c#.  
  
3.  Sob **outros tipos de projeto**, **extensibilidade**. O idioma padrão do projeto é C++.  
  
## <a name="adding-a-vspackage"></a>Adicionando um VSPackage  
 Você pode adicionar um VSPackage ao seu aplicativo de shell isolado. As etapas a seguir mostram como criar uma que adiciona os comandos de menu.  
  
#### <a name="to-add-a-new-vspackage"></a>Para adicionar um novo VSPackage  
  
1.  Adicione um projeto de pacote do Visual Studio chamado `MenuCommandsPackage`.  
  
2.  No **informações básicas de VSPackage** página do assistente, defina **nome da empresa** para `Fabrikam` e **nome VSPackage** para `FabrikamMenuCommands`. Escolha o botão **Avançar**.  
  
3.  Na próxima página, selecione **comando de Menu** e, em seguida, escolha **próxima**.  
  
4.  Na próxima página, defina **nome do comando** à `Fabrikam Command` e **ID do comando** para `cmdidFabrikamCommand`e, em seguida, escolha **Avançar**.  
  
5.  Sobre o **selecionar opções de projeto de teste** página, desmarque as opções de teste e, em seguida, escolha o **concluir** botão.  
  
6.  No projeto ShellExtensionsVSIX, abra o arquivo de vsixmanifest.  
  
     O **ativos** seção deve conter uma entrada para o projeto VSShellStub.AboutBoxPackage.  
  
7.  Escolha o **New** botão.  
  
8.  No **adicionar novo ativo** janela, no **tipo** lista, selecione **VSPackage**.  
  
9. No **fonte** lista, certifique-se de que **um projeto na solução atual** está selecionado. No **Project** caixa de listagem, selecione **MenuCommandsPackage**.  
  
10. Salve e feche o arquivo.  
  
11. Recompile a solução e iniciar a depuração o shell isolado.  
  
12. Na barra de menus, escolha **ferramentas** menu, em seguida, **comando Fabrikam**.  
  
     Deve aparecer uma caixa de mensagem.  
  
13. Pare a depuração do aplicativo.  
  
## <a name="adding-a-mef-component-part"></a>Adicionando uma parte do componente MEF  
 As etapas a seguir mostram como adicionar uma parte do componente de MEF para seu aplicativo de shell isolado.  
  
#### <a name="to-add-a-mef-component"></a>Para adicionar um componente MEF  
  
1.  No **adicionar novo projeto** caixa de diálogo **Visual c#**, **extensibilidade**, use o **margem do Editor** modelo para adicionar um projeto. Nomeie-o como `ShellEditorMargin`.  
  
2.  No projeto ShellExtensionsVSIX, abra o arquivo de vsixmanifest no modo Design, não o modo de exibição de código.  
  
3.  No `Asset` , escolha **adicionar conteúdo**.  
  
4.  No **adicionar novo ativo** janela, no **tipo** lista, selecione **mefcomponent**.  
  
5.  No **fonte** lista, certifique-se de que **um projeto na solução atual** está selecionado. No **Project** caixa de listagem, selecione **ShellEditorMargin**.  
  
6.  Salve e feche o arquivo.  
  
7.  Recompile a solução e iniciar a depuração o shell isolado.  
  
8.  Abra um arquivo de texto.  
  
     Uma margem verde que contém as palavras "Hello world!" deve ser exibida na parte inferior da janela de arquivo de texto.  
  
9. Pare a depuração do aplicativo.  
  
## <a name="adding-a-generic-vsix-project"></a>Adicionando um projeto VSIX genérico  
  
#### <a name="to-add-a-generic-vsix-project"></a>Para adicionar um projeto VSIX genérico  
  
1.  No **adicionar novo projeto** caixa de diálogo **Visual c#**, **extensibilidade**, use o **VSIXProject** modelo para adicionar um projeto. Nomeie-o como `EmptyVSIX`.  
  
2.  No projeto ShellExtensionsVSIX, abra o arquivo de Source.extensions.vsixmanifest na exibição de Design, não o modo de exibição de código.  
  
3.  No `Assets` , escolha **New**.  
  
4.  No **adicionar novo ativo** janela, no **tipo** , selecione o tipo de conteúdo que você deseja adicionar.  
  
5.  Na **fonte**, certifique-se de que o **um projeto na solução atual** opção está selecionada. Na caixa de listagem, selecione o nome do seu projeto VSIX.  
  
6.  Salve e feche o arquivo.  
  
7.  Se esse projeto inclui o código compilado, você deve editar o projeto para que o assembly seja incluído na saída.  
  
    1.  Descarregue o projeto VSIX e abra o arquivo de projeto.  
  
    2.  No primeiro `<PropertyGroup>` bloco, altere o valor da `<CopyBuildOutputToOutputDirectory>` para `true`.  
  
    3.  Salve e recarregue o projeto.  
  
8.  Criar e executar a solução.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: criar um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)

