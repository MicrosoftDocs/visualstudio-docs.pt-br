---
title: Excluir atribuições de assinatura no portal de administração de assinaturas do Visual Studio | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: e49242bc-e9f2-49e8-8caa-f574d508aba6
ms.date: 06/16/2020
ms.topic: how-to
description: Saiba como os administradores podem excluir atribuições de assinatura
ms.openlocfilehash: e6ce84aa84e25bcdeb44b93954289a65a3454010
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902907"
---
# <a name="delete-assignments-in-visual-studio-subscriptions"></a>Excluir atribuições em assinaturas do Visual Studio
Quando um assinante não precisar mais de uma assinatura do Visual Studio, por exemplo, ao deixar a empresa, ao concluir um projeto ou ao mudar para um novo cargo de trabalho, será possível remover essa assinatura e atribuí-la a outra pessoa. Observe que quando você reatribui uma assinatura, nem todos os benefícios do Assinante serão redefinidos.  O novo usuário poderá solicitar todas as chaves não solicitadas e exibir as chaves anteriormente solicitadas, mas os limites de solicitação **não** serão redefinidos.  Para organizações que têm contratos EA (Contrato Enterprise), todos os benefícios que já tiverem sido usados pelo usuário original, como treinamentos do Pluralsight, serão redefinidos. 

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4yG2q]

## <a name="delete-a-subscription-assignment"></a>Excluir uma atribuição de assinatura
1. Clique no nome do assinante que deseja remover. Para selecionar vários assinantes para remoção, você pode clicar no círculo à esquerda do nome do assinante para selecionar cada um.  Como alternativa, você pode manter pressionada a tecla **Ctrl** e clicar em cada Assinante que deseja remover. Para remover um intervalo de assinantes, clique no primeiro, pressione a tecla **Shift** e clique no último.  Pressione **Ctrl + a** para selecionar e remover todos os assinantes. 
2. Para excluir os assinantes selecionados, clique em **Excluir**.
3. Quando a mensagem aparecer para você confirmar a exclusão, clique em **OK**.
   > [!div class="mx-imgBorder"]
   > ![Excluir assinantes](_img/delete-license/delete-subscribers.png)

   > [!NOTE]
   > A exclusão em massa usando um modelo não está disponível. Para organizações que gerenciam atribuições de assinatura por meio de Azure Active Directory grupos de segurança, consulte [nosso artigo](assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions) para obter mais informações sobre como as exclusões acontecem.  

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](https://docs.microsoft.com/visualstudio/)
- [Documentação do Azure DevOps](https://docs.microsoft.com/azure/devops/)
- [Documentação do Azure](https://docs.microsoft.com/azure/)
- [Documentação do Microsoft 365](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Precisa alterar uma assinatura sem excluí-la?  Saiba como [editar assinaturas](edit-license.md)
- Para obter ajuda para encontrar uma assinatura específica, confira [Pesquisar por uma assinatura](search-license.md).
- Precisa criar uma lista de todas as suas assinaturas?  Confira [Exportar assinaturas](exporting-subscriptions.md).


