---
title: Editar assinaturas no portal do de administração | Microsoft Docs
author: evanwindom
ms.author: lank
manager: lank
ms.assetid: 97ac8e4d-7a03-42f8-98cb-15bcaa90ef65
ms.date: 03/03/2020
ms.topic: how-to
description: Saiba como os administradores podem editar atribuições de assinatura.
ms.openlocfilehash: 32d430ac4afe88541fd839827652ec7613ba03b1
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85902926"
---
# <a name="edit-visual-studio-subscription-assignments"></a>Editar atribuições de assinatura do Visual Studio
Como administrador de assinaturas, você pode fazer alterações nas assinaturas atribuídas às pessoas na organização.  Este artigo descreve os tipos de alterações que você pode fazer e fornece as etapas necessárias.

   > [!NOTE]
   > Se você precisar alterar os detalhes da assinatura de um assinante atribuído por meio de um grupo de Azure Active Directory, será necessário removê-los do grupo e adicioná-los ao portal de administração individualmente.  

## <a name="change-subscriber-information"></a>Alterar informações do assinante
Você pode editar as informações do assinante para corrigir erros ou para atualizar as informações.

Para editar um assinante, selecione as reticências (...) que aparecem ao lado do endereço de email do assinante ao passar o mouse sobre ele. Será exibida uma lista suspensa.  Selecione **Editar** para modificar os detalhes do assinante. 
> [!div class="mx-imgBorder"]
> ![Selecione um assinante a ser editado](_img/edit-license/select-subscriber.png)

Você pode atualizar o nome, sobrenome, nível de assinatura, endereço de email, país, idioma, downloads e campo de referência do Assinante. Edite as informações do assinante e clique em **salvar**.

## <a name="edit-multiple-subscribers-using-bulk-edit"></a>Editar vários assinantes usando a edição em massa


Você pode editar vários assinantes de uma vez usando o processo de edição em massa. Esse recurso é usado principalmente para organizações que estão passando por alterações de endereço de email corporativo ou quando uma organização decide restringir o acesso a downloads.

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vkAF]

   > [!IMPORTANT]
   > Os níveis de assinatura (ou seja, Enterprise, Professional etc.) e os GUIDs de assinatura não podem ser alterados usando a edição em massa.  Se você precisar atribuir GUIDs de assinatura específicos a seus usuários, use o processo para adicionar usuários escolhendo a ID da assinatura. Se você tentar um upload com esses itens alterados no modelo de edição em massa, o carregamento falhará.

1. Para editar vários assinantes de uma vez, navegue até a guia assinantes. Na faixa de faixas na parte superior, clique em **edição em massa**.

2. A edição em massa usa um modelo do Excel para fazer edições nas informações dos assinantes. Na caixa de edição em massa, clique em **Exportar este Excel** para baixar a lista atual de assinantes, incluindo todas as suas informações.
   > [!div class="mx-imgBorder"]
   > ![Editando uma licença – exportar a lista de edições em massa](_img/edit-license/edit-license-bulk-edit-export.png)

3. Em seguida, salve o arquivo localmente para que ele possa ser encontrado com facilidade e faça as alterações necessárias antes de carregá-lo. Para garantir um upload bem-sucedido, **não edite o nível da assinatura ou o GUID da assinatura** no arquivo de edição em massa, pois isso fará com que o carregamento falhe.

4. Retorne ao Portal de Administração de Assinaturas do Visual Studio e na caixa de diálogo Edição em Massa, clique em **Procurar**. Selecione o arquivo do Excel que você salvou e clique em **OK**. O andamento do upload será exibido na tela.
   > [!div class="mx-imgBorder"]
   > ![Editando uma licença – upload do arquivo de edições em massa](_img/edit-license/edit-license-bulk-file-upload1.png)

5. Depois de carregar o arquivo, será exibida uma notificação informando que o upload foi bem-sucedido. Neste ponto, suas edições serão refletidas nas informações do assinante.

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](https://docs.microsoft.com/visualstudio/)
- [Documentação do Azure DevOps](https://docs.microsoft.com/azure/devops/)
- [Documentação do Azure](https://docs.microsoft.com/azure/)
- [Documentação do Microsoft 365](https://docs.microsoft.com/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Precisa atribuir uma ID de assinatura específica? Confira atribuindo uma ID de assinatura. 
- Para obter ajuda para encontrar uma assinatura específica, confira [Pesquisar por uma assinatura](search-license.md).
- Precisa criar uma lista de todas as suas assinaturas?  Confira [Exportar assinaturas](exporting-subscriptions.md).


