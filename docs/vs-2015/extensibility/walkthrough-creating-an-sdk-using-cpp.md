---
title: 'Passo a passo: Criando um SDK usando C++ | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
caps.latest.revision: 33
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0932759213d064c3df717b7b6735c1201e62ce14
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51773464"
---
# <a name="walkthrough-creating-an-sdk-using-c"></a>Passo a passo: criando um SDK usando C++
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo mostra como criar uma biblioteca C++ nativa matemática SDK, o pacote SDK como um Visual Studio VSIX (extensão), e, em seguida, usá-lo para criar um aplicativo. O passo a passo é dividida nestas etapas:  
  
-   [Para criar o nativo e bibliotecas de tempo de execução do Windows](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)  
  
-   [Para criar o projeto de extensão NativeMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)  
  
-   [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
##  <a name="createClassLibrary"></a> Para criar o nativo e bibliotecas de tempo de execução do Windows  
  
1.  Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
2.  Na lista de modelos, expanda **Visual C++**, **Windows Store**e, em seguida, selecione o **DLL (aplicativos da Windows Store)** modelo. No **nome** , especifique `NativeMath`e, em seguida, escolha o **Okey** botão.  
  
3.  Atualize NativeMath.h para coincidir com o código a seguir.  
  
     [!code-cpp[CreatingAnSDKUsingCpp#1](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.h#1)]  
  
4.  Atualize NativeMath.cpp de acordo com este código:  
  
     [!code-cpp[CreatingAnSDKUsingCpp#2](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemath/nativemath.cpp#2)]  
  
5.  Na **Gerenciador de soluções**, abra o menu de atalho **solução 'NativeMath'** e, em seguida, escolha **Add**, **novo projeto**.  
  
6.  Na lista de modelos, expanda **Visual C++** e, em seguida, selecione o **componente de tempo de execução do Windows** modelo. No **nome** , especifique `NativeMathWRT`e, em seguida, escolha o **Okey** botão.  
  
7.  Atualize Class1.h de acordo com este código:  
  
     [!code-cpp[CreatingAnSDKUsingCpp#3](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.h#3)]  
  
8.  Atualize Class1.cpp de acordo com este código:  
  
     [!code-cpp[CreatingAnSDKUsingCpp#4](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathwrt/class1.cpp#4)]  
  
9. Na barra de menus, escolha **Compilar**, **Compilar Solução**.  
  
##  <a name="createVSIX"></a> Para criar o projeto de extensão NativeMathVSIX  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho **solução 'NativeMath'** e, em seguida, escolha **Add**, **novo projeto**.  
  
2.  Na lista de modelos, expanda **Visual c#**, **extensibilidade**e, em seguida, selecione **pacote VSIX**. No **nome** , especifique **NativeMathVSIX**e, em seguida, escolha o **Okey** botão.  
  
3.  Quando o designer de manifesto do VSIX for exibida, feche-o.  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho **vsixmanifest**e, em seguida, escolha **Exibir código**.  
  
5.  Use o seguinte XML para substituir o XML existente.  
  
    [!code-xml[CreatingAnSDKUsingCpp#6](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]
  
6.  Na **Gerenciador de soluções**, abra o menu de atalho para o **NativeMathVSIX** do projeto e, em seguida, escolha **Add**, **Novo Item**.  
  
7.  Na lista de **itens do Visual c#**, expanda **dados**e, em seguida, selecione **arquivo XML**. No **nome** , especifique `SDKManifest.xml`e, em seguida, escolha o **Okey** botão.  
  
8.  Use esse XML para substituir o conteúdo do arquivo:  
  
     [!code-xml[CreatingAnSDKUsingCpp#5](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcpp/cpp/nativemathvsix/sdkmanifest.xml#5)]  
  
9. Na **Gerenciador de soluções**, no **NativeMathVSIX** de projeto, crie a estrutura de pastas:  
  
    ```  
  
    \DesignTime  
          \CommonConfiguration  
                \Neutral  
                      \Include  
          \Debug  
                \x86  
    \Redist  
          \Debug  
                \x86  
    \References  
          \CommonConfiguration  
                \Neutral  
    ```  
  
10. Na **Gerenciador de soluções**, abra o menu de atalho **solução 'NativeMath'** e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
11. No **Explorador de arquivos**, copie \NativeMath\NativeMath.h e, em seguida, na **Gerenciador de soluções**, no **NativeMathVSIX** do projeto, cole-o no \DesignTime\ Pasta CommonConfiguration\Neutral\Include\.  
  
     Copie \Debug\NativeMath\NativeMath.lib e, em seguida, cole-o na pasta \DesignTime\Debug\x86\.  
  
     Copie \Debug\NativeMath\NativeMath.dll e cole-o na pasta \Redist\Debug\x86\.  
  
     Copie DebugNativeMathWRTNativeMathWRT.dll e cole-o na pasta RedistDebugx86.  
  
     Copie DebugNativeMathWRTNativeMathWRT.winmd e cole-o na pasta ReferencesCommonConfigurationNeutral.  
  
     Copie DebugNativeMathWRTNativeMathWRT.pri e cole-o na pasta ReferencesCommonConfigurationNeutral.  
  
12. Na pasta \DesignTime\Debug\x86\, crie um arquivo de texto chamado NativeMathSDK.props e, em seguida, cole o seguinte conteúdo nele:  
  
    [!code-xml[CreatingAnSDKUsingCpp#7](../../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]  
  
13. Na barra de menus, escolha **modo de exibição**, **Other Windows**, **janela propriedades** (teclado: escolha a tecla F4).  
  
14. Na **Gerenciador de soluções**, selecione o **NativeMathWRT.winmd** arquivo. No **propriedades** janela, altere o **Build Action** propriedade a ser **conteúdo**e, em seguida, altere o **incluir em VSIX** propriedade  **True**.  
  
     Repita esse processo para o **SimpleMath.pri** arquivo.  
  
     Repita esse processo para o **NativeMath.Lib** arquivo.  
  
     Repita esse processo para o **NativeMathSDK.props** arquivo.  
  
15. Na **Gerenciador de soluções**, selecione o **NativeMath.h** arquivo. No **propriedades** janela, altere o **incluir em VSIX** propriedade a ser **verdadeiro**.  
  
     Repita esse processo para o **NativeMath.dll** arquivo.  
  
     Repita esse processo para o **NativeMathWRT.dll** arquivo.  
  
     Repita esse processo para o **Sdkmanifest** arquivo.  
  
16. Na barra de menus, escolha **Compilar**, **Compilar Solução**.  
  
17. Na **Gerenciador de soluções**, abra o menu de atalho para o **NativeMathVSIX** do projeto e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
18. Na **Explorador de arquivos**, navegue até a pasta \bin\Debug\ e, em seguida, executar NativeMathVSIX.vsix para iniciar a instalação.  
  
19. Escolha o **instalar** botão, aguarde a conclusão da instalação e, em seguida, reinicie o Visual Studio.  
  
##  <a name="createSample"></a> Para criar um aplicativo de exemplo que usa a biblioteca de classes  
  
1. Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
2. Na lista de modelos, expanda **Visual C++**, **Windows Store**e, em seguida, selecione **aplicativo em branco**. No **nome** , especifique **NativeMathSDKSample**e, em seguida, escolha o **Okey** botão.  
  
3. Na **Gerenciador de soluções**, abra o menu de atalho para o **NativeMathSDKSample** do projeto e, em seguida, escolha **Add**, **referência**.  
  
4. Sobre o **propriedades comuns**, **estrutura e referências** página de propriedades, na lista de tipos de referência, expanda **Windows**e, em seguida, selecione **extensões** . No painel de detalhes, selecione a **nativo SDK de matemática** extensão e, em seguida, escolha o **adicionar nova referência** botão.  
  
5. No **adicionar referência** caixa de diálogo, selecione o **SDK nativo de matemática** caixa de seleção e, em seguida, escolha o **Okey** botão.  
  
6. Exiba as propriedades de projeto para NativeMathSDKSample.  
  
    As propriedades que você definiu no NativeMathSDK.props foram aplicadas quando você adicionou a referência. Você pode verificar isso examinando a **diretórios VC + +** propriedade do projeto **propriedades de configuração**.  
  
7. Na **Gerenciador de soluções**, abra MainPage. XAML e, em seguida, use o seguinte XAML para substituir seu conteúdo:  
  
    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml#1)]  
  
8. Atualize MainPage de acordo com este código:  
  
    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.h#2)]  
  
9. Atualize MainPage de acordo com este código:  
  
     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../snippets/cpp/VS_Snippets_VSSDK/creatingansdkusingcppdemoapp/cpp/mainpage.xaml.cpp#3)]  
  
10. Escolha a tecla F5 para executar o aplicativo.  
  
11. No aplicativo, insira quaisquer dois números, selecione uma operação e, em seguida, escolha o **=** botão.  
  
     O resultado correto é exibido.  
  
    Este passo a passo mostrou como criar e usar um SDK de extensão para chamar um [!INCLUDE[wrt](../includes/wrt-md.md)] biblioteca e um não -[!INCLUDE[wrt](../includes/wrt-md.md)] biblioteca.  
  
## <a name="next-steps"></a>Próximas etapas  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criando um SDK usando c# ou Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)   
 [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md)

