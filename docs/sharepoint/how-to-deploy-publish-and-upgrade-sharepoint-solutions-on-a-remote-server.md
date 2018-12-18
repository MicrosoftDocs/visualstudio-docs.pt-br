---
title: 'Como: implantar, publicar e atualizar soluções do SharePoint em um servidor remoto | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- remote deployment [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, remote deployment
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fbd21016d00bdfecfcb606e9fe2b720ab97bf3d0
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118363"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>Como: implantar, publicar e atualizar soluções do SharePoint em um servidor remoto
  Além de implantar soluções do SharePoint para o sistema local, você pode publicar soluções em área restrita do SharePoint em locais remotos ou sites locais do SharePoint. As cópias de processo de publicação remoto a *. wsp* arquivo para o servidor do SharePoint instala a solução e, em seguida, permite que você ative a solução. Você também pode atualizar uma instalação remota de solução do SharePoint depois que forem feitas alterações a ele.  
  
## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>Para publicar uma solução em área restrita do SharePoint em um servidor remoto do SharePoint  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o projeto na área restrita do SharePoint que você deseja publicar e, em seguida, escolha **publicar**.  
  
2.  No **Publish** diálogo caixa, escolha o **publicar no Site do SharePoint** botão de opção e, em seguida, insira uma URL para um site de publicação online, como: `https://mytestsite.sharepoint.microsoftonline.com`.  
  
3.  Escolha o **abrir página Galeria de soluções no navegador após a publicação** botão de opção para exibir a lista de soluções na **Galeria de soluções** página após a publicação.  
  
4.  Escolha o **publicar** botão.  
  
5.  Faça logon no servidor remoto se a autenticação do usuário é necessária.  
  
     O andamento da publicação é exibido no Visual Studio **saída** janela. Quando o processo for concluído, a solução (*. wsp*) arquivo é instalado no servidor do SharePoint remoto. No entanto, ele ainda deve ser ativado antes que ele pode ser usado no SharePoint.  
  
6.  Sobre o **Galeria de soluções** página, selecione o aplicativo do SharePoint e, em seguida, na faixa de opções, escolha o **ativar** botão.  
  
7.  No **ativar solução** caixa de diálogo, na faixa de opções, escolha o **ativar** novamente no botão.  
  
     O **Status** coluna sobre o **Galeria de soluções** página indica que o aplicativo está ativo.  
  
## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>Para atualizar uma solução em área restrita do SharePoint em um servidor remoto do SharePoint  
 Se uma solução em área restrita do SharePoint já estiver publicada em um servidor remoto, o processo a seguir permite que você atualizá-lo depois de fazer alterações para o aplicativo em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
1.  Renomeie o pacote do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para fazer isso, em **Gerenciador de soluções** abrir o pacote. Ele aparece na **Explorador de pacotes**.  
  
2.  Na **Explorador de pacotes**, no **nome** , altere o nome do pacote para um nome exclusivo.  
  
3.  Salvar o projeto.  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho para o projeto e, em seguida, escolha **publicar**.  
  
5.  No **Publish** diálogo caixa, escolha o **publicar no Site do SharePoint** botão de opção e, em seguida, se a URL para o servidor remoto em que a solução foi salvo estiver ausente, insira.  
  
6.  Escolha o **abrir página Galeria de soluções no navegador após a publicação** botão de opção para exibir a lista de soluções na **Galeria de soluções** página após a publicação.  
  
7.  Escolha o **publicar** botão.  
  
8.  Faça logon no servidor remoto se a autenticação do usuário é necessária.  
  
     Se você conectado ao servidor remoto recentemente, a autenticação não pode ser necessária.  
  
     Se a versão mais antiga do aplicativo que tem o mesmo nome ainda existe no servidor do SharePoint, você receberá um erro que um pacote com o mesmo nome já existe no servidor do SharePoint. Você deve renomear o pacote para um nome exclusivo antes da publicação.  
  
9. Escolha o novo aplicativo no SharePoint e, em seguida, na faixa de opções, escolha o **atualizar** botão.  
  
10. No **atualizar solução** caixa de diálogo, na faixa de opções, escolha o **atualizar** novamente no botão. O **Status** coluna sobre o **Galeria de soluções** página agora deve indicar que o aplicativo está ativo.  
  
     A versão antiga da solução é desativada, a nova versão da solução é atualizada com os dados mantidos da solução antiga e a nova solução é ativada no SharePoint.  
  
## <a name="see-also"></a>Consulte também
 [Como: implantar e publicar uma solução do SharePoint em um site do SharePoint local](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)   
 [Criar pacotes de solução do SharePoint](../sharepoint/creating-sharepoint-solution-packages.md)   
 [Como: personalizar um pacote de solução do SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)   
 [Como: adicionar e remover funcionalidades e itens de um pacote usando o Designer de pacote](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)  
  
