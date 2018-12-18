---
title: 'Passo a passo: Criando um SDK usando C++ | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6311526df299da860c829520a2087ecc8d786600
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49930630"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>Passo a passo: Criar um SDK usando C++
Este passo a passo mostra como criar uma biblioteca C++ nativa matemática SDK, o pacote SDK como um Visual Studio VSIX (extensão), e, em seguida, usá-lo para criar um aplicativo. O passo a passo é dividida nestas etapas:  
  
-   [Para criar o nativo e bibliotecas de tempo de execução do Windows](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)  
  
-   [Para criar o projeto de extensão NativeMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)  
  
-   [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
##  <a name="createClassLibrary"></a> Para criar o nativo e bibliotecas de tempo de execução do Windows  
  
1.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
2.  Na lista de modelos, expanda **Visual C++** > **Windows Universal**e, em seguida, selecione o **DLL (aplicativos universais do Windows)** modelo. No **nome** , especifique `NativeMath`e, em seguida, escolha o **Okey** botão.  
  
3.  Atualização *NativeMath.h* para coincidir com o código a seguir.  
  
     [!code-cpp[CreatingAnSDKUsingCpp#1](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_1.h)]  
  
4.  Atualização *NativeMath.cpp* para corresponder a este código:  
  
     [!code-cpp[CreatingAnSDKUsingCpp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_2.cpp)]  
  
5.  Na **Gerenciador de soluções**, abra o menu de atalho **solução 'NativeMath'** e, em seguida, escolha **Add** > **novo projeto**.  
  
6.  Na lista de modelos, expanda **Visual C++** e, em seguida, selecione o **componente de tempo de execução do Windows** modelo. No **nome** , especifique `NativeMathWRT`e, em seguida, escolha o **Okey** botão.  
  
7.  Atualização *Class1.h* para corresponder a este código:  
  
     [!code-cpp[CreatingAnSDKUsingCpp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_3.h)]  
  
8.  Atualização *Class1.cpp* para corresponder a este código:  
  
     [!code-cpp[CreatingAnSDKUsingCpp#4](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_4.cpp)]  
  
9. Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
##  <a name="createVSIX"></a> Para criar o projeto de extensão NativeMathVSIX  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho **solução 'NativeMath'** e, em seguida, escolha **Add** > **novo projeto**.  
  
2.  Na lista de modelos, expanda **Visual c#** > **extensibilidade**e, em seguida, selecione **projeto VSIX**. No **nome** , especifique **NativeMathVSIX**e, em seguida, escolha o **Okey** botão.
  
3.  Na **Gerenciador de soluções**, abra o menu de atalho **vsixmanifest**e, em seguida, escolha **Exibir código**.  
  
4.  Use o seguinte XML para substituir o XML existente.  
  
    [!code-xml[CreatingAnSDKUsingCpp#6](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]

5.  Na **Gerenciador de soluções**, abra o menu de atalho para o **NativeMathVSIX** do projeto e, em seguida, escolha **Add** > **Novo Item**.  
  
6.  Na lista de **itens do Visual c#**, expanda **dados**e, em seguida, selecione **arquivo XML**. No **nome** , especifique `SDKManifest.xml`e, em seguida, escolha o **Okey** botão.  
  
7.  Use esse XML para substituir o conteúdo do arquivo:  
  
     [!code-xml[CreatingAnSDKUsingCpp#5](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_5.xml)]  
  
8. Na **Gerenciador de soluções**, sob o **NativeMathVSIX** de projeto, crie a estrutura de pastas:  
  
    ```xml  
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
  
9. Na **Gerenciador de soluções**, abra o menu de atalho **solução 'NativeMath'** e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
10. Na **Explorador de arquivos**, cópia *$SolutionRoot$\NativeMath\NativeMath.h*e, em seguida, na **Gerenciador de soluções**, sob o **NativeMathVSIX**do projeto, cole-o a *$SolutionRoot$ \NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include\\*  pasta.  
  
     Cópia *$SolutionRoot$\Debug\NativeMath\NativeMath.lib*e, em seguida, cole-o na *$SolutionRoot$ \NativeMathVSIX\DesignTime\Debug\x86\\*  pasta.  
  
     Cópia *$SolutionRoot$\Debug\NativeMath\NativeMath.dll* e cole-à *$SolutionRoot$ \NativeMathVSIX\Redist\Debug\x86\\*  pasta.  
  
     Cópia *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.dll* e cole-à *$SolutionRoot$ \NativeMathVSIX\Redist\Debug\x86* pasta.  
     Cópia *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.winmd* e cole-à *$SolutionRoot$ \NativeMathVSIX\References\CommonConfiguration\Neutral* pasta.  
  
     Cópia *$SolutionRoot$\Debug\NativeMathWRT\NativeMathWRT.pri* e cole-à *$SolutionRoot$ \NativeMathVSIX\References\CommonConfiguration\Neutral* pasta.  
  
11. No *$SolutionRoot$ \NativeMathVSIX\DesignTime\Debug\x86\\*  pasta, crie um arquivo de texto chamado *NativeMathSDK.props*e, em seguida, cole o seguinte conteúdo nele:  
  
    [!code-xml[CreatingAnSDKUsingCpp#7](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]  
  
12. Na barra de menus, escolha **modo de exibição** > **Other Windows** > **janela propriedades** (teclado: escolha o **F4**chave).  
  
13. Na **Gerenciador de soluções**, selecione o **NativeMathWRT.winmd** arquivo. No **propriedades** janela, altere o **Build Action** propriedade a ser **conteúdo**e, em seguida, altere o **incluir em VSIX** propriedade  **True**.  
  
     Repita esse processo para o **NativeMath.h** arquivo.  
  
     Repita esse processo para o **NativeMathWRT.pri** arquivo.  
  
     Repita esse processo para o **NativeMath.Lib** arquivo.  
  
     Repita esse processo para o **NativeMathSDK.props** arquivo.  
  
14. Na **Gerenciador de soluções**, selecione o **NativeMath.h** arquivo. No **propriedades** janela, altere o **incluir em VSIX** propriedade a ser **verdadeiro**.  
  
     Repita esse processo para o **NativeMath.dll** arquivo.  
  
     Repita esse processo para o **NativeMathWRT.dll** arquivo.  
  
     Repita esse processo para o **Sdkmanifest** arquivo.  
  
15. Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
16. Na **Gerenciador de soluções**, abra o menu de atalho para o **NativeMathVSIX** do projeto e, em seguida, escolha **Abrir pasta no Explorador de arquivos**.  
  
17. Na **Explorador de arquivos**, navegue até a *$SolutionRoot$ \NativeMathVSIX\bin\Debug* pasta e, em seguida, execute *NativeMathVSIX.vsix* para iniciar a instalação.  
  
18. Escolha o **instalar** botão, aguarde a conclusão da instalação e, em seguida, inicie o Visual Studio.  
  
##  <a name="createSample"></a> Para criar um aplicativo de exemplo que usa a biblioteca de classes  
  
1. Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
2. Na lista de modelos, expanda **Visual C++** > **Windows Universal** e, em seguida, selecione **aplicativo em branco**. No **nome** , especifique **NativeMathSDKSample**e, em seguida, escolha o **Okey** botão.  
  
3. Na **Gerenciador de soluções**, abra o menu de atalho para o **NativeMathSDKSample** do projeto e, em seguida, escolha **Add** > **referência**.  
  
4. No **adicionar referência** caixa de diálogo, na lista de tipos de referência, expanda **Windows Universal**e, em seguida, selecione **extensões**. Por fim, selecione o **nativo SDK de matemática** caixa de seleção e, em seguida, escolha o **Okey** botão.
  
5. Exiba as propriedades de projeto para NativeMathSDKSample.  
  
    As propriedades que você definiu na *NativeMathSDK.props* foram aplicados quando você adicionou a referência. Você pode verificar as propriedades foram aplicadas, examinando os **diretórios VC + +** propriedade do projeto **propriedades de configuração**.  
  
6. Na **Gerenciador de soluções**, abra **MainPage. XAML**e, em seguida, use o XAML a seguir para substituir seu conteúdo:  
  
    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../extensibility/codesnippet/Xaml/walkthrough-creating-an-sdk-using-cpp_8.xaml)]  
  
7. Atualização *MainPage* para corresponder a este código:  
  
    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_9.h)]  
  
8. Atualização *MainPage* para corresponder a este código:  
  
     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_10.cpp)]  
  
9. Escolha o **F5** chave para executar o aplicativo.  
  
10. No aplicativo, insira quaisquer dois números, selecione uma operação e, em seguida, escolha o **=** botão.  
  
     O resultado correto é exibido.  
  
    Este passo a passo mostrou como criar e usar um SDK de extensão para chamar um [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] biblioteca e um não -[!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] biblioteca.  
  
## <a name="next-steps"></a>Próximas etapas  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criar um SDK usando c# ou Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)   
 [Criar um kit de desenvolvimento de software](../extensibility/creating-a-software-development-kit.md)
