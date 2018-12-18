---
title: Gerenciar recursos do Azure com o Cloud Explorer | Microsoft Docs
description: Saiba como usar o Cloud Explorer para navegar e gerenciar recursos do Azure dentro do Visual Studio.
author: ghogen
manager: douge
assetId: 6347dc53-f497-49d5-b29b-e8b9f0e939d7
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/25/2017
ms.author: ghogen
ms.openlocfilehash: a5b75aa5e1310e02befe162199472eef987d7cd9
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001146"
---
# <a name="manage-the-resources-associated-with-your-azure-accounts-in-visual-studio-cloud-explorer"></a>Gerenciar os recursos associados às suas contas do Azure no Visual Studio Cloud Explorer

Cloud Explorer permite exibir os recursos do Azure e grupos de recursos, inspecionar suas propriedades e executar ações de diagnóstico de chave do desenvolvedor de dentro do Visual Studio. 

Como o [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), Cloud Explorer é criado na pilha do Azure Resource Manager. Portanto, o Cloud Explorer compreende recursos como grupos de recursos do Azure e serviços do Azure como aplicativos lógicos e aplicativos de API, e ele dá suporte a [controle de acesso baseado em função](/azure/role-based-access-control/role-assignments-portal.md) (RBAC). 

## <a name="prerequisites"></a>Pré-requisitos

* Visual Studio 2015 com o [Microsoft Azure SDK para .NET 2.9](https://www.microsoft.com/en-us/download/details.aspx?id=51657).
* Conta do Microsoft Azure – se você não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](http://go.microsoft.com/fwlink/?LinkId=623901) ou [ativar seus benefícios de assinante do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=623901).

> [!NOTE]
> Para exibir o Gerenciador de nuvem, selecione **modo de exibição** > **Cloud Explorer** na barra de menus.

## <a name="add-an-azure-account-to-cloud-explorer"></a>Adicione um Azure da conta ao Cloud Explorer

Para exibir os recursos associados com uma conta do Azure, primeiro você deve adicionar a conta ao Cloud Explorer. 

1. Na **Cloud Explorer**, selecione **configurações de conta do Azure**.

   ![Ícone de configurações de conta do Azure no Gerenciador de nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Selecione **gerenciar contas**. 

   ![Link de adicionar a conta do Gerenciador de nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/manage-accounts-link.png)

1. Faça logon conta do Azure cujos recursos você deseja procurar. 

1. Após fazer logon uma conta do Azure, exibem as assinaturas associadas à conta. Marque as caixas de seleção para as assinaturas de conta que você deseja procurar e, em seguida, selecione **aplicar**. 

   ![Cloud Explorer: selecione as assinaturas do Azure para exibir](./media/vs-azure-tools-resources-managing-with-cloud-explorer/select-subscriptions.png)

1. Depois de selecionar as assinaturas cujos recursos você deseja procurar, essas assinaturas e recursos exibem no Gerenciador de nuvem.

   ![Recursos do Cloud Explorer listagem para uma conta do Azure](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-listed.png)

## <a name="remove-an-azure-account-from-cloud-explorer"></a>Remover uma conta do Azure no Cloud Explorer 

1. Na **Cloud Explorer**, selecione **gerenciamento de conta**.

   ![Ícone de configurações de conta do Azure no Gerenciador de nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/azure-account-settings.png)

1. Ao lado da conta que deseja remover, selecione **gerenciar contas**.

   ![Ícone de configurações de conta do Azure no Gerenciador de nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/remove-account.png)

1. Escolher **remover** para remover uma conta.

    ![Caixa de diálogo Gerenciar o Gerenciador de contas da nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/accountmanage.PNG)

## <a name="view-resource-types-or-resource-groups"></a>Exibir tipos de recursos ou grupos de recursos

Para exibir os recursos do Azure, você pode escolher **tipos de recursos** ou **grupos de recursos** modo de exibição.

1. Na **Cloud Explorer**, selecione o menu suspenso modo de exibição de recursos.

   ![Lista de lista suspensa do Cloud Explorer para selecionar a exibição de recursos desejados](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resources-view-dropdown.png)

1. No menu de contexto, selecione o modo de exibição desejado: 

   * **Tipos de recursos** exibir - a exibição comumente usada na [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040), mostra os recursos do Azure categorizados por tipo, como aplicativos web, contas de armazenamento e máquinas virtuais. 
   * **Grupos de recursos** exibir - recursos do Azure categoriza pelo grupo de recursos do Azure com o qual estão associadas. Um grupo de recursos é um pacote de recursos do Azure, normalmente usadas por um aplicativo específico. Para saber mais sobre grupos de recursos do Azure, consulte [visão geral do Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview).

   A imagem a seguir mostra uma comparação dos modos de exibição de dois recursos:

   ![Comparação de modos de exibição de recursos do Gerenciador de nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/resource-views-comparison.png)

## <a name="view-and-navigate-resources-in-cloud-explorer"></a>Exibir e navegar por recursos no Cloud Explorer

Para navegar até um recurso do Azure e exibir suas informações no Cloud Explorer, expanda o tipo do item ou o grupo de recursos associado e, em seguida, selecione o recurso. Quando você seleciona um recurso, informações aparecem nas duas guias – **ações** e **propriedades** – na parte inferior do Cloud Explorer.

* **Ações** guia – exibe as ações que podem ser executadas no Cloud Explorer para o recurso selecionado. Você também pode exibir essas opções clicando com o recurso para exibir o menu de contexto.

* **Propriedades** guia - mostra as propriedades do recurso, como seu tipo, localidade e grupo de recursos ao qual está associado.

A imagem a seguir mostra uma comparação de exemplo do que você vê em cada guia para um serviço de aplicativo:

  ![Captura de tela do Gerenciador de nuvem](./media/vs-azure-tools-resources-managing-with-cloud-explorer/actions-and-properties.png)

Cada recurso tem a ação **abrir no portal**. Quando você seleciona essa ação, o Cloud Explorer exibe o recurso selecionado na [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040). O **abrir no portal** recurso é útil para navegar para recursos muito aninhados.

Ações adicionais e valores de propriedade também podem aparecer com base no recurso do Azure. Por exemplo, aplicativos web e aplicativos lógicos também têm as ações **abrir no navegador** e **Anexar depurador** além **abrir no portal**. Ações para abrir editores aparecem quando você escolhe um blob da conta de armazenamento, fila ou tabela. Aplicativos do Azure têm **URL** e **Status** propriedades, enquanto os recursos de armazenamento têm propriedades de cadeia de caracteres de conexão e de chave.

## <a name="find-resources-in-cloud-explorer"></a>Localizar recursos no Cloud Explorer

Para localizar recursos com um nome específico em assinaturas de sua conta do Azure, digite o nome na **pesquisa** caixa no Cloud Explorer.

  ![Localizando recursos no Cloud Explorer](./media/vs-azure-tools-resources-managing-with-cloud-explorer/search-for-resources.png)

Conforme você insere caracteres na **pesquisa** caixa, apenas os recursos que correspondem a esses caracteres são exibidos na árvore de recursos.
