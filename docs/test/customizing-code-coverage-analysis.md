---
title: Personalizando análise de cobertura de código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 09af57ca64524dafa506d57d486e9385a4c35a93
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53054928"
---
# <a name="customize-code-coverage-analysis"></a>Personalizar a análise de cobertura de código

Por padrão, a cobertura de código analisa todos os assemblies de solução que são carregados durante os testes de unidade. Recomendamos que esse comportamento padrão seja mantido, pois geralmente ele funciona bem. Para obter mais informações, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

Para excluir o código de teste dos resultados da cobertura de código e incluir apenas o código do aplicativo, adicione o atributo <xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute> à classe de teste.

Para incluir os assemblies que não fazem parte da solução, obtenha os arquivos *.pdb* desses assemblies e copia-os na mesma pasta que os arquivos *.dll* do assembly.

## <a name="run-settings-file"></a>Arquivo de configurações de execução

O [arquivo de configurações de execução](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md) é o arquivo de configuração usado pelas ferramentas de teste da unidade. As configurações avançadas da cobertura de código são especificadas em um arquivo *.runsettings*.

Para personalizar a cobertura de código, siga estas etapas:

1. Adicione um arquivo de configurações de execução à sua solução. Na **Gerenciador de Soluções**, no menu de atalho da solução, escolha **Adicionar** > **Novo Item** e selecione **arquivo XML**. Salve o arquivo com um nome como *CodeCoverage.runsettings*.

1. Adicione o conteúdo do arquivo de exemplo no final deste artigo e personalize-o de acordo com suas necessidades, conforme descrito nas seções a seguir.

1. Para selecionar o arquivo de configurações de execução, no menu **Testar**, escolha **Testar Configurações** > **Selecionar Arquivo de Configurações do Teste**. Para especificar um arquivo de configurações de execução para executar testes usando a linha de comando ou em um fluxo de trabalho de build, confira [Configurar testes de unidade usando um arquivo *.runsettings*](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md#specify-a-run-settings-file).

   Quando você seleciona **Analisar Cobertura de Código**, as informações de configuração são lidas no arquivo de configurações de execução.

   > [!TIP]
   > Os resultados da cobertura de código e a coloração de código anteriores não são ocultados automaticamente quando você executa testes ou atualiza o código.

Para ativar ou desativar as configurações personalizadas, desmarque ou selecione o arquivo no menu **Teste** > **Configurações de Teste**.

![Menu de configurações de teste com o arquivo de configurações personalizadas](../test/media/codecoverage-settingsfile.png)

### <a name="specify-symbol-search-paths"></a>Especificar caminhos de pesquisa de símbolo

A cobertura de código exige arquivos de símbolo (arquivos *.pdb*) para assemblies. Para assemblies compilados por sua solução, os arquivos de símbolos estão geralmente presentes nos arquivos binários e a cobertura de código funciona automaticamente. Mas, em alguns casos, você pode incluir os assemblies referenciados na análise de cobertura de código. Nesses casos, os arquivos *.pdb* podem não estar adjacentes aos binários, mas você pode especificar o caminho de pesquisa de símbolos no arquivo *.runsettings*.

```xml
<SymbolSearchPaths>
      <Path>\\mybuildshare\builds\ProjectX</Path>
      <!--More paths if required-->
</SymbolSearchPaths>
```

> [!NOTE]
> A resolução de símbolos pode ser demorada, especialmente ao usar um local de arquivo remoto com muitos assemblies. Portanto, considere copiar os arquivos *.pdb* no mesmo local que os arquivos binários (*.dll* e *.exe*).

### <a name="exclude-and-include"></a>Excluir e incluir

Você pode excluir os assemblies especificados da análise de cobertura de código. Por exemplo:

```xml
<ModulePaths>
  <Exclude>
   <ModulePath>Fabrikam.Math.UnitTest.dll</ModulePath>
   <!-- Add more ModulePath nodes here. -->
  </Exclude>
</ModulePaths>
```

Como alternativa, você pode especificar que assemblies devem ser incluídos. Esta abordagem tem a desvantagem de que, ao adicionar mais assemblies à solução, você tem que se lembrar de adicioná-los à lista:

```xml
<ModulePaths>
  <Include>
   <ModulePath>Fabrikam.Math.dll</ModulePath>
   <!-- Add more ModulePath nodes here. -->
  </Include>
</ModulePaths>
```

Se **Incluir** estiver vazio, o processamento de cobertura de código incluirá todos os assemblies que são carregados e para os quais os arquivos *.pdb* podem ser encontrados. A cobertura de código não inclui itens que correspondem a uma cláusula em uma lista **Excluir**.

**Incluir** é processado antes de **Excluir**.

### <a name="regular-expressions"></a>Expressões regulares

Os nós de inclusão e exclusão usam expressões regulares. Para obter mais informações, confira [Usar expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md). As expressões regulares não são o mesmo que curingas. Em particular:

- **.\\*** corresponde a uma cadeia de quaisquer caracteres

- **\\.** corresponde a um ponto ".")

- **\\(   \\)** corresponde a parênteses "(  )"

- **\\\\** corresponde a um delimitador de caminho de arquivo "\\"

- **^** corresponde ao início da cadeia de caracteres

- **$** corresponde ao final da cadeia de caracteres

Todas as correspondências não diferenciam maiúsculas de minúsculas.

Por exemplo:

```xml
<ModulePaths>
  <Include>
    <!-- Include all loaded .dll assemblies (but not .exe assemblies): -->
    <ModulePath>.*\.dll$</ModulePath>
  </Include>
  <Exclude>
    <!-- But exclude some assemblies: -->
    <ModulePath>.*\\Fabrikam\.MyTests1\.dll$</ModulePath>
    <!-- Exclude all file paths that contain "Temp": -->
    <ModulePath>.*Temp.*</ModulePath>
  </Exclude>
</ModulePaths>
```

> [!WARNING]
> Se houver um erro em uma expressão regular, como um parêntese sem correspondência ou sem escape, a análise de cobertura de código não será executada.

### <a name="other-ways-to-include-or-exclude-elements"></a>Outras maneiras de incluir ou excluir elementos

- **ModulePath** – corresponde aos assemblies especificados pelo caminho de arquivo do assembly.

- **CompanyName** – corresponde aos assemblies pelo atributo **Company**.

- **PublicKeyToken**– correspondências aos assemblies assinados pelo token de chave pública.

- **Source** – corresponde aos elementos pelo nome do caminho do arquivo de origem no qual eles são definidos.

- **Attribute** – corresponde aos elementos aos quais um atributo específico está anexado. Especifique o nome completo do atributo e inclua "Attribute" no final do nome.

- **Function** – corresponde a procedimentos, funções ou métodos pelo nome totalmente qualificado. Para corresponder a um nome de função, a expressão regular precisa corresponder ao nome totalmente qualificado da função, incluindo o namespace, o nome de classe, o nome do método e a lista de parâmetros. Por exemplo:

   ```csharp
   Fabrikam.Math.LocalMath.SquareRoot(double);
   ```

   ```cpp
   Fabrikam::Math::LocalMath::SquareRoot(double)
   ```

   ```xml
   <Functions>
     <Include>
       <!-- Include methods in the Fabrikam namespace: -->
       <Function>^Fabrikam\..*</Function>
       <!-- Include all methods named EqualTo: -->
       <Function>.*\.EqualTo\(.*</Function>
     </Include>
     <Exclude>
       <!-- Exclude methods in a class or namespace named UnitTest: -->
       <Function>.*\.UnitTest\..*</Function>
     </Exclude>
   </Functions>
   ```

## <a name="sample-runsettings-file"></a>Arquivo .runsettings de exemplo

Copie esse código e edite-o para atender às suas necessidades.

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- File name extension must be .runsettings -->
<RunSettings>
  <DataCollectionRunSettings>
    <DataCollectors>
      <DataCollector friendlyName="Code Coverage" uri="datacollector://Microsoft/CodeCoverage/2.0" assemblyQualifiedName="Microsoft.VisualStudio.Coverage.DynamicCoverageDataCollector, Microsoft.VisualStudio.TraceCollector, Version=11.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a">
        <Configuration>
          <CodeCoverage>
<!--
Additional paths to search for .pdb (symbol) files. Symbols must be found for modules to be instrumented.
If .pdb files are in the same folder as the .dll or .exe files, they are automatically found. Otherwise, specify them here.
Note that searching for symbols increases code coverage runtime. So keep this small and local.
-->
<!--
            <SymbolSearchPaths>
                   <Path>C:\Users\User\Documents\Visual Studio 2012\Projects\ProjectX\bin\Debug</Path>
                   <Path>\\mybuildshare\builds\ProjectX</Path>
            </SymbolSearchPaths>
-->

<!--
About include/exclude lists:
Empty "Include" clauses imply all; empty "Exclude" clauses imply none.
Each element in the list is a regular expression (ECMAScript syntax). See https://docs.microsoft.com/visualstudio/ide/using-regular-expressions-in-visual-studio.
An item must first match at least one entry in the include list to be included.
Included items must then not match any entries in the exclude list to remain included.
-->

            <!-- Match assembly file paths: -->
            <ModulePaths>
              <Include>
                <ModulePath>.*\.dll$</ModulePath>
                <ModulePath>.*\.exe$</ModulePath>
              </Include>
              <Exclude>
                <ModulePath>.*CPPUnitTestFramework.*</ModulePath>
              </Exclude>
            </ModulePaths>

            <!-- Match fully qualified names of functions: -->
            <!-- (Use "\." to delimit namespaces in C# or Visual Basic, "::" in C++.)  -->
            <Functions>
              <Exclude>
                <Function>^Fabrikam\.UnitTest\..*</Function>
                <Function>^std::.*</Function>
                <Function>^ATL::.*</Function>
                <Function>.*::__GetTestMethodInfo.*</Function>
                <Function>^Microsoft::VisualStudio::CppCodeCoverageFramework::.*</Function>
                <Function>^Microsoft::VisualStudio::CppUnitTestFramework::.*</Function>
              </Exclude>
            </Functions>

            <!-- Match attributes on any code element: -->
            <Attributes>
              <Exclude>
                <!-- Don't forget "Attribute" at the end of the name -->
                <Attribute>^System\.Diagnostics\.DebuggerHiddenAttribute$</Attribute>
                <Attribute>^System\.Diagnostics\.DebuggerNonUserCodeAttribute$</Attribute>
                <Attribute>^System\.Runtime\.CompilerServices.CompilerGeneratedAttribute$</Attribute>
                <Attribute>^System\.CodeDom\.Compiler.GeneratedCodeAttribute$</Attribute>
                <Attribute>^System\.Diagnostics\.CodeAnalysis.ExcludeFromCodeCoverageAttribute$</Attribute>
              </Exclude>
            </Attributes>

            <!-- Match the path of the source files in which each method is defined: -->
            <Sources>
              <Exclude>
                <Source>.*\\atlmfc\\.*</Source>
                <Source>.*\\vctools\\.*</Source>
                <Source>.*\\public\\sdk\\.*</Source>
                <Source>.*\\microsoft sdks\\.*</Source>
                <Source>.*\\vc\\include\\.*</Source>
              </Exclude>
            </Sources>

            <!-- Match the company name property in the assembly: -->
            <CompanyNames>
              <Exclude>
                <CompanyName>.*microsoft.*</CompanyName>
              </Exclude>
            </CompanyNames>

            <!-- Match the public key token of a signed assembly: -->
            <PublicKeyTokens>
              <!-- Exclude Visual Studio extensions: -->
              <Exclude>
                <PublicKeyToken>^B77A5C561934E089$</PublicKeyToken>
                <PublicKeyToken>^B03F5F7F11D50A3A$</PublicKeyToken>
                <PublicKeyToken>^31BF3856AD364E35$</PublicKeyToken>
                <PublicKeyToken>^89845DCD8080CC91$</PublicKeyToken>
                <PublicKeyToken>^71E9BCE111E9429C$</PublicKeyToken>
                <PublicKeyToken>^8F50407C4E9E73B6$</PublicKeyToken>
                <PublicKeyToken>^E361AF139669C375$</PublicKeyToken>
              </Exclude>
            </PublicKeyTokens>

            <!-- We recommend you do not change the following values: -->
            <UseVerifiableInstrumentation>True</UseVerifiableInstrumentation>
            <AllowLowIntegrityProcesses>True</AllowLowIntegrityProcesses>
            <CollectFromChildProcesses>True</CollectFromChildProcesses>
            <CollectAspDotNet>False</CollectAspDotNet>

          </CodeCoverage>
        </Configuration>
      </DataCollector>
    </DataCollectors>
  </DataCollectionRunSettings>
</RunSettings>
```

## <a name="see-also"></a>Consulte também

- [Configurar testes de unidade usando um arquivo de configurações de execução](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
- [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)
- [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)