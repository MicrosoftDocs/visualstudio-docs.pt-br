---
title: Personalização da análise de cobertura de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f6337c35-acae-4c5f-b5d9-ac5ff687ef18
caps.latest.revision: 18
ms.author: gewarren
manager: douge
ms.openlocfilehash: d8a0b09bf2e67813548865b6ed56fee0b0170cc5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49890160"
---
# <a name="customizing-code-coverage-analysis"></a>Personalizando análise de cobertura de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Por padrão, a ferramenta de cobertura de código do Visual Studio analisa todos os assemblies de solução (.exe/.dll) que são carregados durante os testes de unidade. Recomendamos manter esse padrão, pois funciona bem na maioria das vezes. Para obter mais informações, consulte [Usando cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).  
  
 Antes de personalizar o comportamento de cobertura de código, considere algumas alternativas:  
  
- *Desejo excluir o código de teste dos resultados de cobertura de código e incluir apenas o código do aplicativo.*  
  
   Adicione `ExcludeFromCodeCoverage Attribute` à sua classe de teste.  
  
- *Desejo incluir os assemblies que não fazem parte da minha solução.*  
  
   Obtenha os arquivos .pdb desses assemblies e os copia na mesma pasta que os arquivos .dll do assembly.  
  
  Para personalizar o comportamento da cobertura de código, copie o [exemplo no final deste tópico](#sample) e o adicione à sua solução usando a extensão de arquivo .runsettings. Edite-o de acordo com suas necessidades e, no menu **Teste**, escolha **Configurações de Teste**, **Selecionar Arquivo de Configurações de Teste**. O restante deste tópico descreve este procedimento com mais detalhes.  
  
## <a name="the-runsettings-file"></a>O arquivo .runsettings  
 As configurações avançadas da cobertura de código são especificadas em um arquivo .runsettings. Esse é o arquivo de configuração usado por ferramentas de teste da unidade. Recomendamos que você copie o [exemplo no final deste tópico](#sample) e o edite de acordo com suas necessidades.  
  
- *O que aconteceu com o arquivo .testsettings que usei no Visual Studio 2010?*  
  
   No Visual Studio 2010, o arquivo .testsettings se aplica apenas aos testes de unidade baseados na estrutura MSTest. No Visual Studio 2012, as ferramentas de teste não se aplicam apenas ao MSTest, mas também a outras estruturas como NUnit e xUnit.net. O arquivo .testsettings não funcionará com eles. O arquivo .runsettings é criado para personalizar as ferramentas de teste de maneira que funcione com todas as estruturas de teste.  
  
  Para personalizar a cobertura de código, você precisará adicionar um arquivo .runsettings à sua solução:  
  
1. Adicione um arquivo .xml como um item da solução com a extensão `.runsettings`:  
  
    No Gerenciador de Soluções, no menu de atalho da sua solução, escolha **Adicionar**, **Novo Item** e selecione **Arquivo XML**. Salve o arquivo com um nome terminando como`CodeCoverage.runsettings`  
  
2. Adicione o conteúdo fornecido no exemplo no final deste tópico, e personalize-o de acordo com suas necessidades conforme descrito nas seções a seguir.  
  
3. No menu **Teste**, escolha **Configurações de Teste**, **Selecionar Arquivo de Configurações de Teste** e selecione o arquivo.  
  
4. Agora, quando você executar **Analisar Cobertura de Código**, esse arquivo `.runsettings` controlará seu comportamento. Não se esqueça de que você deve executar a cobertura de código novamente: os resultados anteriores de cobertura e coloração de código não são ocultos automaticamente quando você executa testes ou atualiza o código.  
  
5. Para ativar ou desativar as configurações personalizadas, desmarque ou selecione o arquivo no menu **Teste**, **Configurações de Teste**.  
  
   ![Menu de configurações de teste com o arquivo de configurações personalizadas](../test/media/codecoverage-settingsfile.png "CodeCoverage-settingsFile")  
  
   Outros aspectos dos testes de unidade podem ser configurados no mesmo arquivo .runsettings. Para obter mais informações, consulte [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md).  
  
### <a name="specifying-symbol-search-paths"></a>Especificando caminhos de busca de símbolo  
 A cobertura de código requer símbolos (arquivos .pdb) para assemblies estarem presentes. Para assemblies compilados por sua solução, os arquivos de símbolos estão geralmente presentes nos arquivos binários, e a cobertura de código funciona automaticamente. Mas, em alguns casos, você pode incluir os assemblies referenciados na análise de cobertura de código. Nesses casos, os arquivos .pdb podem não estar adjacentes aos binários, mas você pode especificar o caminho de pesquisa de símbolos no arquivo .runsettings.  
  
```xml  
<SymbolSearchPaths>                
      <Path>\\mybuildshare\builds\ProjectX</Path>  
      <!--More paths if required-->  
</SymbolSearchPaths>  
  
```  
  
> [!WARNING]
>  A resolução de símbolos pode ser demorada, especialmente ao usar um local de arquivo remoto com muitos assemblies. Consequentemente, considere copiar arquivos remotos .pdb no mesmo local dos arquivos binários (.dll e .exe).  
  
### <a name="excluding-and-including"></a>Excluindo e incluindo  
 Você pode excluir os assemblies especificados da análise de cobertura de código. Por exemplo:  
  
```minterastlib  
<ModulePaths>  
  <Exclude>  
   <ModulePath>Fabrikam.Math.UnitTest.dll</ModulePath>  
   <!-- Add more ModulePath nodes here. -->  
  </Exclude>  
</ModulePaths>  
```  
  
 Como alternativa, você pode especificar que assemblies devem ser incluídos. Esta abordagem tem a desvantagem de que, ao adicionar mais assemblies à solução, você tem que se lembrar de adicioná-los à lista:  
  
```minterastlib  
<ModulePaths>  
  <Include>  
   <ModulePath>Fabrikam.Math.dll</ModulePath>  
   <!-- Add more ModulePath nodes here. -->  
  </Include>  
</ModulePaths>  
```  
  
 Se `<Include>` estiver vazio, o processamento de cobertura de código incluirá todos os assemblies (arquivos .dll e .exe) que são carregados e para os quais os arquivos **.pdb** podem ser encontrados, com exceção dos itens que correspondem a uma cláusula em uma lista `<Exclude>`.  
  
 `Include` é processado antes de `Exclude`.  
  
### <a name="regular-expressions"></a>Expressões regulares  
 Os nós de inclusão e exclusão usam expressões regulares. Para obter mais informações, consulte [Usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md). As expressões regulares não são iguais a curingas. Em particular:  
  
1. **\.\\*** corresponde a uma cadeia de caracteres  
  
2. **\\.** corresponde a um ponto ".")  
  
3. **\\(   \\)** corresponde a parênteses "(  )"  
  
4. **\\\\** corresponde a um delimitador de caminho de arquivo "\\"  
  
5. **^** corresponde ao início da cadeia de caracteres  
  
6. **$** corresponde ao final da cadeia de caracteres  
  
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
>  Se houver um erro em uma expressão regular, como parênteses sem escape ou ímpar, a análise de cobertura de código não será executada.  
  
### <a name="other-ways-to-include-or-exclude-elements"></a>Outras maneiras de incluir ou excluir elementos  
 Confira o exemplo [ no final deste tópico](#sample).  
  
- `ModulePath` – Assemblies especificados pelo caminho do arquivo de assembly.  
  
- `CompanyName` – faz a correspondência de assemblies pelo atributo Company.  
  
- `PublicKeyToken` – faz a correspondência de assemblies assinados pelo token de chave pública. Por exemplo, para fazer a correspondência de todos os componentes e extensões do Visual Studio, use `<PublicKeyToken>^B03F5F7F11D50A3A$</PublicKeyToken>`.  
  
- `Source` – faz a correspondência de elementos pelo nome do caminho do arquivo de código-fonte no qual são definidos.  
  
- `Attribute` – faz a correspondência de elementos aos quais um atributo específico está anexado. Especifique o nome completo do atributo, inclusive a palavra "Attribute" no final do nome.  
  
- `Function` – faz a correspondência de procedimentos, funções ou métodos pelo nome totalmente qualificado.  
  
  **Correspondência de um nome de função**  
  
  A expressão regular deve corresponder ao nome totalmente qualificado da função, incluindo o namespace, o nome da classe, o nome do método e a lista de parâmetros. Por exemplo,  
  
- C# ou Visual Basic: `Fabrikam.Math.LocalMath.SquareRoot(double)`  
  
- C++: `Fabrikam::Math::LocalMath::SquareRoot(double)`  
  
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
  
## <a name="how-to-specify-runsettings-files-while-running-tests"></a>Como especificar arquivos .runsettings ao executar testes  
  
### <a name="to-customize-runsettings-in-visual-studio-tests"></a>Para personalizar configurações de execução em testes do Visual Studio  
 Escolha **Teste**, **Configurações de Teste**, **Selecionar Arquivo de Configurações de Teste** e selecione o arquivo .runsettings. O arquivo aparece no menu Configurações de Teste, e você pode selecionar ou cancelar. Quando selecionado, o arquivo .runsettings se aplica sempre que você usar **Analisar Cobertura de Código**.  
  
### <a name="to-customize-run-settings-in-a-command-line-test"></a>Para personalizar as configurações de execução em um teste de linha de comando  
 Para executar testes a partir da linha de comando, use vstest.console.exe. O arquivo de configurações é um parâmetro desse utilitário. Para obter mais informações, confira [usando VSTest.console na linha de comando](http://msdn.microsoft.com/library/852812d8-b3bb-407e-bc43-04d511fcb27a).  
  
1.  Inicie o Prompt de Comando do Desenvolvedor do Visual Studio:  
  
     No menu **Iniciar** do Windows, escolha **Todos os Programas**, **Microsoft Visual Studio**, **Ferramentas do Visual Studio** e **Prompt de Comando do Desenvolvedor**.  
  
2.  Execute:  
  
     `vstest.console.exe MyTestAssembly.dll /EnableCodeCoverage /Settings:CodeCoverage.runsettings`  
  
### <a name="to-customize-run-settings-in-a-build-definition"></a>Para personalizar as configurações de execução em uma definição de compilação  
 Você pode obter dados de cobertura de código de uma compilação de equipe.  
  
 ![Especificação do runsettings em uma definição de compilação](../test/media/codecoverage-buildrunsettings.png "CodeCoverage-buildRunsettings")  
  
1. Verifique se o arquivo .runsettings passou por check-in.  
  
2. No Team Explorer, abra **Compilações** e adicione ou edite uma definição de build.  
  
3. Na página **Processo**, expanda **Testes Automatizados**, **Fonte de Teste**, **Configurações de Execução**. Selecione o seu arquivo **.runsettings**.  
  
   - <em>Mas **Assembly de teste</em>* aparecerá em vez de **testar fonte**. Quando tento definir o campo Configurações de Execução**, só consigo selecionar arquivos .testsettings.*  
  
      Em **Testes Automatizados**, selecione **Assembly de Teste** e escolha **[...]** no final da linha. Na caixa de diálogo **Adicionar/Editar Execução de Teste**, defina **Test Runner** para **Visual Studio Test Runner**.  
  
   Os resultados são visíveis na seção de resumo do relatório de compilação.  
  
##  <a name="sample"></a>Exemplo de arquivo .runsettings  
 Copie este código e edite-o de acordo com suas necessidades. Este é o arquivo .runsettings padrão.  
  
 (Para outros usos do arquivo .runsettings confira [Configuração de testes de unidade usando um arquivo .runsettings](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md).)  
  
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
Each element in the list is a regular expression (ECMAScript syntax). See http://msdn.microsoft.com/library/2k3te2cs.aspx.  
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
                <!—Don't forget "Attribute" at the end of the name -->  
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
 [Uso da cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)   
 [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)



