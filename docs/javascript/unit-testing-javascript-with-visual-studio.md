---
title: Teste de unidade no Node.js
description: O Visual Studio fornece suporte ao teste de unidade do código JavaScript usando as Ferramentas Node.js para Visual Studio
ms.custom: ''
ms.date: 06/06/2018
ms.technology: vs-nodejs
ms.topic: conceptual
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: douge
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 071f64c4239441d3c3fd2c111d1b912175e23316
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766549"
---
# <a name="unit-testing-in-nodejs"></a>Teste de unidade no Node.js

As Ferramentas Node.js para Visual Studio permitem que você escreva e execute testes de unidade usando algumas das estruturas mais populares do JavaScript, sem a necessidade de alternar para um prompt de comando.

As estruturas compatíveis são:
* Mocha ([mochajs.org](http://mochajs.org/))
* Jasmine ([Jasmine.github.io](https://jasmine.github.io/))
* Tape ([github.com/substack/tape](https://github.com/substack/tape))
* Executor de Exportação (essa estrutura é específica das Ferramentas Node.js para Visual Studio)

> [!WARNING]
> Atualmente, um problema no Tape impede a execução dos testes do Tape. Se o [PR #361](https://github.com/substack/tape/pull/361) for mesclado, o problema deverá ser resolvido.

Se não houver suporte para sua estrutura favorita, confira [Adicionar suporte para uma estrutura de teste de unidade](#addingFramework) para obter informações sobre como adicionar o suporte.

## <a name="write-unit-tests"></a>Escrever testes de unidade

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

Depois de abrir o Gerenciador de Testes (escolha **Teste** > **Windows** > **Gerenciador de Testes**), o Visual Studio detecta e exibe os testes. Se os testes não estiverem sendo mostrados inicialmente, recompile o projeto para atualizar a lista.

![Gerenciador de Testes](../javascript/media/UnitTestsDiscoveryMocha.png)

> [!NOTE]
> Não use a opção `outdir` ou `outfile` em *tsconfig.json*, porque o Gerenciador de Testes não conseguirá localizar os testes de unidade nos arquivos TypeScript.

## <a name="run-tests"></a>Executar testes

Execute testes no Visual Studio 2017 ou na linha de comando.

### <a name="run-tests-in-visual-studio-2017"></a>Executar testes no Visual Studio 2017

Execute os testes clicando no link **Executar Tudo** no Gerenciador de Testes. Ou se preferir, execute os testes selecionando um ou mais testes ou grupos, clicando com o botão direito do mouse e escolhendo **Executar Testes Selecionados** no menu de atalho. Os testes são executados em segundo plano e o Gerenciador de Testes atualiza e mostra os resultados automaticamente. Além disso, depure também testes selecionados selecionando **Depurar Testes Selecionados**.

> [!Warning]
> Atualmente, a depuração de testes de unidade usando o Node 8 e superior só funciona em arquivos de teste JavaScript. Os arquivos de teste TypeScript não conseguirão atingir os pontos de interrupção. Como alternativa, use a palavra-chave `debugger`.

> [!NOTE]
> No momento, não damos suporte à criação de perfil de testes nem à cobertura de código.

### <a name="run-tests-from-the-command-line"></a>Executar testes na linha de comando

Execute os testes no [Prompt de Comando do Desenvolvedor](/dotnet/framework/tools/developer-command-prompt-for-vs) do Visual Studio 2017 usando o seguinte comando:

```
vstest.console.exe <path to project file>\NodejsConsoleApp23.njsproj /TestAdapterPath:<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter
```

Esse comando mostra uma saída semelhante à seguinte:

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

## <a name="addingFramework"></a>Adicionar suporte para uma estrutura de teste de unidade

Adicione suporte para estruturas de teste adicionais implementando a lógica de descoberta e execução usando o JavaScript. Faça isso adicionando uma pasta com o nome da estrutura de teste em:

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks`

Essa pasta deve conter um arquivo JavaScript com o mesmo nome, que exporta as duas seguintes funções:

* `find_tests`
* `run_tests`

Para obter um bom exemplo das implementações `find_tests` e `run_tests`, confira a implementação da estrutura de teste de unidade Mocha em:

`<VisualStudioFolder>\Common7\IDE\Extensions\Microsoft\NodeJsTools\TestAdapter\TestFrameworks\mocha\mocha.js`

A descoberta das estruturas de teste disponíveis ocorre na inicialização do Visual Studio. Se uma estrutura for adicionada enquanto o Visual Studio estiver em execução, reinicie o Visual Studio para detectar a estrutura. No entanto, você não precisa reiniciar ao fazer alterações na implementação.

## <a name="unit-tests-in-other-project-types"></a>Testes de unidade em outros tipos de projeto
Você não está limitado a escrever testes de unidade apenas em seus projetos Node.js. Quando você adicionar as propriedades TestFramework e TestRoot a qualquer projeto de C# ou Visual Basic, esses testes serão enumerados e você poderá executá-los usando a janela do Gerenciador de Testes.

Para habilitar isso, clique com o botão direito do mouse no nó do projeto no Gerenciador de Soluções, escolha **Descarregar Projeto** e, em seguida, escolha **Editar Projeto**. Em seguida, no arquivo de projeto, adicione os dois elementos a seguir a um grupo de propriedades.

> [!NOTE]
> Certifique-se de que o grupo de propriedades a que você está adicionando os elementos não tenha uma condição especificada.
> Isso pode causar um comportamento inesperado.

```xml
<PropertyGroup>
    <JavaScriptTestRoot>tests\</JavaScriptTestRoot>
    <JavaScriptTestFramework>Tape</JavaScriptTestFramework>
</PropertyGroup>
```

Em seguida, adicione seus testes à pasta raiz de teste especificada por você e eles ficarão disponíveis para execução na janela do Gerenciador de Testes. Se eles não aparecerem inicialmente, você precisará recompilar o projeto.

> [!NOTE]
> Atualmente, isso não funciona para projetos do .NET Standard e do .NET Core.
