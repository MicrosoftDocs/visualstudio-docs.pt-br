---
title: 'Walkthrough: Adicionar receptores de evento de recurso | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, advanced packaging tools
- SharePoint development in Visual Studio, event receivers
- SharePoint development in Visual Studio, feature event receivers
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f40358c157ec24557947f36b0c6eadb6d8a2622d
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015360"
---
# <a name="walkthrough-add-feature-event-receivers"></a>Walkthrough: Adicionar receptores de evento de recurso
  Os receptores de evento de recurso são métodos que são executados quando um dos seguintes eventos relacionados ao recurso ocorre no SharePoint:

- Um recurso está instalado.

- Um recurso é ativado.

- Um recurso é desativado.

- Um recurso é removido.

  Este tutorial demonstra como adicionar um receptor de eventos a um recurso em um projeto do SharePoint. Ele demonstra as seguintes tarefas:

- Criando um projeto vazio com um receptor de eventos de recurso.

- Manipulando o método **FeatureDeactivating** .

- Usando o modelo de objeto de projeto do SharePoint para adicionar um comunicado à lista de anúncios.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Microsoft Windows e do SharePoint.

- Visual Studio.

## <a name="create-a-feature-event-receiver-project"></a>Criar um projeto de receptor de evento de recurso
 Primeiro, crie um projeto para conter o receptor de evento de recurso.

#### <a name="to-create-a-project-with-a-feature-event-receiver"></a>Para criar um projeto com um receptor de eventos de recurso

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** .

2. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

3. No painel **modelos** , escolha o modelo de **projeto do SharePoint 2010** .

     Você usa esse tipo de projeto para receptores de eventos de recurso porque eles não têm nenhum modelo de projeto.

4. Na caixa **nome** , digite **FeatureEvtTest**e, em seguida, escolha o botão **OK** para exibir o assistente para **personalização do SharePoint**.

5. Na página **especificar o site e o nível de segurança para depuração** , insira a URL do site do SharePoint Server ao qual você deseja adicionar o novo item de campo personalizado ou use o local padrão (http:// \<*system name*> /).

6. Na seção **o que é o nível de confiança para esta solução do SharePoint?** , escolha o botão de opção **implantar como uma solução de farm** .

     Para obter mais informações sobre soluções em área restrita versus soluções de farm, consulte [Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

7. Escolha o botão **concluir** e observe que um recurso chamado Feature1 aparece sob o nó **recursos** .

## <a name="add-an-event-receiver-to-the-feature"></a>Adicionar um receptor de eventos ao recurso
 Em seguida, adicione um receptor de eventos ao recurso e adicione o código que é executado quando o recurso é desativado.

#### <a name="to-add-an-event-receiver-to-the-feature"></a>Para adicionar um receptor de eventos ao recurso

1. Abra o menu de atalho do nó recursos e escolha **Adicionar recurso** para criar um recurso.

2. No nó **recursos** , abra o menu de atalho para **Feature1**e escolha **Adicionar receptor de eventos** para adicionar um receptor de eventos ao recurso.

     Isso adiciona um arquivo de código em Feature1. Nesse caso, ele é nomeado *Feature1.EventReceiver.cs* ou *Feature1. EventReceiver. vb*, dependendo da linguagem de desenvolvimento do seu projeto.

3. Se o projeto for escrito em [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] , adicione o seguinte código na parte superior do receptor de eventos se ele ainda não estiver lá:

     [!code-csharp[SP_FeatureEvt#1](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#1)]

4. A classe receptor de evento contém vários métodos comentados que atuam como eventos. Substitua o método **FeatureDeactivating** pelo seguinte:

     [!code-vb[SP_FeatureEvt#2](../sharepoint/codesnippet/VisualBasic/featureevt2vb/features/feature1/feature1.eventreceiver.vb#2)]
     [!code-csharp[SP_FeatureEvt#2](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#2)]

## <a name="test-the-feature-event-receiver"></a>Testar o receptor de eventos de recurso
 Em seguida, desative o recurso para testar se o método **FeatureDeactivating** gera um comunicado para a lista de anúncios do SharePoint.

#### <a name="to-test-the-feature-event-receiver"></a>Para testar o receptor de evento de recurso

1. Defina o valor da propriedade de **configuração de implantação ativa** do projeto como **sem ativação**.

     Definir essa propriedade impede que o recurso seja ativado no SharePoint e permite que você depure os receptores de evento de recurso. Para obter mais informações, consulte [depurar soluções do SharePoint](../sharepoint/debugging-sharepoint-solutions.md).

2. Escolha a tecla **F5** para executar o projeto e implantá-lo no SharePoint.

3. Na parte superior da página da Web do SharePoint, abra o menu **ações do site** e escolha **configurações do site**.

4. Na seção **ações do site** da página **configurações do site** , escolha o link **gerenciar recursos do site** .

5. Na página **recursos** , escolha o botão **Ativar** ao lado do recurso **FeatureEvtTest Feature1** .

6. Na página **recursos** , escolha o botão **desativar** ao lado do recurso **FeatureEvtTest Feature1** e escolha o link **desativar este recurso** para desativar o recurso.

7. Escolha o botão **página inicial** .

     Observe que um anúncio aparece na lista **comunicados** depois que o recurso é desativado.

## <a name="see-also"></a>Consulte também

- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)