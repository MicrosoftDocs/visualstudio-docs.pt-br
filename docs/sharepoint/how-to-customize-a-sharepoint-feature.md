---
title: 'Como: personalizar um recurso do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.RAD.FeatureDesigner.SwitchView
- VS.SharePointTools.RAD.featureDesigner.Manifest
- VS.SharePointTools.RAD.FeatureDesignerProperties
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9be9ba70bb94e743a788db11b55c188275bcad64
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118353"
---
# <a name="how-to-customize-a-sharepoint-feature"></a>Como: personalizar um recurso do SharePoint
  Você pode criar e personalizar os recursos do SharePoint usando o Designer de recursos no Visual Studio. Por exemplo, você pode definir o escopo do recurso e adicionar outros recursos como dependências. Por padrão, o Designer de recursos é aberto quando você adiciona um novo recurso no Gerenciador de soluções ou o Explorador de pacotes do SharePoint.  
  
## <a name="opening-the-feature-designer"></a>Abrir o Designer de recursos  
 Você pode adicionar ou remover itens de projeto do SharePoint para um recurso usando o Designer de recursos.  
  
#### <a name="to-open-the-feature-designer"></a>Para abrir o Designer de recursos
  
1.  Na **Gerenciador de soluções**, expanda **recursos**.  
  
2.  Clique duas vezes o *Feature1* de item, ou abra o menu de atalho para o *Feature1* de item e, em seguida, escolha **View Designer**.  
  
## <a name="view-the-packaged-manifest-file"></a>Exibir o arquivo de manifesto de pacote  
 Você pode usar o Designer de recursos para modificar e gerar o arquivo de manifesto de pacote para o recurso (*Feature*). Em seguida, você pode exibir o código XML para esse arquivo no Visual Studio.  
  
#### <a name="to-view-the-packaged-manifest-file"></a>Para exibir o arquivo de manifesto de pacote  
  
1.  No **Designer de recursos**, escolha o **manifesto** guia.  
  
#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>Para exibir o arquivo de manifesto empacotado usando o Gerenciador de soluções  
  
1.  Na **Gerenciador de soluções**, escolha o **Mostrar todos os arquivos** ícone.  
  
2.  Expanda recursos, expanda o nome do recurso, expanda FeatureName.feature e, em seguida, abra o  *\<FeatureName >. Template* arquivo.  
  
    > [!NOTE]  
    >  Quando você abre o arquivo de manifesto de modelo de recurso XML, os arquivos são validados automaticamente e os avisos que aparecem na janela lista de erros podem ser ignorados.  
  
## <a name="change-the-manifest-template"></a>Alterar o modelo de manifesto  
 Você pode alterar o código XML para o arquivo de manifesto de recurso no Editor de XML do Visual Studio ou no painel de modelo de manifesto. Todas as alterações no código XML é mesclado no arquivo de manifesto do pacote para o recurso. Por exemplo, você talvez queira alterar o modelo de manifesto para personalizar uma propriedade de recurso.  
  
#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>Para alterar o modelo de manifesto usando o Editor de XML  
  
1.  No **Designer de recursos**, escolha o **manifesto** guia, expanda o **editar opções** nó e, em seguida, escolha o **aberto no Editor de XML** link.  
  
     Alterações ao XML sejam mescladas no arquivo de manifesto do pacote.  
  
#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>Para alterar o modelo de manifesto usando o painel do modelo de manifesto  
  
1.  No **Designer de recursos**, escolha o **manifesto** guia, expanda o **editar opções** nó e altere o XML que aparece no painel modelo de manifesto.  
  
     Alterações ao XML aparecem na **versão prévia do empacotado manifesto** painel.  
  
## <a name="overwrite-the-packaged-manifest-file"></a>Substituir o arquivo de manifesto de pacote  
 Você pode desabilitar o Designer de recursos e criar o *Feature* arquivo manualmente. Na primeira vez que você executar esse procedimento, as configurações atuais no Designer de recurso são salvas no arquivo de XML do modelo de recurso. Em seguida, você pode modificar ou substituir o código XML.  
  
> [!NOTE]  
>  Se você adicionar ou remove itens de projeto do SharePoint no arquivo XML, enquanto o Designer de recursos estiver desabilitado, esses itens de projeto não são compactados.  
  
#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>Para substituir o arquivo de manifesto empacotado, desabilitando o designer  
  
1.  No **Designer de recursos**, escolha o **manifesto** guia.  
  
2.  Expanda o **editar opções** nó, escolher o **substituição XML e editar manifesto gerado no editor de XML** vincular e, em seguida, escolha o **Sim** botão.  
  
     O modelo é atualizado com o arquivo de manifesto de pacote atual.  
  
## <a name="enable-the-feature-designer"></a>Habilitar o Designer de recursos  
 Você pode habilitar novamente o Designer de recursos para personalizar o *Feature* arquivo.  
  
#### <a name="to-re-enable-the-designer"></a>Para habilitar novamente o designer  
  
1.  No **Designer de recursos**, escolha o **descarte as edições de manifesto e habilite novamente o designer** vincular e, em seguida, escolha o **Sim** botão.  
  
2.  O modelo é atualizado com o texto original, e todas as alterações ao XML serão perdidas.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
