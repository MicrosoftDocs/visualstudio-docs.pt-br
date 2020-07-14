---
title: 'Walkthrough: Criando um SDK usando C++ | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 36ea793b-3832-41a1-b906-69e680ad5e1d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 15fa0714097efda31b52f1d389d3a26cf581e506
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905011"
---
# <a name="walkthrough-create-an-sdk-using-c"></a>Walkthrough: criar um SDK usando C++
Este tutorial mostra como criar um SDK de biblioteca matemática C++ nativo, empacotar o SDK como um VSIX (extensão do Visual Studio) e, em seguida, usá-lo para criar um aplicativo. O passo a passo é dividido nestas etapas:

- [Para criar as bibliotecas de Windows Runtime e nativas](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createClassLibrary)

- [Para criar o projeto de extensão NativeMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createVSIX)

- [Para criar um aplicativo de exemplo que usa a biblioteca de classes](../extensibility/walkthrough-creating-an-sdk-using-cpp.md#createSample)

## <a name="prerequisites"></a>Pré-requisitos
 Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="to-create-the-native-and-windows-runtime-libraries"></a><a name="createClassLibrary"></a>Para criar as bibliotecas de Windows Runtime e nativas

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na lista de modelos, expanda **Visual C++**  >  **Windows universal**e, em seguida, selecione o modelo **dll (aplicativos do Windows universal)** . Na caixa **nome** , especifique `NativeMath` e, em seguida, escolha o botão **OK** .

3. Atualize *NativeMath. h* para corresponder ao código a seguir.

     [!code-cpp[CreatingAnSDKUsingCpp#1](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_1.h)]

4. Atualize *NativeMath. cpp* para corresponder a este código:

     [!code-cpp[CreatingAnSDKUsingCpp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_2.cpp)]

5. No **Gerenciador de soluções**, abra o menu de atalho da **solução ' NativeMath '** e escolha **Adicionar**  >  **novo projeto**.

6. Na lista de modelos, expanda **Visual C++** e, em seguida, selecione o modelo de **componente de Windows Runtime** . Na caixa **nome** , especifique `NativeMathWRT` e, em seguida, escolha o botão **OK** .

7. Atualize *Class1. h* para corresponder a este código:

     [!code-cpp[CreatingAnSDKUsingCpp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_3.h)]

8. Atualize *Class1. cpp* para corresponder a este código:

     [!code-cpp[CreatingAnSDKUsingCpp#4](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_4.cpp)]

9. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

## <a name="to-create-the-nativemathvsix-extension-project"></a><a name="createVSIX"></a>Para criar o projeto de extensão NativeMathVSIX

1. No **Gerenciador de soluções**, abra o menu de atalho da **solução ' NativeMath '** e escolha **Adicionar**  >  **novo projeto**.

2. Na lista de modelos, expanda extensibilidade do **Visual C#**  >  **Extensibility**e selecione **projeto VSIX**. Na caixa **nome** , especifique **NativeMathVSIX**e, em seguida, escolha o botão **OK** .

3. No **Gerenciador de soluções**, abra o menu de atalho para **Source. Extension. vsixmanifest**e escolha **Exibir código**.

4. Use o XML a seguir para substituir o XML existente.

    [!code-xml[CreatingAnSDKUsingCpp#6](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_6.xml)]

5. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **NativeMathVSIX** e escolha **Adicionar**  >  **novo item**.

6. Na lista de **itens do Visual C#**, expanda **dados**e, em seguida, selecione **arquivo XML**. Na caixa **nome** , especifique `SDKManifest.xml` e, em seguida, escolha o botão **OK** .

7. Use esse XML para substituir o conteúdo do arquivo:

     [!code-xml[CreatingAnSDKUsingCpp#5](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_5.xml)]

8. No **Gerenciador de soluções**, no projeto **NativeMathVSIX** , crie esta estrutura de pastas:

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

9. No **Gerenciador de soluções**, abra o menu de atalho da **solução ' NativeMath '** e, em seguida, escolha **abrir pasta no explorador de arquivos**.

10. No **Explorador de arquivos**, copie *$solutionroot $ \NativeMath\NativeMath.h*e, em **Gerenciador de soluções**, no projeto **NativeMathVSIX** , Cole-o na pasta *$solutionroot $ \NativeMathVSIX\DesignTime\CommonConfiguration\Neutral\Include \\ * .

     Copie *$solutionroot $ \Debug\NativeMath\NativeMath.lib*e cole-o na pasta *$solutionroot $ \NativeMathVSIX\DesignTime\Debug\x86 \\ * .

     Copie *$solutionroot $\Debug\NativeMath\NativeMath.dll* e cole-o na pasta *$solutionroot $ \\ \NativeMathVSIX\Redist\Debug\x86*

     Copie *$solutionroot $\Debug\NativeMathWRT\NativeMathWRT.dll* e cole-o na pasta *$solutionroot $ \NativeMathVSIX\Redist\Debug\x86*
     Copie *$solutionroot $ \Debug\NativeMathWRT\NativeMathWRT.winmd* e cole-o na pasta *$solutionroot $ \NativeMathVSIX\References\CommonConfiguration\Neutral* .

     Copie *$solutionroot $ \Debug\NativeMathWRT\NativeMathWRT.pri* e cole-o na pasta *$solutionroot $ \NativeMathVSIX\References\CommonConfiguration\Neutral* .

11. Na pasta *$solutionroot $ \NativeMathVSIX\DesignTime\Debug\x86 \\ * , crie um arquivo de texto chamado *NativeMathSDK. props*e cole o seguinte conteúdo nele:

    [!code-xml[CreatingAnSDKUsingCpp#7](../extensibility/codesnippet/XML/walkthrough-creating-an-sdk-using-cpp_7.xml)]

12. Na barra de menus, escolha **Exibir**  >  **outras**  >  **janela Propriedades** do Windows (teclado: escolha a tecla **F4** ).

13. Em **Gerenciador de soluções**, selecione o arquivo **NativeMathWRT. winmd** . Na janela **Propriedades** , altere a propriedade **ação de compilação** para **conteúdo**e, em seguida, altere a propriedade **incluir na VSIX** para **true**.

     Repita esse processo para o arquivo **NativeMath. h** .

     Repita esse processo para o arquivo **NativeMathWRT. pri** .

     Repita esse processo para o arquivo **NativeMath. lib** .

     Repita esse processo para o arquivo **NativeMathSDK. props** .

14. Em **Gerenciador de soluções**, selecione o arquivo **NativeMath. h** . Na janela **Propriedades** , altere a propriedade **include in VSIX** para **true**.

     Repita esse processo para o arquivo de **NativeMath.dll** .

     Repita esse processo para o arquivo de **NativeMathWRT.dll** .

     Repita esse processo para o arquivo de **SDKManifest.xml** .

15. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

16. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **NativeMathVSIX** e, em seguida, escolha **abrir pasta no explorador de arquivos**.

17. No **Explorador de arquivos**, navegue até a pasta *$solutionroot $ \NativeMathVSIX\bin\Debug* e execute *NativeMathVSIX. vsix* para iniciar a instalação.

18. Escolha o botão **instalar** , aguarde a conclusão da instalação e, em seguida, abra o Visual Studio.

## <a name="to-create-a-sample-app-that-uses-the-class-library"></a><a name="createSample"></a>Para criar um aplicativo de exemplo que usa a biblioteca de classes

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na lista de modelos, expanda **Visual C++**  >  **Windows universal** e, em seguida, selecione **aplicativo em branco**. Na caixa **nome** , especifique **NativeMathSDKSample**e, em seguida, escolha o botão **OK** .

3. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **NativeMathSDKSample** e escolha **Adicionar**  >  **referência**.

4. Na caixa de diálogo **Adicionar referência** , na lista de tipos de referência, expanda **Universal do Windows**e selecione **extensões**. Por fim, marque a caixa de seleção **SDK de matemática nativa** e escolha o botão **OK** .

5. Exiba as propriedades do projeto para NativeMathSDKSample.

    As propriedades que você definiu em *NativeMathSDK. props* foram aplicadas quando você adicionou a referência. Você pode verificar se as propriedades foram aplicadas examinando a propriedade **diretórios do vc + +** das **Propriedades de configuração**do projeto.

6. No **Gerenciador de soluções**, abra **MainPage. XAML**e, em seguida, use o XAML a seguir para substituir seu conteúdo:

    [!code-xml[CreatingAnSDKUsingCppDemoApp#1](../extensibility/codesnippet/Xaml/walkthrough-creating-an-sdk-using-cpp_8.xaml)]

7. Atualize *MainPage. XAML. h* para corresponder a este código:

    [!code-cpp[CreatingAnSDKUsingCppDemoApp#2](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_9.h)]

8. Atualize *MainPage. XAML. cpp* para corresponder a este código:

     [!code-cpp[CreatingAnSDKUsingCppDemoApp#3](../extensibility/codesnippet/CPP/walkthrough-creating-an-sdk-using-cpp_10.cpp)]

9. Escolha a tecla **F5** para executar o aplicativo.

10. No aplicativo, insira dois números, selecione uma operação e, em seguida, escolha o **=** botão.

     O resultado correto é exibido.

    Este tutorial mostrou como criar e usar um SDK de extensão para chamar uma [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] biblioteca e uma não [!INCLUDE[wrt](../extensibility/includes/wrt_md.md)] biblioteca.

## <a name="next-steps"></a>Próximas etapas

## <a name="see-also"></a>Confira também
- [Walkthrough: criar um SDK usando C# ou Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md)
