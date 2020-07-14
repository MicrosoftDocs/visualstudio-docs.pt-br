---
title: 'Como: personalizar um pacote de solução do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerAdvanced
- VS.SharePointTools.RAD.PackageDesigner.Manifest
- VS.SharePointTools.RAD.PackageDesignerProperties
- VS.SharePointTools.RAD.PackageDesigner.SwitchView
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 77b66160d489f711b5588fdcdd024d13769d734f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016871"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>Como: personalizar um pacote de solução do SharePoint
  Você pode usar o designer de pacote para criar e personalizar um pacote (*. wsp*). Por exemplo, você pode adicionar recursos e itens de projeto do SharePoint, especificar se o servidor Web é redefinido quando a solução é implantada e definir o tipo de servidor de implantação.

## <a name="open-the-package-designer"></a>Abrir o designer de pacotes

#### <a name="to-open-the-package-designer"></a>Para abrir o designer de pacotes

- Em **Gerenciador de soluções**, clique duas vezes em **pacote**ou escolha **Designer de exibição** no menu de atalho do **pacote**.

## <a name="view-the-packaged-manifestffile"></a>Exibir o pacote de manifestfFile
 Você pode usar o designer de pacote para modificar e gerar o arquivo de manifesto empacotado. Em seguida, você pode exibir o código XML para este arquivo no Visual Studio.

#### <a name="to-view-the-xml-source-file"></a>Para exibir o arquivo de origem XML

1. No **Designer de pacotes**, escolha **manifesto**.

#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>Para exibir o arquivo de manifesto empacotado usando Gerenciador de Soluções

1. Em **Gerenciador de soluções**, escolha **Mostrar todos os arquivos**.

2. Expanda pacote, expanda pacote. pacote e abra o arquivo *Package.Template.xml* .

    > [!NOTE]
    > Quando você abre o arquivo XML do manifesto para o modelo de pacote, os arquivos são validados automaticamente e você pode ignorar os avisos que aparecem na janela Lista de Erros.

## <a name="change-the-manifest-template"></a>Alterar o modelo de manifesto
 Você pode alterar o código XML do arquivo de manifesto empacotado no editor de XML do Visual Studio ou no painel modelo de manifesto. Todas as alterações no código XML são mescladas no arquivo de manifesto empacotado para o pacote.

#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>Para alterar o modelo de manifesto usando o editor de XML

1. No **Designer de pacotes**, escolha a guia **manifesto** , expanda o nó opções de **edição** e, em seguida, escolha o link **abrir no editor de XML** .

     As alterações no XML são mescladas no arquivo de manifesto empacotado.

#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>Para alterar o modelo de manifesto usando o painel modelo de manifesto

1. No **Designer de pacotes**, escolha a guia **manifesto** , expanda o nó opções de **edição** e, em seguida, altere o XML que aparece no painel modelo de manifesto.

     As alterações no XML aparecem na **visualização do painel manifesto empacotado** .

## <a name="overwrite-the-packaged-manifest-file"></a>Substituir o arquivo de manifesto empacotado
 Você pode desabilitar o designer de pacotes e criar o arquivo de *manifest.xml* manualmente. Na primeira vez que você executar esse procedimento, as configurações atuais no designer de pacotes serão salvas no arquivo XML do modelo de pacote. Em seguida, você pode modificar ou substituir o código XML.

> [!NOTE]
> Se você adicionar ou remover itens de projeto do SharePoint e recursos no arquivo XML enquanto o designer de pacotes estiver desabilitado, esses itens e recursos de projeto não serão empacotados.

#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>Para substituir o arquivo de manifesto empacotado desabilitando o designer

1. No **Designer de pacotes**, escolha a guia **manifesto** .

2. Expanda o nó **Opções de edição** , escolha o link **substituir XML gerado e editar manifesto no editor de XML** e, em seguida, escolha o botão **Sim** .

     O modelo é atualizado com o arquivo de manifesto empacotado atual.

## <a name="enable-the-package-designer"></a>Habilitar o designer de pacotes
 Você pode reabilitar o designer de pacote para personalizar o arquivo de *manifest.xml* .

#### <a name="to-re-enable-the-designer"></a>Para reabilitar o designer

1. No **Designer de pacotes**, escolha a **descartar as edições do manifesto e reabilitar o link do designer** e, em seguida, escolha o botão **Sim** .

     O modelo é atualizado com o texto original e todas as alterações no XML são perdidas.

## <a name="see-also"></a>Consulte também
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
