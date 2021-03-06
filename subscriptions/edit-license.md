---
title: Editar assinaturas do Visual Studio no portal de administração | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 97ac8e4d-7a03-42f8-98cb-15bcaa90ef65
ms.date: 02/18/2021
ms.topic: how-to
description: Saiba como os administradores podem editar as atribuições de assinatura.
ms.openlocfilehash: f24c949224d895f4cc2926ab30db637835e7886c
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249795"
---
# <a name="edit-visual-studio-subscription-assignments"></a>Editar atribuições de assinatura do Visual Studio
Como administrador de assinatura, você pode fazer alterações nas assinaturas atribuídas a indivíduos dentro da sua organização.  Este artigo descreve os tipos de alterações que você pode fazer e fornece as etapas necessárias.

   > [!NOTE]
   > Se você precisar alterar os detalhes da assinatura de um assinante atribuído por meio de um grupo de Azure Active Directory, será necessário removê-los do grupo e adicioná-los ao portal de administração individualmente.  

## <a name="change-subscriber-information"></a>Alterar informações do assinante
Você pode editar as informações do assinante para corrigir erros ou para atualizar as informações.

Para editar um assinante, selecione as reticências (...) que aparecem ao lado do endereço de email do assinante ao passar o mouse sobre ele. Será exibida uma lista suspensa.  Selecione **Editar** para modificar os detalhes do assinante. 
> [!div class="mx-imgBorder"]
> ![Selecione um assinante a ser editado](_img/edit-license/select-subscriber.png "Clique nas reticências e escolha Editar.")

Você pode atualizar o nome, sobrenome, nível de assinatura, endereço de email, país, idioma, downloads e campo de referência do Assinante. Edite as informações do assinante e clique em **salvar**.

## <a name="edit-multiple-subscribers-using-bulk-edit"></a>Editar vários assinantes usando a edição em massa

Você pode editar vários assinantes de uma vez usando o processo de edição em massa. Esse recurso é usado principalmente para organizações que estão passando por alterações de endereço de email corporativo ou quando uma organização decide restringir o acesso a downloads.

Assista a este vídeo ou Continue lendo para saber como editar vários assinantes usando a edição em massa. 
<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vkAF]

> [!NOTE]
> Não altere os GUIDs de assinatura no modelo. Consulte nosso artigo sobre como [atribuir GUIDs de assinatura específicos](assign-guid.md).

1. Para editar vários assinantes de uma vez, navegue até a guia assinantes. Na faixa de faixas na parte superior, clique em **edição em massa**.

2. A edição em massa usa um modelo do Excel para fazer edições nas informações dos assinantes. Na caixa de edição em massa, clique em **Exportar este Excel** para baixar a lista atual de assinantes, incluindo todas as suas informações.
   > [!div class="mx-imgBorder"]
   > ![Editando uma licença – exportar a lista de edições em massa](_img/edit-license/edit-license-bulk-edit-export.png "Clique em exportar este Excel para criar uma lista de suas assinaturas atuais.")

3. Em seguida, salve o arquivo localmente para que ele possa ser encontrado com facilidade e faça as alterações necessárias antes de carregá-lo. 

4. Retorne ao Portal de Administração de Assinaturas do Visual Studio e na caixa de diálogo Edição em Massa, clique em **Procurar**. Selecione o arquivo do Excel que você salvou e clique em **OK**. O andamento do upload será exibido na tela.
   > [!div class="mx-imgBorder"]
   > ![Editando uma licença – upload do arquivo de edições em massa](_img/edit-license/edit-license-bulk-file-upload1.png "Navegue até o local do arquivo concluído do Excel, selecione-o e clique em OK.")

5. Depois de carregar o arquivo, será exibida uma notificação informando que o upload foi bem-sucedido. Neste ponto, suas edições serão refletidas nas informações do assinante.

## <a name="resources"></a>Recursos
- [Suporte a assinaturas](https://visualstudio.microsoft.com/subscriptions/support/)

## <a name="see-also"></a>Confira também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Precisa atribuir uma ID de assinatura específica? Confira atribuindo uma ID de assinatura. 
- Para obter ajuda para encontrar uma assinatura específica, confira [Pesquisar por uma assinatura](search-license.md).
- Precisa criar uma lista de todas as suas assinaturas?  Confira [Exportar assinaturas](exporting-subscriptions.md).