---
title: Atribuir assinaturas do Visual Studio aos usuários | Microsoft Docs
author: evanwindom
ms.author: v-evwin
manager: cabuschl
ms.assetid: 4e529a43-7aed-4eee-895d-862a631952df
ms.date: 03/21/2021
ms.topic: conceptual
description: Saiba como os administradores podem atribuir licenças aos assinantes
ms.openlocfilehash: a1b68a45754e0fb466ae12b59d63fa14d50e9a3e
ms.sourcegitcommit: d7d9fb79448b3534923cc95071d1f91eabde88e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2021
ms.locfileid: "104776513"
---
# <a name="assign-licenses-in-the-visual-studio-subscriptions-administration-portal"></a>Atribuir licenças no portal de administração de assinaturas do Visual Studio
Como administrador de assinaturas do Visual Studio, você pode usar o portal de administração para atribuir assinaturas a usuários individuais e grupos de usuários.

Para grupos de usuários, você tem opções de como atribuir assinaturas.  
- Você pode atribuir assinaturas uma de cada vez.
- Você também pode carregar rapidamente e facilmente listas de assinantes e suas informações de assinatura usando o recurso de [adição em massa](assign-license-bulk.md) .
- Se sua organização usa o Microsoft Azure Active Directory (AD do Azure), você pode [usar os grupos do Azure ad para atribuir assinaturas](./assign-license-bulk.md#use-azure-active-directory-groups-to-assign-subscriptions) a grupos de usuários.  


## <a name="add-a-single-subscriber"></a>Adicionar um único assinante
Assista ao vídeo ou Continue lendo para saber como atribuir uma assinatura do Visual Studio a um novo usuário para que ele possa acessar os benefícios da assinatura.

<br>

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE4vpPh]


1. Entre no portal de [Administração](https://manage.visualstudio.com).
2. Para atribuir uma licença a um único assinante do Visual Studio, na parte superior da tabela, selecione **Adicionar** e, em seguida, escolha **assinante individual**.
   > [!div class="mx-imgBorder"]
   > ![Adicionar um único assinante](_img/assign-license-add/add-subscriber-individual.png "Selecione Adicionar e, em seguida, escolha assinante individual para atribuir uma única assinatura.")
3. Insira as informações do novo assinante nos campos do formulário. Se sua organização estiver usando o Azure Active Directory, o campo **Nome** terá uma função de pesquisa para localizar pessoas no diretório atual, permitindo selecionar o usuário correto nos resultados da pesquisa. Quando você selecionar essa pessoa, o email de conexão e o email de notificação serão populados automaticamente.  Se o Assinante não for encontrado em sua organização, o email de notificação não será preenchido automaticamente, mas estará disponível para você adicionar manualmente um endereço de email diferente ao qual os emails relacionados à assinatura serão enviados.  Se o seu serviço de email bloquear emails de entrada para os endereços de email de entrada, é importante especificar um endereço de email de notificação diferente para que os assinantes e administradores recebam emails importantes relacionados à assinatura da Microsoft.
   > [!div class="mx-imgBorder"]
   > ![Detalhes do assinante](_img/assign-license-add/subscriber-details.png "Insira o nome do assinante e outros detalhes ou escolha um dos membros do locatário.")

    > [!NOTE]
    > Para que os membros de um locatário de Azure Active Directory fiquem visíveis quando você insere um nome de assinante, o administrador deve ser um membro do locatário. 


    Caso deseje que esse assinante tenha acesso a downloads de software quando ele entrar no [Portal de Assinaturas do Visual Studio](https://my.visualstudio.com?wt.mc_id=o~msft~docs), deixe a alternância de downloads habilitada na seção **Configurações de Download**. Se você optar por desabilitar os downloads, o usuário não terá acesso aos downloads de software.  O acesso às chaves do produto também será desabilitado.  O assinante ainda terá acesso a todos os outros benefícios incluídos na assinatura.
   > [!div class="mx-imgBorder"]
   > ![Acesso a downloads](media/access-to-downloads.png "Escolha ' permitir ' para fornecer ao Assinante acesso aos downloads de software.")

    Caso deseje adicionar suas próprias anotações de referência para a assinatura, faça isso na seção **Adicionar referência**.
   > [!div class="mx-imgBorder"]
   > ![Adicionar suas próprias anotações de referência a cada assinatura](media/add-subscriber-reference-notes.png "Use o campo de referência para registrar observações sobre esta assinatura.")

    Quando terminar de selecionar as opções e inserir os dados do assinante, escolha **Adicionar** na parte inferior do submenu **Adicionar Assinante**.
   > [!div class="mx-imgBorder"]
   > ![Escolha o botão Adicionar](media/add-button.png "Selecione Adicionar para salvar as informações e atribuir a assinatura ao Assinante.")

## <a name="why-use-a-different-notification-email-address"></a>Por que usar um endereço de email de notificação diferente?
Algumas organizações configuram seus serviços de email para bloquear emails de entrada de outros domínios.  O bloqueio de emails de entrada significa que os assinantes e administradores perderão comunicações importantes:
- Os assinantes não receberão uma notificação de que uma assinatura foi atribuída a eles.  Isso também impedirá que eles ativem alguns dos benefícios incluídos.  
- Os assinantes que receberam assinaturas do Visual Studio com o GitHub Enterprise não receberão o convite para ingressar em sua organização do GitHub, o que significa que eles não poderão aceitar o convite. Eles **devem aceitar o convite por email** para obter acesso à sua organização do github. 
- Os administradores não serão notificados quando forem adicionados a um contrato, receberão instruções de administrador mensais ou notificações de alterações de recursos que afetam a maneira como gerenciam assinaturas.

Usar um endereço de email de notificação fornece a opção de permitir que seus assinantes recebam comunicações importantes sobre suas assinaturas sem alterar a funcionalidade de seus endereços de email de entrada.  

## <a name="resend-assignment-emails"></a>Reenviar emails de atribuição
Depois de adicionar um assinante, um email de atribuição será enviado automaticamente para o novo assinante com mais instruções. Você pode enviar o email de atribuição novamente a qualquer momento selecionando o Assinante e, em seguida, selecionando o botão **reenviar** no menu superior.  Para reenviar emails a vários usuários, mantenha pressionada a tecla **Ctrl** enquanto seleciona os assinantes.  Ao selecionar o botão **reenviar** , você verá uma caixa de diálogo solicitando que você confirme se deseja reenviar para esses assinantes.  


## <a name="resources"></a>Recursos
- Precisa de ajuda?  [Suporte a assinaturas](https://aka.ms/vsadminhelp)de contato.

## <a name="see-also"></a>Veja também
- [Documentação do Visual Studio](/visualstudio/)
- [Documentação do Azure DevOps](/azure/devops/)
- [Documentação do Azure](/azure/)
- [Documentação do Microsoft 365](/microsoft-365/)

## <a name="next-steps"></a>Próximas etapas
- Tem muitos usuários para adicionar?  Saiba como atribuir assinaturas a [vários assinantes](assign-license-bulk.md).
