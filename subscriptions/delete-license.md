---
title: Excluir atribuições de assinatura do Visual Studio no portal de administração de assinaturas | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: e49242bc-e9f2-49e8-8caa-f574d508aba6
ms.date: 02/18/2021
ms.topic: how-to
description: Saiba como os administradores podem excluir atribuições de assinatura no portal de administração de assinaturas do Visual Studio
ms.openlocfilehash: efd0e149f390dd21a286b6ab7405ec36a43b8f78
ms.sourcegitcommit: 9da787bf5b4281f933dc22083dc0bdeae3bc9461
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2021
ms.locfileid: "103225970"
---
# <a name="delete-assignments-in-visual-studio-subscriptions"></a>Excluir atribuições em assinaturas do Visual Studio
Quando um assinante não precisar mais de uma assinatura do Visual Studio, como quando ele sair da empresa, concluir um projeto ou alternar para uma nova função de trabalho, você poderá remover sua assinatura e atribuí-la a outra pessoa. Observe que quando você reatribui uma assinatura, nem todos os benefícios do Assinante serão redefinidos.  O novo usuário poderá solicitar todas as chaves não solicitadas e exibir as chaves anteriormente solicitadas, mas os limites de solicitação **não** serão redefinidos.  Para organizações que têm contratos EA (Contrato Enterprise), todos os benefícios que já tiverem sido usados pelo usuário original, como treinamentos do Pluralsight, serão redefinidos. 
> [!Important]
> As assinaturas só poderão ser atribuídas a usuários diferentes se um mínimo de 90 dias tiver passado desde que a assinatura foi atribuída pela última vez.  Por exemplo, se uma assinatura foi atribuída a um assinante em 1º de junho, ela não poderá ser atribuída a um novo assinante até, pelo menos, 30 de agosto. 

Assista a este vídeo ou Continue lendo para saber como excluir atribuições.  

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4yG2q]

## <a name="delete-a-subscription-assignment"></a>Excluir uma atribuição de assinatura
1. Clique no nome do assinante que deseja remover. Para selecionar vários assinantes para remoção, você pode clicar no círculo à esquerda do nome do assinante para selecionar cada um.  Como alternativa, você pode manter pressionada a tecla **Ctrl** e clicar em cada Assinante que deseja remover. Para remover um intervalo de assinantes, clique no primeiro, pressione a tecla **Shift** e clique no último.  Pressione **Ctrl + a** para selecionar e remover todos os assinantes. Neste exemplo, três assinantes-âmbar, Kai e Madison-serão excluídos. 
2. Para excluir os assinantes selecionados, clique em **Excluir**.
3. Quando a mensagem aparecer para você confirmar a exclusão, clique em **OK**.
   > [!div class="mx-imgBorder"]
   > ![Excluir assinantes](_img/delete-license/delete-subscribers.png "Escolha os usuários que você deseja excluir e clique em excluir. Você pode usar as teclas CTRL e Shift para selecionar vários assinantes.")

   > [!NOTE]
   > A exclusão em massa usando um modelo não está disponível. 
   >
   > Se você adicionou atribuições de assinatura por meio de Azure Active Directory grupos de segurança, pode levar até 24 horas para que a exclusão seja atualizada no portal de administração.  Consulte [nosso artigo](assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions) para obter mais informações sobre como usar grupos de Azure Active Directory para gerenciar assinaturas. 

## <a name="resources"></a>Recursos
- [Suporte a assinaturas](https://visualstudio.microsoft.com/subscriptions/support/)

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Precisa alterar uma assinatura sem excluí-la?  Saiba como [editar assinaturas](edit-license.md)
- Para obter ajuda para encontrar uma assinatura específica, confira [Pesquisar por uma assinatura](search-license.md).
- Precisa criar uma lista de todas as suas assinaturas?  Confira [Exportar assinaturas](exporting-subscriptions.md).