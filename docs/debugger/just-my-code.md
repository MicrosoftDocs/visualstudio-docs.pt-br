---
title: Depurar código de usuário com Apenas Meu Código | Microsoft Docs
ms.date: 02/13/2019
ms.topic: how-to
ms.assetid: 0f0df097-bbaf-46ad-9ad1-ef5f40435079
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 867477fd3e490f91e81fb91c8be267ede83c8d2c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536559"
---
# <a name="debug-only-user-code-with-just-my-code"></a>Depurar apenas o código de usuário com Apenas Meu Código

*Apenas meu código* é um recurso de depuração do Visual Studio que percorre automaticamente as chamadas para System, Framework e outros códigos que não são de usuário. Na janela **pilha de chamadas** , apenas meu código recolhe essas chamadas em quadros **[código externo]** .

Apenas Meu Código funciona de forma diferente em projetos .NET, C++ e JavaScript.

## <a name="enable-or-disable-just-my-code"></a><a name="BKMK_Enable_or_disable_Just_My_Code"></a> Habilitar ou desabilitar Apenas Meu Código

Para a maioria das linguagens de programação, Apenas Meu Código é habilitada por padrão.

- Para habilitar ou desabilitar apenas meu código no Visual Studio, em **ferramentas**  >  **Opções** (ou **Debug**  >  **Opções**de depuração) > **depuração**  >  **geral**, selecione ou desmarque **habilitar apenas meu código**.

![Habilitar Apenas Meu Código na caixa de diálogo opções](../debugger/media/dbg_justmycode_options.png "Habilitar Apenas Meu Código")

> [!NOTE]
> **Habilitar apenas meu código** é uma configuração global que se aplica a todos os projetos do Visual Studio em todos os idiomas.

## <a name="just-my-code-debugging"></a>depuração Apenas Meu Código

Durante uma sessão de depuração, a janela **módulos** mostra quais módulos de código o depurador está tratando como meu código (código do usuário), junto com o status de carregamento de seu símbolo. Para obter mais informações, consulte familiarize- [se com o modo como o depurador se anexa ao seu aplicativo](../debugger/debugger-tips-and-tricks.md#modules_window).

![Código do usuário na janela módulos](../debugger/media/dbg_justmycode_module.png "Código do usuário na janela módulos")

Na janela **pilha de chamadas** ou **tarefas** , apenas meu código recolhe o código que não é do usuário em um quadro de código anotado e esmaecido rotulado `[External Code]` .

![Quadro de código externo na janela pilha de chamadas](../debugger/media/dbg_justmycode_externalcode.png "Quadro de código externo")

>[!TIP]
>Para abrir os **módulos**, **pilha de chamadas**, **tarefas**ou a maioria das outras janelas de depuração, você deve estar em uma sessão de depuração. Durante a depuração, em **depurar**  >  **janelas**, selecione as janelas que você deseja abrir.

<a name="BKMK_Override_call_stack_filtering"></a>Para exibir o código em um quadro de **[código externo]** recolhido, clique com o botão direito do mouse na **pilha de chamadas** ou na janela de **tarefas** e selecione **Mostrar código externo** no menu de contexto. As linhas de código externo expandidas substituem o quadro **[código externo**].

![Mostrar código externo na janela pilha de chamadas](../debugger/media/dbg_justmycode_showexternalcode.png "Mostrar Código Externo")

> [!NOTE]
> **Mostrar código externo** é uma configuração do criador de perfil do usuário atual que se aplica a todos os projetos em todos os idiomas que são abertos pelo usuário.

Clicar duas vezes em uma linha de código externo expandida na janela **pilha de chamadas** realça a linha do código de chamada em verde no código-fonte. Para DLLs ou outros módulos não encontrados ou carregados, uma página de símbolo ou fonte não encontrada pode ser aberta.

## <a name="net-just-my-code"></a><a name="BKMK__NET_Framework_Just_My_Code"></a>Apenas Meu Código .NET

Em projetos do .NET, o Apenas Meu Código usa arquivos de símbolo (*. pdb*) e otimizações de programa para classificar o código de usuário e não usuário. O depurador .NET considera binários otimizados e arquivos *. pdb* não carregados como código de não-usuário.

Três atributos de compilador também afetam o que o depurador .NET considera como código de usuário:

- <xref:System.Diagnostics.DebuggerNonUserCodeAttribute>informa ao depurador que o código ao qual ele é aplicado não é o código do usuário.
- <xref:System.Diagnostics.DebuggerHiddenAttribute> oculta o código do depurador, mesmo que Apenas Meu Código esteja desativado.
- <xref:System.Diagnostics.DebuggerStepThroughAttribute>instrui o depurador a percorrer o código em que ele é aplicado, em vez de entrar no código.

O depurador .NET considera que todos os outros códigos sejam do código do usuário.

Durante a depuração do .NET:

- **Depurar**  >  **Intervir** (ou **F11**) em etapas de código não-usuário sobre o código para a próxima linha de código de usuário.
- **Depurar**  >  **Step Out** (ou **Shift** + **F11**) em código de não usuário é executado na próxima linha do código do usuário.

Se não houver mais código de usuário, a depuração continuará até que seja encerrada, atingirá outro ponto de interrupção ou lançará um erro.

<a name="BKMK_NET_Breakpoint_behavior"></a>Se o depurador interromper o código que não é de usuário (por exemplo, você usa **debug**  >  **Break All** e Pause em código que não seja de usuário), a janela **nenhuma fonte** será exibida. Você pode usar um comando de etapa de **depuração**  >  **Step** para ir para a próxima linha de código de usuário.

Se uma exceção sem tratamento ocorrer no código que não é do usuário, o depurador interromperá a linha de código do usuário em que a exceção foi gerada.

Se as exceções de primeira chance estiverem habilitadas para a exceção, a linha de código de usuário de chamada será realçada em verde no código-fonte. A janela **pilha de chamadas** exibe o quadro anotado rotulado **[código externo]**.

## <a name="c-just-my-code"></a><a name="BKMK_C___Just_My_Code"></a> Apenas Meu Código do C++

A partir do Visual Studio 2017 versão 15,8, também há suporte para Apenas Meu Código para a depuração de código. Esse recurso também requer o uso da opção de compilador [/JMC (apenas meu código de depuração)](/cpp/build/reference/jmc) . A opção é habilitada por padrão em projetos C++. Para o suporte de janela de **pilha de chamadas** e pilha de chamadas no apenas meu código, a opção/JMC não é necessária.

<a name="BKMK_CPP_User_and_non_user_code"></a>Para ser classificado como código de usuário, o PDB do binário que contém o código do usuário deve ser carregado pelo depurador (use a janela **módulos** para verificar isso).

Para o comportamento da pilha de chamadas, como na janela **pilha de chamadas** , apenas meu código em C++ considera que apenas essas funções *não são código de usuário*:

- Funções com informações de origem retiradas no respectivo arquivo de símbolos.
- Funções nas quais os arquivos de símbolos indicam que não há nenhum arquivo de origem que corresponde ao quadro de pilhas.
- Funções especificadas em arquivos * \* . natjmc* na pasta *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* .

Para o comportamento de depuração de código, Apenas Meu Código em C++ considera apenas que essas funções *não são código de usuário*:

- Funções para as quais o arquivo PDB correspondente não foi carregado no depurador.
- Funções especificadas em arquivos * \* . natjmc* na pasta *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* .

> [!NOTE]
> Para o suporte de Stepping de código na Apenas Meu Código, o código C++ deve ser compilado usando os compiladores MSVC no Visual Studio 15,8 Preview 3 ou posterior, e a opção de compilador/JMC deve ser habilitada (habilitada por padrão). Para obter detalhes adicionais, consulte [Personalizar a pilha de chamadas C++ e o comportamento de depuração de código](#BKMK_CPP_Customize_call_stack_behavior)) e esta [postagem de blog](https://devblogs.microsoft.com/cppblog/announcing-jmc-stepping-in-visual-studio/). Para o código compilado usando um compilador mais antigo, os arquivos *. natstepfilter* são a única maneira de personalizar a depuração de código, que é independente do apenas meu código. Consulte [Personalizar o comportamento de depuração do C++](#BKMK_CPP_Customize_stepping_behavior).

<a name="BKMK_CPP_Stepping_behavior"></a>Durante a depuração de C++:

- **Depurar**  >  **Intervir** (ou **F11**) em etapas de código não-usuário sobre o código para a próxima linha de código de usuário.
- **Depurar**  >  **Step Out** (ou **Shift** + **F11**) em código de não usuário é executado na próxima linha do código do usuário.

Se não houver mais código de usuário, a depuração continuará até que seja encerrada, atingirá outro ponto de interrupção ou lançará um erro.

Se o depurador interromper o código que não é de usuário (por exemplo, você usa **debug**  >  **Break All** e Pause em código que não seja de usuário), a depuração continua no código que não é do usuário.

Se o depurador atingir uma exceção, ele parará na exceção, seja em código de usuário ou não de usuário. As opções não **tratadas do usuário** na caixa de diálogo **configurações de exceção** são ignoradas.

### <a name="customize-c-call-stack-and-code-stepping-behavior"></a><a name="BKMK_CPP_Customize_call_stack_behavior"></a>Personalizar a pilha de chamadas C++ e o comportamento de depuração de código

Para projetos C++, você pode especificar os módulos, os arquivos de origem e as funções que a janela **pilha de chamadas** trata como código que não é de usuário, especificando-os nos arquivos * \* . natjmc* . Essa personalização também se aplicará à depuração de código se você estiver usando o compilador mais recente (consulte [C++ apenas meu código](#BKMK_CPP_User_and_non_user_code)).

- Para especificar código de não usuário para todos os usuários do computador do Visual Studio, adicione o arquivo *.natjmc* à pasta *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers*.
- Para especificar um código que não seja de usuário para um usuário individual, adicione o arquivo *. natjmc* aos *documentos do%USERPROFILE%\My<pasta do \\ Visual Studio versão \> \Visualizers* .

Um arquivo *. natjmc* é um arquivo XML com esta sintaxe:

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
|`Name`|Obrigatórios. O caminho completo do módulo ou dos módulos. Você pode usar os caracteres curinga do Windows `?` (zero ou um caractere) e `*` (zero ou mais caracteres). Por exemplo,<br /><br /> `<Module Name="?:\3rdParty\UtilLibs\*" />`<br /><br /> informa o depurador para tratar todos os módulos em *\3rdParty\UtilLibs* em qualquer unidade como código externo.|
|`Company`|Opcional. O nome da empresa que publica o módulo inserido no arquivo executável. Você pode usar esse atributo para resolver a ambiguidade dos módulos.|

 **Atributos do elemento de arquivo**

|Atributo|Descrição|
|---------------|-----------------|
|`Name`|Obrigatórios. O caminho completo do arquivo ou arquivos de origem a serem tratados como código externo. Você pode usar os caracteres curinga do Windows `?` e `*` quando especificar o caminho.|

 **Atributos do elemento de função**

|Atributo|Descrição|
|---------------|-----------------|
|`Name`|Obrigatórios. O nome totalmente qualificado da função a ser tratada como código externo.|
|`Module`|Opcional. O nome ou o caminho completo do módulo que contém a função. Você pode usar esse atributo para resolver a ambiguidade de funções com o mesmo nome.|
|`ExceptionImplementation`|Quando definido como `true` , a pilha de chamadas exibe a função que gerou a exceção em vez dessa função.|

### <a name="customize-c-stepping-behavior-independent-of-just-my-code-settings"></a><a name="BKMK_CPP_Customize_stepping_behavior"></a>Personalizar o comportamento de depuração do C++ independentemente das configurações de Apenas Meu Código

Em projetos do C++, você pode especificar funções para percorrer, listando-as como código que não é de usuário em arquivos * \* . natstepfilter* . As funções listadas nos arquivos * \* . natstepfilter* não são dependentes das configurações de apenas meu código.

- Para especificar código que não seja de usuário para todos os usuários locais do Visual Studio, adicione o arquivo *. natstepfilter* à pasta *%VsInstallDirectory%\Common7\Packages\Debugger\Visualizers* .
- Para especificar um código que não seja de usuário para um usuário individual, adicione o arquivo *. natstepfilter* aos *documentos do%USERPROFILE%\My<pasta do \\ Visual Studio versão \> \Visualizers* .

Um arquivo *. natstepfilter* é um arquivo XML com esta sintaxe:

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
|`Function`|Obrigatórios. Especifica uma ou mais funções como funções de não usuário.|
|`Name`|Obrigatórios. Uma expressão regular formatada como ECMA-262 que especifica o nome completo da função a ser correspondida. Por exemplo:<br /><br /> `<Name>MyNS::MyClass.*</Name>`<br /><br /> informa ao depurador que todos os métodos em `MyNS::MyClass` devem ser considerados como código de não usuário. A correspondência diferencia maiúsculas e minúsculas.|
|`Module`|Opcional. Uma expressão regular formatada como ECMA-262 que especifica o caminho completo do módulo que contém a função. A correspondência não diferencia maiúsculas de minúsculas.|
|`Action`|Obrigatórios. Um destes valores que diferenciam maiúsculas e minúsculas:<br /><br /> `NoStepInto`-informa o depurador para percorrer a função.<br /> `StepInto`– informa ao depurador para entrar na função, substituindo qualquer outra `NoStepInto` para a função correspondente.|

## <a name="javascript-just-my-code"></a><a name="BKMK_JavaScript_Just_My_Code"></a> Apenas Meu Código do JavaScript

<a name="BKMK_JS_User_and_non_user_code"></a>O JavaScript Apenas Meu Código controla a depuração e a exibição da pilha, categorizando o código em uma dessas classificações:

|classificação|Descrição|
|-|-|
|**MyCode**|Código do usuário que você possui e controla.|
|**LibraryCode**|Código não-usuário de bibliotecas que você usa regularmente e seu aplicativo depende para funcionar corretamente (por exemplo, WinJS ou jQuery).|
|**UnrelatedCode**|Código não-usuário em seu aplicativo que você não possui e seu aplicativo não depende para funcionar corretamente. Por exemplo, um SDK de anúncios que exibe anúncios pode ser UnrelatedCode. Em projetos UWP, qualquer código carregado em seu aplicativo a partir de um URI HTTP ou HTTPS também é considerado UnrelatedCode.|

O depurador do JavaScript classifica o código como usuário ou não-usuário nesta ordem:

1. As classificações padrão.
   - O script executado passando uma cadeia de caracteres para a função fornecida pelo host `eval` é **MyCode**.
   - O script executado passando uma cadeia de caracteres para o `Function` Construtor é **LibraryCode**.
   - O script em uma referência de estrutura, como WinJS ou SDK do Azure, é **LibraryCode**.
   - O script executado passando uma cadeia de caracteres para as `setTimeout` `setImmediate` funções, ou `setInterval` é **UnrelatedCode**.

2. Classificações especificadas para todos os projetos JavaScript do Visual Studio na *% VSInstallDirectory% \JavaScript\JustMyCode\mycode.default.wwa.jsno* arquivo.

3. As classificações na *mycode.jsno* arquivo do projeto atual.

Cada etapa de classificação substitui as etapas anteriores.

Todos os demais códigos são classificados como **MyCode**.

Você pode modificar as classificações padrão e classificar arquivos e URLs específicos como usuário ou código de não usuário, adicionando um arquivo *. JSON* chamado *mycode.jsna* pasta raiz de um projeto JavaScript. Consulte [personalizar apenas meu código de JavaScript](#BKMK_JS_Customize_Just_My_Code).

<a name="BKMK_JS_Stepping_behavior"></a>Durante a depuração de JavaScript:

- Se uma função for um código que não seja de usuário, **depurar**  >  **etapa em** (ou **F11**) se comportará da mesma forma que a **depuração**  >  **Step Over** (ou **F10**).
- Se uma etapa começar no código que não é de usuário (**LibraryCode** ou **UnrelatedCode**), a depuração se comporta temporariamente como se apenas meu código não estiver habilitada. Quando você voltar ao código do usuário, Apenas Meu Código a depuração será reabilitada.
- Quando uma etapa de código de usuário resulta na saída do contexto de execução atual, o depurador para a próxima linha de código de usuário executada. Por exemplo, se um retorno de chamada for executado em código **LibraryCode**, o depurador continuará até que a próxima linha de código de usuário seja executada.
- **Step Out** (ou **Shift** + **F11**) para a próxima linha do código do usuário.

Se não houver mais código de usuário, a depuração continuará até que seja encerrada, atingirá outro ponto de interrupção ou lançará um erro.

Os pontos de interrupção definidos no código sempre são atingidos, mas o código é classificado.

- Se a `debugger` palavra-chave ocorrer em **LibraryCode**, o depurador sempre interromperá.
- Se a `debugger` palavra-chave ocorrer em **UnrelatedCode**, o depurador não é interrompido.

<a name="BKMK_JS_Exception_behavior"></a>Se uma exceção sem tratamento ocorrer no código **MyCode** ou **LibraryCode** , o depurador sempre interromperá.

Se uma exceção sem tratamento ocorrer em **UnrelatedCode**e **MyCode** ou **LibraryCode** estiver na pilha de chamadas, o depurador será interrompido.

Se as exceções de primeira chance estiverem habilitadas para a exceção, e a exceção ocorrer em **LibraryCode** ou **UnrelatedCode**:

- Se a exceção for tratada, o depurador não será interrompido.
- Se a exceção não for tratada, o depurador será interrompido.

### <a name="customize-javascript-just-my-code"></a><a name="BKMK_JS_Customize_Just_My_Code"></a>Personalizar Apenas Meu Código JavaScript

Para categorizar o usuário e o código de não usuário para um único projeto JavaScript, você pode adicionar um arquivo *. JSON* chamado *mycode.jsna* pasta raiz do projeto.

As especificações nesse arquivo substituem as classificações padrão e a *mycode.default.wwa.jsno* arquivo. O *mycode.jsno* arquivo não precisa listar todos os pares chave-valor. O **MyCode**, as **bibliotecas**e os valores não **relacionados** podem ser matrizes vazias.

*Mycode.jsem* arquivos, use esta sintaxe:

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

|Nome|Descrição|
|-|-|
|**Eval**|Script que é executado passando uma cadeia de caracteres à função `eval` fornecida pelo host. Por padrão, o script Eval é classificado como **MyCode**.|
|**Função**|Script que é executado passando uma cadeia de caracteres para o construtor `Function`. Por padrão, o script Function é classificado como **LibraryCode**.|
|**Bloco de script**|Script que é executado passando uma cadeia de caracteres para a função `setTimeout`, `setImmediate` ou `setInterval`. Por padrão, o script ScriptBlock é classificado como **UnrelatedCode**.|

Você pode alterar o valor para um destas palavras-chave:

- `MyCode` classifica o script como **MyCode**.
- `Library` classifica o script como **LibraryCode**.
- `Unrelated` classifica o script como **UnrelatedCode**.

**MyCode, Libraries e Unrelated**

Os pares chave-valor **MyCode**, **Libraries** e **Unrelated** especificam as URLs ou os arquivos que você deseja incluir em uma classificação:

|Nome|Descrição|
|-|-|
|**MyCode**|Uma matriz de URLs ou arquivos classificados como **MyCode**.|
|**Bibliotecas**|Uma matriz de URLs ou arquivos classificados como **LibraryCode**.|
|**Unrelated**|Uma matriz de URLs ou arquivos classificados como **UnrelatedCode**.|

A cadeia de caracteres da URL ou do arquivo pode ter um ou mais `*` caracteres, que correspondem a zero ou mais caracteres. `*`é o mesmo que a expressão regular `.*` .
