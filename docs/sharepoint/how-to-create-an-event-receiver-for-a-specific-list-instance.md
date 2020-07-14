---
title: 'Como: criar um receptor de eventos para uma instância de lista específica | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
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
ms.openlocfilehash: 54c384742afba3d5af7f08ee62a9ec56c7f1438c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016957"
---
# <a name="how-to-create-an-event-receiver-for-a-specific-list-instance"></a>Como: criar um receptor de eventos para uma instância de lista específica
  Um receptor de eventos de instância de lista responde a eventos que ocorrem em qualquer instância de uma definição de lista. Embora o modelo receptor de eventos não habilite o direcionamento de uma instância de lista específica, você pode modificar um receptor de eventos que tem como escopo uma definição de lista para responder a eventos em uma instância de lista específica.

 Para direcionar uma instância de lista específica, no *Elements.xml* para o receptor de evento, substitua `ListTemplateId` por `ListUrl` e adicione a URL da instância da lista.

## <a name="create-a-list-instance-event-receiver"></a>Criar um receptor de eventos de instância de lista
 As etapas a seguir mostram como modificar um receptor de evento de item de lista para responder somente a eventos que ocorrem em uma instância de lista de anúncios personalizados.

#### <a name="to-modify-an-event-receiver-to-respond-to-a-specific-list-instance"></a>Para modificar um receptor de eventos para responder a uma instância de lista específica

1. Em um navegador, abra o site do SharePoint.

2. No painel de navegação, **liste** link.

3. Na página **conteúdo do site inteiro** , escolha o link **criar** .

4. Na caixa de diálogo **criar** , escolha o tipo de **comunicados** , nomeie o anúncio **TestAnnouncements**e, em seguida, escolha o botão **criar** .

5. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , crie um projeto receptor de eventos.

6. Na lista **que tipo de receptor de evento você deseja?** , escolha **eventos de item de lista**.

    > [!NOTE]
    > Você também pode selecionar qualquer outro tipo de receptor de evento que seja escopos para uma definição de lista, por exemplo, **listar eventos de email** ou **listar eventos de fluxo de trabalho**.

7. Na lista o **item que deve ser a origem do evento?** , escolha **anúncios**.

8. Na lista **manipular os eventos a seguir** , marque a caixa de seleção **um item está sendo adicionado** e, em seguida, escolha o botão **concluir** .

9. Em **Gerenciador de soluções**, em EventReceiver1, abra *Elements.xml*.

     Atualmente, o receptor de eventos faz referência à definição da lista de anúncios usando a seguinte linha:

    ```xml
    <Receivers ListTemplateId="104">
    ```

     Altere esta linha para o seguinte texto:

    ```xml
    <Receivers ListUrl="Lists/TestAnnouncements">
    ```

     Isso instrui o receptor de eventos a responder somente a eventos que ocorrem na nova lista de anúncios do **TestAnnouncements** que você acabou de criar. Você pode alterar o `ListURL` atributo para fazer referência a qualquer instância de lista no servidor do SharePoint.

10. Abra o arquivo de código do receptor de eventos e coloque um ponto de interrupção no método de adição.

11. Escolha a tecla **F5** para compilar e executar a solução.

12. No SharePoint, escolha o link **TestAnnouncements** no painel de navegação.

13. Escolha o link **Adicionar novo comunicado** .

14. Insira um título para o comunicado e, em seguida, escolha o botão **salvar** .

     Observe que o ponto de interrupção é atingido quando o novo item é adicionado à lista de anúncios personalizados.

15. Escolha a tecla **F5** para retomar.

16. No painel de navegação, escolha o link **listas** e, em seguida, escolha o link **anúncios** .

17. Adicione um novo comunicado.

     Observe que o receptor de eventos não é disparado no novo comunicado porque o receptor está configurado para responder somente a eventos na instância de lista de anúncios personalizada, **TestAnnouncements**.

## <a name="see-also"></a>Consulte também
- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
