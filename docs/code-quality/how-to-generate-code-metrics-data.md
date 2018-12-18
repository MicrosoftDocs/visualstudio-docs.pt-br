---
title: Gerar as métricas de código do IDE ou na linha de comando
ms.date: 11/02/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code metrics data
- code metrics results
- code metrics [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e3f8d6f2df0b0d9ec6e3f9d8ead7fd1e08929f8e
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50966525"
---
# <a name="how-to-generate-code-metrics-data"></a>Como: gerar dados de métricas de código

Você pode gerar resultados de métricas de código para um ou mais projetos ou uma solução inteira. As métricas de código estão disponível dentro do ambiente de desenvolvimento interativo (IDE) do Visual Studio e, para C# e projetos do Visual Basic, na linha de comando.

Além disso, você pode instalar um [pacote do NuGet](https://dotnet.myget.org/feed/roslyn-analyzers/package/nuget/Microsoft.CodeAnalysis.FxCopAnalyzers/2.6.2-beta2-63202-01) que inclui quatro métricas de código [analisador](roslyn-analyzers-overview.md) regras: CA1501, CA1502, CA1505 e CA1506. Essas regras são desabilitadas por padrão, mas você pode habilitá-las a partir **Gerenciador de soluções** ou em um [conjunto de regras](using-rule-sets-to-group-code-analysis-rules.md) arquivo.

## <a name="visual-studio-ide-code-metrics"></a>Métricas de código do Visual Studio IDE

### <a name="generate-code-metrics-results-for-an-entire-solution"></a>Gerar resultados de métricas de código para uma solução inteira

Você pode gerar resultados de métricas de código para uma solução inteira em qualquer uma das seguintes maneiras:

- Na barra de menus, escolha **Analyze** > **calcular métricas de código** > **para solução**.

- Na **Gerenciador de soluções**, a solução com o botão direito e, em seguida, escolha **calcular métricas de código**.

- No **resultados de métricas de código** janela, escolha o **calcular métricas de código para solução** botão.

Os resultados são gerados e o **resultados de métricas de código** janela é exibida. Para exibir os detalhes de resultados, expanda a árvore na **hierarquia** coluna.

### <a name="generate-code-metrics-results-for-one-or-more-projects"></a>Gerar resultados de métricas de código para um ou mais projetos

1. Na **Gerenciador de soluções**, selecione um ou mais projetos.

1. Na barra de menus, escolha **Analyze** > **calcular métricas de código** > **para projetos selecionados**.

Os resultados são gerados e o **resultados de métricas de código** janela é exibida. Para exibir os detalhes de resultados, expanda a árvore na **hierarquia**.

## <a name="command-line-code-metrics"></a>Métricas de código de linha de comando

Você pode gerar dados de métricas de código da linha de comando para C# e projetos do Visual Basic para aplicativos do .NET Framework, .NET Core e .NET Standard. As ferramentas de métricas de código de linha de comando é chamado *Metrics.exe*.

Para obter o *Metrics.exe* executável, deve [gerá-lo](#generate-the-executable). Em breve, uma [versão publicada do *Metrics.exe* estarão disponíveis](https://github.com/dotnet/roslyn-analyzers/issues/1756) para que você não precise compilá-lo.

### <a name="generate-the-executable"></a>Gerar o executável

Para gerar o executável *Metrics.exe*, siga estas etapas:

1. Clone o [dotnet/roslyn-analyzers](https://github.com/dotnet/roslyn-analyzers) repositório.
2. Abra o Prompt de comando do desenvolvedor para Visual Studio como administrador.
3. Da raiz de **analisadores de roslyn** repositório, execute o seguinte comando: `Restore.cmd`
4. Altere o diretório para *src\Tools*.
5. Execute o seguinte comando para criar o **Metrics.csproj** projeto:

   ```shell
   msbuild /m /v:m /p:Configuration=Release Metrics.csproj
   ```

   Um arquivo executável chamado *Metrics.exe* é gerado na *binários* diretório sob a raiz do repositório.

   > [!TIP]
   > Para construir *Metrics.exe* na [modo herdado](#legacy-mode), execute o seguinte comando:
   >
   > ```shell
   > msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
   > ```

### <a name="usage"></a>Uso

Para executar *Metrics.exe*, fornecer um projeto ou solução e um XML de saída de arquivo como argumentos. Por exemplo:

```shell
C:\>Metrics.exe /project:ConsoleApp20.csproj /out:report.xml
Loading ConsoleApp20.csproj...
Computing code metrics for ConsoleApp20.csproj...
Writing output to 'report.xml'...
Completed Successfully.
```

### <a name="output"></a>Saída

A saída XML gerada recebe o seguinte formato:

```xml
<?xml version="1.0" encoding="utf-8"?>
<CodeMetricsReport Version="1.0">
  <Targets>
    <Target Name="ConsoleApp20.csproj">
      <Assembly Name="ConsoleApp20, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null">
        <Metrics>
          <Metric Name="MaintainabilityIndex" Value="100" />
          <Metric Name="CyclomaticComplexity" Value="1" />
          <Metric Name="ClassCoupling" Value="1" />
          <Metric Name="DepthOfInheritance" Value="1" />
          <Metric Name="LinesOfCode" Value="11" />
        </Metrics>
        <Namespaces>
          <Namespace Name="ConsoleApp20">
            <Metrics>
              <Metric Name="MaintainabilityIndex" Value="100" />
              <Metric Name="CyclomaticComplexity" Value="1" />
              <Metric Name="ClassCoupling" Value="1" />
              <Metric Name="DepthOfInheritance" Value="1" />
              <Metric Name="LinesOfCode" Value="11" />
            </Metrics>
            <Types>
              <NamedType Name="Program">
                <Metrics>
                  <Metric Name="MaintainabilityIndex" Value="100" />
                  <Metric Name="CyclomaticComplexity" Value="1" />
                  <Metric Name="ClassCoupling" Value="1" />
                  <Metric Name="DepthOfInheritance" Value="1" />
                  <Metric Name="LinesOfCode" Value="7" />
                </Metrics>
                <Members>
                  <Method Name="void Program.Main(string[] args)" File="C:\Users\mavasani\source\repos\ConsoleApp20\ConsoleApp20\Program.cs" Line="7">
                    <Metrics>
                      <Metric Name="MaintainabilityIndex" Value="100" />
                      <Metric Name="CyclomaticComplexity" Value="1" />
                      <Metric Name="ClassCoupling" Value="1" />
                      <Metric Name="LinesOfCode" Value="4" />
                    </Metrics>
                  </Method>
                </Members>
              </NamedType>
            </Types>
          </Namespace>
        </Namespaces>
      </Assembly>
    </Target>
  </Targets>
</CodeMetricsReport>
```

### <a name="tool-differences"></a>Diferenças de ferramenta

As versões anteriores do Visual Studio, incluindo o Visual Studio 2015, incluíam uma ferramenta de métricas de código de linha de comando chamada *Metrics.exe*. Nesta versão anterior da ferramenta fez uma análise binária, ou seja, uma análise baseada em assembly. A nova ferramenta analisa o código-fonte em vez disso. Porque o novo *Metrics.exe* é o código-fonte baseado em código, os resultados são diferentes para o que é gerado por versões anteriores do *Metrics.exe* e dentro do IDE do Visual Studio 2017.

O novo *Metrics.exe* ferramenta pode computar métricas mesmo na presença de erros de código fonte, desde que a solução e projeto podem ser carregados.

#### <a name="metric-value-differences"></a>Diferenças de valor de métrica

O `LinesOfCode` métrica é mais precisos e confiáveis no novo *Metrics.exe*. Ele é independente de quaisquer diferenças de geração de código e não muda quando o conjunto de ferramentas ou tempo de execução é alterado. O novo *Metrics.exe* contagens real de linhas de código, incluindo linhas em branco e comentários.

Outras métricas, como `CyclomaticComplexity` e `MaintainabilityIndex` usar as mesmas fórmulas como as versões anteriores do *Metrics.exe*, mas o novo *Metrics.exe* conta o número de `IOperations` (lógico instruções da fonte) em vez de instruções de IL (linguagem intermediária). Os números serão ligeiramente diferentes das versões anteriores do *Metrics.exe* e dos resultados de métricas de código do IDE do Visual Studio 2017.

### <a name="legacy-mode"></a>Modo herdado

Você também pode optar por compilar *Metrics.exe* na *modo herdado*. A versão do modo herdado da ferramenta gera valores de métrica que estejam mais perto que versões mais antigas da ferramenta gerada. Além disso, no modo herdado, *Metrics.exe* gera métricas de código para o mesmo conjunto de método de tipos que as métricas de código gerada de ferramenta para as versões anteriores. Por exemplo, ele não gera dados de métricas de código para inicializadores de campo e propriedade. Modo herdado é útil para versões anteriores compatibilidade ou, se você tiver portões de check-in do código com base em métricas de código números. O comando para compilar *Metrics.exe* no modo herdado é:

```shell
msbuild /m /v:m /t:rebuild /p:LEGACY_CODE_METRICS_MODE=true Metrics.csproj
```

Para obter mais informações, consulte [habilitar a geração de métricas de código no modo herdado](https://github.com/dotnet/roslyn-analyzers/pull/1841).

## <a name="see-also"></a>Consulte também

- [Use a janela de resultados de métricas de código](../code-quality/working-with-code-metrics-data.md)
- [Valores de métricas de código](../code-quality/code-metrics-values.md)