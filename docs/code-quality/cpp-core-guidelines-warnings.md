---
title: Avisos de diretrizes principais do C++
ms.date: 08/10/2017
ms.topic: conceptual
ms.assetid: 7c83814a-f21d-4323-ad5f-13bac40d3e38
author: mblome
ms.author: mblome
manager: wpickett
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.workload:
- cplusplus
ms.openlocfilehash: 086a977ce5ef69da94316fd708b42b79623d596c
ms.sourcegitcommit: 1abb9cf4c3ccb90e3481ea8079272c98aad12875
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50143262"
---
# <a name="using-the-c-core-guidelines-checkers"></a>Usando os verificadores de diretrizes principais do C++

Diretrizes principais do C++ são um conjunto portátil de diretrizes, regras e as práticas recomendadas sobre como codificar em C++ criado pelos designers e especialistas em C++. Atualmente, o Visual Studio suporta um subconjunto dessas regras como parte de suas ferramentas de análise de código para C++. Os verificadores de diretrizes de núcleo são instalados por padrão no Visual Studio 2017 e são [disponível como um pacote do NuGet para Visual Studio 2015](#vs2015_corecheck).

## <a name="the-c-core-guidelines-project"></a>O projeto de diretrizes principais do C++

Diretrizes principais do C++ criado por Bjarne Stroustrup e outros, são um guia para usar o C++ moderno com segurança e eficácia. As diretrizes enfatizam a segurança de tipo estático e segurança de recursos. Eles identificarem maneiras de eliminar ou minimizar as partes mais propensas a erro da linguagem e sugerem como tornar seu código mais simples e mais eficaz de forma confiável. Essas diretrizes são mantidas pelo Standard C++ Foundation. Para obter mais informações, consulte a documentação [diretrizes principais do C++](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)e acessar os arquivos de projeto de documentação de diretrizes principais do C++ no [GitHub](https://github.com/isocpp/CppCoreGuidelines).

## <a name="enable-the-c-core-check-guidelines-in-code-analysis"></a>Habilitar as diretrizes da verificação principal do C++ na análise de código

Você pode habilitar a análise de código em seu projeto, selecionando o **habilitar análise de código no Build** caixa de seleção na **análise de código** seção o **páginas de propriedade** caixa de diálogo para seu projeto.

![Página de propriedades para configurações gerais de análise de código](../code-quality/media/cppcorecheck_codeanalysis_general.png)

As regras de verificação principal do C++ são extensões para os conjuntos de regra padrão que são executados quando a análise de código está habilitada. Como as regras de verificação principal do C++ estão em desenvolvimento, algumas regras são bem estabelecidas, e alguns podem não estar prontas para uso em todo o código, mas ainda podem ser informativas. As regras são divididas em dois grupos: experimental e lançadas. Você pode optar por executar as regras de lançamento ou experimentais nas propriedades de seu projeto.

![Página de propriedades para configurações de extensões de análise de código](../code-quality/media/cppcorecheck_codeanalysis_extensions.png)

Para habilitar ou desabilitar os conjuntos de regra de verificação principal do C++, abra o **páginas de propriedade** caixa de diálogo para seu projeto. Sob **propriedades de configuração**, expanda **análise de código**, **extensões**. Na lista suspensa próxima ao controle **habilitar a verificação principal do C++ (liberados)** ou **Habilitar verificação principal do C++ (Experimental)**, escolha **Sim** ou **não**. Escolher **Okey** ou **aplicar** para salvar suas alterações.

## <a name="examples"></a>Exemplos

Aqui está um exemplo de alguns dos problemas que as regras de verificação principal do C++ podem encontrar:

```cpp
// CoreCheckExample.cpp
// Add CppCoreCheck package and enable code analysis in build for warnings.

int main()
{
    int arr[10];           // warning C26494
    int* p = arr;          // warning C26485

    [[gsl::suppress(bounds.1)]] // This attribute suppresses Bounds rule #1
    {
        int* q = p + 1;    // warning C26481 (suppressed)
        p = q++;           // warning C26481 (suppressed)
    }

    return 0;
}
```

Este exemplo demonstra alguns dos avisos que as regras de verificação principal do C++ podem encontrar:

- C26494 é regra Type.5: sempre inicialize um objeto.

- C26485 é regra Bounds.3: decaimento nenhum ponteiro de matriz.

- C26481 é regra Bounds.1: não use aritmética de ponteiro. Use `span` em seu lugar.

Se o rulesets de análise do código de verificação principal do C++ estão instalado e habilitado quando você compila esse código, os dois primeiros avisos forem gerados, mas o terceiro é suprimido. Aqui está a saída da compilação do código de exemplo:

```Output
1>------ Build started: Project: CoreCheckExample, Configuration: Debug Win32 ------
1>  CoreCheckExample.cpp
1>  CoreCheckExample.vcxproj -> C:\Users\username\documents\visual studio 2015\Projects\CoreCheckExample\Debug\CoreCheckExample.exe
1>  CoreCheckExample.vcxproj -> C:\Users\username\documents\visual studio 2015\Projects\CoreCheckExample\Debug\CoreCheckExample.pdb (Full PDB)
c:\users\username\documents\visual studio 2015\projects\corecheckexample\corecheckexample\corecheckexample.cpp(6): warning C26494: Variable 'arr' is uninitialized. Always initialize an object. (type.5: http://go.microsoft.com/fwlink/p/?LinkID=620421)
c:\users\username\documents\visual studio 2015\projects\corecheckexample\corecheckexample\corecheckexample.cpp(7): warning C26485: Expression 'arr': No array to pointer decay. (bounds.3: http://go.microsoft.com/fwlink/p/?LinkID=620415)
========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
```

Diretrizes principais do C++ estão lá para ajudá-lo a escrever código melhor e mais seguro. No entanto, se você tiver uma instância em que uma regra ou um perfil não deve ser aplicado, é fácil suprimi-lo diretamente no código. Você pode usar o `gsl::suppress` atributo para manter a verificação principal do C++ de detectar e relatar qualquer violação de uma regra no bloco de código a seguir. Você pode marcar instruções individuais para suprimir regras específicas. Você pode até mesmo suprimir todo o perfil limites escrevendo `[[gsl::suppress(bounds)]]` sem incluir um número específico de regra.

## <a name="supported-rule-sets"></a>Suporte para conjuntos de regras

Conforme novas regras são adicionadas ao verificador de diretrizes de núcleo do C++, pode aumentar o número de avisos que são produzidos para código pré-existente. Você pode usar conjuntos de regras predefinidas para filtrar quais tipos de regras para permitir. A partir do Visual Studio 2017 versão 15.3, os conjuntos de regra com suporte são:

  - **Regras de ponteiro de proprietário** impor [verificações de gerenciamento de recursos relacionados ao proprietário<T> das diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#r-resource-management).

  - **Regras de const** impor [verificações relacionadas a const das diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#con-constants-and-immutability).

  - **Regras de ponteiro bruto** impor [gerenciamento de recursos verifica ponteiros relacionados a brutos das diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#r-resource-management).

  - **Regras de ponteiro exclusivo** impor [verificações de gerenciamento de recursos relacionadas aos tipos com semânticas de ponteiros exclusivos das diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#r-resource-management).

  - **Regras de limites** impor a [delimita o perfil das diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#probounds-bounds-safety-profile).

  - **Regras de tipo** impor a [tipo de perfil de diretrizes principais do C++](http://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#prosafety-type-safety-profile).


Você pode optar por limitar os avisos para apenas um ou alguns dos grupos. O **mínimo nativo** e **recomendado nativo** regra conjuntos incluem regras de verificação principal do C++, além de outras verificações PREfast. Para ver o disponíveis conjuntos de regra, abra a caixa de diálogo Propriedades do projeto, selecione **código Analysis\General**, abra a lista suspensa na **conjuntos de regras** caixa de combinação e selecionar com **escolher vários conjuntos de regras** . Para obter mais informações sobre como usar conjuntos de regra no Visual Studio, consulte [usando os conjuntos de regras para agrupar regras de análise de código](using-rule-sets-to-group-code-analysis-rules.md).

## <a name="macros"></a>Macros

O verificador de diretrizes do C++ Core vem com um arquivo de cabeçalho que define as macros que tornam mais fácil suprimir todas categorias de avisos no código:

```cpp
ALL_CPPCORECHECK_WARNINGS
CPPCORECHECK_TYPE_WARNINGS
CPPCORECHECK_RAW_POINTER_WARNINGS
CPPCORECHECK_CONST_WARNINGS
CPPCORECHECK_OWNER_POINTER_WARNINGS
CPPCORECHECK_UNIQUE_POINTER_WARNINGS
CPPCORECHECK_BOUNDS_WARNINGS
```

Essas macros correspondem aos conjuntos de regras e expandem em uma lista separada por espaço de números de aviso. Usando as construções de pragma apropriado, você pode configurar o conjunto efetivo de regras que é interessante para um projeto ou uma seção de código. No exemplo a seguir, a análise de código somente alertará sobre ausentes modificadores constante:

```cpp
#include <CppCoreCheck\Warnings.h>
#pragma warning(disable: ALL_CPPCORECHECK_WARNINGS)
#pragma warning(default: CPPCORECHECK_CONST_WARNINGS)
```

## <a name="attributes"></a>Atributos

O compilador Microsoft Visual C++ tem um suporte limitado para a GSL suprimir o atributo. Ele pode ser usado para suprimir avisos em expressões e instruções de blocos dentro de uma função.

```cpp
// Suppress only warnings from the 'r.11' rule in expression.
[[gsl::suppress(r.11)]] new int;

// Suppress all warnings from the 'r' rule group (resource management) in block.
[[gsl::suppress(r)]]
{
    new int;
}

// Suppress only one specific warning number.
// For declarations, you may need to use the surrounding block.
// Macros are not expanded inside of attributes.
// Use plain numbers instead of macros from the warnings.h.
[[gsl::suppress(26400)]]
{
    int *p = new int;
}
```

## <a name="suppressing-analysis-by-using-command-line-options"></a>Suprimindo a análise, usando as opções de linha de comando

Em vez de #pragmas, você pode usar opções de linha de comando na página de propriedades do arquivo para suprimir avisos para um projeto ou um único arquivo. Por exemplo, para desabilitar o aviso 26400 para um arquivo:

1. Clique no arquivo em **Gerenciador de soluções**

2. Escolha **propriedades | C / C + + | Linha de comando**

3. No **opções adicionais** janela, adicione `/wd26400`.

Você pode usar a opção de linha de comando para desabilitar temporariamente todas as análises de código para um arquivo, especificando `/analyze-`. Isso gerará o aviso *D9025 substituindo '/ANALYZE' com ' /ANALYZE -'*, que o lembrará de habilitar a análise de código novamente mais tarde.

## <a name="corecheck_per_file"></a> Habilitar o verificador de diretrizes do C++ Core nos arquivos de projeto específico

Às vezes, pode ser útil para análise de código foco e ainda aproveitar o IDE do Visual Studio. Abaixo está um cenário de exemplo que pode ser usado para projetos grandes para economizar tempo de compilação e para facilitar para filtrar os resultados.

1.  No shell de comando, defina as `esp.extension` e `esp.annotationbuildlevel` variáveis de ambiente.
2.  Inicie o Visual Studio no shell de comando para herdar essas variáveis.
3.  Carregue seu projeto e abra suas propriedades.
4.  Habilitar análise de código, selecione os conjuntos de regra apropriado, mas não habilitar extensões de análise de código.
5.  Vá até o arquivo que você deseja analisar com o verificador de diretrizes de núcleo do C++ e abrir suas propriedades.
6.  Escolher **C / C + + \Command opções de linha de** e adicionar `/analyze:plugin EspXEngine.dll`
7.  Desabilitar o uso de cabeçalho pré-compilado (**C / C + + \Precompiled cabeçalhos**). Isso é necessário porque o mecanismo de extensões pode tentar ler suas informações internas de cabeçalho pré-compilado e se a última opção tiver sido compilado com as opções de projeto padrão, ele não será compatível.
8.  Recompile o projeto. As verificações de PREFast comuns devem ser executado em todos os arquivos. Porque o verificador de diretrizes do C++ Core não está habilitado por padrão, ele só deve ser executado no arquivo que está configurado para usá-lo.

## <a name="how-to-use-the-c-core-guidelines-checker-outside-of-visual-studio"></a>Como usar o verificador de diretrizes do C++ Core fora do Visual Studio
Você pode usar as verificações de diretrizes principais do C++ em compilações automatizadas.

### <a name="msbuild"></a>MSBuild
 O verificador de análise de código nativo (PREfast) é integrado ao ambiente do MSBuild pelos arquivos de destinos personalizados. Você pode usar as propriedades do projeto para habilitá-lo e adicionar o verificador de diretrizes do C++ Core (que se baseia no PREfast):

 ```xml
  <PropertyGroup>
    <EnableCppCoreCheck>true</EnableCppCoreCheck>
    <CodeAnalysisRuleSet>CppCoreCheckRules.ruleset</CodeAnalysisRuleSet>¬¬
    <RunCodeAnalysis>true</RunCodeAnalysis>
  </PropertyGroup>
```

Verifique se que você adicionar essas propriedades antes da importação do arquivo Microsoft.Cpp.targets. Você pode escolher os conjuntos de regras específicas ou criar um conjunto de regras personalizadas ou usar o conjunto de regras padrão que inclui outras verificações PREfast.

Você pode executar o verificador de núcleo do C++ somente em arquivos especificados usando a mesma abordagem [descritos anteriormente](#coreckeck_per_file), mas usando arquivos do MSBuild. As variáveis de ambiente podem ser definidas usando o `BuildMacro` item:

```xml
<ItemGroup>
    <BuildMacro Include="Esp_AnnotationBuildLevel">
      <EnvironmentVariable>true</EnvironmentVariable>
      <Value>Ignore</Value>
    </BuildMacro>
    <BuildMacro Include="Esp_Extensions">
      <EnvironmentVariable>true</EnvironmentVariable>
      <ValueCppCoreCheck.dll</Value>
    </BuildMacro>
</ItemGroup>
```

Se você não quiser modificar o arquivo de projeto, você pode passar as propriedades na linha de comando:

```cmd
msbuild /p:EnableCppCoreCheck=true /p:RunCodeAnalysis=true /p:CodeAnalysisRuleSet=CppCoreCheckRules.ruleset ...
```

### <a name="non-msbuild-projects"></a>Projetos não MSBuild
Se você usar um sistema de compilação que não depende do MSBuild ainda é possível executar o verificador, mas você precisará se familiarizar com alguns recursos internos da configuração do mecanismo de análise de código (que não é garantida para ter suporte no futuro).

Você precisará definir algumas variáveis de ambiente e usar as opções de linha de comando adequadas para o compilador. É melhor trabalhar no ambiente do "Prompt de comando de ferramentas nativas" para que você não precisa pesquisar caminhos específicos para o compilador, incluir diretórios etc.

1. **Variáveis de ambiente**
   - `set esp.extensions=cppcorecheck.dll` Isso informa ao mecanismo para carregar o módulo de diretrizes principais do C++.
   - `set esp.annotationbuildlevel=ignore` Isso desabilita a lógica que processa as anotações de SAL. As anotações não afetam a análise de código no verificador de diretrizes de núcleo de C++, ainda que suas leva de processamento de tempo (às vezes, muito tempo). Essa configuração é opcional, mas altamente recomendado.
   - `set caexcludepath=%include%` É altamente recomendável que você desabilite os avisos que são acionados em cabeçalhos padrão. Você pode adicionar mais caminhos aqui, por exemplo, o caminho para os cabeçalhos comuns em seu projeto.
2. **Opções de linha de comando**
   - `/analyze`  Habilita a análise de código (Considere também usar /ANALYZE: somente e /ANALYZE: quiet).
   - `/analyze:plugin EspXEngine.dll` Esta opção carrega o mecanismo de extensões de análise de código para o PREfast. Esse mecanismo, por sua vez, carrega o verificador de diretrizes de núcleo do C++.

## <a name="use-the-guideline-support-library"></a>Use a biblioteca de suporte de diretriz
 A biblioteca de suporte de diretriz é projetada para ajudá-lo a seguir as diretrizes de núcleo. O GSL inclui definições que permitem que você substitua construções propenso a erro alternativas mais seguras. Por exemplo, você pode substituir uma `T*, length` par de parâmetros com o `span<T>` tipo. A GSL está disponível em [ http://www.nuget.org/packages/Microsoft.Gsl ](http://www.nuget.org/packages/Microsoft.Gsl). A biblioteca é software livre, portanto, você pode exibir as fontes de, fazer comentários ou contribuir com. O projeto pode ser encontrado em [ https://github.com/Microsoft/GSL ](https://github.com/Microsoft/GSL).

 ## <a name="vs2015_corecheck"></a> Use as diretrizes de verificação principal do C++ em projetos do Visual Studio 2015
  Se você usar o Visual Studio 2015, conjuntos de regras de análise de código verificação principal do C++ não são instalados por padrão. Você deve executar algumas etapas adicionais antes de habilitar as ferramentas de análise de código de verificação principal do C++ no Visual Studio 2015. Microsoft fornece suporte para projetos do Visual Studio 2015 usando um pacote do Nuget. O pacote é chamado Microsoft.CppCoreCheck e está disponível em [ http://www.nuget.org/packages/Microsoft.CppCoreCheck ](http://www.nuget.org/packages/Microsoft.CppCoreCheck). Este pacote requer que você tem pelo menos o Visual Studio 2015 com atualização 1 instalado.

 O pacote também instala outro pacote como uma dependência, uma biblioteca de suporte diretriz (GSL) somente de cabeçalho. A GSL também está disponível no GitHub em [ https://github.com/Microsoft/GSL ](https://github.com/Microsoft/GSL).

 Por causa da maneira que as regras de análise de código são carregadas, você deve instalar o pacote do Microsoft.CppCoreCheck NuGet em cada projeto de C++ que você deseja verificar no Visual Studio 2015.

### <a name="to-add-the-microsoftcppcorecheck-package-to-your-project-in-visual-studio-2015"></a>Para adicionar o pacote de Microsoft.CppCoreCheck ao seu projeto no Visual Studio 2015

1. Na **Gerenciador de soluções**, clique com botão direito para abrir o menu de contexto do seu projeto na solução que você deseja adicionar o pacote. Escolher **gerenciar pacotes NuGet** para abrir o **Gerenciador de pacotes NuGet**.

2. No **Gerenciador de pacotes NuGet** janela, procure Microsoft.CppCoreCheck.

    ![Janela Gerenciador de pacotes do NuGet mostra o pacote de CppCoreCheck](../code-quality/media/cppcorecheck_nuget_window.png)

3. Selecione o pacote Microsoft.CppCoreCheck e, em seguida, escolha o **instalar** botão para adicionar as regras ao seu projeto.

   O pacote NuGet adiciona um arquivo. targets do MSBuild adicional ao seu projeto que é invocado quando você habilita a análise de código em seu projeto. Esse arquivo. targets adiciona as regras de verificação principal do C++ como uma extensão adicional para a ferramenta de análise de código do Visual Studio. Quando o pacote é instalado, você pode usar a caixa de diálogo páginas de propriedades para habilitar ou desabilitar as regras de experimentais e lançadas.