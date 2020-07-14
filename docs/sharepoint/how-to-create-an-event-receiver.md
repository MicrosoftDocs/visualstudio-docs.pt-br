---
title: 'Como: criar um receptor de eventos | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- VS.SharePointTools.SPE.EventReceiver
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, event receivers
- event receivers [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 26d8c9f433fad051716b6ebd37e3d1f3b3f9f4eb
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016903"
---
# <a name="how-to-create-an-event-receiver"></a>Como: criar um receptor de eventos
  Ao criar *receptores de eventos*, você pode responder quando um usuário interage com itens do SharePoint, como listas ou itens de lista. Por exemplo, o código em um receptor de eventos pode ser disparado quando um usuário altera o calendário ou exclui um nome de uma lista de contatos. Seguindo este tópico, você pode aprender a adicionar um receptor de evento a uma instância de lista.

 Para concluir essas etapas, você deve ter as [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] edições instaladas e com suporte do Windows e do SharePoint. Como este exemplo requer um projeto do SharePoint, você também deve ter concluído o procedimento no tópico [passo a passos: criar uma coluna de site, tipo de conteúdo e lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md).

## <a name="adding-an-event-receiver"></a>Adicionando um receptor de eventos
 O projeto que você criou em [Walkthrough: criar uma coluna de site, tipo de conteúdo e lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) inclui colunas de site personalizadas, uma lista personalizada e um tipo de conteúdo. No procedimento a seguir, você expandirá esse projeto adicionando um manipulador de eventos simples (um receptor de eventos) a uma instância de lista para mostrar como manipular eventos que ocorrem em itens do SharePoint, como listas.

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>Para adicionar um receptor de eventos à instância de lista

1. Abra o projeto que você criou em [Walkthrough: criar uma coluna de site, tipo de conteúdo e lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md).

2. Em **Gerenciador de soluções**, escolha o nó do projeto do SharePoint, chamado **clínica**.

3. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

4. Em **Visual C#** ou **Visual Basic**, expanda o nó do **SharePoint** e escolha o item **2010** .

5. No painel **modelos** , escolha **receptor de eventos**, nomeie-o **TestEventReceiver1**e escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido.

6. Na lista **que tipo de receptor de evento você deseja?** , escolha **eventos de item de lista**.

7. Na lista o **item que deve ser a origem do evento?** , escolha **pacientes (Clinic\Patients)**.

8. Na lista **manipular os eventos a seguir** , marque a caixa de seleção ao lado de **um item foi adicionado**e, em seguida, escolha o botão **concluir** .

     O arquivo de código para o novo receptor de evento contém um único método nomeado `ItemAdded` . Na próxima etapa, você adicionará código a esse método, de modo que cada contato será nomeado Scott Brown por padrão.

9. Substitua o `ItemAdded` método existente pelo código a seguir e escolha a tecla **F5** :

     [!code-csharp[SP_EventReceiver#1](../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs#1)]
     [!code-vb[SP_EventReceiver#1](../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb#1)]

     O código é executado e o site do SharePoint é exibido no navegador da Web.

10. Na barra de início rápido, escolha o link **pacientes** e, em seguida, escolha o link **Adicionar novo item** .

     O formulário de entrada para novos itens é aberto.

11. Insira dados nos campos e, em seguida, escolha o botão **salvar** .

     Depois de escolher o botão **salvar** , a coluna **nome do paciente** é atualizada automaticamente para o nome Scott Brown.

## <a name="see-also"></a>Consulte também

- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)