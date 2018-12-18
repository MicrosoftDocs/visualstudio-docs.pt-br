---
title: Configuração de administradores para assinaturas de nuvem | Microsoft Docs
author: evanwindom
ms.author: jaunger
manager: evelynp
ms.date: 03/28/2018
ms.topic: Get-Started-Article
description: Configuração de administradores para assinaturas de nuvem
ms.prod: vs-subscription
ms.technology: vs-subscriptions
searchscope: VS Subscription
ms.openlocfilehash: 861862d964d5ccd8e926730f648a41bc790bc64d
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44283438"
---
# <a name="set-up-administrators-for-visual-studio-cloud-subscriptions"></a>Configure administradores para assinaturas de nuvem do Visual Studio

As assinaturas de nuvem do Visual Studio são gerenciadas por administradores. Essas pessoas podem atribuir assinaturas, editar atribuições, adicionar ou excluir assinaturas e executar outras tarefas de gerenciamento de assinatura.

## <a name="the-azure-subscription-owner-is-the-first-administrator"></a>O proprietário da assinatura do Azure é o primeiro administrador

Ao comprar assinaturas de nuvem do Visual Studio, como o proprietário da assinatura do Azure usado para fazer as compras, você é configurado automaticamente como administrador dessas assinaturas.

Você pode comprar assinaturas de nuvem por meio do [Visual Studio Marketplace](https://marketplace.visualstudio.com/subscriptions) ou contatando um Provedor de Soluções na Nuvem. Se comprar por meio do Visual Studio Marketplace, no final da experiência de compra, você terá a oportunidade de gerenciar usuários. Ao escolher essa opção, você será levado para o portal de gerenciamento de assinaturas do Visual Studio – [https://manage.visualstudio.com](https://manage.visualstudio.com).

Depois de comprar assinaturas, você poderá visitar o [portal de gerenciamento](https://manage.visualstudio.com) a qualquer momento. Basta entrar no portal e selecionar a assinatura do Azure apropriada no canto superior esquerdo.

Como o proprietário da assinatura do Azure usado para comprar as assinaturas de nuvem, você também pode atribuir outros administradores.

## <a name="add-administrators"></a>Adicionar administradores

Para adicionar administradores:

1. Conecte-se ao Portal do Azure em [portal.azure.com](https://portal.azure.com).
2. Entre com a conta usada para comprar as assinaturas de nuvem do Visual Studio.
3. No painel de navegação esquerdo, role para baixo até **Gerenciamento de Custos + Cobrança**.
4. Na lista **Minhas assinaturas**, escolha a assinatura do Azure que você usou para fazer a compra.
5. Clique em **Controle de acesso**, que está localizado na parte superior da lista no painel de navegação esquerdo.
6. Clique na guia **Adicionar** na parte superior da página.
7. No painel de submenu à direita, clique no nome do assinante que deseja tornar um administrador.
8. Clique na lista suspensa **Função** na parte superior do painel, role para baixo e selecione **Administrador de Acesso do Usuário**.
9. Clique em **Salvar**.

O assinante designado aparecerá no centro da página e sua função será mostrada como "Administrador de Acesso do Usuário".

Agora, o novo administrador pode entrar no [portal de gerenciamento](https://manage.visualstudio.com), selecionar a mesma assinatura do Azure que foi usada para comprar as assinaturas de nuvem na lista no canto superior esquerdo da página e começar a gerenciar essas assinaturas.


> [!NOTE]
> Se você vir os usuários com acesso para editar suas assinaturas de nuvem que você não estabeleceu como administradores, isso poderá significar que eles têm funções na assinatura do Azure subjacente que lhes permite gerenciar assinaturas. Essas funções incluem: proprietário, colaborador, administrador de serviços ou coadministrador. Para obter mais informações, visite [Add billing managers](/azure/devops/organizations/billing/add-backup-billing-managers?view=vsts) (Adicionar gerenciadores de cobrança).

Para obter informações sobre assinaturas de nuvem do Visual Studio, confira [Visão geral](vscloud-overview.md) em Comprando assinaturas de nuvem. Para comprar assinaturas de nuvem do Visual Studio, visite o Visual Studio Marketplace em [https://marketplace.visualstudio.com/subscriptions](https://marketplace.visualstudio.com/subscription).