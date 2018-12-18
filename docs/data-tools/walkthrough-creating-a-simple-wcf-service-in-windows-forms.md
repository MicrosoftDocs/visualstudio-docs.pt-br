---
title: 'Passo a passo: Criando um serviço WCF simples no Windows Forms'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- WCF, walkthrough [Visual Studio]
- WCF, Visual Studio tools for
- WCF services
- WCF services, walkthrough
ms.assetid: 5fef1a64-27a4-4f10-aa57-29023e28a2d6
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: e2c9d0bd58adcd0a0595c061fa4dfaa81f629601
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174241"
---
# <a name="walkthrough-create-a-simple-wcf-service-in-windows-forms"></a>Passo a passo: Criar um serviço WCF simples no Windows Forms

Este passo a passo demonstra como criar um simples [!INCLUDE[vsindigo](../data-tools/includes/vsindigo_md.md)] de serviço, testá-lo e, em seguida, acessá-lo de um aplicativo Windows Forms.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="create-the-service"></a>Criar o serviço

### <a name="to-create-a-wcf-service"></a>Para criar um serviço WCF

1.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.

2.  No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** nó e clique em **WCF**, seguido por **WCF Biblioteca de serviço**. Clique em **Okey** para abrir o projeto.

     ![O projeto de biblioteca de serviço do WCF](../data-tools/media/wcf1.png)

    > [!NOTE]
    >  Isso cria um serviço de trabalho que pode ser testado e acessado. As duas etapas a seguir demonstram como você pode modificar o método padrão para usar um tipo de dados diferentes. Em um aplicativo real, você também adicionaria suas próprias funções para o serviço.

3.  ![O arquivo IService1](../data-tools/media/wcf2.png)

     Na **Gerenciador de soluções**, clique duas vezes em **IService1.vb** ou **IService1.cs** e localize a seguinte linha:

     [!code-csharp[WCFWalkthrough#4](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_1.cs)]
     [!code-vb[WCFWalkthrough#4](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_1.vb)]

     Alterar o tipo para o `value` parâmetro de cadeia de caracteres:

     [!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_2.cs)]
     [!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_2.vb)]

     No código acima, observe os `<OperationContract()>` ou `[OperationContract]` atributos. Esses atributos são necessários para qualquer método exposto pelo serviço.

4.  ![O arquivo Service1](../data-tools/media/wcf3.png)

     Na **Gerenciador de soluções**, clique duas vezes em **Service1.vb** ou **Service1.cs** e localize a seguinte linha:

     [!code-vb[WCFWalkthrough#5](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_3.vb)]
     [!code-csharp[WCFWalkthrough#5](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_3.cs)]

     Alterar o tipo para o `value` parâmetro de cadeia de caracteres:

     [!code-csharp[WCFWalkthrough#2](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_4.cs)]
     [!code-vb[WCFWalkthrough#2](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_4.vb)]

## <a name="test-the-service"></a>Testar o serviço

### <a name="to-test-a-wcf-service"></a>Para testar um serviço WCF

1.  Pressione **F5** para executar o serviço. Um **cliente de teste do WCF** formulário é exibida e carrega o serviço.

2.  No **cliente de teste do WCF** de formulário, clique duas vezes o **GetData ()** método sob **IService1**. O **GetData** guia é exibida.

     ![O GetData&#40; &#41; método](../data-tools/media/wcf4.png)

3.  No **solicitar** caixa, selecione a **valor** campo e digite `Hello`.

     ![O campo de valor](../data-tools/media/wcf5.png)

4.  Clique o **Invoke** botão. Se um **aviso de segurança** caixa de diálogo for exibida, clique em **Okey**. O resultado exibe o **resposta** caixa.

     ![O resultado na caixa de resposta](../data-tools/media/wcf6.png)

5.  Sobre o **arquivo** menu, clique em **sair** para fechar o formulário de teste.

## <a name="access-the-service"></a>O serviço de acesso

### <a name="to-reference-a-wcf-service"></a>Para fazer referência a um serviço WCF

1.  Sobre o **arquivo** , aponte para **Add** e, em seguida, clique em **novo projeto**.

2.  No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** nó, selecione **Windows**e, em seguida, selecione  **Aplicativo de formulários do Windows**. Clique em **Okey** para abrir o projeto.

     ![Projeto de aplicativo do Windows Forms](../data-tools/media/wcf7.png)

3.  Clique com botão direito **WindowsApplication1** e clique em **Add Service Reference**. O **adicionar referência de serviço** caixa de diálogo é exibida.

4.  No **adicionar referência de serviço** caixa de diálogo, clique em **Discover**.

     ![A caixa de diálogo Adicionar referência de serviço](../data-tools/media/wcf8.png)

     **Service1** exibe as **Services** painel.

5.  Clique em **Okey** para adicionar a referência de serviço.

### <a name="to-build-a-client-application"></a>Para criar um aplicativo cliente

1.  Na **Gerenciador de soluções**, clique duas vezes em **Form1.vb** ou **Form1.cs** para abrir o Designer de formulários do Windows, se ele não ainda estiver aberto.

2.  Dos **caixa de ferramentas**, arraste um `TextBox` controle, um `Label` controle e um `Button` controle para o formulário.

     ![Adicionando controles ao formulário](../data-tools/media/wcf9.png)

3.  Clique duas vezes o `Button`e adicione o seguinte código no `Click` manipulador de eventos:

     [!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/walkthrough-creating-a-simple-wcf-service-in-windows-forms_5.cs)]
     [!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-simple-wcf-service-in-windows-forms_5.vb)]

4.  Na **Gerenciador de soluções**, clique com botão direito **WindowsApplication1** e clique em **Set as StartUp Project**.

5.  Pressione **F5** para executar o projeto. Digite algum texto e clique no botão. Exibe o rótulo "você digitou:" e mostra o texto que você inseriu.

     ![O formulário mostrando o resultado](../data-tools/media/wcf10.png)

## <a name="see-also"></a>Consulte também

- [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)