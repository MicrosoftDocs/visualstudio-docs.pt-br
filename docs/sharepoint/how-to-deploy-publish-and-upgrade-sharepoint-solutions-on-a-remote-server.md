---
title: Implantar, publicar, & atualizar soluções do SharePoint remotamente
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- remote deployment [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, remote deployment
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f05f42f8aed35696b962e71a5fce86c2956b3661
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016810"
---
# <a name="how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server"></a>Como implantar, publicar e atualizar soluções do SharePoint em um servidor remoto
  Além de implantar soluções do SharePoint no sistema local, você pode publicar soluções do SharePoint em área restrita em sites remotos ou sites locais do SharePoint. O processo de publicação remota copia o arquivo *. wsp* para o servidor do SharePoint, instala a solução e, em seguida, permite que você ative a solução. Você também pode atualizar uma instalação de solução do SharePoint remota depois que as alterações forem feitas.

## <a name="to-publish-a-sandboxed-sharepoint-solution-to-a-remote-sharepoint-server"></a>Para publicar uma solução do SharePoint em área restrita em um servidor remoto do SharePoint

1. No **Gerenciador de soluções**, abra o menu de atalho do projeto do SharePoint em área restrita que você deseja publicar e escolha **publicar**.

2. Na caixa de diálogo **publicar** , escolha o botão de opção **publicar no site do SharePoint** e, em seguida, insira uma URL para um site de publicação online, como: `https://mytestsite.sharepoint.microsoftonline.com` .

3. Escolha a **página abrir a Galeria de soluções no navegador após** o botão de publicação para exibir a lista de soluções na página **Galeria de soluções** após a publicação.

4. Escolha o botão **Publicar**.

5. Entre no servidor remoto se a autenticação do usuário for necessária.

     O progresso da publicação aparece na janela **saída** do Visual Studio. Quando o processo é concluído, o arquivo da solução (*. wsp*) é instalado no servidor remoto do SharePoint. No entanto, ele ainda deve ser ativado antes que possa ser usado no SharePoint.

6. Na página **Galeria de soluções** , selecione o aplicativo SharePoint e, em seguida, na faixa de opções, escolha o botão **Ativar** .

7. Na caixa de diálogo **Ativar solução** , na faixa de faixas, escolha o botão **Ativar** novamente.

     A coluna **status** na página **Galeria de soluções** indica que o aplicativo está ativo.

## <a name="to-upgrade-a-sandboxed-sharepoint-solution-on-a-remote-sharepoint-server"></a>Para atualizar uma solução do SharePoint em área restrita em um servidor remoto do SharePoint
 Se uma solução do SharePoint em área restrita já estiver publicada em um servidor remoto, o processo a seguir permitirá que você o atualize depois de fazer alterações no aplicativo no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

1. Renomeie o pacote do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Para fazer isso, em **Gerenciador de soluções** Abra o pacote. Ele aparece no **Explorador de pacotes**.

2. No **Explorador de pacotes**, na caixa **nome** , altere o nome do pacote para um nome exclusivo.

3. Salve o projeto.

4. No **Gerenciador de soluções**, abra o menu de atalho do projeto e escolha **publicar**.

5. Na caixa de diálogo **publicar** , escolha o botão de opção **publicar no site do SharePoint** e, em seguida, se a URL do servidor remoto em que a solução está salva estiver ausente, insira-a.

6. Escolha a **página abrir a Galeria de soluções no navegador após** o botão de publicação para exibir a lista de soluções na página **Galeria de soluções** após a publicação.

7. Escolha o botão **Publicar**.

8. Entre no servidor remoto se a autenticação do usuário for necessária.

     Se você fez logon no servidor remoto recentemente, a autenticação pode não ser necessária.

     Se a versão mais antiga do aplicativo com o mesmo nome ainda existir no servidor do SharePoint, você receberá um erro informando que já existe um pacote com o mesmo nome no servidor do SharePoint. Você deve renomear o pacote para um nome exclusivo antes da publicação.

9. Escolha o novo aplicativo no SharePoint e, na faixa de faixas, escolha o botão **Atualizar** .

10. Na caixa de diálogo **Atualizar solução** , na faixa de faixas, escolha o botão **Atualizar** novamente. A coluna **status** na página da **Galeria de soluções** agora deve indicar que o aplicativo está ativo.

     A versão antiga da solução é desativada, a nova versão da solução é atualizada com os dados mantidos da solução antiga, e a nova solução é ativada no SharePoint.

## <a name="see-also"></a>Consulte também
- [Como implantar e publicar uma solução do SharePoint em um site do SharePoint local](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md)
- [Criar pacotes de solução do SharePoint](../sharepoint/creating-sharepoint-solution-packages.md)
- [Como: personalizar um pacote de solução do SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [Como adicionar e remover recursos e itens para um pacote usando o designer de pacotes](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
