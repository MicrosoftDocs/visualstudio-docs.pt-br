---
title: Depurar o código do usuário com apenas meu código | Microsoft Docs
ms.custom: ''
ms.date: 10/22/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 01e36c528b71bb49b29265890ca6c48863f01be9
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389021"
---
# <a name="debug-only-user-code-with-just-my-code"></a>Depurar somente código de usuário com apenas meu código 

*Apenas meu código* é um recurso de depuração do Visual Studio que automaticamente as etapas em chamadas para o sistema, o framework e o outro código de não usuário. No **pilha de chamadas** janela, apenas meu código recolhe essas chamadas em **[código externo]** quadros. 

Apenas meu código funciona de maneira diferente em projetos do .NET Framework, C++ e JavaScript.

##  <a name="BKMK_Enable_or_disable_Just_My_Code"></a> Habilitar ou desabilitar Apenas Meu Código  

Para a maioria das linguagens de programação, apenas meu código está habilitado por padrão. 

- Para habilitar ou desabilitar apenas meu código no Visual Studio, sob **ferramentas** > **opções** (ou **depurar** > **opções**) > **Debugging** > **geral**, marque ou desmarque **habilitar apenas meu código**.
  
 ![Habilitar apenas meu código na caixa de diálogo Opções](../debugger/media/dbg_justmycode_options.png "habilitar apenas meu código")  
  
> [!NOTE]
> **Habilitar apenas meu código** é uma configuração global que se aplica a todos os projetos do Visual Studio em todos os idiomas.  
  
##  <a name="just-my-code-debugging"></a>depuração Apenas Meu Código

Durante uma sessão de depuração, o **módulos** janela mostra que o depurador está tratando como My Code (código do usuário), os módulos de código, juntamente com seu status de carregamento de símbolo. Para obter mais informações, consulte [se familiarizar mais com como o depurador se anexa ao aplicativo](../debugger/debugger-tips-and-tricks.md#modules_window).

 ![Código do usuário na janela de módulos](../debugger/media/dbg_justmycode_module.png "código do usuário na janela de módulos")
  
No **pilha de chamadas** ou **tarefas** janela, apenas meu código recolhe o código de não usuário em um quadro de código com anotações de acinzentado rotulado `[External Code]`.

 ![Quadro de código externo na janela pilha de chamadas](../debugger/media/dbg_justmycode_externalcode.png "quadro do código externo")
  
>[!TIP]
>Para abrir o **módulos**, **pilha de chamadas**, **tarefas**, ou a maioria das outras janelas de depuração, você deve estar em uma sessão de depuração. Durante a depuração, sob **Debug** > **Windows**, selecione as janelas que você deseja abrir. 

<a name="BKMK_Override_call_stack_filtering"></a> Para exibir o código em um recolhido **[código externo]** de quadro, clique com botão direito no **pilha de chamadas** ou **tarefa** janela e selecione **Mostrar código externo**no menu de contexto. Substitua as linhas de código externo expandido a **[código externo**] quadro. 

 ![Mostrar código externo na janela pilha de chamadas](../debugger/media/dbg_justmycode_showexternalcode.png "Mostrar código externo")
  
> [!NOTE]
> **Mostrar código externo** é um criador de perfil de usuário atual que se aplicam a todos os projetos em todos os idiomas que são abertos pelo usuário.

Clicar duas vezes em uma linha de código externo expandido na **pilha de chamadas** janela realça a linha de código de chamada em verde no código-fonte. DLLs ou outros módulos não foi encontrada ou carregada, um símbolo ou origem não encontrado pode abrir a página.

##  <a name="BKMK__NET_Framework_Just_My_Code"></a>Apenas Meu Código do .NET Framework 

Em projetos do .NET Framework, apenas meu código usa o símbolo (*. PDB*) arquivos e otimizações de programa para classificar o código de usuário e de não usuário. O depurador do .NET Framework considera otimizado binários e não carregado *. PDB* arquivos de código de não usuário.
  
Três atributos de compilador também afetam o que o depurador .NET considera como código de usuário:  

- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute> informa o depurador que o código que é aplicado não é código do usuário.  
- <xref:System.Diagnostics.DebuggerHiddenAttribute> oculta o código do depurador, mesmo que Apenas Meu Código esteja desativado.  
- <xref:System.Diagnostics.DebuggerStepThroughAttribute> informa o depurador para percorrer o código que ele é aplicado, em vez de depurar o código.  

O depurador do .NET Framework considera todos os outros códigos para o código de usuário.  

Durante a depuração do .NET Framework:

- **Depurar** > **intervir** (ou **F11**) no código de não usuário percorre o código para a próxima linha do código do usuário. 
- **Depurar** > **depuração circular** (ou **Shift**+**F11**) no código de não usuário é executado para a próxima linha do código do usuário. 

Se não houver nenhum outro código de usuário, depuração continua até que ele termina, acessa outro ponto de interrupção ou gera um erro. 

<a name="BKMK_NET_Breakpoint_behavior"></a> Se o depurador for interrompido no código de não usuário (por exemplo, você usa **Debug** > **interromper tudo** e pausa no código de não usuário), o **sem código fonte** janela é exibida. Você pode usar um **Debug** > **etapa** comando para ir para a próxima linha de código do usuário.

Se ocorrer uma exceção sem tratamento no código de não usuário, o depurador interromperá na linha de código de usuário em que a exceção foi gerada.  
  
Se as exceções de primeira chance são habilitadas para a exceção, a linha de código de usuário chamada é realçada em verde no código-fonte. O **pilha de chamadas** janela exibe um quadro anotado rotulado **[código externo]**.  

##  <a name="BKMK_C___Just_My_Code"></a> Apenas Meu Código do C++  
  
No C++, permitindo que apenas meu código é o mesmo que usar o [/JMC (apenas meu código de depuração)](/cpp/build/reference/jmc) comutador de compilador.

<a name="BKMK_CPP_User_and_non_user_code"></a> Apenas meu código é diferente em C++ do que no .NET Framework e o JavaScript, porque você pode especificar arquivos de não usuário separadamente para o comportamento de depuração e o **pilha de chamadas** janela. 

Apenas meu código em C++ considera apenas estas funções como código não-usuário:

- Para o **pilha de chamadas** janela: 

  - Funções com informações de origem retiradas no respectivo arquivo de símbolos.  
  - Funções nas quais os arquivos de símbolos indicam que não há nenhum arquivo de origem que corresponde ao quadro de pilhas.  
  - Funções especificadas na  *\*. natjmc* arquivos de *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* pasta.  
  
- Para comportamento de depuração:
  
  - Funções especificadas na  *\*. natstepfilter* arquivos de *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* pasta.  
  
Você pode criar *. natstepfilter* e *. natjmc* arquivos para personalizar o comportamento de depuração apenas meu código e o **pilha de chamadas** janela. Ver [comportamento de depuração de C++ personalizar](#BKMK_CPP_Customize_stepping_behavior) e [comportamento de pilha de chamada de C++ personalizar](#BKMK_CPP_Customize_call_stack_behavior). 

<a name="BKMK_CPP_Stepping_behavior"></a> Durante a depuração de C++:

- **Depurar** > **intervir** (ou **F11**) no código de não usuário percorre o código para a próxima linha do código do usuário. 
- **Depurar** > **depuração circular** (ou **Shift**+**F11**) no código de não usuário é executado para a próxima linha do código do usuário. 

Se não houver nenhum outro código de usuário, depuração continua até que ele termina, acessa outro ponto de interrupção ou gera um erro. 

Se o depurador for interrompido no código de não usuário (por exemplo, você usa **Debug** > **interromper tudo** e pausa em código não-usuário), a depuração continua no código de não usuário.

Se o depurador atinge uma exceção, ele parará na exceção, se ele está no código do usuário ou de não usuário. **Sem tratamento do usuário** as opções de **configurações de exceção** caixa de diálogo são ignorados.  

###  <a name="BKMK_CPP_Customize_stepping_behavior"></a> Personalizar o comportamento de depuração de C++  

 Em projetos do C++, você pode especificar funções para percorrer listando-os como código de não usuário em  *\*. natstepfilter* arquivos.  
  
- Para especificar o código de não usuário para todos os usuários locais do Visual Studio, adicione a *. natstepfilter* do arquivo para o *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* pasta.  
- Para especificar código de não usuário para um usuário individual, adicione o arquivo *.natstepfilter* à pasta *%USERPROFILE%\Meus Documentos\Visual Studio 2017\Visualizers*.  
  
Um *. natstepfilter* arquivo é um arquivo XML com esta sintaxe:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<StepFilter xmlns="http://schemas.microsoft.com/vstudio/debugger/natstepfilter/2010">  
    <Function>  
        <Name>FunctionSpec</Name>  
        <Action>StepAction</Action>  
    </Function>  
    <Function>  
        <Name>FunctionSpec</Name>  
        <Module>ModuleSpec</Module>  
        <Action>StepAction</Action>  
    </Function>  
</StepFilter>  
  
```  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|`Function`|Necessário. Especifica uma ou mais funções como funções de não usuário.|  
|`Name`|Necessário. Uma expressão regular formatada como ECMA-262 que especifica o nome completo da função a ser correspondida. Por exemplo:<br /><br /> `<Name>MyNS::MyClass.*</Name>`<br /><br /> informa ao depurador que todos os métodos em `MyNS::MyClass` devem ser considerados como código de não usuário. A correspondência diferencia maiúsculas e minúsculas.|  
|`Module`|Opcional. Uma expressão regular formatada como ECMA-262 que especifica o caminho completo do módulo que contém a função. A correspondência não diferencia maiúsculas de minúsculas.|  
|`Action`|Necessário. Um destes valores que diferenciam maiúsculas e minúsculas:<br /><br /> `NoStepInto`  – informa o depurador para percorrer a função.<br /> `StepInto`  – informa o depurador para entrar em função, substituindo qualquer outro `NoStepInto` para a função correspondente.|  
  
###  <a name="BKMK_CPP_Customize_call_stack_behavior"></a> Personalizar o comportamento de pilha de chamada de C++  

Para projetos C++, você pode especificar os módulos, arquivos de origem e funções de **pilha de chamadas** janela trata como código de não usuário especificando-os na  *\*. natjmc* arquivos.  
  
-   Para especificar código de não usuário para todos os usuários do computador do Visual Studio, adicione o arquivo *.natjmc* à pasta *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*.  
-   Para especificar código de não usuário para um usuário individual, adicione o arquivo *.natjmc* à pasta *%USERPROFILE%\Meus Documentos\Visual Studio 2017\Visualizers*.  

Um *. natjmc* arquivo é um arquivo XML com esta sintaxe:  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<NonUserCode xmlns="http://schemas.microsoft.com/vstudio/debugger/jmc/2015">  
  
  <!-- Modules -->  
  <Module Name="ModuleSpec" />  
  <Module Name="ModuleSpec" Company="CompanyName" />  
  
  <!-- Files -->  
  <File Name="FileSpec"/>  
  
  <!-- Functions -->  
  <Function Name="FunctionSpec" />  
  <Function Name="FunctionSpec" Module ="ModuleSpec" />  
  <Function Name="FunctionSpec" Module ="ModuleSpec" ExceptionImplementation="true" />  
  
</NonUserCode>  
  
```  
  
 **Atributos do elemento de módulo**  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. O caminho completo do módulo ou dos módulos. Você pode usar os caracteres curinga do Windows `?` (zero ou um caractere) e `*` (zero ou mais caracteres). Por exemplo,<br /><br /> `<Module Name="?:\3rdParty\UtilLibs\*" />`<br /><br /> informa o depurador para tratar todos os módulos em *\3rdParty\UtilLibs* em qualquer unidade como código externo.|  
|`Company`|Opcional. O nome da empresa que publica o módulo inserido no arquivo executável. Você pode usar esse atributo para resolver a ambiguidade dos módulos.|  
  
 **Atributos do elemento de arquivo**  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. O caminho completo do arquivo ou arquivos de origem a serem tratados como código externo. Você pode usar os caracteres curinga do Windows `?` e `*` quando especificar o caminho.|  
  
 **Atributos do elemento de função**  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Name`|Necessário. O nome totalmente qualificado da função a ser tratada como código externo.|  
|`Module`|Opcional. O nome ou o caminho completo do módulo que contém a função. Você pode usar esse atributo para resolver a ambiguidade de funções com o mesmo nome.|  
|`ExceptionImplementation`|Quando definido como `true`, a pilha de chamadas exibe a função que lançou a exceção em vez dessa função.|  
  
##  <a name="BKMK_JavaScript_Just_My_Code"></a> Apenas Meu Código do JavaScript  

<a name="BKMK_JS_User_and_non_user_code"></a> O Apenas Meu Código do JavaScript controla a depuração e a exibição da pilha de chamadas categorizando o código em uma destas classificações:  

|||  
|-|-|  
|**MyCode**|Código do usuário que você possui e controla.|  
|**LibraryCode**|Código de não usuário de bibliotecas que você usa com regularidade e seu aplicativo depende para funcionar corretamente (por exemplo WinJS ou jQuery).|  
|**UnrelatedCode**|Código de não usuário em seu aplicativo que você não possui e seu aplicativo não depende para funcionar corretamente. Por exemplo, um anúncio do SDK que exibe anúncios poderia ser UnrelatedCode. Em projetos UWP, qualquer código que é carregado no seu aplicativo a partir de um URI HTTP ou HTTPS também é considerado UnrelatedCode.|  

O depurador do JavaScript classifica um código como o usuário ou usuário nesta ordem:  
  
1. As classificações padrão.  
   -   Script executado passando uma cadeia de caracteres para o host fornecidos pelo `eval` função é **MyCode**.  
   -   Script executado passando uma cadeia de caracteres para o `Function` construtor é **LibraryCode**.  
   -   O script em uma referência de framework, como WinJS ou o SDK do Azure, está **LibraryCode**.  
   -   Script executado passando uma cadeia de caracteres para o `setTimeout`, `setImmediate`, ou `setInterval` functions é **UnrelatedCode**.  
   
2. As classificações especificadas para todos os projetos de JavaScript do Visual Studio a *%VSInstallDirectory%\JavaScript\JustMyCode\mycode.default.wwa.json* arquivo.  
   
3. Classificações na *mycode.json* arquivo do projeto atual.  
  
Cada etapa de classificação substitui as etapas anteriores. 

Todos os demais códigos são classificados como **MyCode**.  

Você pode alterar as classificações padrão e classificar arquivos específicos e URLs como código de usuário ou de não usuário, adicionando um *. JSON* arquivo chamado *mycode.json* para a pasta raiz de um projeto de JavaScript. Ver [personalizar apenas meu código do JavaScript](#BKMK_JS_Customize_Just_My_Code). 

<a name="BKMK_JS_Stepping_behavior"></a> Durante a depuração de JavaScript: 

- Se uma função é o código de não usuário, **Debug** > **intervir** (ou **F11**) tem o mesmo comportamento **depurar**  >  **Step Over** (ou **F10**).  
- Se uma etapa começar em não-usuário (**LibraryCode** ou **UnrelatedCode**) código, depuração temporária se comportará como se apenas meu código não está habilitado. Quando você percorrer de volta até o código do usuário, apenas meu código passo a passo é habilitado novamente.  
- Quando um usuário código etapa resulta em deixar o contexto de execução atual, o depurador para na próxima linha de código de usuário executada. Por exemplo, se um retorno de chamada for executado em código **LibraryCode**, o depurador continuará até que a próxima linha de código de usuário seja executada.
- **Depuração circular** (ou **Shift**+**F11**) interrompe na próxima linha do código do usuário. 

Se não houver nenhum outro código de usuário, depuração continua até que ele termina, acessa outro ponto de interrupção ou gera um erro. 

Pontos de interrupção definidos no código sempre são atingidos, mas o código é classificado.  

- Se o `debugger` palavra-chave ocorre no **LibraryCode**, o depurador sempre interromperá.  
- Se o `debugger` palavra-chave ocorre no **UnrelatedCode**, o depurador não será interrompido.  
  
<a name="BKMK_JS_Exception_behavior"></a> Se ocorrer uma exceção sem tratamento no **MyCode** ou **LibraryCode** código, o depurador sempre interromperá.  

Se ocorrer uma exceção sem tratamento no **UnrelatedCode**, e **MyCode** ou **LibraryCode** está na pilha de chamadas, o depurador será interrompido.  
  
Se exceções de primeira chance são habilitadas para a exceção e a exceção ocorre no **LibraryCode** ou **UnrelatedCode**:  
  
-   Se a exceção for tratada, o depurador não será interrompido.  
-   Se a exceção não for tratada, o depurador será interrompido.  
  
###  <a name="BKMK_JS_Customize_Just_My_Code"></a> Personalizar apenas meu código do JavaScript  

Para categorizar o usuário e código de não usuário para um único projeto de JavaScript, você pode adicionar um *. JSON* arquivo chamado *mycode.json* para a pasta raiz do projeto.  
  
Especificações nesse arquivo substituem as classificações padrão e o *mycode.default.wwa.json* arquivo. O *mycode.json* arquivo não precisa listar todos os pares chave-valor. O **MyCode**, **bibliotecas**, e **Unrelated** valores podem ser matrizes vazias.  
  
*MyCode.JSON* arquivos usam a seguinte sintaxe:  
  
```json  
{  
    "Eval" : "Classification",  
    "Function" : "Classification",  
    "ScriptBlock" : "Classification",  
    "MyCode" : [  
        "UrlOrFileSpec",  
        . . .  
        "UrlOrFileSpec"  
    ],  
    "Libraries" : [  
        "UrlOrFileSpec",  
        . .  
        "UrlOrFileSpec"  
    ],  
    "Unrelated" : [  
        "UrlOrFileSpec",  
        . . .  
        "UrlOrFileSpec"  
    ]  
}  
  
```  
  
 **Eval, Function e ScriptBlock**  
  
 Os pares chave-valor **Eval**, **Function** e **ScriptBlock** determinam como o código gerado dinamicamente é classificado:  
  
|||  
|-|-|  
|**Eval**|Script que é executado passando uma cadeia de caracteres à função `eval` fornecida pelo host. Por padrão, o script Eval é classificado como **MyCode**.|  
|**Função**|Script que é executado passando uma cadeia de caracteres para o construtor `Function`. Por padrão, o script Function é classificado como **LibraryCode**.|  
|**ScriptBlock**|Script que é executado passando uma cadeia de caracteres para a função `setTimeout`, `setImmediate` ou `setInterval`. Por padrão, o script ScriptBlock é classificado como **UnrelatedCode**.|  
  
 Você pode alterar o valor para um destas palavras-chave:  
  
-   `MyCode` classifica o script como **MyCode**.  
-   `Library` classifica o script como **LibraryCode**.  
-   `Unrelated` classifica o script como **UnrelatedCode**.  
  
  **MyCode, Libraries e Unrelated**  
  
 Os pares chave-valor **MyCode**, **Libraries** e **Unrelated** especificam as URLs ou os arquivos que você deseja incluir em uma classificação:  
  
|||  
|-|-|  
|**MyCode**|Uma matriz de URLs ou arquivos classificados como **MyCode**.|  
|**Libraries**|Uma matriz de URLs ou arquivos classificados como **LibraryCode**.|  
|**Unrelated**|Uma matriz de URLs ou arquivos classificados como **UnrelatedCode**.|  
  
 A cadeia de caracteres de URL ou o arquivo pode ter um ou mais `*` caracteres, que correspondem a zero ou mais caracteres. `*` é o mesmo que a expressão regular `.*`.
