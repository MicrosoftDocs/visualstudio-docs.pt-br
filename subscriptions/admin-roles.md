---
title: Superadministrador e funções de administrador para assinaturas do Visual Studio
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 6601c395-f778-48c1-ab76-cf454b9193e4
ms.date: 03/19/2021
ms.topic: conceptual
description: Saiba mais sobre as funções de superadministrador e administrador e como atribuir administradores.
ms.openlocfilehash: eca87026c681454925974f2e394737092c3e226d
ms.sourcegitcommit: d8d230791890cda532c263d04288dc13d2261c7f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2021
ms.locfileid: "104757588"
---
# <a name="super-admins-and-admins-for-visual-studio-subscription-agreements"></a>Superadministradores e administradores para contratos de assinatura do Visual Studio

Há duas funções diferentes no novo Portal de Administração de Assinaturas do Visual Studio para clientes do licenciamento por volume. Essas funções são semelhantes à função Contato Principal/para Notificações e à função Gerente de Assinaturas que existiam no VLSC.

**Superadministradores:** Quando uma organização é inicialmente configurada, o contato principal ou avisos se torna um superadministrador por padrão. O contato principal ou avisos pode optar por atribuir superadministradores ou administradores adicionais. Um superadministrador pode adicionar e remover outros administradores, bem como assinantes. Se houver mais de dois superadministradores no sistema, um superadministrador poderá excluir todos, exceto os dois últimos por segurança.

**Administradores:** Um administrador só pode ser atribuído por um superadministrador. Um administrador só pode gerenciar assinantes nos acordos que o superadministrador atribui a eles.

Assista a uma demonstração sobre como gerenciar administradores. 
> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4th6L]

## <a name="assigning-admins"></a>Atribuindo administradores
Para atribuir novos administradores (administradores):
1. Entre em https://manage.visualstudio.com usando um endereço de email atribuído como um superadministrador do contrato por meio do qual as assinaturas foram adquiridas.
2. Clique na guia rotulada **Gerenciar Administradores**.
3. Clique em **Adicionar**.
   > [!div class="mx-imgBorder"]
   > ![Adicionar administradores](_img/admin-roles/add-admins.png "Clique na folha gerenciar administradores e, em seguida, clique em Adicionar para atribuir novos administradores.")
4. Preencha o formulário com as informações do novo administrador.  
   > [!div class="mx-imgBorder"]
   > ![Adicionar formulário de administrador](_img/admin-roles/add-form.png "Insira as informações de entrada para o novo administrador e escolha se deseja torná-las um superadministrador.  Em seguida, clique em Adicionar.")

   > [!NOTE]
   > Caso deseje que esse administrador tenha a capacidade de atribuir administradores adicionais, lembre-se de marcar a caixa **Superadministrador**.

5. Depois de clicar em **Adicionar** para atribuir o novo administrador, ele receberá um email convidando-o para entrar no portal.  

## <a name="resources"></a>Recursos
- [Suporte para administração e assinaturas do Visual Studio](https://aka.ms/vsadminhelp)

## <a name="see-also"></a>Veja também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)



## <a name="next-steps"></a>Próximas etapas
- Saiba como [atribuir assinaturas](assign-license.md)
- Saiba mais sobre a gama completa de [benefícios da assinatura](https://visualstudio.microsoft.com/vs/benefits/)
- [Definir preferências de contrato](admin-prefs.md)