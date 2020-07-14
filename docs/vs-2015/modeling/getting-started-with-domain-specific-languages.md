---
title: Introdução com linguagens específicas de domínio | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 024392a2-2c04-404f-a27b-7273553c3b60
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6fe720b380133d15f9bc60485896d4b7acbf2c4b
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543189"
---
# <a name="getting-started-with-domain-specific-languages"></a>Introdução às linguagens específicas do domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico explica os conceitos básicos de definição e uso de uma DSL (linguagem específica de domínio) criada com o SDK de modelagem do Visual Studio.

## <a name="what-can-you-do-with-a-domain-specific-language"></a>O que você pode fazer com uma linguagem específica de domínio?
 Uma linguagem específica de domínio é uma notação, geralmente gráfica, que é projetada para ser usada para uma finalidade específica. Por outro lado, linguagens como UML são de finalidade geral. Em uma DSL, você pode definir os tipos de elemento de modelo e suas relações e como eles são apresentados na tela.

 Quando você tiver criado uma DSL, poderá distribuí-la como parte de um pacote de VSIX (extensão de integração do Visual Studio). Os usuários trabalham com a DSL em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] :

 ![Diagrama de árvore da família, caixa de ferramentas e Explorer](../modeling/media/familyt-instance.png "FamilyT_Instance")

 A notação é apenas parte de uma DSL. Junto com a notação, seu pacote VSIX inclui ferramentas que os usuários podem aplicar para ajudá-los a editar e gerar materiais a partir de seus modelos.

 Um dos principais aplicativos de DSLs é gerar código de programa, arquivos de configuração e outros artefatos. Especialmente em projetos grandes e linhas de produtos, em que várias variantes de um produto serão criadas, gerar muitos aspectos variáveis de DSLs pode fornecer um grande aumento na confiabilidade e uma resposta muito rápida a alterações de requisitos.

 O restante desta visão geral é uma explicação que apresenta as operações básicas de criação e uso de uma linguagem específica de domínio no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

## <a name="prerequisites"></a>Pré-requisitos
 Para definir uma DSL, é necessário ter instalados os seguintes componentes:

|Produto|Link de download|
|-|-|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185579](https://www.visualstudio.com/)|
|[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]|[http://go.microsoft.com/fwlink/?LinkId=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts)|
|SDK de modelagem para Visual Studio|[Baixar o MSDK](https://www.microsoft.com/download/details.aspx?id=48148)|

## <a name="creating-a-dsl-solution"></a>Criando uma solução de DSL
 Para criar uma nova linguagem específica de domínio, você cria uma nova [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução usando o modelo de projeto de linguagem específica de domínio.

#### <a name="to-create-a-dsl-solution"></a>Para criar uma solução DSL

1. No menu **Arquivo** , aponte para **Novo**e clique em **Projeto**.

2. Em **tipos de projeto**, expanda o nó **outros tipos de projeto** e clique em **extensibilidade**.

3. Clique em **Designer de linguagem específica de domínio**.

    ![Criar caixa de diálogo DSL](../modeling/media/create-dsldialog.png "Create_DSLDialog")

4. Na caixa **nome** , digite **FamilyTree**. Clique em **OK**.

    O **Assistente de linguagem específica de domínio** é aberto e exibe uma lista de soluções de DSL de modelo.

    Clique em cada modelo para ver uma descrição,

    Os modelos são pontos de partida úteis. Cada uma delas fornece uma DSL de trabalho completa, que você pode editar de acordo com suas necessidades. Normalmente, você escolheria o modelo mais próximo do que deseja criar.

5. Para esta explicação, escolha o modelo de **linguagem mínima** .

6. Insira uma extensão de nome de arquivo para sua DSL na página do assistente apropriada. Essa é a extensão que será usada pelos arquivos que contêm as instâncias de sua DSL.

   - Escolha uma extensão que não esteja associada a nenhum aplicativo em seu computador ou em qualquer computador em que você queira instalar a DSL. Por exemplo, **docx** e **htm** seriam extensões de nome de arquivo inaceitáveis.

   - O assistente o avisará se a extensão inserida está sendo usada como uma DSL. Considere usar uma extensão de nome de arquivo diferente. Também é possível redefinir a instância Experimental do SDK do Visual Studio para limpar os designers experimentais antigos. Clique em **Iniciar**, **todos os programas**, **Microsoft Visual Studio SDK 2010**, **ferramentas**e, em seguida, **redefina a instância experimental Microsoft Visual Studio 2010**.

7. Inspecione as outras páginas e clique em **concluir**.

    É gerada uma solução que contém dois projetos. Eles são nomeados DSL e DslPackage. Um arquivo de diagrama é aberto chamado DslDefinition. DSL.

   > [!NOTE]
   > A maior parte do código que você pode ver nas pastas nos dois projetos é gerada a partir de DslDefinition. DSL. Por esse motivo, a maioria das modificações em sua DSL é feita nesse arquivo.

   A interface do usuário agora se assemelha à imagem a seguir.

   ![Designer de DSL](../modeling/media/dsl-designer.png "dsl_designer")

   Essa solução define uma linguagem específica de domínio. Para obter mais informações, consulte [visão geral da interface do usuário do ferramentas de linguagem específica de domínio](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md).

## <a name="the-important-parts-of-the-dsl-solution"></a>As partes importantes da solução de DSL
 Observe os seguintes aspectos da nova solução.

- **Dsl\DslDefinition.DSL** Esse é o arquivo que você vê ao criar uma solução de DSL. Quase todo o código na solução é gerado a partir desse arquivo, e a maioria das alterações feitas em uma definição de DSL é feita aqui. Para obter mais informações, consulte trabalhando com o [diagrama de definição de trabalho de DSL](../modeling/working-with-the-dsl-definition-diagram.md).

- **Projeto DSL** Este projeto contém código que define a linguagem específica do domínio.

- **Projeto DslPackage** Este projeto contém código que permite que instâncias do DSL sejam abertas e editadas no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

## <a name="running-the-dsl"></a><a name="Debugging"></a>Executando a DSL
 Você pode executar a solução DSL assim que a tiver criado. Posteriormente, você pode modificar a definição de DSL gradualmente, executando a solução novamente após cada alteração.

#### <a name="to-experiment-with-the-dsl"></a>Para experimentar a DSL

1. Clique em **transformar todos os modelos** na barra de ferramentas Gerenciador de soluções. Isso regenera a maior parte do código-fonte de DslDefinition. DSL.

   > [!NOTE]
   > Sempre que você alterar DslDefinition. DSL, deverá clicar em **transformar todos os modelos** antes de recompilar a solução. Você pode automatizar esta etapa. Para obter mais informações, consulte [como automatizar a transformação de todos os modelos](https://msdn.microsoft.com/b63cfe20-fe5e-47cc-9506-59b29bca768a).

2. Pressione F5 ou, no menu **depurar** , clique em **Iniciar Depuração**.

    A DSL cria e é instalada na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

    Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciada. A instância experimental usa suas configurações de uma subárvore separada do registro, onde [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] as extensões são registradas para fins de depuração. As instâncias normais do não [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] têm acesso às extensões registradas lá.

3. Na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra o arquivo de modelo chamado **teste** de **Gerenciador de soluções**.

    \- ou –

    Clique com o botão direito do mouse no projeto de depuração, aponte para **Adicionar**e clique em **Item**. Na caixa de diálogo **Adicionar item** , selecione o tipo de arquivo de sua DSL.

    O arquivo de modelo é aberto como um diagrama em branco.

    A caixa de ferramentas é aberta e exibe as ferramentas apropriadas para o tipo de diagrama.

4. Use as ferramentas para criar formas e conectores no diagrama.

   1. Para criar formas, arraste do exemplo ferramenta Forma para o diagrama.

   2. Para conectar duas formas, clique na ferramenta de conector de exemplo, clique na primeira forma e, em seguida, clique na segunda forma.

5. Clique nos rótulos das formas para alterá-las.

   Seu experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] será semelhante ao exemplo a seguir:

   ![](../modeling/media/dsl-min.png "DSL_min")

### <a name="the-content-of-a-model"></a>O conteúdo de um modelo
 O conteúdo de um arquivo que é uma instância de uma DSL é chamado de *modelo*. O modelo contém *elementos de modelo* e *links* entre os elementos. A definição de DSL especifica que tipos de elementos de modelo e links podem existir no modelo. Por exemplo, em uma DSL criada a partir do modelo de linguagem mínima, há um tipo de elemento de modelo e um tipo de link.

 A definição de DSL pode especificar como o modelo aparece em um diagrama. Você pode escolher entre uma variedade de estilos de formas e conectores. Você pode especificar que algumas formas apareçam dentro de outras formas.

 Você pode exibir um modelo como uma árvore no modo de exibição do **Explorer** enquanto estiver editando um modelo. À medida que você adiciona formas ao diagrama, os elementos de modelo também aparecem no Gerenciador. O Gerenciador pode ser usado mesmo se não houver nenhum diagrama.

 Se você não conseguir ver o Explorer na instância de depuração do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , no menu **Exibir** aponte para **outras janelas**e clique em *\<Your Language>* **Gerenciador**.

### <a name="the-api-of-your-dsl"></a>A API de sua DSL
 Sua DSL gera uma API que permite que você leia e atualize modelos que são instâncias da DSL. Um aplicativo da API é para gerar arquivos de texto de um modelo. Para obter mais informações, consulte [geração de código em tempo de design usando modelos de texto T4](../modeling/design-time-code-generation-by-using-t4-text-templates.md).

 Na solução de depuração, abra os arquivos de modelo com a extensão ". tt". Esses exemplos demonstram como você pode gerar texto de modelos e permitem testar a API de sua DSL. Um dos exemplos é escrito em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] , o outro no [!INCLUDE[csprcs](../includes/csprcs-md.md)] .

 Em cada arquivo de modelo está o arquivo que ele gera. Expanda o arquivo de modelo em Gerenciador de Soluções e abra o arquivo gerado.

 O arquivo de modelo contém um pequeno segmento de código que lista todos os elementos no modelo.

 O arquivo gerado contém o resultado.

 Ao alterar um arquivo de modelo, você verá as alterações correspondentes nos arquivos gerados depois de regenerar os arquivos.

##### <a name="to-regenerate-text-files-after-you-change-the-model-file"></a>Para regenerar arquivos de texto depois de alterar o arquivo de modelo

1. Na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , salve o arquivo de modelo.

2. Certifique-se de que o parâmetro de nome de arquivo em cada arquivo. tt se refere ao arquivo de modelo que você está usando para experimentos. Salve o arquivo. tt.

3. Clique em **transformar todos os modelos** na barra de ferramentas de **Gerenciador de soluções**.

    \- ou –

    Clique com o botão direito do mouse nos modelos que você deseja regenerar e clique em **executar ferramenta personalizada**.

   Você pode adicionar qualquer número de arquivos de modelo de texto a um projeto. Cada modelo gera um arquivo de resultado.

> [!NOTE]
> Quando você altera a definição de DSL, o código de modelo de texto de exemplo não funcionará, a menos que você o atualize.

 Para obter mais informações, consulte [gerando código de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md) e [escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md).

## <a name="customizing-the-dsl"></a>Personalizando a DSL
 Quando você quiser modificar a definição de DSL, feche a instância experimental e atualize a definição na instância principal [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

> [!NOTE]
> Depois de modificar a definição de DSL, você pode perder informações nos modelos de teste que você criou usando versões anteriores.  Por exemplo, a solução de depuração contém um arquivo chamado Sample, que contém algumas formas e conectores. Depois de começar a desenvolver sua definição de DSL, elas não estarão visíveis e serão perdidas quando você salvar o arquivo.

 Você pode fazer uma ampla variedade de extensões para sua DSL. Os exemplos a seguir fornecerão uma impressão das possibilidades.

 Após cada alteração, salve a definição de DSL, clique em **transformar todos os modelos** em **Gerenciador de soluções**e pressione **F5** para experimentar o DSL alterado.

### <a name="rename-the-types-and-tools"></a>Renomear os tipos e as ferramentas
 Renomeie as classes e relações de domínio existentes. Por exemplo, a partir de uma definição de DSL criada com base no modelo de linguagem mínima, você pode executar as seguintes operações de renomeação para fazer com que a DSL represente árvores de família.

##### <a name="to-rename-domain-classes-relationships-and-tools"></a>Para renomear classes de domínio, relações e ferramentas

1. No diagrama DslDefinition, renomeie **ExampleModel** como **FamilyTreeModel**, **exampleelement** para **Person**, **targets** para **pais**e **fontes** para **filhos**. Você pode clicar em cada rótulo para alterá-lo.

     ![Diagrama de definição de DSL &#45; modelo de árvore da família](../modeling/media/familyt-person.png "FamilyT_Person")

2. Renomeie as ferramentas de elemento e conector.

    1. Abra a janela Gerenciador de DSL clicando na guia em Gerenciador de Soluções. Se você não puder vê-lo, no menu **Exibir** aponte para **outras janelas** e clique em **Gerenciador de DSL**. O Gerenciador de DSL só é visível quando o diagrama de definição de DSL é a janela ativa.

    2. Abra o janela Propriedades e posicione-o para que você possa ver o Gerenciador de DSL e as propriedades ao mesmo tempo.

    3. No Gerenciador de DSL, expanda **Editor**, **guias da caixa de ferramentas**, e, *\<your DSL>* em seguida, **ferramentas**.

    4. Clique no **exemploelement**. Esse é o item da caixa de ferramentas usado para criar elementos.

    5. No janela Propriedades, altere a propriedade **Name** para **Person**.

         Observe que a propriedade **Caption** também é alterada.

    6. Da mesma maneira, altere o nome da ferramenta **ExampleConnector** para **ParentLink**. Altere a propriedade **Caption** para que ela não seja uma cópia da propriedade Name. Por exemplo, insira **link pai**.

3. Reconstrua a DSL.

    1. Salve o arquivo de definição de DSL.

    2. Clique em **transformar todos os modelos** na barra de ferramentas de Gerenciador de soluções

    3. Pressione F5. Aguarde até que a instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] seja exibida.

4. Na solução de depuração na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra um arquivo de modelo de teste. Arraste elementos para ele na caixa de ferramentas. Observe que as legendas da ferramenta e os nomes de tipo no Gerenciador de DSL foram alterados.

5. Salve o arquivo de modelo.

6. Abra um arquivo. tt e substitua as ocorrências dos nomes de tipo e Propriedade antigos pelos novos nomes.

7. Verifique se o nome do arquivo especificado no arquivo. tt especifica seu modelo de teste.

8. Salve o arquivo. tt. Abra o arquivo gerado para ver o resultado da execução do código no arquivo. tt. Verifique se está correto.

### <a name="add-domain-properties-to-classes"></a>Adicionar propriedades de domínio a classes
 Adicione Propriedades a uma classe de domínio, por exemplo, para representar os anos de nascimento e morte de uma pessoa.

 Para tornar as novas propriedades visíveis no diagrama, você deve adicionar *decoradores* à forma que exibe o elemento de modelo. Você também deve mapear as propriedades para os decoradores.

##### <a name="to-add-properties-and-display-them"></a>Para adicionar propriedades e exibi-las

1. Adicione as propriedades.

   1. No diagrama de definição de DSL, clique com o botão direito do mouse na classe de domínio **Person** , aponte para **Adicionar**e clique em **propriedade de domínio**.

   2. Digite uma lista de novos nomes de propriedade, como **aniversário** e **morte**. Pressione **Enter** depois de cada um.

2. Adicione decoradores que exibirão as propriedades na forma.

   1. Siga a linha cinza que se estende da classe de domínio Person para o outro lado do diagrama. Este é um mapa de elementos de diagrama. Ele vincula a classe de domínio a uma classe Shape.

   2. Clique com o botão direito do mouse nessa classe de forma, aponte para **Adicionar**e clique em **decorador de texto**.

   3. Adicione dois decoradores com nomes como **BirthDecorator** e **DeathDecorator**.

   4. Selecione cada novo decorador e, na janela Propriedades, defina o campo **posição** . Isso determina onde o valor da propriedade de domínio será exibido na forma. Por exemplo, defina **InnerBottomLeft** e **InnerBottomRight**.

        ![Definição de forma de compartimento](../modeling/media/familyt-compartment.png "FamilyT_Compartment")

3. Mapeie os decoradores para as propriedades.

   1. Abra a janela Detalhes de DSL. Em geral, ele está em uma guia ao lado da janela saída. Se você não puder vê-lo, no menu **Exibir** , aponte para **outras janelas**e clique em **detalhes de DSL**.

   2. No diagrama de definição de DSL, clique na linha que conecta a classe de domínio **Person** à classe Shape.

   3. Em **detalhes de DSL**, na guia **mapas de decoradores** , clique na caixa de seleção em um decorador não mapeado. Em **Exibir Propriedade**, selecione a propriedade de domínio para a qual você deseja mapear. Por exemplo, mapeie **BirthDecorator** para **Birth**.

4. Salve a DSL, clique em transformar todos os modelos e pressione F5.

5. Em um diagrama de modelo de exemplo, verifique se agora você pode clicar nas posições escolhidas e digitar valores nelas. Além disso, quando você seleciona uma forma **Person** , a janela Propriedades exibe as novas propriedades Birth e morte.

6. Em um arquivo. TT, você pode adicionar código que obtém as propriedades de cada pessoa.

   ![Diagrama de árvore da família, caixa de ferramentas e Explorer](../modeling/media/familyt-instance.png "FamilyT_Instance")

### <a name="define-new-classes"></a>Definir novas classes
 Você pode adicionar classes de domínio e relações a um modelo. Por exemplo, você pode criar uma nova classe para representar cidades e uma nova relação para representar que uma pessoa se envidau em uma cidade.

 Para tornar os diferentes tipos distintos em um diagrama de modelo, você pode mapear as classes de domínio para diferentes tipos de forma ou formas com diferentes geometria e cores.

##### <a name="to-add-and-display-a-new-domain-class"></a>Para adicionar e exibir uma nova classe de domínio

1. Adicione uma classe de domínio e torne-a um filho da raiz do modelo.

    1. No diagrama de definição de DSL, clique na ferramenta de **relação incorporada** , clique na classe raiz **FamilyTreeModel**e, em seguida, clique em uma parte vazia do diagrama.

         Uma nova classe de domínio é exibida, que está conectada ao FamilyTreeModel com uma relação incorporada.

         Defina seu nome, por exemplo, **cidade**.

        > [!NOTE]
        > Cada classe de domínio, exceto a raiz do modelo, deve ser o destino de pelo menos uma relação de incorporação ou deve herdar de uma classe que é o destino de uma incorporação. Por esse motivo, muitas vezes é conveniente criar uma classe de domínio usando a ferramenta de relação incorporada.

    2. Adicione uma propriedade de domínio à nova classe, por exemplo **nome**.

2. Adicione uma relação de referência entre Person e cidade.

    1. Clique na ferramenta **relação de referência** , clique em pessoa e, em seguida, clique em cidade.

         ![Fragmento de definição de DSL: raiz da árvore da família](../modeling/media/familyt-root.png "FamilyT_Root")

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

         ![Definição de árvore da família com mapa de formas adicionado](../modeling/media/familyt-shapemap.png "FamilyT_ShapeMap")

6. Crie uma ferramenta de elemento para criar uma nova cidade.

    1. No **Gerenciador de DSL**, expanda o **Editor** e as guias da **caixa de ferramentas**.

    2. Clique com o botão direito do mouse *\<your DSL>* e clique em **Adicionar novo elemento ferramenta**.

    3. Defina a propriedade **Name** da nova ferramenta e defina sua propriedade de **classe** como cidade.

    4. Defina a propriedade do **ícone da caixa de ferramentas** . Clique em **[...]** e, no campo **nome do arquivo** , selecione um arquivo de ícone.

7. Crie uma ferramenta de conector para fazer um vínculo entre cidades e pessoas.

    1. Clique com o botão direito do mouse *\<your DSL>* e clique em **Adicionar nova ferramenta de conector**.

    2. Defina a propriedade Name da nova ferramenta.

    3. Na propriedade **ConnectionBuilder** , selecione o construtor que contém o nome da relação pessoa-cidade.

    4. Defina o **ícone da caixa de ferramentas**.

8. Salve a definição de DSL, clique em **transformar todos os modelos**e pressione **F5**.

9. Na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , abra um arquivo de modelo de teste. Use as novas ferramentas para criar cidades e links entre cidades e pessoas. Observe que você só pode criar links entre os tipos de elemento corretos.

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

     Quando você salvar o arquivo *. TT, ele criará um arquivo de subsidiária que contém a lista de pessoas e suas residências. Para obter mais informações, consulte [gerando código de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md).

## <a name="validation-and-commands"></a>Validação e comandos
 Você pode desenvolver essa DSL ainda mais adicionando restrições de validação. Essas restrições são métodos que você pode definir, que verificam se o modelo está em um estado correto. Por exemplo, você pode definir uma restrição para garantir que a data de nascimento de um filho seja posterior à de seus pais. O recurso de validação exibirá um aviso se o usuário DSL tentar salvar um modelo que interrompa qualquer uma das restrições. Para obter mais informações, consulte [validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md).

 Você também pode definir comandos de menu que o usuário pode invocar. Os comandos podem modificar o modelo. Eles também podem interagir com outros modelos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e com recursos externos. Para obter mais informações, consulte [como modificar um comando de menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

## <a name="deploying-the-dsl"></a>Implantando a DSL
 Para permitir que outros usuários usem a linguagem específica do domínio, você distribui um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] arquivo de extensão (VSIX). Isso é criado quando você cria a solução de DSL.

 Localize o arquivo. vsix na pasta bin da sua solução. Copie-o para o computador no qual você deseja instalá-lo. Nesse computador, clique duas vezes no arquivo VSIX. A DSL pode ser usada em todas as instâncias do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] no computador.

 Você pode usar o mesmo procedimento para instalar a DSL em seu próprio computador para não precisar usar a instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] .

 Para obter mais informações, confira [Implantando soluções de linguagem específica de domínio](../modeling/deploying-domain-specific-language-solutions.md).

## <a name="removing-old-experimental-dsls"></a><a name="Reset"></a>Removendo DSLs experimentais antigas
 Se você tiver criado DSLs experimentais que não deseja mais, poderá removê-las do computador redefinindo a [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] instância experimental.

 Isso removerá do seu computador todas as DSLs experimentais e outras extensões experimentais [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] . Essas são extensões que foram executadas no modo de depuração.

 Esse procedimento não remove DSLs ou outras [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões que foram totalmente instaladas executando o arquivo VSIX.

#### <a name="to-reset-the-visual-studio-experimental-instance"></a>Para redefinir a instância experimental do Visual Studio

1. Clique em **Iniciar**, **todos os programas**, **Microsoft Visual Studio SDK 2010**, **ferramentas**e, em seguida, **redefina a instância experimental Microsoft Visual Studio 2010**.

2. Reconstrua quaisquer DSLs experimentais ou outras extensões experimentais [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que você ainda deseja usar.

## <a name="see-also"></a>Consulte Também
 [Entendendo modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md) [como definir um](../modeling/how-to-define-a-domain-specific-language.md) [VISUALIZATON](https://www.microsoft.com/download/details.aspx?id=48148) de linguagem e um SDK de modelagem específicos de domínio
