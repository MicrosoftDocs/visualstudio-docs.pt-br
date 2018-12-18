---
title: Perguntas frequentes sobre migração de administrador do Centro de Empresas da Microsoft | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/13/2018
ms.topic: Get-Started-Article
description: Perguntas frequentes sobre migração de administrador no Centro de Empresas da Microsoft
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: e4bc2902c819f4e677127d4c2c857ed1fb5dc015
ms.sourcegitcommit: 4667e6ad223642bc4ac525f57281482c9894daf4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/20/2018
ms.locfileid: "36297541"
---
# <a name="visual-studio-subscriptions-administration-migration"></a>Migração de administração de assinaturas do Visual Studio

Nos próximos meses, serão feitas alterações no gerenciamento de assinaturas do Visual Studio (antigas assinaturas do MSDN). No momento, você pode comprar assinaturas do Visual Studio por meio de licenciamento por volume e as assinaturas são gerenciadas no portal do Centro de Empresas da Microsoft. Um novo portal de gerenciamento está sendo criado e as assinaturas do Visual Studio passarão a ser gerenciadas nesse novo portal. Além das operações existentes fornecidas pelo Centro de Empresas da Microsoft, o novo portal permite a atribuição em massa sem limites, o rastreamento e a filtragem de assinaturas e a capacidade de usar o Azure AD (Azure Active Directory) para gerenciar acesso. O novo Portal de Administração do Visual Studio estará localizado em: [https://manage.visualstudio.com](https://manage.visualstudio.com).

> [!Note]
> Essa migração não afetará os clientes do MPSA.

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="why-is-it-changing"></a>Por que isso está mudando?
O novo portal otimizará a experiência de gerenciamento de assinaturas do Visual Studio e criará uma única experiência de gerenciamento de assinaturas do Visual Studio, independentemente de como elas tenham sido compradas. O novo portal tem uma nova plataforma que habilita o Azure AD e faz frente às inovações futuras. Além disso, ele terá uma interface do usuário atualizada que será mais fácil de navegar e usar, aumentando a eficiência do administrador.

### <a name="who-will-be-impacted"></a>Quem será afetado?
A alteração afetará todos os clientes que tenham contratos ativos de licenciamento por volume e que tenham comprado as assinaturas do Visual Studio por meio de licenciamento por volume.

### <a name="when-is-it-changing"></a>Quando a alteração ocorrerá?
Essa é uma transição grande e será concluída em fases até que todos os clientes com contratos ativos de licenciamento por volume para assinaturas do Visual Studio tenham sido migrados para o novo portal de gerenciamento. A migração foi iniciada durante o primeiro trimestre de 2017. Os clientes de licenciamento por volume serão notificados antecipadamente sobre a semana agendada para migração.

### <a name="does-my-organization-need-to-sign-up-for-azure-active-directory-azure-ad"></a>Minha organização precisa se inscrever no Azure Active Directory (Azure AD)?
Sua organização não precisa se inscrever no Azure AD, mas isso pode ser feito a qualquer momento. Se você optar por se integrar ao Azure AD, faça isso sem nenhum custo usando a camada gratuita do Azure AD. Com o Azure Active Directory, você protegerá sua organização com maior segurança, controle e confiabilidade de longo prazo. No entanto, se você não estiver pronto para o Azure AD, será possível continuar usando as contas da Microsoft (MSAs) que você usa hoje.

### <a name="how-do-i-know-when-my-organization-will-be-migrated"></a>Como saber quando minha organização será migrada?
Os Contatos Principal/para Notificações receberão um email nosso convidando-os para concluir o processo de integração uma semana antes da migração da sua organização. Os Gerentes de Assinatura também receberão um email avisando-os que você contatou os Contatos Principal/para Notificações e forneceu detalhes de como ajudar a garantir o sucesso da integração. Saiba como [Localizar os Contatos Principal/para Notificações da sua organização](#How-do-I-find-out-who-my-Primary-or-Notices-Contact-is?).

### <a name="is-onboarding-different-from-migration"></a>A integração é diferente da migração?
Sim.  Há duas fases nesse processo. Configurar (ou integrar) a organização antes da migração assegura que não haja nenhuma interrupção do seu trabalho como administrador. Depois que as informações da organização forem migradas, você poderá gerenciar assinaturas do Visual Studio no novo portal. Se os Contatos Principal/para Notificações não forem integrados antes de serem migrados, os Gerentes de Assinatura serão bloqueados e não poderão gerenciar assinaturas até que você conclua o processo de integração.

### <a name="what-is-the-onboarding-process"></a>O que é o processo de integração?
Um email é enviado para os Contatos Principal/para Notificações convidando-os a concluir o processo de integração.
Confira abaixo as instruções sobre o processo.
1.  **Localizando o PCN e entrando:**

    a.  No email, os Contatos Principal/para Notificações recebem um link exclusivo e os últimos três dígitos do PCN (número do cliente).*

    b.  Para obter o PCN inteiro, o Contato Principal precisará entrar no Centro de Empresas da Microsoft (instruções para localizar o PCN podem ser encontradas abaixo).

    c.  Depois de obter o PCN, ele precisará selecionar o link exclusivo que permitirá sua entrada. Eles poderão entrar usando uma conta corporativa ou de estudante (se a organização estiver no Azure AD) ou uma conta da Microsoft (MSA) se a organização não estiver no Azure AD.

    d.  Em seguida, será solicitado que eles insiram o PCN.

2.  **Configure os administradores:**

    Depois de inserir o PCN, eles serão levados à página em que é possível adicionar superadministradores e administradores (conhecidos anteriormente como Gerentes de Assinatura). O ideal é que isso seja concluído antes da data de migração da organização, para que não haja nenhuma interrupção no gerenciamento de suas assinaturas.

3.  **Acessando o novo portal de gerenciamento de assinatura:** após a migração da organização, serão enviados emails aos administradores e superadministradores convidando-os para acessar o novo portal e começar a gerenciar assinaturas.

> [!NOTE]
> Se os Contatos Principais ou para Notificações receberem mais de um email, isso significará que eles têm mais de um PCN. Será necessário concluir o processo usando o link exclusivo para o PCN referenciado em cada email.

### <a name="what-is-the-difference-between-a-super-admin-and-an-administrator"></a>Qual é a diferença entre um superadministrador e um administrador?
Quando o Contato Principal/para Notificações entrar pela primeira vez, ele será configurado automaticamente como um superadministrador. Os superadministradores podem gerenciar o acesso de administrador às assinaturas, adicionando e excluindo outros superadministradores ou administradores e também podem gerenciar assinaturas. O superadministrador pode optar por atribuir outros superadministradores além dele mesmo.

Os administradores (conhecidos anteriormente como Gerentes de Assinatura) podem somente gerenciar assinaturas, mas não podem controlar quem tem acesso ao gerenciamento de assinaturas.

### <a name="how-will-i-as-an-administrator-onboard-to-the-new-portal"></a>Como administrador, como posso me integrar ao novo portal?
Os Contatos Principais e os Contatos para Notificações da organização receberão um email com um link exclusivo que os levará a uma página para entrar usando uma conta corporativa ou de estudante, com o apoio do Azure AD (Azure Active Directory) ou de MSAs pessoais. Depois de entrar, eles precisarão inserir o PCN (número do cliente) ou o número de autorização da organização para verificar os contratos. Em seguida, eles serão configurados como superadministradores capazes de adicionar outros administradores, como você, para gerenciar assinaturas do Visual Studio.

### <a name="where-do-i-manage-subscriptions-if-my-organization-has-been-onboarded-but-hasnt-been-migrated"></a>Onde vou gerenciar as assinaturas se minha organização for integrada, mas ainda tiver migrado?
Você continuará gerenciando assinaturas por meio do Centro de Empresas da Microsoft até receber o email de Assinaturas do Visual Studio informando que sua organização foi migrada e está pronta para ser gerenciada no novo portal.

### <a name="where-can-i-locate-my-organizations-public-customer-number-pcn-or-authorization-number"></a>Onde localizar o PCN (número do cliente) ou o número de autorização da minha organização?
Entre no [Centro de Empresas da Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx) e navegue até o caminho a seguir: **Assinaturas** > **Assinaturas do Visual Studio**. O PCN está localizado abaixo dos **Resultados de número de cliente/contrato**. Obtenha diretrizes passo a passo de como localizar seu PCN neste [artigo de ajuda](find-pcn.md).

### <a name="how-do-i-find-out-who-my-primary-or-notices-contact-is"></a>Como saber quem é o Contato Principal ou o Contato para Notificações?
Entre no [Centro de Empresas da Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx) e navegue até o caminho a seguir: **Licenças > Resumo de Relação** selecione sua **ID de Licenciamento > Contatos**. Obtenha diretrizes passo a passo de como descobrir quem é o Contato Principal ou o Contato para Notificações neste [artigo de ajuda](find-primary-contact.md).

### <a name="what-if-my-primary-or-notices-contact-is-gone-no-longer-with-the-company-or-not-available-to-complete-onboarding"></a>E se o Contato Principal ou o Contato para Notificações não estiver mais na empresa ou não estiver disponível para concluir a integração?
Você precisará [contatar o suporte](https://visualstudio.microsoft.com/subscriptions/support/#talktous) e fornecer o email que usou no Centro de Empresas da Microsoft para gerenciar assinaturas. Depois de verificar, o suporte poderá ajudá-lo no processo de integração.

### <a name="what-will-happen-with-renewing-customers"></a>O que acontece com a renovação de clientes?
A renovação das assinaturas de clientes deve continuar como de costume, pois os processos de renovação não são afetados pela migração.

### <a name="should-my-organization-wait-to-set-up-a-new-agreement-in-the-new-system-rather-than-renew-an-existing-agreement"></a>Minha organização deve esperar para configurar um novo contrato no novo sistema, em vez de renovar um contrato existente?
Nº  A migração não afetará a criação nem a renovação de contratos.

### <a name="what-if-my-organizations-agreement-is-in-the-grace-period-during-the-transition-will-they-also-be-migrated"></a>E se o contrato da minha organização estiver no período de cortesia durante a transição? Ele também será migrado?
Sim, se o contrato ainda estiver ativo, sua organização será migrada.

### <a name="what-if-my-organization-has-over-claimed-in-the-current-system-will-we-still-be-migrated-to-the-new-system"></a>E se minha organização tiver feito solicitações em excesso no sistema atual? Nós ainda seremos migrados para o novo sistema?
Sim, sua organização ainda será migrada para o novo sistema. No novo sistema, haverá a capacidade de fazer solicitações em excesso (para tipos de contrato que permitem isso).

### <a name="what-if-my-organization-has-more-than-one-subscription-assigned-to-a-single-useremail-address"></a>E se a minha organização tiver mais de uma assinatura atribuída a um único usuário/endereço de email?
Sua organização ainda será migrada.  No entanto, você não poderá atribuir assinaturas adicionais do mesmo nível (ou seja: Enterprise, Professional, etc.) para esse endereço de email/usuário. Todas as assinaturas do mesmo nível que tiverem o mesmo endereço de email após a migração ainda estarão visíveis, mas os administradores precisarão alterar os endereços de email para que eles sejam exclusivos. Não será possível atribuir várias assinaturas do mesmo nível a um único endereço de email/usuário no novo portal.

### <a name="where-can-i-find-the-most-up-to-date-information-about-the-migration"></a>Onde encontrar as informações mais atualizadas sobre a migração?
Para obter as informações mais atualizadas sobre essa migração, visite a [página da Web](https://aka.ms/vs-admin) do administrador de assinaturas do Visual Studio. Se você precisar de suporte, confira a [página de suporte](http://visualstudio.microsoft.com/subscriptions/support/#!collections/962-subscriptions) de assinaturas do Visual Studio, que contém informações de autoajuda e de contato de suporte. Nos próximos meses, continuaremos a fornecer atualizações na página da Web do administrador e por email para ajudar a facilitar essa transição.

## <a name="resources-and-support-information"></a>Recursos e informações de suporte
- [Página da Web do administrador](https://visualstudio.microsoft.com/subscriptions-administration/)

- Assinaturas do Visual Studio e [suporte](https://visualstudio.microsoft.com/subscriptions/support/) de gerenciamento

- [Como localizar meu PCN](find-pcn.md)

- [Como localizar meu Contato Principal ou para Notificações](find-primary-contact.md)

- [Vídeo](https://www.youtube.com/watch?v=ZmnywYGSFMg&list=PLReL099Y5nRfDyvvwzNDBaZe7qTxmuM2T&index=1&t=0s) para integrar sua organização e gerenciar administradores
