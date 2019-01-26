---
title: 'Como: Criar um receptor de eventos | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 395fc5976f31fb2d465c57f036b3e5369aaa0c07
ms.sourcegitcommit: c0202a77d4dc562cdc55dc2e6223c062281d9749
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54865093"
---
# <a name="how-to-create-an-event-receiver"></a>Como: Criar um receptor de eventos
  Criando *receptores de evento*, você pode responder quando um usuário interage com itens do SharePoint, como listas ou itens de lista. Por exemplo, o código em um receptor de evento pode ser disparado quando um usuário altera o calendário ou exclui um nome de uma lista de contatos. Ao seguir este tópico, você pode aprender como adicionar um receptor de eventos a uma instância de lista.

 Para concluir essas etapas, você deve ter instalado [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e edições do Windows e do SharePoint. Como este exemplo exige um projeto do SharePoint, você também deve ter concluído o procedimento no tópico [passo a passo: Criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md).

## <a name="adding-an-event-receiver"></a>Adicionando um receptor de eventos
 O projeto que você criou na [passo a passo: Criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md) inclui colunas de site personalizado, uma lista personalizada e um tipo de conteúdo. No procedimento a seguir, você expandir este projeto, adicionando um manipulador de eventos simples (um receptor de eventos) a uma instância de lista para mostrar como lidar com eventos que ocorrem em itens como listas do SharePoint.

#### <a name="to-add-an-event-receiver-to-the-list-instance"></a>Para adicionar um receptor de eventos para a instância de lista

1.  Abra o projeto que você criou na [passo a passo: Criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md).

2.  Na **Gerenciador de soluções**, escolha o nó do projeto do SharePoint, que é chamado **clínica**.

3.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

4.  Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** item.

5.  No **modelos** painel, escolha **receptor de evento**, nomeie- **TestEventReceiver1**e, em seguida, escolha o **Okey** botão.

     O **Assistente para personalização do SharePoint** é exibida.

6.  No **que tipo de receptor de eventos você deseja?** , escolha **eventos de Item de lista**.

7.  No **qual item deve ser a origem do evento?** , escolha **pacientes (Clinic\Patients)**.

8.  No **manipular os eventos a seguir** , selecione a caixa de seleção ao lado de **um item foi adicionado**e, em seguida, escolha o **concluir** botão.

     O arquivo de código para o novo receptor de evento contém um único método chamado `ItemAdded`. Na próxima etapa, você adicionará código para esse método, de modo que cada contato será denominado Scott Brown por padrão.

9. Substitua a `ItemAdded` método com o seguinte código e, em seguida, escolha o **F5** chave:

     [!code-csharp[SP_EventReceiver#1](../sharepoint/codesnippet/CSharp/CustomField1/TestEventReceiver1/TestEventReceiver1.cs#1)]
     [!code-vb[SP_EventReceiver#1](../sharepoint/codesnippet/VisualBasic/CustomField1_VB/EventReceiver1/EventReceiver1.vb#1)]

     O código é executado e o site é exibido no navegador da web do SharePoint.

10. Na barra de início rápido, escolha o **pacientes** vincular e, em seguida, escolha o **Adicionar Novo Item** link.

     Abre o formulário de entrada para novos itens.

11. Inserir dados nos campos e, em seguida, escolha o **salvar** botão.

     Depois de escolher o **salve** botão, o **paciente nome** coluna atualiza automaticamente para o nome Scott Brown.

## <a name="see-also"></a>Consulte também

- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)