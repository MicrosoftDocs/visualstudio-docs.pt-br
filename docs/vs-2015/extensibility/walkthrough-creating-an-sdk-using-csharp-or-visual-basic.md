---
title: 'Passo a passo: Criando um SDK usando c# ou Visual Basic | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef96a249-5eef-402a-a8d5-d74cb49239bd
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3e0bc88c8581b29f43e7efc55ee86019e1f1c3fb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51736753"
---
# <a name="walkthrough-creating-an-sdk-using-c-or-visual-basic"></a>Passo a passo: criando um SDK usando C# ou Visual Basic
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste passo a passo, você aprenderá como criar um SDK de biblioteca de matemática simples usando o Visual c# e, em seguida, o SDK como um Visual Studio VSIX (extensão) do pacote. Você concluirá os procedimentos a seguir:  
  
-   [Para criar o componente de tempo de execução SimpleMath Windows](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createClassLibrary)  
  
-   [Para criar o projeto de extensão SimpleMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createVSIX)  
  
-   [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md#createSample)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
##  <a name="createClassLibrary"></a> Para criar o componente de tempo de execução SimpleMath Windows  
  
1.  Na barra de menus, escolha **arquivo**, **New**, **novo projeto**.  
  
2.  Na lista de modelos, expanda **Visual c#** ou **Visual Basic**, escolha o **Windows Store** nó e, em seguida, escolha o **componente de tempo de execução do Windows** modelo.  
  
3.  No **nome** , especifique **SimpleMath**e, em seguida, escolha o **Okey** botão.  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMath** nó do projeto e, em seguida, escolha **propriedades**.  
  
5.  Renomeie **Class1.cs** à **Arithmetic.cs** e atualizá-lo de acordo com o código a seguir:  
  
     [!code-csharp[CreatingAnSDKUsingWinRT#3](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmath/arithmetic.cs#3)]
     [!code-vb[CreatingAnSDKUsingWinRT#3](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmath/arithmetic.vb#3)]  
  
6.  Na **Gerenciador de soluções**, abra o menu de atalho para o **solução 'SimpleMath'** nó e, em seguida, escolha **Configuration Manager**.  
  
     O **Configuration Manager** caixa de diálogo é aberta.  
  
7.  No **configuração da solução ativa** , escolha **versão**.  
  
8.  No **Configuration** coluna, verifique **SimpleMath** linha é definida como **versão**e, em seguida, escolha o **fechar** botão para aceitar o Altere.  
  
    > [!IMPORTANT]
    >  O SDK para o componente SimpleMath inclui apenas uma configuração. Essa configuração deve ser o build de versão, ou aplicativos que usam o componente não passam na certificação o[!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)].  
  
9. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMath** nó do projeto e, em seguida, escolha **Build**.  
  
##  <a name="createVSIX"></a> Para criar o projeto de extensão SimpleMathVSIX  
  
1.  No menu de atalho para o **solução 'SimpleMath'** nó, escolha **Add**, **novo projeto**.  
  
2.  Na lista de modelos, expanda **Visual c#** ou **Visual Basic**, escolha o **extensibilidade** nó e, em seguida, escolha o **projeto VSIX** modelo.  
  
3.  No **nome** , especifique **SimpleMathVSIX**e, em seguida, escolha o **Okey** botão.  
  
4.  Na **Gerenciador de soluções**, escolha o **vsixmanifest** item.  
  
5.  Na barra de menus, escolha **Exibir**, **Código**.  
  
6.  Substitua o XML existente com o seguinte XML:  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-csharp-or-visual-basic_2.xml)]
  
7.  Na **Gerenciador de soluções**, escolha o **SimpleMathVSIX** projeto.  
  
8.  Na barra de menus, escolha **Project**, **Adicionar Novo Item**.  
  
9. Na lista de **itens comuns**, expanda **dados**e, em seguida, escolha **arquivo XML**.  
  
10. No **nome** , especifique `SDKManifest.xml`e, em seguida, escolha o **Add** botão.  
  
11. Na **Gerenciador de soluções**, abra o menu de atalho `SDKManifest.xml`, escolha **propriedades**e, em seguida, altere o valor da **incluir em VSIX** propriedade para **Verdadeiro**.  
  
12. Substitua o conteúdo do arquivo pelo XML a seguir:  
  
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrt/cs/winrtmathvsix/sdkmanifest.xml#1)]
     [!code-xml[CreatingAnSDKUsingWinRT#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrt/vb/winrtmathvsix/sdkmanifest.xml#1)]  
  
13. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMathVSIX** do projeto, escolha **Add**e, em seguida, escolha **nova pasta**.  
  
14. Renomear a pasta para `references`.  
  
15. Abra o menu de atalho para o **referências** pasta, escolha **Add**e, em seguida, escolha **nova pasta**.  
  
16. Renomeie a subpasta `commonconfiguration`, crie uma subpasta dentro dele e nomear a subpasta `neutral`.  
  
17. Repita as quatro etapas anteriores, desta vez, a primeira pasta para a renomeação `redist`.  
  
     O projeto agora contém a seguinte estrutura de pasta:  
  
    ```  
    references\commonconfiguration\neutral  
    redist\commonconfiguration\neutral  
    ```  
  
18. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMath** do projeto e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
19. Na **Explorador de arquivos**, navegue até a pasta bin\Release, abra o menu de atalho para o arquivo SimpleMath.winmd e, em seguida, escolha **cópia**.  
  
20. Na **Gerenciador de soluções**, cole o arquivo na pasta references\commonconfiguration\neutral a **SimpleMathVSIX** projeto.  
  
21. Repita a etapa anterior, colando o arquivo SimpleMath.pri na pasta redist\commonconfiguration\neutral a **SimpleMathVSIX** projeto.  
  
22. Na **Gerenciador de soluções**, escolha **SimpleMath.winmd**.  
  
23. Na barra de menus, escolha **modo de exibição**, **propriedades** (teclado: escolha a tecla F4).  
  
24. No **propriedades** janela, altere o **Build Action** propriedade a ser **conteúdo**e, em seguida, altere o **incluir em VSIX** propriedade  **True**.  
  
25. Na **Gerenciador de soluções**, repita esse processo para **SimpleMath.pri**.  
  
26. Na **Gerenciador de soluções**, escolha o **SimpleMathVSIX** projeto.  
  
27. Na barra de menus, escolha **construir**, **SimpleMathVSIX Build**.  
  
28. Na **Gerenciador de soluções**, abra o menu de atalho para o **SimpleMathVSIX** do projeto e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
29. Na **Explorador de arquivos**, navegue até a pasta \bin\Release, e, em seguida, executar SimpleMathVSIX.vsix para instalá-lo.  
  
30. Escolha o **instalar** botão, aguarde a conclusão da instalação e, em seguida, reinicie o Visual Studio.  
  
##  <a name="createSample"></a> Para criar um aplicativo de exemplo que usa a biblioteca de classes  
  
1. Na barra de menus, escolha **arquivo**, **New**, **novo projeto**.  
  
2. Na lista de modelos, expanda **Visual c#** ou **Visual Basic**e, em seguida, escolha o **Windows Store** nó.  
  
3. Escolha o **aplicativo em branco** modelo, o nome do projeto **ArithmeticUI**e, em seguida, escolha o **Okey** botão.  
  
4. Na **Gerenciador de soluções**, abra o menu de atalho para o **ArithmeticUI** do projeto e, em seguida, escolha **Add**, **referência**.  
  
5. Na lista de tipos de referência, expanda **Windows**e, em seguida, escolha **extensões**.  
  
6. No painel de detalhes, escolha o **SDK de matemática simples** extensão.  
  
    Informações adicionais sobre o SDK é exibida. Você pode escolher o **mais informações** link para abrir http://www.msdn.microsoft.com, conforme especificado no arquivo Sdkmanifest no início deste passo a passo.  
  
7. No **Gerenciador de referências** caixa de diálogo, selecione o **SDK de matemática simples** caixa de seleção e, em seguida, escolha o **Okey** botão.  
  
8. Na barra de menus, escolha **modo de exibição**, **Pesquisador de objetos**.  
  
9. No **navegue** , escolha **matemática simples**.  
  
     Agora você pode explorar o que há no SDK.  
  
10. Na **Gerenciador de soluções**, abra MainPage. XAML e substitua seu conteúdo com o XAML a seguir:  
  
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml#1)]
     [!code-xml[CreatingAnSDKUsingWinRTDemoApp#1](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml#1)]  
  
11. Atualize o MainPage.xaml.cs para coincidir com o código a seguir:  
  
     [!code-csharp[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/csharp/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/cs/winrtmathtest/mainpage.xaml.cs#2)]
     [!code-vb[CreatingAnSDKUsingWinRTDemoApp#2](../snippets/visualbasic/VS_Snippets_VSSDK/creatingansdkusingwinrtdemoapp/vb/winrtmathtest/mainpage.xaml.vb#2)]  
  
12. Escolha a tecla F5 para executar o aplicativo.  
  
13. No aplicativo, insira quaisquer dois números, escolha uma operação e, em seguida, escolha o **=** botão.  
  
     O resultado correto é exibido.  
  
    Você criou e usado um SDK de extensão com êxito.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criando um SDK usando C++](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)   
 [Passo a passo: Criando um SDK usando JavaScript](http://msdn.microsoft.com/en-us/6195ff56-4a27-45fc-bd29-4b0451225f4b)   
 [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md)

