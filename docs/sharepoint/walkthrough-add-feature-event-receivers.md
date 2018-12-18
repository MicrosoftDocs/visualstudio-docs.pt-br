---
title: 'Passo a passo: Adicionar receptores de evento | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, advanced packaging tools
- SharePoint development in Visual Studio, event receivers
- SharePoint development in Visual Studio, feature event receivers
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4ab2eded41d9416f03592c9346a379f8a276366a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49948753"
---
# <a name="walkthrough-add-feature-event-receivers"></a>Passo a passo: Adicionar receptores de evento
  Receptores de evento são métodos executados quando ocorre por um dos seguintes eventos relacionados ao recurso no SharePoint:

- Um recurso é instalado.

- Um recurso é ativado.

- Um recurso é desativado.

- Um recurso é removido.

  Este passo a passo demonstra como adicionar um receptor de eventos para um recurso em um projeto do SharePoint. Ele demonstra as seguintes tarefas:

- Criando um projeto vazio com um receptor de evento do recurso.

- Manipulando o **FeatureDeactivating** método.

- Usando o modelo de objeto de projeto do SharePoint para adicionar um comunicado para a lista de avisos.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

-   Edições com suporte do Microsoft Windows e do SharePoint.

-   Visual Studio.

## <a name="create-a-feature-event-receiver-project"></a>Criar um projeto de receptor de evento de recurso
 Primeiro, crie um projeto para conter o receptor de evento de recurso.

#### <a name="to-create-a-project-with-a-feature-event-receiver"></a>Para criar um projeto com um receptor de evento de recurso

1.  Na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto** caixa de diálogo.

2.  Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.

3.  No **modelos** painel, escolha o **o projeto do SharePoint 2010** modelo.

     Você pode usar esse tipo de projeto para receptores de evento porque eles têm nenhum modelo de projeto.

4.  No **nome** , digite **FeatureEvtTest**e, em seguida, escolha o **Okey** botão para exibir o **o Assistente para personalização do SharePoint**.

5.  Sobre o **especificar o nível de site e segurança para depuração** página, insira a URL do servidor do site do SharePoint ao qual você deseja adicionar o novo item de campo personalizado ou usar o local padrão (http://\<*sistema nome*> /).

6.  No **qual é o nível de confiança para essa solução do SharePoint?** , escolha o **implantar como uma solução de farm** botão de opção.

     Para obter mais informações sobre soluções em área restrita em comparação com soluções de farm, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

7.  Escolha o **terminar** botão e, em seguida, observe que um recurso chamado Feature1 aparece sob o **recursos** nó.

## <a name="add-an-event-receiver-to-the-feature"></a>Adicionar um receptor de eventos para o recurso
 Em seguida, adicionar um receptor de eventos para o recurso e adicione o código que é executado quando o recurso for desativado.

#### <a name="to-add-an-event-receiver-to-the-feature"></a>Para adicionar um receptor de eventos para o recurso

1.  Abra o menu de atalho para o nó de recursos e, em seguida, escolha **adicionar recurso** para criar um recurso.

2.  Sob o **recursos** nó, abra o menu de atalho **Feature1**e, em seguida, escolha **adicionar receptor de evento** para adicionar um receptor de eventos para o recurso.

     Isso adiciona um arquivo de código em Feature1. Nesse caso, ele é denominado *Feature1.EventReceiver.cs* ou *Feature1.EventReceiver.vb*, dependendo da linguagem de desenvolvimento do seu projeto.

3.  Se seu projeto é escrito em [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)], adicione o seguinte código na parte superior do receptor do evento, se ele não ainda estiver lá:

     [!code-csharp[SP_FeatureEvt#1](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#1)]

4.  A classe de receptor de evento contém vários métodos de comentada que atuam como eventos. Substitua os **FeatureDeactivating** método com o seguinte:

     [!code-vb[SP_FeatureEvt#2](../sharepoint/codesnippet/VisualBasic/featureevt2vb/features/feature1/feature1.eventreceiver.vb#2)]
     [!code-csharp[SP_FeatureEvt#2](../sharepoint/codesnippet/CSharp/featureevttest2/features/feature1/feature1.eventreceiver.cs#2)]

## <a name="test-the-feature-event-receiver"></a>O receptor de evento do recurso de teste
 Em seguida, desativar o recurso para testar se o **FeatureDeactivating** método gera um comunicado para a lista de anúncios do SharePoint.

#### <a name="to-test-the-feature-event-receiver"></a>Para testar o receptor de evento de recurso

1.  Defina o valor do projeto **configuração de implantação ativa** propriedade **sem ativação**.

     Definir essa propriedade impede que o recurso de ativação no SharePoint e permite que você depure receptores de evento. Para obter mais informações, consulte [soluções do SharePoint depurar](../sharepoint/debugging-sharepoint-solutions.md).

2.  Escolha o **F5** tecla para executar o projeto e implantá-lo no SharePoint.

3.  Na parte superior da página da Web do SharePoint, abra o **ações do Site** menu e, em seguida, escolha **configurações de Site**.

4.  Sob o **ações do Site** seção o **configurações de Site** , escolha o **gerenciar recursos do site** link.

5.  No **recursos** , escolha o **ativar** lado de **FeatureEvtTest Feature1** recurso.

6.  No **recursos** , escolha o **Deactivate** lado a **FeatureEvtTest Feature1** recurso e, em seguida, escolha o **desativar esse recurso**  link de confirmação para desativar o recurso.

7.  Escolha o **Home** botão.

     Observe que um anúncio é exibido na **anúncios** lista depois que o recurso é desativado.

## <a name="see-also"></a>Consulte também

- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)