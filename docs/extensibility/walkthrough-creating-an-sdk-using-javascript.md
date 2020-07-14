---
title: 'Walkthrough: Criando um SDK usando JavaScript | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 29dac6cca7936dde8be2ebc57366f6370b8bcbc6
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904950"
---
# <a name="walkthrough-create-an-sdk-using-javascript"></a>Walkthrough: criar um SDK usando JavaScript
Este tutorial ensina como usar o JavaScript para criar um SDK de matemática simples como uma extensão do Visual Studio (VSIX).  O passo a passo é dividido nestas partes:

- [Para criar o projeto do SDK da extensão SimpleMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)

- [Para criar um aplicativo de exemplo que usa o SDK](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)

  Para JavaScript, não há nenhum tipo de projeto de biblioteca de classes. Neste tutorial, o arquivo de *arithmetic.js* de exemplo é criado diretamente no projeto VSIX. Na prática, recomendamos que você primeiro crie e teste os arquivos JavaScript e CSS como um aplicativo da Windows Store, por exemplo, usando o modelo de **aplicativo em branco** — antes de colocá-los em um projeto VSIX.

## <a name="prerequisites"></a>Pré-requisitos
 Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [Visual Studio SDK](../extensibility/visual-studio-sdk.md).

## <a name="to-create-the-simplemathvsix-extension-sdk-project"></a><a name="createSimpleMathVSIX"></a>Para criar o projeto do SDK da extensão SimpleMathVSIX

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na lista de categorias de modelo, em **Visual C#**, selecione **extensibilidade**e, em seguida, selecione o modelo de **projeto VSIX** .

3. Na caixa de texto **nome** , especifique `SimpleMathVSIX` e escolha o botão **OK** .

4. Se o **Assistente de pacote do Visual Studio** for exibido, escolha o botão **Avançar** na página de **boas-vindas** e, em seguida, na **página 1 de 7**, escolha o botão **concluir** .

     Embora o **Designer de manifesto** seja aberto, mantemos este passo a passos simples modificando o arquivo de manifesto diretamente.

5. No **Gerenciador de soluções**, abra o menu de atalho do arquivo **Source. Extension. vsixmanifest** e escolha **Exibir código**. Use este código para substituir o conteúdo existente no arquivo.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011" xmlns:d="http://schemas.microsoft.com/developer/vsx-schema-design/2011">
      <Metadata>
        <Identity Id="SimpleMathVSIX" Version="1.0" Language="en-US" Publisher="myname" />
        <DisplayName>Simple Math</DisplayName>
        <Description>Does basic arithmetic calculations.</Description>
      </Metadata>
      <Installation Scope="Global" AllUsers="true">
        <InstallationTarget Id="Microsoft.ExtensionSDK" TargetPlatformIdentifier="Windows" TargetPlatformVersion="v8.0" SdkName="SimpleMath" SdkVersion="1.0" />
      </Installation>
      <Dependencies>
        <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" d:Source="Manual" Version="4.5" />
      </Dependencies>
      <Assets>
        <Asset Type="Microsoft.ExtensionSDK" d:Source="File" Path="SDKManifest.xml" />
      </Assets>
    </PackageManifest>
    ```

6. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **SimpleMathVSIX** e escolha **Adicionar**  >  **novo item**.

7. Na categoria de **dados** , selecione **arquivo XML**, nomeie o arquivo `SDKManifest.xml` e escolha o botão **Adicionar** .

8. No **Gerenciador de soluções**, abra o menu de atalho para o arquivo de **SDKManifest.xml** e escolha **abrir** para exibir o arquivo no **Editor de XML**.

9. Adicione o código a seguir ao arquivo de **SDKManifest.xml** .

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <FileList
      DisplayName="Simple Math"
      MinVSVersion="14.0"
      AppliesTo="JavaScript+WindowsAppContainer"
      SupportsMultipleVersions="Error"
      MoreInfo="https://msdn.microsoft.com/">

      <!-- JS -->
      <File Content="js\arithmetic.js" />
    </FileList>

    ```

10. No **Gerenciador de soluções**, no menu de atalho do arquivo de **SDKManifest.xml** , escolha **Propriedades**.

11. Na janela **Propriedades** , defina a propriedade **include in VSIX** como **true**.

12. No **Gerenciador de soluções**, no menu de atalho do projeto **SimpleMathVSIX** , escolha **Adicionar**  >  **nova pasta**e, em seguida, nomeie a pasta `Redist` .

13. Adicione subpastas em Redist para criar esta estrutura de pastas:

     *\Redist\CommonConfiguration\Neutral\SimpleMath\js\\*

14. No menu de atalho da pasta **\js \\ ** , escolha **Adicionar**  >  **novo item**.

15. Em **itens do Visual C#**, selecione a categoria **Web** e, em seguida, selecione o item de **arquivo JavaScript** . Nomeie o arquivo `arithmetic.js` e, em seguida, escolha o botão **Adicionar** .

16. Insira o código a seguir em *arithmetic.js*:

    ```csharp
    (function (global) {
        "use strict";
        global.Arithmetic = {
            add: function (firstNumber, secondNumber) {
                return firstNumber + secondNumber;
            },

            subtract: function (firstNumber, secondNumber) {
                return firstNumber - secondNumber;
            },

            multiply: function (firstNumber, secondNumber) {
                return firstNumber * secondNumber;
            },

            divide: function (firstNumber, secondNumber) {
                return firstNumber / secondNumber;
            }
        };
    })(this);

    ```

17. No **Gerenciador de soluções**, no menu de atalho do arquivo de **arithmetic.js** , escolha **Propriedades**. Faça essas alterações de propriedade:

    - Defina a propriedade **include in VSIX** como **true**.

    - Defina a propriedade **copiar para diretório de saída** como **copiar sempre**.

18. No **Gerenciador de soluções**, no menu de atalho do projeto **SimpleMathVSIX** , escolha **Compilar**.

19. Depois que a compilação for concluída com êxito, no menu de atalho do projeto, escolha **abrir pasta no explorador de arquivos**. Navegue até **\bin\Debug \\ **e execute `SimpleMathVSIX.vsix` para instalá-lo.

20. Escolha o botão **instalar** e deixe a instalação ser concluída.

21. Reinicie o Visual Studio.

## <a name="to-create-a-sample-app-that-uses-the-sdk"></a><a name="createSampleApp"></a>Para criar um aplicativo de exemplo que usa o SDK

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na lista de categorias de modelo, em **JavaScript**, selecione **Windows Store**e, em seguida, selecione o modelo de **aplicativo em branco** .

3. Na caixa **nome** , especifique `ArithmeticUI` . Clique no botão **OK**.

4. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ArithmeticUI** e escolha **Adicionar**  >  **referência**.

5. Em **Windows**, escolha **extensões**e observe que a **matemática simples** é exibida.

6. Marque a caixa de seleção **matemática simples** e escolha o botão **OK** .

7. Em **Gerenciador de soluções**, em **referências**, observe que a referência **matemática simples** é exibida. Expanda-o e observe que há uma pasta **\js \\ ** que inclui **arithmetic.js**. Você pode abrir **arithmetic.js** para confirmar que o código-fonte foi instalado.

8. Use o código a seguir para substituir o conteúdo de *default.htm*.

   ```html
   <!DOCTYPE html>
   <html>
   <head>
       <meta charset="utf-8" />
       <title>ArithmeticUI</title>

       <!-- WinJS references -->
       <link href="//Microsoft.WinJS.1.0/css/ui-dark.css" rel="stylesheet" />
       <script src="//Microsoft.WinJS.1.0/js/base.js"></script>
       <script src="//Microsoft.WinJS.1.0/js/ui.js"></script>

       <!-- ArithmeticUI references -->
       <link href="/css/default.css" rel="stylesheet" />
       <script src="/js/default.js"></script>
       <script src="/SimpleMath/js/arithmetic.js"></script>
   </head>
   <body>
       <form>
       <div id="calculator" class="ms-grid">
           <input name="firstNumber" id="firstNumber" type="number" step="any">
           <div id="operators">
               <button class="operator" type="button">+</button>
               <button class="operator" type="button">-</button>
               <button class="operator" type="button">*</button>
               <button class="operator" type="button">/</button>
           </div>
           <input id="secondNumber" type="number">
           <button class="calculate" type="button">=</button>
           <input id="result" type="number" name="result" disabled="" readonly="">
       </div>
       </form>
   </body>
   </html>
   ```

9. Use o código a seguir para substituir o conteúdo de *\js\default.js*.

    ```csharp
    (function () {
        "use strict";

        var app = WinJS.Application;
        var operation = null;

        function calculateResult() {
            var firstNumber = parseFloat(document.querySelector("#firstNumber").value),
                secondNumber = parseFloat(document.querySelector("#secondNumber").value),
                result = 0;

            if (isNaN(firstNumber) || isNaN(secondNumber)) {
                result = 0;
            }
            else {
                switch (operation) {
                    case "+":
                        result = Arithmetic.add(firstNumber, secondNumber);
                        break;
                    case "-":
                        result = Arithmetic.subtract(firstNumber, secondNumber);
                        break;
                    case "*":
                        result = Arithmetic.multiply(firstNumber, secondNumber);
                        break;
                    case "/":
                        result = Arithmetic.divide(firstNumber, secondNumber);
                        break;
                    default:
                }
            }
            document.querySelector("#result").value = result.toString();
        }

        app.onactivated = function (args) {
            document.querySelector("#calculator").addEventListener("click", function (event) {
                if (event.target.tagName.toLowerCase() === "button") {
                    switch (event.target.className) {
                        case "operator":
                            operation = event.target.innerText;
                            break;
                        case "calculate":
                            calculateResult();
                            break;
                        default:
                            break;
                    }
                }
            });
        };

        app.start();
    })();
    ```

10. Substitua o conteúdo de *\css\default.css* por este código:

    ```xml
    form {
        display: -ms-grid;
        -ms-grid-rows: 1fr auto 1fr;
        -ms-grid-columns: 1fr auto 1fr;
        height: 100%;
        width: 100%;
    }

    button, input[type=number] {
        margin-right: 5px;
        -ms-grid-row-align: center;
    }

    #calculator {
        -ms-grid-column: 2;
        -ms-grid-row: 2;
        display: -ms-grid;
        -ms-grid-rows: 1fr;
        -ms-grid-columns: auto min-content auto auto auto;
    }

    .ms-grid input {
        width: 5em;
    }

    #firstNumber {
        -ms-grid-column: 1;
        -ms-grid-row-align: center;
    }

    #operators {
        -ms-grid-column: 2;
        -ms-grid-row-align: center;
    }

        #operators button.operator {
            margin-bottom: 5px;
            height: 40px;
        }

    #secondNumber {
        -ms-grid-column: 3;
    }

    button.calculate {
        -ms-grid-column: 4;
        -ms-grid-row-align: center;
        height: 40px;
    }

    #result {
        -ms-grid-column: 5;
    }

    ```

11. Escolha a tecla **F5** para compilar e executar o aplicativo.

12. Na interface do usuário do aplicativo, insira dois números, selecione uma operação e, em seguida, escolha o **=** botão. O resultado correto é exibido.

## <a name="see-also"></a>Confira também
- [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md)
