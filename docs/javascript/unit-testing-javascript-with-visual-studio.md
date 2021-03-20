---
title: Teste de unidade em JavaScript e TypeScript
description: O Visual Studio fornece suporte ao teste de unidade do código JavaScript e TypeScript usando as Ferramentas Node.js para Visual Studio
ms.date: 03/18/2021
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: dc44e39223fd252ae8c4130a1b358aa6af981119
ms.sourcegitcommit: 3fc099cdc484344c781f597581f299729c6bfb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2021
ms.locfileid: "104671489"
---
# <a name="unit-testing-javascript-and-typescript-in-visual-studio"></a>Teste de unidade em JavaScript e TypeScript no Visual Studio

Você pode escrever e executar testes de unidade no Visual Studio usando algumas das estruturas JavaScript mais populares sem a necessidade de alternar para um prompt de comando. Há suporte para projetos Node.js e ASP.NET Core.

As estruturas compatíveis são:
* Mocha ([mochajs.org](https://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Jest ([jestjs.io](https://jestjs.io/))
* Executor de Exportação (essa estrutura é específica das Ferramentas Node.js para Visual Studio)

Para ASP.NET Core e JavaScript ou TypeScript, consulte [gravar testes de unidade para ASP.NET Core ](#write-unit-tests-for-aspnet-core).

Se não houver suporte para sua estrutura favorita, confira [Adicionar suporte para uma estrutura de teste de unidade](#addingFramework) para obter informações sobre como adicionar o suporte.

## <a name="write-unit-tests-in-a-nodejs-project"></a>Gravar testes de unidade em um projeto Node.js

Antes de adicionar testes de unidade ao projeto, verifique se a estrutura que você pretende usar está instalada localmente no projeto. É fácil fazer isso usando a [janela de instalação de pacotes npm](npm-package-management.md#npmInstallWindow).

A maneira preferencial de adicionar testes de unidade ao projeto é criar uma pasta *tests* no projeto e configurá-la como a raiz de teste nas propriedades do projeto. Você também precisa selecionar a estrutura de teste que deseja usar.

![Definir a raiz de teste e a estrutura de teste](../javascript/media/unit-test-project-properties.png)

Adicione testes simples em branco ao projeto usando a caixa de diálogo **Adicionar Novo Item**. Há suporte para JavaScript e TypeScript no mesmo projeto.

![Adicionar novo teste de unidade](../javascript/media/unit-test-add-new-item.png)

Para um teste de unidade Mocha, use o seguinte código:

```javascript
var assert = require('assert');

describe('Test Suite 1', function() {
    it('Test 1', function() {
        assert.ok(true, "This shouldn't fail");
    })

    it('Test 2', function() {
        assert.ok(1 === 1, "This shouldn't fail");
        assert.ok(false, "This should fail");
    })
})
```

Se você não definiu as opções de teste de unidade nas propriedades do projeto, garanta que a propriedade **Estrutura de Teste** na janela **Propriedades** esteja definida com a estrutura de teste correta para os arquivos de teste de unidade. Isso é feito automaticamente pelos modelos de arquivo de teste de unidade.

![Estrutura de teste](../javascript/media/UnitTestsFrameworkMocha.png)

> [!Note]
> As opções de teste de unidade terão preferência em relação às configurações de arquivos individuais.

Depois de abrir o Gerenciador de testes (escolha **testar** o  >  **Windows**  >  **Test Explorer**), o Visual Studio descobre e exibe os testes. Se os testes não estiverem sendo mostrados inicialmente, recompile o projeto para atualizar a lista.

![Gerenciador de Testes](../javascript/media/UnitTestsDiscoveryMocha.png)

> [!NOTE]
> Para o TypeScript, não use a `outdir` `outfile` opção ou no *tsconfig.jsno*, porque o Gerenciador de testes não poderá localizar os testes de unidade.

## <a name="run-tests-nodejs"></a>Executar testes (Node.js)

Você pode executar testes no Visual Studio ou na linha de comando.

### <a name="run-tests-in-visual-studio"></a>Executar testes no Visual Studio

::: moniker range=">=vs-2019"
Execute os testes clicando no link **Executar Tudo** no Gerenciador de Testes. Ou, você pode executar testes selecionando um ou mais testes ou grupos, clicando com o botão direito do mouse e selecionando **executar** no menu de atalho. Os testes são executados em segundo plano e o Gerenciador de Testes atualiza e mostra os resultados automaticamente. Além disso, você também pode depurar os testes selecionados clicando com o botão direito do mouse e selecionando **depurar**.
::: moniker-end
::: moniker range="vs-2017"
Execute os testes clicando no link **Executar Tudo** no Gerenciador de Testes. Ou se preferir, execute os testes selecionando um ou mais testes ou grupos, clicando com o botão direito do mouse e escolhendo **Executar Testes Selecionados** no menu de atalho. Os testes são executados em segundo plano e o Gerenciador de Testes atualiza e mostra os resultados automaticamente. Além disso, depure também testes selecionados selecionando **Depurar Testes Selecionados**.
::: moniker-end

Para o TypeScript, os testes de unidade são executados no código JavaScript gerado.

> [!NOTE]
> Na maioria dos cenários do TypeScript, você pode depurar um teste de unidade definindo um ponto de interrupção no código do TypeScript, clicando com o botão direito do mouse em um teste no Gerenciador de testes e escolhendo **depurar**. Em cenários mais complexos, como alguns cenários que usam mapas de origem, você pode ter dificuldade ao atingir pontos de interrupção no código do TypeScript. Como alternativa, tente usar a `debugger` palavra-chave.

> [!NOTE]
> No momento, não damos suporte à criação de perfil de testes nem à cobertura de código.

### <a name="run-tests-from-the-command-line"></a>Executar testes na linha de comando

Você pode executar os testes de [prompt de comando do desenvolvedor para Visual Studio](../ide/reference/command-prompt-powershell.md) usando o seguinte comando:

```
vstest.console.exe <path to project file>\NodejsConsoleApp23.njsproj /TestAdapterPath:<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter
```

Esse comando exibe uma saída semelhante à seguinte:

```
Microsoft (R) Test Execution Command Line Tool Version 15.5.0
Copyright (c) Microsoft Corporation.  All rights reserved.

Starting test execution, please wait...
Processing: NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 1::mocha
  Creating TestCase:NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js::Test Suite 1 Test 2::mocha
Processing finished for framework of Mocha
Passed   Test Suite 1 Test 1
Standard Output Messages:
 Using default Mocha settings
 1..2
 ok 1 Test Suite 1 Test 1

Failed   Test Suite 1 Test 2
Standard Output Messages:
 not ok 1 Test Suite 1 Test 2
   AssertionError [ERR_ASSERTION]: This should fail
       at Context.<anonymous> (NodejsConsoleApp23\NodejsConsoleApp23\UnitTest1.js:10:16)

Total tests: 2. Passed: 1. Failed: 1. Skipped: 0.
Test Run Failed.
Test execution time: 1.5731 Seconds
```

> [!NOTE]
> Se você receber um erro indicando que o *vstest.console.exe* não pode ser encontrado, verifique se você abriu o Prompt de Comando do Desenvolvedor e não um prompt de comando comum.

## <a name="write-unit-tests-for-aspnet-core"></a>Gravar testes de unidade para ASP.NET Core

1. Crie um projeto ASP.NET Core e adicione suporte a TypeScript.

   Para obter um exemplo de projeto, consulte [criar um aplicativo ASP.NET Core com TypeScript](../javascript/tutorial-aspnet-with-typescript.md). Para o suporte a testes de unidade, recomendamos que você comece com um modelo de projeto ASP.NET Core padrão.

   Use o pacote NuGet para adicionar suporte a TypeScript em vez do pacote TypeScript NPM.

1. Instale o pacote NuGet [Microsoft. JavaScript. UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/)

1. Em Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e escolha **descarregar projeto**.

   O arquivo *. csproj* deve ser aberto no Visual Studio.

1. Adicione os seguintes elementos ao arquivo *. csproj* no `PropertyGroup` elemento.

   Este exemplo especifica Mocha como a estrutura de teste. Você pode especificar Jest, tape ou Jasmine em vez disso.

   ```xml
   <PropertyGroup>
      ...
      <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
      <JavaScriptTestFramework>Mocha</JavaScriptTestFramework>
      <GenerateProgramFile>false</GenerateProgramFile>
   </PropertyGroup>
   ```

   O `JavaScriptTestRoot` elemento Especifica que os testes de unidade estarão na pasta *tests* da raiz do projeto.

1. Em Gerenciador de Soluções, clique com o botão direito do mouse no nó do projeto e escolha **recarregar projeto**.

1. Adicione o suporte do NPM conforme descrito no artigo gerenciamento de pacotes do NPM em [ASP.NET Core projetos](../javascript/npm-package-management.md#aspnet-core-projects).

   Isso requer a instalação do Node.js Runtime para suporte NPM e a adição de *package.js* na raiz do projeto.

1. Em *package.jsem*, adicione o pacote NPM que você deseja em dependências.

   Por exemplo, para Mocha, você pode usar o seguinte:

   ```json
   "dependencies": {
     "mocha": "8.3.0",
   ```

   Algumas estruturas de teste de unidade, como jest, exigem pacotes NPM adicionais. Para Jest, use o JSON a seguir:

   ```json
   "dependencies": {
     "jest": "26.6.3",
     "jest-editor-support": "28.1.0"
   ```

   >[!NOTE]
   > Em alguns cenários, Gerenciador de Soluções pode não mostrar o nó NPM devido a um problema conhecido descrito [aqui](https://github.com/aspnet/Tooling/issues/479). Se você precisar ver o nó NPM, você pode descarregar o projeto (clique com o botão direito do mouse no projeto e escolher **descarregar projeto**) e recarregar o projeto para fazer com que o nó NPM seja exibido novamente.

1. Adicione o código para testar.

   Se você estiver usando o exemplo descrito em [criar um aplicativo ASP.NET Core com TypeScript](tutorial-aspnet-with-typescript.md), adicione o código a seguir ao final do arquivo *library. TS* , que está na pasta *scripts* .

   ```typescript
   function getData(value) {
      if (value > 1) {
         return true;
      }
   }
    
   module.exports = getData;
   ```

   Para o TypeScript, os testes de unidade são executados no código JavaScript gerado.

1. Adicione os testes de unidade à pasta *tests* na raiz do projeto.

   Por exemplo, você pode usar o código a seguir selecionando a guia de documentação correta que corresponde à estrutura de teste, neste exemplo, Mocha ou jest. Esse código testa uma função chamada `getData` .

   # <a name="mocha"></a>[Mocha](#tab/mocha)

   ```typescript
   const getData = require('../wwwroot/js/library.js');
   var assert = require('assert');
    
   describe('Test Suite 1', function () {
      it('getData', function () {
         assert.ok(true, getData(2));
      })
   })
   ```

   # <a name="jest"></a>[Jest](#tab/jest)

   ```typescript
   const getData = require('../wwwroot/js/library.js');
    
   test('should return true', () => {
      expect(getData(2)).toBe(true);
   });
   ```

1. Abra o Gerenciador de testes (escolha **testar** o  >  **Windows**  >  **Test Explorer**) e o Visual Studio descobre e exibe testes. Se os testes não estiverem sendo mostrados inicialmente, recompile o projeto para atualizar a lista.

   ![Descoberta de teste do Test Explorer](../javascript/media/unit-tests-aspnet-core-discovery.png)

   > [!NOTE]
   > Para o TypeScript, não use a `outfile` opção no *tsconfig.jsno*, porque o Gerenciador de testes não poderá localizar os testes de unidade. Você pode usar a `outdir` opção, mas certifique-se de que arquivos de configuração, como `package.json` e `tsconfig.json` estão na raiz do projeto.

## <a name="run-tests-aspnet-core"></a>Executar testes (ASP.NET Core)

::: moniker range=">=vs-2019"
Execute os testes clicando no link **Executar Tudo** no Gerenciador de Testes. Ou, você pode executar testes selecionando um ou mais testes ou grupos, clicando com o botão direito do mouse e selecionando **executar** no menu de atalho. Os testes são executados em segundo plano e o Gerenciador de Testes atualiza e mostra os resultados automaticamente. Além disso, você também pode depurar os testes selecionados clicando com o botão direito do mouse e selecionando **depurar**.
::: moniker-end
::: moniker range="vs-2017"
Execute os testes clicando no link **Executar Tudo** no Gerenciador de Testes. Ou se preferir, execute os testes selecionando um ou mais testes ou grupos, clicando com o botão direito do mouse e escolhendo **Executar Testes Selecionados** no menu de atalho. Os testes são executados em segundo plano e o Gerenciador de Testes atualiza e mostra os resultados automaticamente. Além disso, depure também testes selecionados selecionando **Depurar Testes Selecionados**.
::: moniker-end

Para o TypeScript, os testes de unidade são executados no código JavaScript gerado.

![Resultados do Gerenciador de testes](../javascript/media/unit-tests-aspnet-core-run.png)

> [!NOTE]
> Na maioria dos cenários do TypeScript, você pode depurar um teste de unidade definindo um ponto de interrupção no código do TypeScript, clicando com o botão direito do mouse em um teste no Gerenciador de testes e escolhendo **depurar**. Em cenários mais complexos, como alguns cenários que usam mapas de origem, você pode ter dificuldade ao atingir pontos de interrupção no código do TypeScript. Como alternativa, tente usar a `debugger` palavra-chave.

> [!NOTE]
> No momento, não damos suporte à criação de perfil de testes nem à cobertura de código.

## <a name="add-support-for-a-unit-test-framework"></a><a name="addingFramework"></a>Adicionar suporte para uma estrutura de teste de unidade

Adicione suporte para estruturas de teste adicionais implementando a lógica de descoberta e execução usando o JavaScript. Faça isso adicionando uma pasta com o nome da estrutura de teste em:

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks`

Essa pasta deve conter um arquivo JavaScript com o mesmo nome, que exporta as duas seguintes funções:

* `find_tests`
* `run_tests`

Para obter um bom exemplo das implementações `find_tests` e `run_tests`, confira a implementação da estrutura de teste de unidade Mocha em:

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks\mocha\mocha.js`

A descoberta das estruturas de teste disponíveis ocorre na inicialização do Visual Studio. Se uma estrutura for adicionada enquanto o Visual Studio estiver em execução, reinicie o Visual Studio para detectar a estrutura. No entanto, você não precisa reiniciar ao fazer alterações na implementação.

## <a name="unit-tests-in-net-framework"></a>Testes de unidade no .NET Framework

Você não está limitado a escrever testes de unidade apenas em seus projetos Node.js e ASP.NET Core. Quando você adicionar as propriedades TestFramework e TestRoot a qualquer projeto de C# ou Visual Basic, esses testes serão enumerados e você poderá executá-los usando a janela do Gerenciador de Testes.

Para habilitar isso, clique com o botão direito do mouse no nó do projeto no Gerenciador de Soluções, escolha **Descarregar Projeto** e, em seguida, escolha **Editar Projeto**. Em seguida, no arquivo de projeto, adicione os dois elementos a seguir a um grupo de propriedades.

> [!IMPORTANT]
> Certifique-se de que o grupo de propriedades a que você está adicionando os elementos não tenha uma condição especificada.
> Isso pode causar um comportamento inesperado.

```xml
<PropertyGroup>
    <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
    <JavaScriptTestFramework>Tape</JavaScriptTestFramework>
</PropertyGroup>
```

Em seguida, adicione seus testes à pasta raiz de teste especificada por você e eles ficarão disponíveis para execução na janela do Gerenciador de Testes. Se eles não aparecerem inicialmente, você precisará recompilar o projeto.

## <a name="unit-test-net-core-and-net-standard"></a>Teste de unidade no .NET Core e no .NET Standard

Além das propriedades anteriores, você também precisa instalar o pacote NuGet [Microsoft. JavaScript. UnitTest](https://www.nuget.org/packages/Microsoft.JavaScript.UnitTest/) e definir a propriedade:

```xml
<PropertyGroup>
    <GenerateProgramFile>false</GenerateProgramFile>
</PropertyGroup>
```

Algumas estruturas de teste podem exigir pacotes NPM adicionais para detecção de teste. Por exemplo, Jest requer o pacote Jest-editor-support NPM. Se necessário, verifique a documentação da estrutura específica.
