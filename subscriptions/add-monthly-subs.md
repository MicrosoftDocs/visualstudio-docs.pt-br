---
title: Adicionar novas assinaturas mensais do Visual Studio ao portal de administração de assinaturas | Microsoft Docs
author: evanwindom
ms.author: cabuschl
manager: cabuschl
ms.assetid: 36f0d9f1-fe28-469f-a54c-dc46638270a8
ms.date: 06/23/2020
ms.topic: how-to
description: Saiba como comprar recentemente as assinaturas mensais do Visual Studio para o portal de administração de assinaturas
ms.openlocfilehash: 778a3adbc9ca2117b0328a10d52904921bd0b80c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904696"
---
# <a name="add-new-monthly-visual-studio-subscriptions-to-the-subscriptions-administration-portal"></a>Adicionar novas assinaturas mensais do Visual Studio ao portal de administração de assinaturas
Quando você adquire novas assinaturas mensais do Visual Studio usando uma assinatura do Azure, talvez seja necessário adicioná-las ao portal de administração de assinaturas para atribuí-las aos usuários.  

## <a name="how-do-i-know-if-i-need-to-add-my-subscriptions"></a>Como fazer saber se preciso adicionar minhas assinaturas?
As etapas para adicionar assinaturas mensais dependem de quais tipos de assinaturas sua organização já tem e se você é um novo administrador.
- Se você for um novo administrador, verificaremos as assinaturas do Azure nas quais você tem direitos de administrador de acesso de usuário ao entrar no portal de administração de assinaturas na primeira vez.  Se encontrarmos assinaturas mensais para você, vamos adicioná-las automaticamente. 
- Se você tiver adicionado ou administrado assinaturas mensais anteriormente, verificaremos se há novas assinaturas mensais sempre que entrar. 
- Se você já é um administrador de assinaturas adquiridas por meio do licenciamento por volume, mas ainda não adicionou ou gerenciau assinaturas mensais, será necessário adicioná-las usando as etapas fornecidas abaixo.

## <a name="how-to-add-monthly-subscriptions"></a>Como adicionar assinaturas mensais
1. Entre no portal de administração de assinaturas em<https://manage.visualstudio.com>
1. Na guia **gerenciar assinantes** , escolha a lista suspensa **novo contrato** 
1. Escolha **novas assinaturas mensais** na lista suspensa
   > [!div class="mx-imgBorder"]
   > ![Menu suspenso adicionar novas assinaturas mensais](_img/add-monthly-subs/add-subs-drop-down.png)
1. O sistema pesquisará todas as assinaturas do Azure nas quais você tem direitos de administrador de acesso de usuário e importará todas as assinaturas do Visual Studio adquiridas com essas assinaturas do Azure.
1. Se não forem encontradas assinaturas do Azure nas quais você tem direitos de administrador de acesso do usuário ou se as assinaturas do Azure qualificadas forem encontradas, mas nenhuma assinatura do Visual Studio for encontrada, você receberá a seguinte mensagem:
   > [!div class="mx-imgBorder"]
   > ![Nenhuma assinatura mensal nova encontrada](_img/add-monthly-subs/no-subs-found.png)
1. Se novas assinaturas mensais forem encontradas, você receberá uma mensagem de confirmação
   > [!div class="mx-imgBorder"]
   > ![Mensagem de confirmação de assinaturas adicionadas](_img/add-monthly-subs/subs-added-confirmation.png)

## <a name="things-to-keep-in-mind"></a>Algumas coisas que se deve manter em mente
- A opção de adicionar novas assinaturas mensais só estará disponível na primeira vez em que você as comprar.  Depois de adicionar assinaturas mensais, verificaremos se há novas assinaturas cada vez que você entrar no Portal. 
- Quando novas assinaturas forem encontradas, você poderá ver que elas já estão atribuídas aos assinantes.  Isso ocorre porque há outros administradores com acesso à assinatura do Azure e já atribuiram as novas assinaturas do Visual Studio aos usuários.  Agora que você também os adicionou ao seu portal, você pode administrar essas assinaturas. 

## <a name="next-steps"></a>Próximas etapas
Agora que você adicionou assinaturas, você está pronto para atribuí-las aos usuários.  Você pode fazer isso de várias maneiras:
- [Atribuir assinaturas individualmente](assign-license.md)
- [Atribuir assinaturas a vários usuários](assign-license-bulk.md)
- [Atribuir assinaturas específicas a usuários específicos](assign-guid.md)

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](https://docs.microsoft.com/visualstudio/)
- [Documentação do Azure DevOps](https://docs.microsoft.com/azure/devops/)
- [Documentação do Azure](https://docs.microsoft.com/azure/)
- [Documentação do Microsoft 365](https://docs.microsoft.com/microsoft-365/)
