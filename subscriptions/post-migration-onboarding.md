---
title: Integrar o Portal de Administração de Assinaturas do Visual Studio depois da migração da sua organização
Author: evanwindom
Ms.author: jaunger
Manager: evelynp
Ms.date: 07/12/2018
Ms.topic: Get-Started-Article
Description: Learn how to successfully onboard your organization for Visual Studio subscriptions after migrating to the administration portal.
Ms.prod: vs-subscription
Ms.technology: vs-subscriptions
Searchscope: VS Subscription
ms.openlocfilehash: 0740abb865856470b80d0706794f8e49423e72b2
ms.sourcegitcommit: 6672a1e9d135d7e5cca3cceea07c6fe5a0871475
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/28/2018
ms.locfileid: "47443513"
---
# <a name="onboard-to-the-visual-studio-subscriptions-administration-portal-after-your-organization-was-migrated"></a>Integrar o Portal de Administração de Assinaturas do Visual Studio depois da migração da sua organização 

Se recentemente você tiver gerenciado as assinaturas do Visual Studio no VLSC (Centro de Serviços de Licenciamento por Volume) da Microsoft e se tiver visitado o site para gerenciar assinaturas, observará que o gerenciamento de assinatura não está mais disponível no VLSC. Seu processo para gerenciar assinaturas seria semelhante a isso:
> [!div class="mx-imgBorder"]
> ![Captura de tela do VLSC da Microsoft, com a guia Assinaturas realçada](_img/post-migration-onboarding/vlsc-subscriptions.png)

No entanto, as assinaturas agora são gerenciadas por meio de um novo portal chamado de Portal de Administração de Assinaturas do Visual Studio. Normalmente, o contato principal ou de notificações do contrato de licenciamento por volume da sua organização conclui este processo. Caso contrário, as informações a seguir o ajudarão a obter acesso ao gerenciamento de assinaturas. 

Você pode encontrar um dos vários cenários a seguir:
1.  [O contato principal não concluiu o processo de integração.](#Onboarding-not-completed-by-Primary-Contact)<sup>1</sup> 
2.  [O contato principal concluiu a integração, mas não o adicionou como administrador. Suas credenciais foram listadas no VLSC.](#Primary-Contact-did-not-provide-you-administrator-access) 
3.  [O contato principal concluiu a integração, mas não o adicionou como administrador. Suas credenciais não foram listadas no VLSC.](#Your-credentials-were-not-listed-in-VLSC-prior-to-migration)  

<sup>1</sup> Se você for o contato principal ou de notificações e não tiver concluído o processo de integração, precisará seguir as etapas no cenário um para configurar a sua organização. 

As seções a seguir fornecem mais detalhes sobre cada um dos cenários. 

## <a name="onboarding-not-completed-by-primary-contact"></a>A integração não foi concluída pelo contato principal

Se o contato principal não tiver concluído a experiência de integração, você verá a tela a seguir. Se você tiver acesso ao [VLSC (Centro de Serviços de Licenciamento por Volume)](https://www.microsoft.com/Licensing/servicecenter/default.aspx), pode concluir esse processo e obter acesso para gerenciar assinaturas. Você precisará do [número público de cliente (PCN)](find-pcn.md) da sua organização, que pode ser encontrado no VLSC. 

No campo PCN, insira o [PCN](find-pcn.md) e selecione **Enviar Email de Convite**. 
> [!div class="mx-imgBorder"]
> ![Captura de tela do Portal de Administração de Assinaturas do Visual Studio](_img/post-migration-onboarding/send-invitation.png)

Você receberá um email com um link exclusivo para concluir o processo de integração. Clique no link do email, entre com seu endereço de email e digite o PCN mais uma vez. O link exclusivo do email é o que permite que você tenha acesso ao Portal de Administração de Assinaturas do Visual Studio. Você pode acessar e gerenciar as assinaturas. 
> [!div class="mx-imgBorder"]
> ![Captura de tela da Notificação de sucesso](_img/post-migration-onboarding/email-success.png)


## <a name="primary-contact-did-not-provide-you-administrator-access"></a>O contato principal não forneceu o acesso de administrador a você

Se o seu contato principal concluiu o processo de integração e suas credenciais estavam anteriormente no VLSC, mas o contato principal não forneceu acesso, você verá a notificação a seguir. Para se tornar administrador, entre em contato com um dos superadministradores da sua organização listados na notificação.
> [!div class="mx-imgBorder"]
> ![Captura de tela do Portal de Administração de Assinaturas do Visual Studio, com lista de superadministradores](_img/post-migration-onboarding/admin-list.png)

## <a name="your-credentials-were-not-listed-in-vlsc-prior-to-migration"></a>Suas credenciais não estavam listadas no VLSC antes da migração

Se o contato principal concluiu a integração, mas não o adicionou como um usuário e as suas credenciais não foram listadas anteriormente no VLSC, você verá a notificação a seguir. Entre em contato com seu [contato principal](find-primary-contact.md) para ter acesso ao portal. 
> [!div class="mx-imgBorder"]
> ![Captura de tela do Portal de Administração de Assinaturas do Visual Studio com a notificação "Não foi possível encontrá-lo"](_img/post-migration-onboarding/cant-find-you.png)