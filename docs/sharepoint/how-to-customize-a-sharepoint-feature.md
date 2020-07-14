---
title: 'Como: personalizar um recurso do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner.SwitchView
- VS.SharePointTools.RAD.featureDesigner.Manifest
- VS.SharePointTools.RAD.FeatureDesignerProperties
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a330f3c4cbe1e410ddc6a1612796c92eeda281b8
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016900"
---
# <a name="how-to-customize-a-sharepoint-feature"></a>Como: personalizar um recurso do SharePoint
  Você pode criar e personalizar recursos do SharePoint usando o Feature designer no Visual Studio. Por exemplo, você pode definir o escopo do recurso e adicionar outros recursos como dependências. Por padrão, o designer de recursos é aberto quando você adiciona um novo recurso no Gerenciador de Soluções ou no Gerenciador de pacotes do SharePoint.

## <a name="opening-the-feature-designer"></a>Abrindo o designer de recursos
 Você pode adicionar ou remover itens de projeto do SharePoint para um recurso usando o designer de recursos.

#### <a name="to-open-the-feature-designer"></a>Para abrir o designer de recursos

1. Em **Gerenciador de soluções**, expanda **recursos**.

2. Clique duas vezes no item *Feature1* ou abra o menu de atalho para o item *Feature1* e escolha **Designer de exibição**.

## <a name="view-the-packaged-manifest-file"></a>Exibir o arquivo de manifesto empacotado
 Você pode usar o designer de recursos para modificar e gerar o arquivo de manifesto empacotado para o recurso (*feature.xml*). Em seguida, você pode exibir o código XML para este arquivo no Visual Studio.

#### <a name="to-view-the-packaged-manifest-file"></a>Para exibir o arquivo de manifesto empacotado

1. No **Designer de recursos**, escolha a guia **manifesto** .

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>Para exibir o arquivo de manifesto empacotado usando Gerenciador de Soluções

1. Em **Gerenciador de soluções**, escolha o ícone **Mostrar todos os arquivos** .

2. Expanda recursos, expanda FeatureName, expanda FeatureName. Feature e, em seguida, abra o arquivo * \<FeatureName>.Template.xml* .

    > [!NOTE]
    > Quando você abre o arquivo XML de manifesto do modelo de recurso, os arquivos são validados automaticamente e os avisos que aparecem na janela de Lista de Erros podem ser ignorados.

## <a name="change-the-manifest-template"></a>Alterar o modelo de manifesto
 Você pode alterar o código XML para o arquivo de manifesto de recurso no editor de XML do Visual Studio ou no painel de modelo de manifesto. Todas as alterações no código XML são mescladas no arquivo de manifesto empacotado para o recurso. Por exemplo, talvez você queira alterar o modelo de manifesto para personalizar uma propriedade de recurso.

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>Para alterar o modelo de manifesto usando o editor de XML

1. No **Designer de recursos**, escolha a guia **manifesto** , expanda o nó opções de **edição** e, em seguida, escolha o link **abrir no editor de XML** .

     As alterações no XML são mescladas no arquivo de manifesto empacotado.

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>Para alterar o modelo de manifesto usando o painel modelo de manifesto

1. No **Designer de recursos**, escolha a guia **manifesto** , expanda o nó opções de **edição** e, em seguida, altere o XML que aparece no painel modelo de manifesto.

     As alterações no XML aparecem na **visualização do painel manifesto empacotado** .

## <a name="overwrite-the-packaged-manifest-file"></a>Substituir o arquivo de manifesto empacotado
 Você pode desabilitar o designer de recursos e criar o arquivo de *feature.xml* manualmente. Na primeira vez que você executar esse procedimento, as configurações atuais no designer de recursos serão salvas no arquivo XML do modelo de recurso. Em seguida, você pode modificar ou substituir o código XML.

> [!NOTE]
> Se você adicionar ou remover itens de projeto do SharePoint no arquivo XML enquanto o designer de recursos estiver desabilitado, esses itens de projeto não serão empacotados.

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>Para substituir o arquivo de manifesto empacotado desabilitando o designer

1. No **Designer de recursos**, escolha a guia **manifesto** .

2. Expanda o nó **Opções de edição** , escolha o link **substituir XML gerado e editar manifesto no editor de XML** e, em seguida, escolha o botão **Sim** .

     O modelo é atualizado com o arquivo de manifesto empacotado atual.

## <a name="enable-the-feature-designer"></a>Habilitar o designer de recursos
 Você pode reabilitar o designer de recursos para personalizar o arquivo de *feature.xml* .

#### <a name="to-re-enable-the-designer"></a>Para reabilitar o designer

1. No **Designer de recursos**, escolha o **manifesto descartar edições e reabilitar o link do designer** e, em seguida, escolha o botão **Sim** .

2. O modelo é atualizado com o texto original e todas as alterações no XML são perdidas.

## <a name="see-also"></a>Consulte também
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
