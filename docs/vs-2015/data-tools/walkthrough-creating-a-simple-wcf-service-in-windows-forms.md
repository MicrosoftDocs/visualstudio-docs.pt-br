---
title: 'Passo a passo: Criando um serviço WCF simples no Windows Forms | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- WCF, walkthrough [Visual Studio]
- WCF, Visual Studio tools for
- WCF services
- WCF services, walkthrough
ms.assetid: 5fef1a64-27a4-4f10-aa57-29023e28a2d6
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6e73659c2d28cf97a8a7136ed8232cfbc5f0b77c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49247202"
---
# <a name="walkthrough-creating-a-simple-wcf-service-in-windows-forms"></a>Passo a passo: Criando um serviço WCF simples no Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este passo a passo demonstra como criar um simples [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] de serviço, testá-lo e, em seguida, acessá-lo de um aplicativo Windows Forms.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="creating-the-service"></a>Criando o serviço  
  
#### <a name="to-create-a-wcf-service"></a>Para criar um serviço WCF  
  
1.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** nó e clique em **WCF**, seguido por **WCF Biblioteca de serviço**. Clique em **Okey** para abrir o projeto.  
  
     ![O projeto de biblioteca de serviço do WCF](../data-tools/media/wcf1.PNG "wcf1")  
  
    > [!NOTE]
    >  Isso cria um serviço de trabalho que pode ser testado e acessado. As duas etapas a seguir demonstram como você pode modificar o método padrão para usar um tipo de dados diferentes. Em um aplicativo real, você também adicionaria suas próprias funções para o serviço.  
  
3.  ![O arquivo IService1](../data-tools/media/wcf2.png "wcf2")  
  
     Na **Gerenciador de soluções**, clique duas vezes em IService1.vb ou IService1.cs e localize a seguinte linha:  
  
     [! código csharp [WCFWalkthrough n º 4] (... /snippets/CSharp/VS_Snippets_VBCSharp/wcfwalkthrough/CS/IService1 (2).cs n º 4)] [! código vb [WCFWalkthrough n º 4] (... /snippets/VisualBasic/VS_Snippets_VBCSharp/wcfwalkthrough/VB/IService1 (2).vb n º 4)]  
  
     Alterar o tipo para o `value` parâmetro para `String`:  
  
     [!code-csharp[WCFWalkthrough#1](../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/iservice1.cs#1)]
     [!code-vb[WCFWalkthrough#1](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/iservice1.vb#1)]  
  
     No código acima, observe os `<OperationContract()>` ou `[OperationContract]` atributos. Esses atributos são necessários para qualquer método exposto pelo serviço.  
  
4.  ![O arquivo Service1](../data-tools/media/wcf3.png "wcf3")  
  
     Na **Gerenciador de soluções**, clique duas vezes em Service1.vb ou Service1.cs e localize a seguinte linha:  
  
     [! código csharp [WCFWalkthrough n º 5] (... /snippets/CSharp/VS_Snippets_VBCSharp/wcfwalkthrough/CS/Service1 (2).cs n º 5)] [! código vb [WCFWalkthrough n º 5] (... /snippets/VisualBasic/VS_Snippets_VBCSharp/wcfwalkthrough/VB/Service1 (2).vb n º 5)]  
  
     Alterar o tipo para o parâmetro value para `String`:  
  
     [!code-csharp[WCFWalkthrough#2](../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/service1.cs#2)]
     [!code-vb[WCFWalkthrough#2](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/service1.vb#2)]  
  
## <a name="testing-the-service"></a>O serviço de teste  
  
#### <a name="to-test-a-wcf-service"></a>Para testar um serviço WCF  
  
1.  Pressione **F5** para executar o serviço. Um **cliente de teste do WCF** formulário será exibido e ele carregará o serviço.  
  
2.  No **cliente de teste do WCF** de formulário, clique duas vezes o **GetData ()** método sob **IService1**. O **GetData** guia será exibida.  
  
     ![O GetData&#40; &#41; método](../data-tools/media/wcf4.png "wcf4")  
  
3.  No **solicitar** caixa, selecione a **valor** campo e digite `Hello`.  
  
     ![O campo de valor](../data-tools/media/wcf5.png "wcf5")  
  
4.  Clique o **Invoke** botão. Se um **aviso de segurança** caixa de diálogo for exibida, clique em **Okey**. O resultado será exibido na **resposta** caixa.  
  
     ![O resultado na caixa de resposta](../data-tools/media/wcf6.png "wcf6")  
  
5.  Sobre o **arquivo** menu, clique em **sair** para fechar o formulário de teste.  
  
## <a name="accessing-the-service"></a>Acessando o serviço  
  
#### <a name="to-reference-a-wcf-service"></a>Para fazer referência a um serviço WCF  
  
1.  Sobre o **arquivo** , aponte para **Add** e, em seguida, clique em **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** nó e selecione **Windows**e, em seguida, selecione **Aplicativo de formulários do Windows**. Clique em **Okey** para abrir o projeto.  
  
     ![Projeto de aplicativo do Windows Forms](../data-tools/media/wcf7.png "wcf7")  
  
3.  Clique com botão direito **WindowsApplication1** e clique em **Add Service Reference**. O **adicionar referência de serviço** caixa de diálogo será exibida.  
  
4.  No **adicionar referência de serviço** caixa de diálogo, clique em **Discover**.  
  
     ![A caixa de diálogo Add Service Reference](../data-tools/media/wcf8.png "wcf8")  
  
     **O Service1** será exibido na **Services** painel.  
  
5.  Clique em **Okey** para adicionar a referência de serviço.  
  
#### <a name="to-build-a-client-application"></a>Para criar um aplicativo cliente  
  
1.  Na **Gerenciador de soluções**, clique duas vezes em **Form1.vb** ou **Form1.cs** para abrir o Designer de formulários do Windows, se ele não ainda estiver aberto.  
  
2.  Dos **caixa de ferramentas**, arraste um `TextBox` controle, um `Label` controle e um `Button` controle para o formulário.  
  
     ![Adicionando controles ao formulário](../data-tools/media/wcf9.png "wcf9")  
  
3.  Clique duas vezes o `Button`e adicione o seguinte código no `Click` manipulador de eventos:  
  
     [!code-csharp[WCFWalkthrough#3](../snippets/csharp/VS_Snippets_VBCSharp/wcfwalkthrough/cs/form1.cs#3)]
     [!code-vb[WCFWalkthrough#3](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfwalkthrough/vb/form1.vb#3)]  
  
4.  Na **Gerenciador de soluções**, clique com botão direito **WindowsApplication1** e clique em **Set as StartUp Project**.  
  
5.  Pressione **F5** para executar o projeto. Digite algum texto e clique no botão. O rótulo exibirá "você digitou:" e o texto que você inseriu.  
  
     ![O formulário mostrando o resultado](../data-tools/media/wcf10.png "wcf10")  
  
## <a name="see-also"></a>Consulte também  
 [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)

