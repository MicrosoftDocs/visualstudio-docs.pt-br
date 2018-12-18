---
title: Usar e configurar os analisadores de Roslyn
ms.date: 03/26/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 47dc7d38a2ae9b842891d2e36aebd9b009297cbb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49817035"
---
# <a name="configure-and-use-roslyn-analyzer-rules"></a>Configurar e usar regras do analisador Roslyn

Regras do analisador do .NET compiler Platform ("Roslyn"), ou *diagnóstico*, analisar seu código c# ou Visual Basic, conforme você digita. Cada diagnóstico tem um estado de gravidade e supressão de padrão que pode ser substituído para o seu projeto. Este artigo aborda a severidade de regra de configuração, usando conjuntos de regras e suprimindo violações.

## <a name="analyzers-in-solution-explorer"></a>Analisadores no Gerenciador de soluções

Você pode fazer grande parte da personalização do diagnóstico do analisador de **Gerenciador de soluções**. Se você [instalar analisadores](../code-quality/install-roslyn-analyzers.md) como um pacote do NuGet, um **analisadores** nó aparece sob o **referências** ou **dependências** nó no  **Gerenciador de soluções**. Se você expandir **analisadores**e, em seguida, expanda um dos assemblies do analisador, você verá todos os diagnósticos no assembly.

![Nó de analisadores no Gerenciador de soluções](media/analyzers-expanded-in-solution-explorer.png)

Você pode exibir as propriedades de um diagnóstico, incluindo sua descrição e a gravidade de padrão na **propriedades** janela. Para exibir as propriedades, clique com botão direito na regra e selecione **propriedades**, ou selecione a regra e, em seguida, pressione **Alt**+**Enter**.

![Propriedades de diagnóstico na janela Propriedades](media/analyzer-diagnostic-properties.png)

Para ver a documentação online para obter um diagnóstico, clique com botão direito sobre o diagnóstico e selecione **exibir ajuda**.

Os ícones ao lado de cada diagnóstico na **Gerenciador de soluções** correspondem aos ícones que você pode ver na regra definida quando você abri-lo no editor:

- a letra "i" em um círculo indica um [gravidade](#rule-severity) de **informações**
- o "!" em um triângulo indica um [gravidade](#rule-severity) de **aviso**
- o "x" em um círculo indica um [gravidade](#rule-severity) de **erro**
- a letra "i" em um círculo em um plano de fundo de cor clara indica um [gravidade](#rule-severity) de **Hidden**
- a seta apontando para baixo em um círculo que indica que o diagnóstico será suprimido

![Ícones de diagnóstico no Gerenciador de soluções](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-sets"></a>Conjuntos de regras

Um [conjunto de regras](../code-quality/using-rule-sets-to-group-code-analysis-rules.md) é um arquivo XML que armazena o estado de gravidade e supressão de diagnóstico individual. Conjuntos de regras se aplicam a um único projeto, e um projeto pode ter vários conjuntos de regras. Para exibir o conjunto no editor de regras Active Directory, clique com botão direito no **analisadores** nó no **Gerenciador de soluções** e selecione **do conjunto de regras ativo aberto**. Se esta for a primeira vez que você está acessando a regra definido, um arquivo chamado  *\<projectname > RuleSet* é adicionado ao projeto e aparece na **Gerenciador de soluções**.

> [!NOTE]
> Conjuntos de regras de incluem análise de código (binário) estático e regras do analisador Roslyn.

Você pode alterar a regra ativa definido para um projeto na **análise de código** guia de propriedades de um projeto. Selecione a conjunto de regras de **executar este conjunto de regras** lista suspensa. Você também pode abrir a conjunto de regras do **análise de código** página de propriedades, selecionando **abrir**.

## <a name="rule-severity"></a>Gravidade da regra

Você pode configurar a severidade das regras do analisador, ou *diagnósticos*, se você [instalar os analisadores](../code-quality/install-roslyn-analyzers.md) como um pacote do NuGet. A tabela a seguir mostra as opções de severidade para o diagnóstico:

|Severidade|Comportamento de tempo de compilação|Comportamento do Editor|
|-|-|-|
|Erro|As violações são exibidos como *erros* na **lista de erros** e na linha de comando, saída de compilação e causar compilações falhe.|Código incorreto está sublinhado com uma vermelha ondulada e marcada por uma pequena caixa vermelha na barra de rolagem.|
|Aviso|As violações são exibidos como *avisos* na **lista de erros** e na linha de comando saída da compilação, mas não causam compilações falhe.|Código incorreto está sublinhado com verde ondulada e marcado por uma pequena caixa verde na barra de rolagem.|
|Info|As violações são exibidos como *mensagens* na **lista de erros**e nada na saída da compilação de linha de comando.|Código incorreto está sublinhado com um cinza ondulado e marcado por uma pequena caixa cinza na barra de rolagem.|
|Hidden|Não visíveis ao usuário.|Não visíveis ao usuário. O diagnóstico é relatado para o mecanismo de diagnóstico do IDE, no entanto.|
|Nenhum|Suprimido completamente.|Suprimido completamente.|

Além disso, você pode "Redefinir" severidade de uma regra, configurando-a como **padrão**. Cada diagnóstico com severidade padrão que pode ser vista na **propriedades** janela.

Captura de tela a seguir mostra três diferentes violações de diagnóstico no editor de códigos, com três gravidades diferentes. Observe que a cor do ondulada, bem como a pequena caixa na barra de rolagem à direita.

![Violação de erro, aviso e informações no editor de códigos](media/diagnostics-severity-colors.png)

Captura de tela a seguir mostra as violações de três mesmas como aparecem na **Error List**:

![Erro, aviso e informações de violação na lista de erros](media/diagnostics-severities-in-error-list.png)

Você pode alterar a severidade de uma regra de **Gerenciador de soluções**, ou dentro de  *\<projectname > RuleSet* arquivo que é adicionado à solução depois que você alterar a severidade de uma regra no  **Gerenciador de soluções**.

![Arquivo de conjunto de regras no Gerenciador de soluções](media/ruleset-in-solution-explorer.png)

### <a name="to-set-rule-severity-from-solution-explorer"></a>Para definir a gravidade da regra no Gerenciador de soluções

1. Na **Gerenciador de soluções**, expanda **referências** > **analisadores** (**dependências**  >  **Analisadores** para projetos .NET Core).

1. Expanda o assembly que contém a regra que você deseja definir a severidade para.

1. Clique com botão direito na regra e selecione **definir regra definir gravidade**. No menu suspenso, selecione uma das opções de gravidade.

   A gravidade da regra é salvo no arquivo de conjunto de regras ativo.

### <a name="to-set-rule-severity-in-the-rule-set-file"></a>Definir regra de gravidade na regra definida arquivo

1. Abra o conjunto de regras arquivo clicando duas vezes no **Gerenciador de soluções**, selecionando **abrir conjunto de regras de Active Directory** no menu de atalho do **analisadores** nó, ou selecionando **Aberto** na **análise de código** página de propriedades para o projeto.

1. Navegue até a regra, expandindo o seu assembly de contenção.

1. No **ação** coluna, selecione o valor para abrir uma lista suspensa e selecione a severidade desejada na lista.

   ![Arquivo aberto no editor de conjunto de regras](media/ruleset-file-in-editor.png)

## <a name="suppress-violations"></a>Suprimir violações

Há várias maneiras de suprimir as violações de regra:

- Para suprimir todas as violações atuais existentes, selecione **Analyze** > **executar análise de código e suprimir problemas ativos** na barra de menus. Isso é às vezes, chamado "linha de base".

- Para suprimir um diagnóstico de **Gerenciador de soluções**, defina sua gravidade como **None**.

- Para suprimir um diagnóstico do editor de conjunto de regras, desmarque a caixa ao lado de seu nome ou definir **ação** à **None**.

- Para suprimir um diagnóstico do editor de códigos, coloque o cursor na linha de código com a violação e pressione **Ctrl**+**.** Para abrir o **ações rápidas** menu. Selecione **suprimir CAxxxx** > **na fonte** ou **suprimir CAxxxx** > **no arquivo de supressão**.

   ![Suprimir o diagnóstico no menu de ações rápidas](media/suppress-diagnostic-from-editor.png)

- Para suprimir um diagnóstico do **lista de erros**, consulte [suprimir as violações da lista de erros](#suppress-violations-from-the-error-list).

### <a name="suppress-violations-from-the-error-list"></a>Suprimir as violações da lista de erros

Você pode suprimir um ou vários diagnósticos do **lista de erros** selecionar aqueles que você deseja suprimir, e, em seguida, clicando com botão direito e selecionando **suprimir** > **na origem**  ou **suprimir** > **no arquivo de supressão**.

- Se você selecionar **no código-fonte**, o **visualizar alterações** caixa de diálogo é aberta e mostra uma visualização do c# [#pragma aviso](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) ou o Visual Basic [#Disable aviso](/dotnet/visual-basic/language-reference/directives/directives) diretiva é adicionada ao código-fonte.

   ![Visualização de adição de aviso #pragma no arquivo de código](media/pragma-warning-preview.png)

- Se você selecionar **no arquivo de supressão**, o **visualizar alterações** caixa de diálogo é aberta e mostra uma visualização do <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo que é adicionado ao arquivo supressões globais.

   ![Visualização de adicionar o atributo SuppressMessage ao arquivo de supressão](media/preview-changes-in-suppression-file.png)

No **visualizar alterações** caixa de diálogo, selecione **aplicar**.

O **Error List** exibe diagnóstico ou regra violações, tanto em tempo de análise de código e compilação. Como o diagnóstico de compilação pode ser obsoleto, por exemplo, se você editou o código para corrigir a violação, mas ainda não tiver recriado, você não pode suprimir estes diagnósticos a partir de **lista de erros**. No entanto, o diagnóstico de análise em tempo real ou o IntelliSense, esteja sempre atualizado com as fontes atuais e pode ser suprimido do **Error List**. Se a opção de supressão está desabilitada no menu de contexto, ou de mouse, provavelmente porque você tem um ou mais diagnósticos em sua seleção de compilação. Para excluir o diagnóstico de build da sua seleção, alternar os **lista de erros** filtro de origem do **compilação + IntelliSense** para **Intellisense apenas**. Em seguida, selecione os diagnósticos que você deseja suprimir e prossiga conforme descrito anteriormente.

![Filtro de origem de lista de erros no Visual Studio](media/error-list-filter.png)

> [!NOTE]
> Em um projeto .NET Core, se você adicionar uma referência a um projeto que tem os analisadores do NuGet, os analisadores são automaticamente adicionados ao projeto dependente muito. Para desabilitar esse comportamento, por exemplo, se o projeto dependente é um projeto de teste de unidade, marcar o pacote do NuGet como particular na *. csproj* ou *. vbproj* arquivo do projeto referenciado:
>
> ```xml
> <PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.6.0" PrivateAssets="all" />
> ```

## <a name="command-line-usage"></a>Uso de linha de comando

Quando você compila seu projeto na linha de comando, violações de regra aparecem na saída do build se as seguintes condições forem atendidas:

- Os analisadores são instalados como um pacote do Nuget e não como uma extensão do VSIX.

- Uma ou mais regras forem violadas no código do projeto.

- O [gravidade](#rule-severity) de uma regra violada está definida como **aviso**, caso em que as violações não fazem com que a compilação falhar, ou **erro**, caso em que as violações causam compilação falhar.

O detalhamento da saída do build não afeta se as violações de regra são mostradas. Mesmo com **silencioso** detalhamento, violações de regra aparecem na saída da compilação.

> [!TIP]
> Se você estiver acostumado a executar análise de código estático da linha de comando, com *FxCopCmd.exe* ou por meio de msbuild com o **{1&gt;runcodeanalysis&lt;1** sinalizador, aqui está como fazer isso com os analisadores do Roslyn.

Para ver as violações de analisador na linha de comando quando você compila seu projeto usando o msbuild, execute um comando como este:

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

A imagem a seguir mostra a saída de compilação de linha de comando desde a criação de um projeto que contém uma violação de regra do analisador:

![Saída do MSBuild com violação de regra](media/command-line-build-analyzers.png)

## <a name="see-also"></a>Consulte também

- [Visão geral dos analisadores de Roslyn no Visual Studio](../code-quality/roslyn-analyzers-overview.md)
- [Enviar um bug de analisador Roslyn](https://github.com/dotnet/roslyn-analyzers/issues)
- [Usar conjuntos de regras](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [Suprimir avisos da análise de código](../code-quality/in-source-suppression-overview.md)