---
title: 'Passo a passo: Criando um SDK usando JavaScript | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8c89d5d-5b78-4435-817f-c5f25ca6d715
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7d82e40de93a8b3323dbd03d9b76e935a1d303b0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781043"
---
# <a name="walkthrough-creating-an-sdk-using-javascript"></a>Passo a passo: criando um SDK usando JavaScript
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo ensina como usar JavaScript para criar uma matemática simples SDK como um Visual Studio VSIX (extensão).  O passo a passo é dividida nestas partes:  
  
- [Para criar o projeto do SDK de extensão SimpleMathVSIX](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSimpleMathVSIX)  
  
- [Para criar um aplicativo de exemplo que usa o SDK](../extensibility/walkthrough-creating-an-sdk-using-javascript.md#createSampleApp)  
  
  Para JavaScript, não há nenhum tipo de projeto de biblioteca de classe. Neste passo a passo, o arquivo de exemplo arithmetic.js é criado diretamente no projeto VSIX. Na prática, recomendamos que você primeiro compila e testar os arquivos JavaScript e CSS como um aplicativo da Windows Store — por exemplo, usando o **aplicativo em branco** modelo — antes de colocá-los em um projeto VSIX.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [SDK do Visual Studio](../extensibility/visual-studio-sdk.md).  
  
##  <a name="createSimpleMathVSIX"></a> Para criar o projeto do SDK de extensão SimpleMathVSIX  
  
1.  Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
2.  Na lista de categorias de modelo, sob **Visual c#**, selecione **extensibilidade**e, em seguida, selecione o **projeto VSIX** modelo.  
  
3.  No **nome** texto, especifique `SimpleMathVSIX` e escolha o **Okey** botão.  
  
4.  Se o **Assistente de pacote do Visual Studio** for exibida, escolha o **próxima** botão o **boas-vindas** página e, em seguida, na **página 1 de 7**, escolha o **Concluir** botão.  
  
     Embora o **Designer de manifesto** é aberto, vamos manter este passo a passo simples, modificando o arquivo de manifesto diretamente.  
  
5.  Na **Gerenciador de soluções**, abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha **Exibir código**. Use este código para substituir o conteúdo existente no arquivo.  
  
    ```  
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
  
6.  Na **Gerenciador de soluções**, abra o menu de atalho para o projeto SimpleMathVSIX e, em seguida, escolha **Add**, **Novo Item**.  
  
7.  No **dados** categoria, selecione **arquivo XML**, nomeie o arquivo `SDKManifest.xml`e escolha o **Add** botão.  
  
8.  Na **Gerenciador de soluções**, abra o menu de atalho para o arquivo Sdkmanifest e, em seguida, escolha **abra** para exibir o arquivo no **Editor XML**.  
  
9. Adicione o seguinte código ao arquivo Sdkmanifest.  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <FileList  
      DisplayName="Simple Math"  
      MinVSVersion="14.0"  
      AppliesTo="JavaScript+WindowsAppContainer"  
      SupportsMultipleVersions="Error"  
      MoreInfo="http://www.msdn.microsoft.com/">  
  
      <!-- JS -->  
      <File Content="js\arithmetic.js" />  
    </FileList>  
  
    ```  
  
10. Na **Gerenciador de soluções**, no menu de atalho para o arquivo Sdkmanifest, escolha **propriedades**.  
  
11. No **propriedades** janela, defina as **incluir em VSIX** propriedade a ser **verdadeiro**.  
  
12. Na **Gerenciador de soluções**, no menu de atalho para o projeto SimpleMathVSIX, escolha **Add**, **nova pasta**e, em seguida, nomeie a pasta `Redist`.  
  
13. Adicione subpastas em Redist para criar essa estrutura de pastas:  
  
     \Redist\CommonConfiguration\Neutral\SimpleMath\js\  
  
14. No menu de atalho para a pasta \js\, escolha **Add**, **Novo Item**.  
  
15. Sob **itens do Visual c#**, selecione o **Web** categoria e, em seguida, selecione o **arquivo JavaScript** item. Nomeie o arquivo `arithmetic.js`e, em seguida, escolha o **Add** botão.  
  
16. Insira o código a seguir na arithmetic.js:  
  
    ```  
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
  
17. Na **Gerenciador de soluções**, no menu de atalho para o arquivo arithmetic.js, escolha **propriedades**. Faça estas alterações de propriedade:  
  
    -   Defina a **incluir em VSIX** propriedade **verdadeiro**.  
  
    -   Defina a **Copy to Output Directory** propriedade **copiar sempre**.  
  
18. Na **Gerenciador de soluções**, no menu de atalho para o projeto SimpleMathVSIX, escolha **Build**.  
  
19. Depois que a compilação for concluída com êxito, no menu de atalho do projeto, escolha **Abrir pasta no Explorador de arquivos**. Navegue até \bin\debug\\e execute `SimpleMathVSIX.vsix` para instalá-lo.  
  
20. Escolha o **instalar** botão e permitem a instalação completa.  
  
21. Reinicie o Visual Studio.  
  
##  <a name="createSampleApp"></a> Para criar um aplicativo de exemplo que usa o SDK  
  
1.  Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
2.  Na lista de categorias de modelo, sob **JavaScript**, selecione **Windows Store**e, em seguida, selecione o **aplicativo em branco** modelo.  
  
3.  No **nome** , especifique `ArithmeticUI`. Escolha o botão **OK**.  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho para o projeto ArithmeticUI e, em seguida, escolha **Add**, **referência**.  
  
5.  Sob **Windows**, escolha **extensões**e observe que **matemática simples** é exibida.  
  
6.  Selecione o **matemática simples** caixa de seleção e, em seguida, escolha o **Okey** botão.  
  
7.  Na **Gerenciador de soluções**, em **referências**, observe que o **matemática simples** referência é exibida. Expandi-lo e observe que há uma pasta \js\ que inclui arithmetic.js. Você pode abrir arithmetic.js para confirmar que seu código-fonte foi instalado.  
  
8.  Use o código a seguir para substituir o conteúdo de Default. htm.  
  
    ```  
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
  
9. Use o próximo código para substituir o conteúdo de \js\default.js.  
  
    ```  
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
  
10. Substitua o conteúdo de \css\default.css por este código:  
  
    ```  
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
  
11. Escolha a tecla F5 para compilar e executar o aplicativo.  
  
12. No aplicativo da interface do usuário, insira quaisquer dois números, selecione uma operação e, em seguida, escolha o **=** botão. O resultado correto é exibido.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um Software Development Kit](../extensibility/creating-a-software-development-kit.md)

