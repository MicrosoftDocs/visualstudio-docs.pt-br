---
title: Introdução às linguagens específicas do domínio
description: Conheça os conceitos básicos na definição e no uso de uma linguagem específica do domínio (DSL) criada com o SDK de Modelagem para Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2ae488056986afbe35763be1eebb500ff0eab9a8
ms.sourcegitcommit: 674d3fafa7c9e0cb0d1338027ef419a49c028c36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2021
ms.locfileid: "112602260"
---
# <a name="get-started-with-domain-specific-languages"></a>Introdução à Linguagem Específica de Domínio

Este tópico explica os conceitos básicos na definição e no uso de uma linguagem específica do domínio (DSL) criada com o SDK de Modelagem para Visual Studio.

> [!NOTE]
> O SDK de Transformação Modelo de Texto e Visual Studio SDK de Modelagem de Texto são instalados automaticamente quando você instala recursos específicos do Visual Studio. Para obter mais detalhes, consulte [esta postagem no blog](https://devblogs.microsoft.com/devops/the-visual-studio-modeling-sdk-is-now-available-with-visual-studio-2017/).

Se você for novo no DSLs, recomendamos que você trabalhe por meio do Laboratório de Ferramentas **DSL,** que pode encontrar neste site: Visualização e [SDK de Modelagem](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)

## <a name="what-can-you-do-with-a-domain-specific-language"></a>O que você pode fazer com uma linguagem Domain-Specific linguagem?

Uma linguagem específica do domínio é uma notação, geralmente gráfica, que foi projetada para ser usada para uma finalidade específica. Por outro lado, linguagens como UML são de uso geral. Em uma DSL, você pode definir os tipos de elemento de modelo e suas relações e como eles são apresentados na tela.

Quando você tiver projetado uma DSL, poderá distribuí-la como parte de um pacote VSIX (Visual Studio Integration Extension). Os usuários trabalham com a DSL Visual Studio:

![Diagrama de árvore de família, caixa de ferramentas e explorer](../modeling/media/familyt_instance.png)

A notação é apenas parte de uma DSL. Junto com a notação, seu pacote VSIX inclui ferramentas que os usuários podem aplicar para ajudá-los a editar e gerar material de seus modelos.

Um dos principais aplicativos de DSLs é gerar código do programa, arquivos de configuração e outros artefatos. Especialmente em projetos grandes e linhas de produto, em que várias variantes de um produto serão criadas, gerar muitos dos aspectos variáveis de DSLs pode fornecer um grande aumento na confiabilidade e uma resposta muito rápida às alterações de requisitos.

O restante desta visão geral é um passo a passo que apresenta as operações básicas de criação e uso de uma linguagem específica do domínio no Visual Studio.

## <a name="prerequisites"></a>Pré-requisitos

Para definir uma DSL, é necessário ter instalados os seguintes componentes:

| Componente | Link |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkId=185579](https://visualstudio.microsoft.com) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [https://go.microsoft.com/fwlink/?linkid=2166172](../extensibility/visual-studio-sdk.md) |
| SDK de modelagem para Visual Studio | |

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="create-a-dsl-solution"></a>Criar uma solução DSL

Para criar uma nova linguagem específica do domínio, crie uma nova Visual Studio usando o modelo de projeto Domain-Specific Language.

1. No menu **Arquivo** , aponte para **Novo** e clique em **Projeto**.

2. Em **Tipos de projeto,** expanda o **nó Outros Tipos de** Projeto e clique **em Extensibilidade**.

3. Clique **Designer de Linguagem Específica de Domínio**.

     ![Caixa de diálogo Criar DSL](../modeling/media/create_dsldialog.png)

4. Na caixa **Nome,** digite **FamilyTree**. Clique em **OK**.

     O **Assistente de Linguagem Específica do Domínio** é aberto e exibe uma lista de soluções DSL de modelo.

     Clique em cada modelo para ver uma descrição,

     Os modelos são pontos de partida úteis. Cada um deles fornece uma DSL de trabalho completa, que você pode editar para atender às suas necessidades. Normalmente, você escolhe o modelo mais próximo do que deseja criar.

5. Para este passo a passo, escolha o **modelo linguagem** mínima.

6. Insira uma extensão de nome de arquivo para sua DSL na página do assistente apropriada. Essa é a extensão que será usada pelos arquivos que contêm as instâncias de sua DSL.

    - Escolha uma extensão que não está associada a nenhum aplicativo em seu computador ou em qualquer computador em que você deseja instalar a DSL. Por exemplo, **docx e** **htm** seriam extensões de nome de arquivo inaceitáveis.

    - O assistente o avisará se a extensão inserida está sendo usada como uma DSL. Considere usar uma extensão de nome de arquivo diferente. Também é possível redefinir a instância Experimental do SDK do Visual Studio para limpar os designers experimentais antigos. Clique **em** Iniciar , **clique** em Todos os Programas, **Microsoft Visual Studio SDK 2010,** Ferramentas **e,** em seguida, Redefina o **Microsoft Visual Studio 2010 Experimental.**

7. Inspecione as outras páginas e clique em **Concluir**.

     Uma solução é gerada que contém dois projetos. Eles são chamados de Dsl e DslPackage. Um arquivo de diagrama é aberto chamado DslDefinition.dsl.

    > [!NOTE]
    > A maioria do código que você pode ver nas pastas nos dois projetos é gerada de DslDefinition.dsl. Por esse motivo, a maioria das modificações na DSL é feita nesse arquivo.

A interface do usuário agora se assemelha à imagem a seguir.

![designer dsl](../modeling/media/dsl_designer.png)

Essa solução define uma linguagem específica de domínio. Para obter mais informações, consulte [Visão geral do Domain-Specific Language Tools Interface do Usuário](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md).

## <a name="the-important-parts-of-the-dsl-solution"></a>As partes importantes da solução DSL

Observe os seguintes aspectos da nova solução:

- **Dsl\DslDefinition.dsl** Esse é o arquivo que você vê ao criar uma solução DSL. Quase todo o código na solução é gerado a partir desse arquivo e a maioria das alterações feitas em uma definição de DSL é feita aqui. Para obter mais informações, consulte Trabalhando com o [Diagrama de Definição de DSL](../modeling/working-with-the-dsl-definition-diagram.md).

- **Projeto Dsl** Este projeto contém código que define o idioma específico do domínio.

- **Projeto DslPackage** Este projeto contém código que permite que instâncias da DSL sejam abertas e editadas em Visual Studio.

## <a name="running-the-dsl"></a><a name="Debugging"></a> Executando a DSL

Você pode executar a solução DSL assim que a tiver criado. Posteriormente, você pode modificar a definição de DSL gradualmente, executando a solução novamente após cada alteração.

### <a name="to-experiment-with-the-dsl"></a>Para experimentar a DSL

1. Clique **em Transformar Todos os Modelos** na barra **Gerenciador de Soluções** ferramentas. Isso regenera a maior parte do código-fonte de DslDefinition.dsl.

    > [!NOTE]
    > Sempre que você *alterar DslDefinition.dsl*, clique em **Transformar Todos** os Modelos antes de recriar a solução. Você pode automatizar esta etapa. Para obter mais informações, [consulte How to Automate Transform All Templates](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\)).

2. Pressione **F5** ou, no menu **Depurar,** clique **em Iniciar Depuração**.

     O DSL cria e é instalado na instância experimental do Visual Studio.

     Uma instância experimental do Visual Studio é iniciada. A instância experimental usa suas configurações de uma subárvore separada do Registro, em que Visual Studio extensões são registradas para fins de depuração. Instâncias normais de Visual Studio não têm acesso às extensões registradas lá.

3. Na instância experimental do Visual Studio, abra o arquivo de modelo chamado **Teste** de **Gerenciador de Soluções**.

     \- ou –

     Clique com o botão direito do mouse no projeto Depuração, aponte **para Adicionar** e clique em **Item**. Na caixa **de diálogo Adicionar** Item, selecione o tipo de arquivo da DSL.

     O arquivo de modelo é aberto como um diagrama em branco.

     A caixa de ferramentas é aberta e exibe as ferramentas apropriadas para o tipo de diagrama.

4. Use as ferramentas para criar formas e conectores no diagrama.

    1. Para criar formas, arraste do exemplo ferramenta Forma para o diagrama.

    2. Para conectar duas formas, clique na ferramenta Conector de Exemplo, clique na primeira forma e clique na segunda forma.

5. Clique nos rótulos das formas para alterá-las.

Seu Visual Studio experimental será semelhante ao exemplo a seguir:

![Árvore de exemplo de idioma específico do domínio Visual Studio](../modeling/media/dsl_min.png)

### <a name="the-content-of-a-model"></a>O conteúdo de um modelo

O conteúdo de um arquivo que é uma instância de uma DSL é chamado de *modelo*. O modelo contém *elementos de* <em>modelo</em> e *links* entre os elementos. A definição de DSL especifica quais tipos de elementos de modelo e links podem existir no modelo. Por exemplo, em uma DSL criada com o modelo linguagem mínima, há um tipo de elemento de modelo e um tipo de link.

A definição de DSL pode especificar como o modelo aparece em um diagrama. Você pode escolher entre uma variedade de estilos de formas e conectores. Você pode especificar que algumas formas apareçam dentro de outras formas.

Você pode exibir um modelo como uma árvore na **exibição do Explorer** enquanto edita um modelo. Conforme você adiciona formas ao diagrama, os elementos de modelo também aparecem no explorer. O explorer pode ser usado mesmo se não houver nenhum diagrama.

Se você não puder ver o Explorer na instância de depuração do Visual Studio, no **menu** Exibir aponte para Outras **Janelas** e clique em *\<Your Language>* **Explorer**.

### <a name="the-api-of-your-dsl"></a>A API de sua DSL

Sua DSL gera uma API que permite ler e atualizar modelos que são instâncias da DSL. Um aplicativo da API é gerar arquivos de texto de um modelo. Para obter mais informações, consulte Geração de código em tempo [de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

Na solução Depuração, abra os arquivos de modelo com a extensão ".tt". Esses exemplos demonstram como você pode gerar texto de modelos e permitir que você teste a API de sua DSL. Um dos exemplos é escrito em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] , o outro em [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] .

Em cada arquivo de modelo está o arquivo que ele gera. Expanda o arquivo de modelo Gerenciador de Soluções e abra o arquivo gerado.

O arquivo de modelo contém um pequeno segmento de código que lista todos os elementos no modelo.

O arquivo gerado contém o resultado.

Ao alterar um arquivo de modelo, você verá as alterações correspondentes nos arquivos gerados depois de regenerar os arquivos.

#### <a name="to-regenerate-text-files-after-you-change-the-model-file"></a>Para regenerar arquivos de texto depois de alterar o arquivo de modelo

1. Na instância experimental do Visual Studio, salve o arquivo de modelo.

2. Certifique-se de que o parâmetro de nome de arquivo em cada arquivo .tt refere-se ao arquivo de modelo que você está usando para experimentos. Salve o arquivo .tt.

3. Clique **em Transformar Todos os** Modelos na barra de ferramentas do **Gerenciador de Soluções**.

     \- ou –

     Clique com o botão direito do mouse nos modelos que você deseja regenerar e clique **em Executar Ferramenta Personalizada**.

Você pode adicionar qualquer número de arquivos de modelo de texto a um projeto. Cada modelo gera um arquivo de resultado.

> [!NOTE]
> Quando você altera a definição de DSL, o código de modelo de texto de exemplo não funcionará, a menos que você o atualize.

Para obter mais informações, [consulte Gerando código de](../modeling/generating-code-from-a-domain-specific-language.md) uma linguagem Domain-Specific e Escrevendo código para personalizar uma linguagem Domain-Specific [.](../modeling/writing-code-to-customise-a-domain-specific-language.md)

## <a name="customizing-the-dsl"></a>Personalizando a DSL

Quando você quiser modificar a definição de DSL, feche a instância experimental e atualize a definição na instância Visual Studio principal.

> [!NOTE]
> Depois de modificar a definição de DSL, você poderá perder informações nos modelos de teste criados usando versões anteriores.  Por exemplo, a solução de depuração contém um arquivo chamado Sample, que contém algumas formas e conectores. Depois de começar a desenvolver sua definição de DSL, elas não estarão visíveis e serão perdidas quando você salvar o arquivo.

Você pode fazer uma ampla variedade de extensões para sua DSL. Os exemplos a seguir lhe darão uma impressão das possibilidades.

Após cada alteração, salve a definição de DSL, clique em Transformar Todos os Modelos **no** Gerenciador de Soluções e pressione **F5** para experimentar a DSL alterada. 

### <a name="rename-the-types-and-tools"></a>Renomear os tipos e ferramentas

Renomeie as relações e classes de domínio existentes. Por exemplo, começando com uma Definição de DSL criada com o modelo linguagem mínima, você pode executar as seguintes operações de renomeação para fazer com que a DSL represente árvores de família.

#### <a name="to-rename-domain-classes-relationships-and-tools"></a>Para renomear classes de domínio, relações e ferramentas

1. No diagrama DslDefinition, renomeie **ExampleModel** como **FamilyTreeModel,** **ExampleElement** to **Person**, **Targets** to **Parents** e **Sources** to **Children**. Você pode clicar em cada rótulo para alterá-lo.

     ![Diagrama de definição de DSL &#45; de árvore de família](../modeling/media/familyt_person.png)

2. Renomeie as ferramentas de elemento e conector.

    1. Abra a janela DSL Explorer clicando na guia em Gerenciador de Soluções. Se você não conseguir vê-lo, no menu **Exibir,** aponte para **Outras Janelas** e clique em **Explorador DSL.** O DSL Explorer fica visível somente quando o diagrama de Definição de DSL é a janela ativa.

    2. Abra o janela Propriedades e posicione-o para que você possa ver o DSL Explorer e as Propriedades ao mesmo tempo.

    3. No DSL Explorer, **expanda Editor**, Guias da Caixa **de Ferramentas**, e Ferramentas *\<your DSL>* . 

    4. Clique **em ExampleElement**. Esse é o item da caixa de ferramentas usado para criar elementos.

    5. No janela Propriedades, altere a **propriedade Nome** para **Pessoa**.

         Observe que a **propriedade Legenda** também muda.

    6. Da mesma maneira, altere o nome da ferramenta **ExampleConnector** para **ParentLink.** Altere **a propriedade Legenda** para que ela não seja uma cópia da propriedade Name. Por exemplo, insira **Link Pai.**

3. Recomar a DSL.

    1. Salve o arquivo de Definição de DSL.

    2. Clique **em Transformar Todos os Modelos** na barra de ferramentas do Gerenciador de Soluções

    3. Pressione F5. Aguarde até que a instância experimental do Visual Studio seja exibida.

4. Na solução Depuração na instância experimental do Visual Studio, abra um arquivo de modelo de teste. Arraste elementos para ele da caixa de ferramentas. Observe que as legendas da ferramenta e os nomes de tipo no DSL Explorer foram alterados.

5. Salve o arquivo de modelo.

6. Abra um arquivo .tt e substitua as ocorrências dos nomes de propriedade e tipo antigos por novos nomes.

7. Certifique-se de que o nome de arquivo especificado no arquivo .tt especifique o modelo de teste.

8. Salve o arquivo .tt. Abra o arquivo gerado para ver o resultado da execução do código no arquivo .tt. Verifique se ele está correto.

### <a name="add-domain-properties-to-classes"></a>Adicionar propriedades de domínio a classes
 Adicione propriedades a uma classe de domínio, por exemplo, para representar os anos de nascimento e a morte de uma Pessoa.

 Para tornar as novas propriedades visíveis no diagrama, você deve adicionar *decoradores* à forma que exibe o elemento de modelo. Você também deve mapear as propriedades para os decoradores.

##### <a name="to-add-properties-and-display-them"></a>Para adicionar propriedades e exibi-las

1. Adicione as propriedades.

   1. No diagrama definição de DSL, clique com o botão direito do mouse na classe de domínio **Pessoa,** aponte para **Adicionar** e clique em **Propriedade de Domínio**.

   2. Digite uma lista de novos nomes de propriedade, como **Nascimento** e **Morte.** Pressione **Enter** após cada um.

2. Adicione decoradores que exibirão as propriedades na forma.

   1. Siga a linha cinza que se estende da classe de domínio Person para o outro lado do diagrama. Este é um mapa de elemento de diagrama. Ele vincula a classe de domínio a uma classe de forma.

   2. Clique com o botão direito do mouse nessa classe de forma, aponte **para Adicionar** e clique em **Decorador de Texto.**

   3. Adicione dois decoradores com nomes como **BirthDecorator** e **DeathDecorator**.

   4. Selecione cada novo decorador e, no janela Propriedades, decore o **campo** Posição. Isso determina onde o valor da propriedade de domínio será exibido na forma. Por exemplo, de definir **InnerBottomLeft** e **InnerBottomRight**.

        ![Definição de forma do compartimento](../modeling/media/familyt_compartment.png)

3. Mapeie os decoradores para as propriedades.

   1. Abra a janela Detalhes de DSL. Normalmente, ele está em uma guia ao lado da janela Saída. Se você não conseguir vê-lo, no menu **Exibir,** aponte para **Outras Janelas** e clique em **Detalhes de DSL**.

   2. No diagrama de definição de DSL, clique na linha que conecta a **classe de** domínio Person à classe de forma.

   3. Em **Detalhes de DSL**, na guia **Mapas** do Decorador , clique na caixa de seleção em um decorador não mapeado. Em **Exibir Propriedade**, selecione a propriedade de domínio para a qual você deseja mapeá-la. Por exemplo, **mapeie BirthDecorator** para **Birth**.

4. Salve a DSL, clique em Transformar Todos os Modelos e pressione F5.

5. Em um diagrama de modelo de exemplo, verifique se agora você pode clicar nas posições escolhidas e digitar valores neles. Além disso, quando você seleciona uma **forma De** pessoa, o janela Propriedades exibe as novas propriedades Nascimento e Morte.

6. Em um arquivo .tt, você pode adicionar código que obtém as propriedades de cada pessoa.

   ![Diagrama de árvore de família, caixa de ferramentas e explorer](../modeling/media/familyt_instance.png)

### <a name="define-new-classes"></a>Definir novas classes
 Você pode adicionar classes de domínio e relações a um modelo. Por exemplo, você pode criar uma nova classe para representar cidades e uma nova relação para representar que uma pessoa se envidau em uma cidade.

 Para tornar os diferentes tipos distintos em um diagrama de modelo, você pode mapear as classes de domínio para diferentes tipos de forma ou formas com diferentes geometria e cores.

##### <a name="to-add-and-display-a-new-domain-class"></a>Para adicionar e exibir uma nova classe de domínio

1. Adicione uma classe de domínio e torne-a um filho da raiz do modelo.

    1. No diagrama de definição de DSL, clique na ferramenta de **relação incorporada** , clique na classe raiz **FamilyTreeModel** e, em seguida, clique em uma parte vazia do diagrama.

         Uma nova classe de domínio é exibida, que está conectada ao FamilyTreeModel com uma relação incorporada.

         Defina seu nome, por exemplo, **cidade**.

        > [!NOTE]
        > Cada classe de domínio, exceto a raiz do modelo, deve ser o destino de pelo menos uma relação de incorporação ou deve herdar de uma classe que é o destino de uma incorporação. Por esse motivo, muitas vezes é conveniente criar uma classe de domínio usando a ferramenta de relação incorporada.

    2. Adicione uma propriedade de domínio à nova classe, por exemplo **nome**.

2. Adicione uma relação de referência entre Person e cidade.

    1. Clique na ferramenta **relação de referência** , clique em pessoa e, em seguida, clique em cidade.

         ![Fragmento de definição de DSL: raiz da árvore da família](../modeling/media/familyt_root.png)

        > [!NOTE]
        > Relações de referência representam referências cruzadas de uma parte da árvore de modelo para outra.

3. Adicione uma forma para representar cidades nos diagramas de modelo.

    1. Arraste uma **forma de geometria** da caixa de ferramentas para o diagrama e renomeie-a, por exemplo **TownShape**.

    2. Na janela Propriedades, defina os campos de aparência da nova forma, como cor de preenchimento e geometria.

    3. Adicione um decorador para exibir o nome da cidade e renomeie-o NameDecorator. Defina sua propriedade Position.

4. Mapeie a classe de domínio da cidade para o TownShape.

    1. Clique na ferramenta **mapa de elementos de diagrama** , clique na classe de domínio cidade e, em seguida, na classe forma TownShape.

    2. Na guia **mapas de decoradores** da janela **detalhes de DSL** com o conector de mapa selecionado, marque NameDecorator e defina **Exibir Propriedade** como nome.

5. Crie um conector para exibir a relação entre Person e cidades.

    1. Arraste um conector da caixa de ferramentas para o diagrama. Renomeie-o e defina suas propriedades de aparência.

    2. Use a ferramenta **mapa de elementos de diagrama** para vincular o novo conector à relação entre Person e cidade.

         ![Definição de árvore da família com mapa de formas adicionado](../modeling/media/familyt_shapemap.png)

6. Crie uma ferramenta de elemento para criar uma nova cidade.

    1. No **Gerenciador de DSL**, expanda o **Editor** e as guias da **caixa de ferramentas**.

    2. Clique com o botão direito do mouse *\<your DSL>* e clique em **Adicionar novo elemento ferramenta**.

    3. Defina a propriedade **Name** da nova ferramenta e defina sua propriedade de **classe** como cidade.

    4. Defina a propriedade do **ícone da caixa de ferramentas** . Clique em **[...]** e, no campo **nome do arquivo** , selecione um arquivo de ícone.

7. Crie uma ferramenta de conector para fazer um vínculo entre cidades e pessoas.

    1. Clique com o botão direito do mouse *\<your DSL>* e clique em **Adicionar nova ferramenta de conector**.

    2. Defina a propriedade Name da nova ferramenta.

    3. Na propriedade **ConnectionBuilder** , selecione o construtor que contém o nome da relação de Person-Town.

    4. Defina o **ícone da caixa de ferramentas**.

8. Salve a definição de DSL, clique em **transformar todos os modelos** e pressione **F5**.

9. Na instância experimental do Visual Studio, abra um arquivo de modelo de teste. Use as novas ferramentas para criar cidades e links entre cidades e pessoas. Observe que você só pode criar links entre os tipos de elemento corretos.

10. Crie um código que liste a cidade em que cada pessoa vive. Os modelos de texto são um dos lugares onde você pode executar esse código. Por exemplo, você pode modificar o arquivo Sample.tt existente na solução de depuração para que ele contenha o seguinte código:

    ```
    <#@ template inherits="Microsoft.VisualStudio.TextTemplating.VSHost.ModelingTextTransformation" debug="true" #>
    <#@ output extension=".txt" #>
    <#@ FamilyTree processor="FamilyTreeDirectiveProcessor" requires="fileName='Sample.ftree'" #>

    <#
      foreach (Person person in this.FamilyTreeModel.People)
      {
    #>
        <#= person.Name #><#if (person.Town != null) {#> of <#= person.Town.Name #> <#}#>

    <#
          foreach (Person child in person.Children)
      {
    #>
                <#= child.Name #>
    <#
      }
      }
    #>

    ```

     Quando você salvar o arquivo *. TT, ele criará um arquivo de subsidiária que contém a lista de pessoas e suas residências. Para obter mais informações, consulte [gerando código a partir de um idioma Domain-Specific](../modeling/generating-code-from-a-domain-specific-language.md).

## <a name="validation-and-commands"></a>Validação e comandos
 Você pode desenvolver essa DSL ainda mais adicionando restrições de validação. Essas restrições são métodos que você pode definir, que verificam se o modelo está em um estado correto. Por exemplo, você pode definir uma restrição para garantir que a data de nascimento de um filho seja posterior à de seus pais. O recurso de validação exibirá um aviso se o usuário DSL tentar salvar um modelo que interrompa qualquer uma das restrições. Para obter mais informações, consulte [validação em um idioma de Domain-Specific](../modeling/validation-in-a-domain-specific-language.md).

 Você também pode definir comandos de menu que o usuário pode invocar. Os comandos podem modificar o modelo. Eles também podem interagir com outros modelos no Visual Studio e com recursos externos. Para obter mais informações, consulte [como modificar um comando de menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

## <a name="deploying-the-dsl"></a>Implantando a DSL
 Para permitir que outros usuários usem a linguagem específica de domínio, você distribui um arquivo de VSIX (extensão do Visual Studio). Isso é criado quando você cria a solução de DSL.

 Localize o arquivo. vsix na pasta bin da sua solução. Copie-o para o computador no qual você deseja instalá-lo. Nesse computador, clique duas vezes no arquivo VSIX. A DSL pode ser usada em todas as instâncias do Visual Studio nesse computador.

 Você pode usar o mesmo procedimento para instalar a DSL em seu próprio computador para não precisar usar a instância experimental do Visual Studio.

 Para obter mais informações, confira [Implantando soluções de linguagem específica de domínio](msi-and-vsix-deployment-of-a-dsl.md).

## <a name="removing-old-experimental-dsls"></a><a name="Reset"></a> Removendo DSLs experimentais antigas
 Se você tiver criado DSLs experimentais que não deseja mais, poderá removê-las do computador redefinindo a instância experimental do Visual Studio.

 Isso removerá do seu computador todas as DSLs experimentais e outras extensões experimentais do Visual Studio. Essas são extensões que foram executadas no modo de depuração.

 Esse procedimento não remove DSLs ou outras extensões do Visual Studio que foram totalmente instaladas executando o arquivo VSIX.

#### <a name="to-reset-the-visual-studio-experimental-instance"></a>Para redefinir a instância experimental do Visual Studio

1. Clique em **Iniciar**, **todos os programas**, **Microsoft Visual Studio SDK 2010**, **ferramentas** e, em seguida, **redefina a instância experimental Microsoft Visual Studio 2010**.

2. Reconstrua quaisquer DSLs experimentais ou outras extensões experimentais do Visual Studio que você ainda deseja usar.

## <a name="see-also"></a>Confira também

- [Noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md)
- [Como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md)
