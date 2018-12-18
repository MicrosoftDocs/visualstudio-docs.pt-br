---
title: 'Como: personalizar um pacote de solução do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.RAD.PackageDesignerAdvanced
- VS.SharePointTools.RAD.PackageDesigner.Manifest
- VS.SharePointTools.RAD.PackageDesignerProperties
- VS.SharePointTools.RAD.PackageDesigner.SwitchView
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fd1ebe9e49a0b3e26d090fdbbdbbe4dd37c0344a
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118536"
---
# <a name="how-to-customize-a-sharepoint-solution-package"></a>Como: personalizar um pacote de solução do SharePoint
  Você pode usar o Designer de pacote para criar e personalizar um pacote (*. wsp*). Por exemplo, você pode adicionar itens de projeto do SharePoint e recursos, especifique se o servidor Web é redefinido quando a solução é implantada e defina o tipo de servidor de implantação.  
  
## <a name="open-the-package-designer"></a>Abra o Designer de pacote  
  
#### <a name="to-open-the-package-designer"></a>Para abrir o Designer de pacote
  
-   Na **Gerenciador de soluções**, clique duas vezes em **pacote**, ou escolha **View Designer** no menu de atalho para **pacote**.  
  
## <a name="view-the-packaged-manifestffile"></a>Exibir o manifestfFile empacotado  
 Você pode usar o Designer de pacote para modificar e gerar o arquivo de manifesto empacotado. Em seguida, você pode exibir o código XML para esse arquivo no Visual Studio.  
  
#### <a name="to-view-the-xml-source-file"></a>Para exibir o arquivo de origem XML  
  
1.  No **Designer de pacote**, escolha **manifesto**.  
  
#### <a name="to-view-the-packaged-manifest-file-by-using-solution-explorer"></a>Para exibir o arquivo de manifesto empacotado usando o Gerenciador de soluções  
  
1.  Na **Gerenciador de soluções**, escolha **Mostrar todos os arquivos**.  
  
2.  Expanda o pacote, expanda o pacote e, em seguida, abra o *Package.Template.xml* arquivo.  
  
    > [!NOTE]  
    >  Quando você abre o arquivo de manifesto XML para o modelo de pacote, os arquivos são validados automaticamente e você pode ignorar os avisos que aparecem na janela lista de erros.  
  
## <a name="change-the-manifest-template"></a>Alterar o modelo de manifesto  
 Você pode alterar o código XML para o arquivo de manifesto empacotado no Editor de XML do Visual Studio ou no painel de modelo de manifesto. Todas as alterações no código XML são mescladas no arquivo de manifesto empacotado para o pacote.  
  
#### <a name="to-change-the-manifest-template-by-using-the-xml-editor"></a>Para alterar o modelo de manifesto usando o Editor de XML  
  
1.  No **Designer de pacote**, escolha o **manifesto** guia, expanda o **editar opções** nó e, em seguida, escolha o **aberto no Editor de XML** link.  
  
     Alterações ao XML sejam mescladas no arquivo de manifesto do pacote.  
  
#### <a name="to-change-the-manifest-template-by-using-the-manifest-template-pane"></a>Para alterar o modelo de manifesto usando o painel do modelo de manifesto  
  
1.  No **Designer de pacote**, escolha o **manifesto** guia, expanda o **editar opções** nó e altere o XML que aparece no painel modelo de manifesto.  
  
     Alterações ao XML aparecem na **versão prévia do empacotado manifesto** painel.  
  
## <a name="overwrite-the-packaged-manifest-file"></a>Substituir o arquivo de manifesto de pacote  
 Você pode desabilitar o Designer de pacote e criar o *manifest. XML* arquivo manualmente. Na primeira vez que você executar esse procedimento, as configurações atuais no Designer de pacote são salvas no arquivo de XML do modelo de pacote. Em seguida, você pode modificar ou substituir o código XML.  
  
> [!NOTE]  
>  Se você adicionar ou remove itens de projeto do SharePoint e recursos no arquivo XML, enquanto o Designer de pacote estiver desabilitado, esses itens de projeto e os recursos não são empacotados.  
  
#### <a name="to-overwrite-packaged-manifest-file-by-disabling-the-designer"></a>Para substituir o arquivo de manifesto empacotado, desabilitando o designer  
  
1.  No **Designer de pacote**, escolha o **manifesto** guia.  
  
2.  Expanda o **editar opções** nó, escolher o **substituição XML e editar manifesto gerado no editor de XML** vincular e, em seguida, escolha o **Sim** botão.  
  
     O modelo é atualizado com o arquivo de manifesto de pacote atual.  
  
## <a name="enable-the-package-designer"></a>Habilitar o Designer de pacote  
 Você pode habilitar novamente o Designer de pacote para personalizar o *manifest. XML* arquivo.  
  
#### <a name="to-re-enable-the-designer"></a>Para habilitar novamente o designer  
  
1.  No **Designer de pacote**, escolha o **descarte as edições de manifesto e habilite novamente o designer** vincular e, em seguida, escolha o **Sim** botão.  
  
     O modelo é atualizado com o texto original, e todas as alterações ao XML serão perdidas.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
