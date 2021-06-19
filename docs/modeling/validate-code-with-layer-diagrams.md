---
title: Validar o código com diagramas de dependência
description: Saiba que, para garantir que o código não entre em conflito com seu design, você deve validar seu código com diagramas de dependência Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 09/28/2018
ms.topic: conceptual
helpviewer_keywords:
- dependency diagrams, validating
- validation, dependency diagrams
- validation, code
- code exploration, validating
- architecture, validating
- Visual Studio Ultimate, validating code
- validation, architecture
- validation, dependencies
- MSBuild, tasks
- MSBuild, dependency diagrams
- MSBuild, validating code
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1f2d62433d150f61e9a7e21cceb20eb715a0767a
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388354"
---
# <a name="validate-code-with-dependency-diagrams"></a>Validar o código com diagramas de dependência

## <a name="why-use-dependency-diagrams"></a>Por que usar diagramas de dependência?

Para garantir que o código não entre em conflito com seu design, valide seu código com diagramas de dependência Visual Studio. Isso pode ajudar a:

- Encontre conflitos entre dependências em seu código e dependências no diagrama de dependência.

- Encontre dependências que talvez sejam afetadas por alterações propostas.

   Por exemplo, você pode editar o diagrama de dependência para mostrar possíveis alterações de arquitetura e validar o código para ver as dependências afetadas.

- Refatore ou migre o código para um design diferente.

   Encontre o código ou as dependências que exijam trabalho quando você move o código para uma arquitetura diferente.

**Requirements**

- Visual Studio

  Para criar um diagrama de dependência para um projeto do .NET Core, você deve ter Visual Studio 2019 versão 16.2 ou posterior.

- Uma solução que tem um projeto de modelagem com um diagrama de dependência. Esse diagrama de dependência deve estar vinculado a artefatos em C# ou Visual Basic projetos que você deseja validar. Consulte [Criar diagramas de dependência com o código](../modeling/create-layer-diagrams-from-your-code.md).

Para ver quais edições do Visual Studio suporte a esse recurso, confira [Suporte à edição para ferramentas de arquitetura e modelagem](../modeling/analyze-and-model-your-architecture.md#VersionSupport).

Você pode validar o código manualmente de um diagrama de dependência aberto Visual Studio ou de um prompt de comando. Você também pode validar o código automaticamente ao executar builds locais ou Azure Pipelines builds. Consulte [Vídeo do Channel 9: Projetar e validar sua arquitetura usando diagramas de dependência](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Using-layer-diagrams-to-design-and-validate-your-architecture).

> [!IMPORTANT]
> Se você quiser executar a validação de camada usando Team Foundation Server (TFS), também deverá instalar a mesma versão do Visual Studio em seu servidor de build.

## <a name="live-dependency-validation"></a>Validação de dependência ao vivo

A validação de dependência ocorre em tempo real e os erros são mostrados imediatamente na **Lista de Erros**.

* A validação ao vivo tem suporte para C# e Visual Basic.

* Para habilitar a análise completa da solução ao usar a validação de dependência ativa, abra as configurações de opções na barra ouro que aparece na Lista **de Erros**.

  - Você poderá descartar permanentemente a barra ouro se não estiver interessado em ver todos os problemas de arquitetura em sua solução.
  - Se você não habilitar a análise completa da solução, a análise será feita somente para os arquivos que estão sendo editados.

* Ao atualizar projetos para habilitar a validação ao vivo, uma caixa de diálogo mostra o progresso da conversão.

* Ao atualizar um projeto para validação de dependência ao vivo, a versão do pacote NuGet é atualizada para ser a mesma para todos os projetos e é a versão mais alta em uso.

* Adicionar um novo projeto de validação de dependência dispara uma atualização de projeto.

## <a name="see-if-an-item-supports-validation"></a>Verificar se um item dá suporte à validação

Você pode vincular camadas a sites, documentos do Office, arquivos de texto sem-texto e arquivos em projetos compartilhados entre vários aplicativos, mas o processo de validação não os incluirá. Os erros de validação não serão exibidos para referências a projetos ou assemblies vinculados a camadas separadas quando nenhuma dependência for exibida entre essas camadas. Essas referências não serão consideradas dependências, a menos que o código use essas referências.

1. No diagrama de dependência, selecione uma ou mais camadas, clique com o botão direito do mouse na seleção e clique em **Exibir Links.**

2. No **Layer Explorer,** veja a coluna Suporte **à validação.** Se o valor for falso, o item não dará suporte à validação.

## <a name="include-other-net-assemblies-and-projects-for-validation"></a>Incluir outros assemblies e projetos do .NET para validação

Quando você arrasta itens para o diagrama de dependência, as referências aos assemblies ou projetos correspondentes do .NET são **adicionadas** automaticamente à pasta Referências de Camada no projeto de modelagem. Essa pasta contém referências aos assemblies e aos projetos analisados durante a validação. Você pode incluir outros assemblies e projetos do .NET para validação sem arrastá-los manualmente para o diagrama de dependência.

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de modelagem ou na pasta **Referências de** Camada e clique em Adicionar **Referência**.

2. Na caixa **de diálogo Adicionar** Referência, selecione os assemblies ou projetos e clique em **OK.**

## <a name="validate-code-manually"></a>Validar código manualmente

Se você tiver um diagrama de dependência aberto vinculado aos itens da solução, poderá executar o comando **De** validar atalho do diagrama. Você também pode usar o prompt de comando para executar o **comando msbuild** com a propriedade personalizada **/p:ValidateArchitecture** definida como **True.** Por exemplo, à medida que fizer alterações no código, execute a validação da camada regularmente de forma que você possa capturar conflitos de dependência com antecedência.

### <a name="validate-code-from-an-open-dependency-diagram"></a>Validar o código de um diagrama de dependência aberto

1. Clique com o botão direito do mouse na superfície do diagrama e clique em **Validar Arquitetura**.

    > [!NOTE]
    > Por padrão, a propriedade **Ação** de Build no arquivo de diagrama de dependência (.layerdiagram) é definida como **Validar** para que o diagrama seja incluído no processo de validação.

     A **janela Lista de** Erros relata os erros que ocorrem. Para obter mais informações sobre erros de validação, consulte Solucionar [problemas de validação de camada](#troubleshoot-layer-validation-issues).

2. Para exibir a origem de cada erro, clique duas vezes no erro na janela **Lista de** Erros.

    > [!NOTE]
    > Visual Studio pode mostrar um mapa de código em vez da origem do erro. Isso ocorre quando o código tem uma dependência em um assembly que não é especificado pelo diagrama de dependência ou o código não tem uma dependência especificada pelo diagrama de dependência. Revise o mapa de código ou o código para determinar se a dependência deve existir. Para obter mais informações sobre mapas de código, consulte [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md).

3. Para gerenciar erros, consulte Resolver [erros de validação de camada](#resolve-layer-validation-errors).

### <a name="validate-code-at-the-command-prompt"></a>Validar o código no prompt de comando

1. Abra o prompt Visual Studio comando.

2. Escolha uma destas opções:

   - Para validar o código em relação a um projeto de modelagem específico na solução, execute o MSBuild com a propriedade personalizada a seguir.

       ```
       msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true
       ```

     - ou –

       Navegue até a pasta que contém o arquivo de projeto de modelagem (.modelproj) e o diagrama de dependência e execute o MSBuild com a seguinte propriedade personalizada:

       ```
       msbuild /p:ValidateArchitecture=true
       ```

   - Para validar o código em relação a todos os projetos de modelagem na solução, execute o MSBuild com a seguinte propriedade personalizada:

       ```
       msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true
       ```

     - ou –

       Navegue até a pasta da solução, que deve conter um projeto de modelagem que contém um diagrama de dependência e execute o MSBuild com a seguinte propriedade personalizada:

       ```
       msbuild /p:ValidateArchitecture=true
       ```

     Todos os erros ocorridos serão listados. Para obter mais informações sobre o MSBuild, consulte [MSBuild](../msbuild/msbuild.md) e [Tarefa MSBuild](../msbuild/msbuild-task.md).

   Para obter mais informações sobre erros de validação, consulte Solucionar [problemas de validação de camada](#troubleshoot-layer-validation-issues).

### <a name="manage-validation-errors"></a>Gerenciar erros na validação

Durante o processo de desenvolvimento, você talvez queira suprimir alguns dos conflitos reportados durante a validação. Por exemplo, você talvez queira suprimir erros que já esteja resolvendo ou que não sejam relevantes para seu cenário específico. Quando você suprimir um erro, é uma boa prática registrar um item de trabalho no Team Foundation.

> [!WARNING]
> Você já deve estar conectado ao SCC (Controle de Código-Fonte) do TFS para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão com um SCC do TFS diferente, Visual Studio fechará a solução atual automaticamente. Verifique se você já está conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores Visual Studio, os comandos de menu não estarão disponíveis se você não estiver conectado a um SCC.

#### <a name="create-a-work-item-for-a-validation-error"></a>Criar um item de trabalho para um erro de validação

- Na janela **Lista de** Erros, clique com o botão direito do mouse no erro, aponte para Criar **Item** de Trabalho e clique no tipo de item de trabalho que você deseja criar.

Use estas tarefas para gerenciar erros de validação na janela **Lista de** Erros:

|**Para**|**Siga estas etapas**|
|-|-|
|Suprimir erros selecionados durante a validação|Clique com o botão direito do mouse em um ou vários erros selecionados, aponte para Gerenciar Erros de Validação e clique em **Suprimir Erros**.<br /><br /> Os erros suprimidos são exibidos com formatação de tachado. Quando você executar a validação da próxima vez, esses erros não serão exibidos.<br /><br /> Erros suprimidos são rastreados em um arquivo .suppressions para o arquivo de diagrama de dependência correspondente.|
|Parar a supressão de erros selecionados|Clique com o botão direito do mouse no erro ou nos erros suprimidos selecionados, aponte para Gerenciar Erros de Validação e clique em **Parar Suprimir Erros**.<br /><br /> Os erros suprimidos selecionados serão exibidos quando você executar a validação na próxima vez.|
|Restaurar todos os erros suprimidos na janela **Lista de** Erros|Clique com o  botão direito do mouse em qualquer lugar na janela Lista de Erros, aponte para Gerenciar Erros de Validação e clique em **Mostrar Todos os Erros Suprimidos**.|
|Ocultar todos os erros suprimidos da janela **Lista de** Erros|Clique com o  botão direito do mouse em qualquer lugar na janela Lista de Erros, aponte para Gerenciar Erros de Validação e clique em Ocultar **Todos os Erros Suprimidos**.|

## <a name="validate-code-automatically"></a>Validar código automaticamente

É possível executar a validação da camada sempre que você executa uma compilação local. Se sua equipe usar Azure DevOps, você poderá executar a validação de camada com check-ins fechados, que podem ser especificados criando uma tarefa personalizada do MSBuild e usar relatórios de build para coletar erros de validação. Para criar builds de check-in fechados, consulte [Check-in TFVC fechado.](/azure/devops/pipelines/build/triggers)

### <a name="to-validate-code-automatically-during-a-local-build"></a>Para validar automaticamente o código durante uma compilação local

Use um editor de texto para abrir o arquivo do projeto de modelagem (.modelproj) e, em seguida, inclua a seguinte propriedade:

```xml
<ValidateArchitecture>true</ValidateArchitecture>
```

\- ou –

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de modelagem que contém o diagrama de dependência ou diagramas e clique em **Propriedades**.

2. Na janela **Propriedades,** de definir a propriedade Validar Arquitetura do projeto **de** modelagem como **True.**

    Isso inclui o projeto de modelagem no processo de validação.

3. No **Gerenciador de Soluções**, clique no arquivo de diagrama de dependência (.layerdiagram) que você deseja usar para validação.

4. Na janela **Propriedades,** certifique-se de que a propriedade Ação de **Build** do diagrama está definida como **Validar**.

    Isso inclui o diagrama de dependência no processo de validação.

Para gerenciar erros na janela Lista de Erros, consulte [Resolver erros de validação de camada](#resolve-layer-validation-errors).

## <a name="troubleshoot-layer-validation-issues"></a>Solucionar problemas de validação da camada

A tabela a seguir descreve problemas na validação da camada e sua resolução. Esses problemas são diferentes dos erros resultantes de conflitos entre o código e o design. Para obter mais informações sobre esses erros, consulte Solucionar [problemas de validação de camada](#troubleshoot-layer-validation-issues).

|**Problema**|**Causa possível**|**Resolução**|
|-|-|-|
|Os erros de validação não ocorrem como esperado.|A validação não funciona em diagramas de dependência copiados de outros diagramas de dependência no Gerenciador de Soluções e que estão no mesmo projeto de modelagem. Diagramas de dependência copiados dessa maneira contêm as mesmas referências que o diagrama de dependência original.|Adicione um novo diagrama de dependência ao projeto de modelagem.<br /><br /> Copie os elementos do diagrama de dependência de origem para o novo diagrama.|

## <a name="resolve-layer-validation-errors"></a>Resolver erros de validação de camada

Quando você valida o código em um diagrama de dependência, ocorrem erros de validação quando o código entra em conflito com o design. Por exemplo, as seguintes condições podem fazer os erros de validação ocorrerem:

- Um artefato é atribuído à camada errada. Nesse caso, mova o artefato.

- Um artefato como, por exemplo, uma classe usa outra classe de maneira a entrar em conflito com a arquitetura. Nesse caso, refatore o código para remover a dependência.

Para resolver esses erros, atualize o código até que mais nenhum erro seja exibido durante a validação. É possível realizar essa tarefa de maneira iterativa.

A seção a seguir descreve a sintaxe usada nesses erros, explica o significado desses erros e sugere o que é possível fazer para o resolver ou gerenciá-los.

|**Sintaxe**|**Descrição**|
|-|-|
|*ArtifactN*(*ArtifactTypeN*)|*ArtifactN* é um artefato associado a uma camada no diagrama de dependência.<br /><br /> *ArtifactTypeN* é o tipo de *ArtifactN*, como uma **classe** ou **método**, por exemplo:<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|
|*NomeNamespaceN*|O nome de um namespace.|
|*NomeCamadaN*|O nome de uma camada no diagrama de dependência.|
|*DependencyType*|O tipo de relação de dependência entre *Artifact1* e *Artifact2.* Por exemplo, *Artifact1* tem uma **relação De chamadas** com *Artifact2*.|

| **Erro de Sintaxe** | **Descrição do erro** |
|-|-|
| DV0001: **Dependência inválida** | Esse problema é relatado quando um elemento de código (namespace, tipo, membro) mapeado para uma Camada faz referência a um elemento de código mapeado para outra camada, mas não há nenhuma seta de dependência entre essas camadas no diagrama de validação de dependência que contém essas camadas. Essa é uma violação de restrição de dependência. |
| DV1001: **nome de namespace inválido** | Esse problema é relatado em um elemento de código associado a uma camada que a propriedade "Nomes de Namespace Permitidos" não contém o namespace no qual esse elemento de código está definido. Trata-se de uma violação de restrição de nomen por nome. Observe que a sintaxe de "Nomes de Namespace Permitidos" deve ser uma lista de pontos e vírgulas de namespaces nos quais os elementos de código associados a são camadas têm permissão para serem definidos. |
| DV1002: **dependência de namespace irreferencial** | Esse problema é relatado em um elemento de código associado a uma camada e referenciando outro elemento de código definido em um namespace que é definido na propriedade "Namespace não referencial" da camada. Trata-se de uma violação de restrição de nomen por nome. Observe que a propriedade "Namespaces não referenciados" é definida como uma lista separada por ponto e vírgula de namespaces que não devem ser referenciados em elementos de código associados a essa camada. |
| DV1003: **nome do namespace não permitido** | Esse problema é relatado em um elemento de código associado a uma camada que a propriedade "Nomes de Namespace não permitidos" contém o namespace no qual esse elemento de código é definido. Trata-se de uma violação de restrição de nomen por nome. Observe que a propriedade "Nome do namespace não permitido" é definida como uma lista separada por pontos e vírgulas de namespaces nos quais os elementos de código associados a essa camada não devem ser definidos. |
| DV2001: Presença **do diagrama de camada** | Esse problema é relatado em um projeto que não inclui um arquivo de diagrama de dependência, mas refere-se aos analisadores de validação de dependência. Se a Validação de Dependência não tiver sido usada, você poderá remover "Microsoft.DependencyValidation.Analyzers" diretamente do Gerenciador de Soluções ou suprimir esse aviso. Para adicionar um diagrama de dependência, [consulte Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md). |
| DV2002: **Base de tipos não mapeados** | Esse problema é relatado quando um elemento de código não é mapeado para nenhuma camada. |
| DV3001: **Link ausente** | A camada '*LayerName*' vincula-se a '*Artifact*' que não pode ser encontrado. Você não tem uma referência de assembly? |
| DV9001: a **análise de arquitetura encontrou erros internos** | Os resultados talvez não estejam completos. Para obter mais informações, consulte o log de eventos da compilação detalhado ou a janela de saída. |

## <a name="see-also"></a>Confira também

- [Validação de dependência em tempo real Visual Studio](https://devblogs.microsoft.com/devops/live-dependency-validation-in-visual-studio-2017/)
- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)
- [Vídeo: Validar suas dependências de arquitetura em tempo real](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)
