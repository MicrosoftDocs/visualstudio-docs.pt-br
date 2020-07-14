---
title: 'Gerenciador de empacotamento: Adicionar & remover recursos & itens ao pacote'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.RAD.PackagingExplorer
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c3ea7e30737855cbbb9434e8763f4903d80b82da
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014556"
---
# <a name="how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer"></a>Como adicionar e remover recursos e itens para um pacote usando o Gerenciador de empacotamento
  Para configurar um pacote para implantar itens e recursos do SharePoint, você pode usar o Gerenciador de empacotamento. Você pode ajustar os itens e recursos de projeto do SharePoint dentro de seu arquivo. wsp.

 Como alternativa, você pode usar o designer de empacotamento para exibir e reordenar os recursos para alterar a ordem de ativação. Para obter mais informações, consulte [como adicionar e remover recursos e itens para um pacote usando o designer de pacotes](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md).

## <a name="open-the-packaging-explorer"></a>Abrir o Gerenciador de empacotamento
 Você pode usar o procedimento a seguir para abrir o Gerenciador de empacotamento, se sua solução do Visual Studio tiver pelo menos um projeto do SharePoint. Como alternativa, o Gerenciador de empacotamento é aberto automaticamente quando você exibe um recurso ou designer de pacote. Depois de fechar todos os designers de recursos e pacotes, o Gerenciador de pacotes também é fechado.

#### <a name="to-open-the-packaging-explorer"></a>Para abrir o Gerenciador de empacotamento

1. Na barra de menus, escolha **Exibir**  >  **outro Windows**  >  **Packaging Explorer**.

     O **Gerenciador de empacotamento** aparece na **caixa de ferramentas**.

## <a name="adding-a-feature-to-a-package"></a>Adicionando um recurso a um pacote
 Você pode adicionar recursos novos e existentes a um pacote usando o Gerenciador de empacotamento.

#### <a name="to-add-a-sharepoint-feature"></a>Para adicionar um recurso do SharePoint

1. Abra o **Gerenciador de empacotamento**, abra o menu de atalho para o projeto e escolha **Adicionar recurso**.

#### <a name="to-move-an-existing-sharepoint-feature"></a>Para mover um recurso existente do SharePoint

1. Abra o **Gerenciador de empacotamento**e execute uma das seguintes etapas:

    - Arraste um **recurso** de um projeto para outro projeto.

    - Abra o menu de atalho para um recurso, escolha **recortar**, abra o menu de atalho do projeto para o qual você deseja mover o recurso e, em seguida, escolha **colar**.

    > [!NOTE]
    > Use este procedimento se você tiver mais de um projeto do SharePoint em sua solução.

## <a name="validate-a-feature-or-package"></a>Validar um recurso ou pacote
 Você pode identificar possíveis problemas nos recursos e pacotes do SharePoint Validando os arquivos. Avisos e erros são exibidos na janela de saída e na janela de Lista de Erros.

#### <a name="to-validate-a-sharepoint-feature-or-package"></a>Para validar um recurso ou pacote do SharePoint

1. Abra o **Gerenciador de empacotamento**.

2. Abra um menu de atalho para um recurso ou pacote e, em seguida, escolha **validar**.

## <a name="see-also"></a>Consulte também
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
