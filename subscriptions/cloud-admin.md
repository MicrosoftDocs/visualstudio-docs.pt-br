---
title: Configurando administradores para assinaturas mensais do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 8b30e2bc-2ac3-4fcc-b296-128731471032
ms.date: 02/18/2021
ms.topic: how-to
description: Configurando administradores para assinaturas mensais
ms.openlocfilehash: c018dbc3437c03c6d029a98c84e0b6cceaef9e2c
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249533"
---
# <a name="set-up-admins-for-visual-studio-monthly-subscriptions"></a>Configurar administradores para assinaturas mensais do Visual Studio

As assinaturas mensais do Visual Studio são gerenciadas por administradores. Essas pessoas podem atribuir assinaturas, editar atribuições, adicionar ou excluir assinaturas e executar outras tarefas de gerenciamento de assinatura.

## <a name="the-azure-subscription-owner-is-the-first-admin"></a>O proprietário da assinatura do Azure é o primeiro administrador

Quando você adquire assinaturas mensais do Visual Studio, como o proprietário da assinatura do Azure usada para fazer as compras, você é automaticamente configurado como um administrador para essas assinaturas.

Você pode adquirir assinaturas mensais por meio do [Visual Studio Marketplace](https://marketplace.visualstudio.com/subscriptions)ou contatando um provedor de soluções na nuvem. Se comprar por meio do Visual Studio Marketplace, no final da experiência de compra, você terá a oportunidade de gerenciar usuários. Escolher essa opção levará você para o portal de administração de assinaturas do Visual Studio- [https://manage.visualstudio.com](https://manage.visualstudio.com) .

Depois de comprar assinaturas, será possível acessar o [Portal de Administração](https://manage.visualstudio.com) a qualquer momento. Basta entrar no portal e selecionar a assinatura apropriada do Azure no canto superior esquerdo.

Como o proprietário da assinatura do Azure usado para comprar as assinaturas mensais, você também pode atribuir administradores adicionais.

## <a name="add-admins"></a>Adicionar administradores

Para adicionar administradores:

1. Conecte-se ao portal do Azure em [Portal.Azure.com](https://portal.azure.com).
2. Entre com a conta que você usou para comprar as assinaturas mensais do Visual Studio.
3. Em **Serviços do Azure**, escolha **Gerenciamento de custos + cobrança**.
   > [!div class="mx-imgBorder"]
   > ![Escolha gerenciamento de custos + cobrança em serviços do Azure](_img/cloud-admin/azure-cost-billing.png "Escolha o gerenciamento de custos no grupo de serviços do Azure")
4. Na lista **minhas assinaturas** , escolha a assinatura do Azure que você usou para fazer a compra.
   > [!div class="mx-imgBorder"]
   > ![Escolha uma assinatura](_img/cloud-admin/subscription-list.png "Escolha a assinatura do Azure que você deseja usar para fazer sua compra.")
5. Clique em **controle de acesso (iam)**, que está localizado próximo à parte superior da lista no painel de navegação esquerdo.
6. Clique na guia **Adicionar** na parte superior da página.
7. Clique em **Adicionar atribuição de função**.
   > [!div class="mx-imgBorder"]
   > ![Escolher controle de acesso, adicionar, adicionar atribuição de função](_img/cloud-admin/access-control-add.png "Escolha controle de acesso na lista à esquerda e, em seguida, escolha Adicionar.")
8. No painel de submenu à direita, clique na lista suspensa **Função** na parte superior do painel, role para baixo e selecione **Administrador de Acesso do Usuário**.
9. Na lista de usuários role para baixo até o usuário que você deseja tornar administrador e selecione-o. 
   > [!div class="mx-imgBorder"]
   > ![Escolher função, administrador de acesso do usuário](_img/cloud-admin/add-role-user-access-admin.png "Escolha função, selecione administrador de acesso do usuário e, em seguida, selecione o nome do usuário para torná-lo um administrador.")
10. Clique em **Salvar**.
11. Clique na guia **Atribuições de função** para verificar se o usuário selecionado é exibido como um Administrador de Acesso do Usuário.

Agora, o novo administrador pode entrar no [portal de administração](https://manage.visualstudio.com), selecionar a mesma assinatura do Azure que foi usada para comprar as assinaturas mensais da lista no canto superior esquerdo da página e começar a gerenciar essas assinaturas.

> [!NOTE]
> Se você vir os usuários com acesso para editar suas assinaturas mensais que você não estabeleceu como administradores, eles podem ter funções na assinatura subjacente do Azure que permitem gerenciar assinaturas. Essas funções incluem: proprietário, colaborador, administrador de serviços ou coadministrador. Para obter mais informações, visite [Adicionar gerentes de cobrança](/azure/devops/organizations/billing/add-backup-billing-managers).

Para obter informações sobre assinaturas mensais do Visual Studio, consulte a [visão geral](vscloud-overview.md) em comprando assinaturas. Para comprar as assinaturas mensais do Visual Studio, visite a Visual Studio Marketplace em [https://marketplace.visualstudio.com/subscriptions](https://marketplace.visualstudio.com/subscription) .

## <a name="resources"></a>Recursos
- [Suporte a assinaturas](https://visualstudio.microsoft.com/subscriptions/support/)


## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como gerenciar assinaturas do Visual Studio.
- [Atribuir assinaturas individuais](assign-license.md)
- [Atribuir várias assinaturas](assign-license-bulk.md)
- [Editar assinaturas](edit-license.md)
- [Determinar o uso máximo](maximum-usage.md)