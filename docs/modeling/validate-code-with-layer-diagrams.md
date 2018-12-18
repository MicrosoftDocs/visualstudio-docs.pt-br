---
title: Validar o código com diagramas de dependência
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
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 71eebd95db1a616d4f86866ef60fb32251634cc0
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967279"
---
# <a name="validate-code-with-dependency-diagrams"></a>Validar o código com diagramas de dependência

## <a name="why-use-dependency-diagrams"></a>Por que usar diagramas de dependência?

Para certificar-se de que o código não causa conflito com seu design, valide o código com diagramas de dependência no Visual Studio. Isso pode ajudar a:

- Encontre conflitos entre dependências no código e dependências no diagrama de dependência.

- Encontre dependências que talvez sejam afetadas por alterações propostas.

   Por exemplo, você pode editar o diagrama de dependência para mostrar as alterações de arquitetura potenciais e, em seguida, validar o código para ver as dependências afetadas.

- Refatore ou migre o código para um design diferente.

   Encontre o código ou as dependências que exijam trabalho quando você move o código para uma arquitetura diferente.

**Requisitos**

- Visual Studio

- Uma solução que tem um projeto de modelagem com um diagrama de dependência. Este diagrama de dependência deve ser vinculado a artefatos em projetos do c# ou Visual Basic que você deseja validar. Ver [criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md).

> [!NOTE]
> Não há suporte para diagramas de dependência para projetos do .NET Core no Visual Studio 2017.

Para ver quais edições do Visual Studio dão suporte a esse recurso, consulte [suporte de edição para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

Você pode validar código manualmente a partir de um diagrama de dependência aberto no Visual Studio ou em um prompt de comando. Você também pode validar código automaticamente ao executar compilações locais ou Pipelines do Azure compilações. Ver [vídeo do Channel 9: Design e validar sua arquitetura usando diagramas de dependência](http://go.microsoft.com/fwlink/?LinkID=252073).

> [!IMPORTANT]
> Se você quiser executar a validação de camada usando o Team Foundation Server (TFS), você deve instalar também a mesma versão do Visual Studio no seu servidor de compilação.

## <a name="live-dependency-validation"></a>Validação de dependência dinâmica

Validação de dependência ocorre em tempo real e erros são exibidos imediatamente na **Error List**.

* Há suporte para c# e Visual Basic de validação em tempo real.

* Para habilitar análise completa da solução ao usar a validação de dependência dinâmica, abra as configurações de opções da barra de ouro que aparece na **Error List**.

   - Você poderá ignorar permanentemente a barra de ouro, se você não estiver interessado em ver todos os problemas de arquiteturas em sua solução.
   - Se você não habilitar a análise de solução completa, a análise é feita apenas para os arquivos que está sendo editados.

* Ao atualizar projetos para habilitar a validação em tempo real, uma caixa de diálogo mostra o andamento da conversão.

* Ao atualizar um projeto para a validação de dependência dinâmica, a versão do pacote do NuGet é atualizada para ser o mesmo para todos os projetos e é a versão mais recente em uso.

* Adicionando um novo gatilhos de projeto de validação de dependência de uma atualização de projeto.

## <a name="see-if-an-item-supports-validation"></a>Verificar se um item dá suporte à validação

É possível vincular camadas a sites, documentos do Office, arquivos de texto sem formatação e arquivos em projetos que são compartilhados entre vários aplicativos, mas o processo de validação não os incluirá. Os erros de validação não serão exibidos para referências a projetos ou assemblies vinculados a camadas separadas quando nenhuma dependência for exibida entre essas camadas. Essas referências não serão consideradas dependências, a menos que o código use essas referências.

1.  No diagrama de dependência, selecione uma ou mais camadas, clique com botão direito sua seleção e, em seguida, clique em **Exibir Links**.

2.  Na **Gerenciador de camadas**, examine o **dá suporte à validação** coluna. Se o valor for falso, o item não dará suporte à validação.

## <a name="include-other-net-assemblies-and-projects-for-validation"></a>Incluir outros assemblies e projetos do .NET para validação

Quando você arrasta itens para o diagrama de dependência, referências a projetos ou assemblies do .NET correspondentes são adicionadas automaticamente para o **referências de camada** pasta no projeto de modelagem. Essa pasta contém referências aos assemblies e aos projetos analisados durante a validação. Você pode incluir outros assemblies .NET e projetos para validação sem arrastá-los manualmente para o diagrama de dependência.

1.  Na **Gerenciador de soluções**, clique com botão direito no projeto de modelagem ou o **referências de camada** pasta e clique **Add Reference**.

2.  No **adicionar referência** caixa de diálogo, selecione os assemblies ou projetos e, em seguida, clique em **Okey**.

## <a name="validate-code-manually"></a>Validar código manualmente

Se você tiver um diagrama de dependência aberto que esteja vinculado a itens de solução, você pode executar o **validar** comando de atalho do diagrama. Você também pode usar o prompt de comando para executar o **msbuild** com o **validatearchitecture** propriedade personalizada definida como **verdadeiro**. Por exemplo, à medida que fizer alterações no código, execute a validação da camada regularmente de forma que você possa capturar conflitos de dependência com antecedência.

### <a name="validate-code-from-an-open-dependency-diagram"></a>Validar o código de um diagrama de dependência aberto

1.  Clique com botão direito na superfície do diagrama e, em seguida, clique em **validar arquitetura**.

    > [!NOTE]
    > Por padrão, o **ação de compilação** no arquivo de diagrama (. layerdiagram) dependência estiver definida como **validar** para que o diagrama seja incluído no processo de validação.

     O **Error List** janela relata os erros que ocorrem. Para obter mais informações sobre erros de validação, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors).

2.  Para exibir a origem de cada erro, clique duas vezes no erro na **Error List** janela.

    > [!NOTE]
    > Visual Studio pode mostrar um mapa de código em vez da origem do erro. Isso ocorre quando o código tem uma dependência em um assembly que não é especificado no diagrama de dependência ou o código não tem uma dependência que é especificada no diagrama de dependência. Examine o mapa de códigos ou o código para determinar se a dependência deve existir. Para obter mais informações sobre mapas de código, consulte [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).

3.  Para gerenciar erros, consulte [gerenciar erros de validação](#ManageErrors).

### <a name="validate-code-at-the-command-prompt"></a>Validar o código no prompt de comando

1. Abra o prompt de comando do Visual Studio.

2. Escolha uma das seguintes opções:

   - Para validar o código em um projeto de modelagem específico na solução, execute MSBuild com a seguinte propriedade personalizada.

       ```
       msbuild <FilePath+ModelProjectFileName>.modelproj /p:ValidateArchitecture=true
       ```

     - ou –

       Navegue até a pasta que contém o projeto de modelagem (. modelproj) o arquivo e a dependência de diagrama e, em seguida, executar o MSBuild com a seguinte propriedade personalizada:

       ```
       msbuild /p:ValidateArchitecture=true
       ```

   - Para validar o código em todos os projetos de modelagem na solução, execute MSBuild com a seguinte propriedade personalizada:

       ```
       msbuild <FilePath+SolutionName>.sln /p:ValidateArchitecture=true
       ```

     - ou –

       Navegue até a pasta de solução, que deve conter um projeto de modelagem que contém um diagrama de dependência e, em seguida, executar o MSBuild com a seguinte propriedade personalizada:

       ```
       msbuild /p:ValidateArchitecture=true
       ```

     Todos os erros ocorridos serão listados. Para obter mais informações sobre o MSBuild, consulte [MSBuild](../msbuild/msbuild.md) e [tarefa MSBuild](../msbuild/msbuild-task.md).

   Para obter mais informações sobre erros de validação, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors).

### <a name="manage-validation-errors"></a>Gerenciar erros na validação

Durante o processo de desenvolvimento, você talvez queira suprimir alguns dos conflitos reportados durante a validação. Por exemplo, você talvez queira suprimir erros que já esteja resolvendo ou que não sejam relevantes para seu cenário específico. Quando você suprime um erro, é uma boa prática para fazer logon de um item de trabalho no Team Foundation.

> [!WARNING]
> Você já deve estar conectado ao TFS fonte de código de controle (SCC) para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão em um SCC diferentes do TFS, o Visual Studio fecha automaticamente a solução atual. Certifique-se de que você já estiver conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores do Visual Studio, os comandos de menu não estão disponíveis se você não estiver conectado a um SCC.

#### <a name="create-a-work-item-for-a-validation-error"></a>Criar um item de trabalho para um erro de validação

- No **lista de erros** janela, o erro com o botão direito, aponte para **Criar Item de trabalho**e, em seguida, clique no tipo de item de trabalho que você deseja criar.

Use essas tarefas para gerenciar erros de validação na **Error List** janela:

|**To**|**Siga estas etapas**|
|-|-|
|Suprimir erros selecionados durante a validação|Clique em um ou vários erros selecionados, aponte para **gerenciar erros de validação**e, em seguida, clique em **suprimir erros**.<br /><br /> Os erros suprimidos são exibidos com formatação de tachado. Quando você executar a validação da próxima vez, esses erros não serão exibidos.<br /><br /> Erros suprimidos são acompanhados em um arquivo. suppressions para o arquivo de diagrama de dependência correspondente.|
|Parar a supressão de erros selecionados|Clique com botão direito o erros ou erros suprimidos selecionados, aponte para **gerenciar erros de validação**e, em seguida, clique em **parar de suprimir erros**.<br /><br /> Os erros suprimidos selecionados serão exibidos quando você executar a validação na próxima vez.|
|Restaurar todos os erros suprimidos na **Error List** janela|Clique com botão direito em qualquer lugar na **lista de erros** janela, aponte para **gerenciar erros de validação**e, em seguida, clique em **Mostrar todos os erros suprimidos**.|
|Ocultar todos os erros suprimidos do **Error List** janela|Clique com botão direito em qualquer lugar na **lista de erros** janela, aponte para **gerenciar erros de validação**e, em seguida, clique em **ocultar todos os erros suprimidos**.|

## <a name="validate-code-automatically"></a>Validar código automaticamente

É possível executar a validação da camada sempre que você executa uma compilação local. Se sua equipe usa DevOps do Azure, você pode executar a validação de camada com check-ins, que você pode especificar criando uma tarefa MSBuild personalizada e usar relatórios de compilação para coletar erros de validação. Para criar compilações de check-in, consulte [TFVC check-in restringido](/azure/devops/pipelines/build/triggers#gated).

### <a name="to-validate-code-automatically-during-a-local-build"></a>Para validar automaticamente o código durante uma compilação local

Use um editor de texto para abrir o arquivo do projeto de modelagem (.modelproj) e, em seguida, inclua a seguinte propriedade:

```xml
<ValidateArchitecture>true</ValidateArchitecture>
```

\- ou -

1.  Na **Gerenciador de soluções**, o projeto de modelagem que contém o diagrama de dependência ou diagramas com o botão direito e, em seguida, clique em **propriedades**.

2.  No **propriedades** janela, defina o projeto de modelagem **validar arquitetura** propriedade a ser **verdadeiro**.

    Isso inclui o projeto de modelagem no processo de validação.

3.  Na **Gerenciador de soluções**, clique no arquivo de diagrama (. layerdiagram) de dependência que você deseja usar para validação.

4.  No **propriedades** janela, certifique-se de que o diagrama **Build Action** estiver definida como **validar**.

    Isso inclui o diagrama de dependência no processo de validação.

Para gerenciar erros na janela lista de erros, consulte [gerenciar erros de validação](#ManageErrors).

## <a name="troubleshoot-layer-validation-issues"></a>Solucionar problemas de validação da camada

A tabela a seguir descreve problemas na validação da camada e sua resolução. Esses problemas são diferentes dos erros resultantes de conflitos entre o código e o design. Para obter mais informações sobre esses erros, consulte [compreender e resolver erros de validação de camada](#UnderstandingValidationErrors).

|**Problema**|**Possível causa**|**Resolução**|
|-|-|-|
|Os erros de validação não ocorrem como esperado.|A validação não funciona em diagramas de dependência que são copiados de outros diagramas de dependência no Gerenciador de soluções e que estão no mesmo projeto de modelagem. diagramas de dependência são copiados dessa maneira contêm as mesmas referências que o diagrama de dependência original.|Adicione um novo diagrama de dependência ao projeto de modelagem.<br /><br /> Copie os elementos do diagrama de dependência de origem para o novo diagrama.|

## <a name="resolve-layer-validation-errors"></a>Resolver erros de validação de camada

Quando você valida o código em um diagrama de dependência, erros de validação ocorrem quando o código entra em conflito com o design. Por exemplo, as seguintes condições podem fazer os erros de validação ocorrerem:

- Um artefato é atribuído à camada errada. Nesse caso, mova o artefato.

- Um artefato como, por exemplo, uma classe usa outra classe de maneira a entrar em conflito com a arquitetura. Nesse caso, refatore o código para remover a dependência.

Para resolver esses erros, atualize o código até que mais nenhum erro seja exibido durante a validação. É possível realizar essa tarefa de maneira iterativa.

A seção a seguir descreve a sintaxe usada nesses erros, explica o significado desses erros e sugere o que é possível fazer para o resolver ou gerenciá-los.

|**Sintaxe**|**Descrição**|
|-|-|
|*ArtifactN*(*ArtifactTypeN*)|*{1&gt;artefaton&lt;1* é um artefato associado uma camada no diagrama de dependência.<br /><br /> *1&gt;tipoartefaton&lt;1* é o tipo de *2&gt;artefaton&lt;2*, como um **classe** ou **método**, por exemplo:<br /><br /> MySolution.MyProject.MyClass.MyMethod(Method)|
|*NamespaceNameN*|O nome de um namespace.|
|*LayerNameN*|O nome de uma camada no diagrama de dependência.|
|*Tipodependência*|O tipo de relação de dependência entre *artefato1* e *artefato2*. Por exemplo, *artefato1* tem um **chamadas** relação com *artefato2*.|

| **Erro de sintaxe** | **Descrição do erro** |
|-|-|
| DV0001: **dependência inválida** | Esse problema é relatado quando um elemento de código (namespace, tipo, membro) mapeada para referências de uma camada um elemento de código mapeado para outra camada, mas não há nenhuma seta de dependência entre essas camadas no diagrama de validação de dependência que contém esse camadas. Essa é uma violação de restrição de dependência. |
| DV1001: **nome de namespace inválido** | Esse problema é relatado em um elemento de código associado a uma camada que a propriedade "Permitidos em nomes de Namespace" não contém o namespace no qual este elemento de código é definido. Isso é uma violação de restrição de nomenclatura. Observe que a sintaxe de "Permitidos em nomes de Namespace" deve ser uma lista de ponto e vírgula de namespaces na qual o código elementos associados são camada são podem ser definidos. |
| DV1002: **dependência no namespace não referenciáveis** | Esse problema é relatado em um elemento de código associado a uma camada e fazendo referência a outro elemento de código definido em um namespace que é definido na propriedade "Namespace não Referenciáveis" da camada. Isso é uma violação de restrição de nomenclatura. Observe que a propriedade "Namespaces não Referenciáveis" é definida como uma lista de ponto e vírgula separada de namespaces que não devem ser referenciados em elementos de código associados a essa camada. |
| DV1003: **nome do namespace não permitido** | Esse problema é relatado em um elemento de código associado a uma camada que a propriedade "Não permitidos em nomes de Namespace" contém o namespace no qual este elemento de código é definido. Isso é uma violação de restrição de nomenclatura. Observe que a propriedade "Nome do namespace não permitido" é definida como uma lista separada por dois pontos de namespaces na qual o código elementos associados a essa camada não devem ser definidos. |
| DV3001: **Link ausente** | Camada '*Nomecamada*'contém links para'*artefato*' que não foi encontrado. Você não tem uma referência de assembly? |
| DV9001: **análise arquitetônica encontrou erros internos** | Os resultados talvez não estejam completos. Para obter mais informações, consulte o log de eventos da compilação detalhado ou a janela de saída. |

## <a name="see-also"></a>Consulte também

- [Validação de dependência dinâmica no Visual Studio 2017](https://blogs.msdn.microsoft.com/devops/2016/11/30/live-dependency-validation-in-visual-studio-2017/)
- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)
- [Vídeo: Validar suas dependências de arquitetura em tempo real](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)