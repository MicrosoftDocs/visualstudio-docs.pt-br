---
title: Como definir uma linguagem específica do domínio
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.domainrelationship
- vs.dsltools.dsldesigner.domainclass
- vs.dsltools.dsldesigner.domaintype
helpviewer_keywords:
- Domain-Specific Language, domain class
- Domain-Specific Language, external types
- Domain-Specific Language, relationships
- Domain-Specific Language, domain properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ca9cc6b853ea95cedcb0ce109b9618fc0eb455ba
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542747"
---
# <a name="how-to-define-a-domain-specific-language"></a>Como definir uma linguagem específica do domínio
Para definir uma DSL (linguagem específica de domínio), você cria uma solução do Visual Studio a partir de um modelo. A parte fundamental da solução é o diagrama de Definição de DSL, que é armazenado em DslDefinition.dsl. A Definição de DSL define as classes e formas da DSL. Depois de modificar e adicionar esses elementos, você pode adicionar o código do programa para personalizar a DSL com mais detalhes.

Se você for novo nas DSLs, recomendamos que você trabalhe no **laboratório de ferramentas DSL**, que pode ser encontrado neste site: [SDK de modelagem e visualização](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db)

## <a name="selecting-a-template-solution"></a><a name="templates"></a>Selecionando uma solução de modelo

Para definir uma DSL, é necessário ter instalados os seguintes componentes:

- Visual Studio
- Carga de trabalho de desenvolvimento de extensão do Visual Studio (inclui o SDK do Visual Studio)
- SDK de modelagem (instale-o como um componente individual no Visual Studio)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Para criar uma nova linguagem específica de domínio, você cria uma nova solução do Visual Studio usando o modelo de projeto de linguagem específica de domínio.

### <a name="to-create-a-dsl-solution"></a>Para criar uma solução DSL

1. Crie um novo projeto **de linguagem específica de domínio** .

   ::: moniker range="vs-2017"

    ![Criar caixa de diálogo DSL](../modeling/media/create_dsldialog.png)

   ::: moniker-end

    O **Assistente de linguagem específica de domínio** é aberto e exibe uma lista de soluções de modelo de DSL.

2. Clique em cada modelo para ver uma descrição. Escolha a solução que mais se assemelha ao que você deseja criar.

    Cada modelo DSL define uma DSL de trabalho básica. Você editará essa DSL para atender aos seus próprios requisitos.

    Clique em cada exemplo para obter mais informações.

   - Selecione **fluxo de tarefas** para criar uma DSL que tenha raias. As raias são partições verticais ou horizontais do diagrama.

   - Selecione **modelos de componente** para criar uma DSL que tem portas. As portas são pequenas formas na borda de uma forma maior.

   - Selecione **diagramas de classe** para definir uma DSL que tenha formas de compartimento. As formas do compartimento contêm listas de itens.

   - Selecione o **idioma mínimo** em outros casos ou, se você não tiver certeza.

   - Selecione o **designer do WinForm mínimo** ou o **designer do WPF mínimo** para criar uma DSL que é exibida em uma superfície do Windows Forms ou do WPF. Você precisará gravar um código para definir o editor. Para obter mais informações, consulte estes tópicos:

        [Criando uma linguagem específica do domínio baseada no Windows Forms](../modeling/creating-a-windows-forms-based-domain-specific-language.md)

        [Criando uma linguagem específica de domínio baseada no WPF](../modeling/creating-a-wpf-based-domain-specific-language.md)

3. Insira uma extensão de nome de arquivo para sua DSL na página do assistente apropriada. Essa é a extensão que será usada pelos arquivos que contêm as instâncias de sua DSL.

   - Escolha uma extensão de nome de arquivo que não esteja associada a nenhum aplicativo em seu computador ou em nenhum computador que você deseja instalar a DSL. Por exemplo, **docx** e **htm** seriam extensões de nome de arquivo inaceitáveis.

   - O assistente o avisará se a extensão inserida está sendo usada como uma DSL. Considere usar uma extensão de nome de arquivo diferente. Também é possível redefinir a instância Experimental do SDK do Visual Studio para limpar os designers experimentais antigos. Clique em **Iniciar**, **todos os programas**, **Microsoft Visual Studio SDK 2010**, **ferramentas**e, em seguida, **redefina a instância experimental Microsoft Visual Studio 2010**.

4. Você pode ajustar as configurações nas outras páginas ou manter os valores padrão.

5. Clique em **Concluir**.

    O assistente cria uma solução que contém dois ou três projetos e gera código a partir da definição da DSL.

   A interface do usuário agora se assemelha à imagem a seguir.

   ![Designer de DSL](../modeling/media/dsl_designer.png)

   Essa solução define uma linguagem específica de domínio. Para obter mais informações, consulte [visão geral da interface do usuário do ferramentas de linguagem específica de domínio](../modeling/overview-of-the-domain-specific-language-tools-user-interface.md).

### <a name="test-the-solution"></a>Testar a solução
 A solução de modelo fornece uma DSL de trabalho, que pode ser modificada ou usada da forma como se encontra.

 Para testar a solução, pressione F5 ou CTRL+F5. Uma nova instância do Visual Studio é aberta no modo experimental.

 Na nova instância do Visual Studio, em Gerenciador de Soluções, abra o arquivo de exemplo. Ele se abre como um diagrama, com uma caixa de ferramentas.

 Se você executar uma solução que você criou a partir do modelo de **linguagem mínima** , seu Visual Studio experimental será semelhante ao exemplo a seguir:

 ![Árvore de exemplo de linguagem específica de domínio no Visual Studio](../modeling/media/dsl_min.png)

 Experimente com as ferramentas. Crie elementos e os conecte.

 Feche a instância experimental do Visual Studio.

> [!NOTE]
> Após modificar a DSL, não será possível mais ver as formas no arquivo de teste Exemplo. Entretanto, poderá criar novos elementos.

### <a name="modifying-the-template-dsl"></a>Modificando a DSL do modelo
 Renomeie e mantenha algumas ou todas as classes de domínio e classes de formas na definição da DSL do modelo. Os novos nomes de classes devem ser nomes de CLR válidos, sem espaços ou pontuação.

 É especialmente útil manter estas classes:

- A classe raiz aparece no canto superior esquerdo do diagrama de definição de DSL, em **classes e relações**. Renomeie-a com um nome diferente da DSL. Por exemplo, uma DSL chamada **MusicLibrary** pode ter uma classe raiz chamada **Music**.

- A classe de diagrama aparece no canto inferior direito do diagrama de definição de DSL, na coluna **elementos de diagrama** . Talvez seja necessário rolar para a direita para vê-la. Normalmente, ele é chamado de**diagrama** _YourDsl_.

- Se você usou o modelo de **fluxo de tarefas** e deseja criar diagramas com raias, mantenha e renomeie a classe de domínio do ator e a forma ActorSwimlane.

  Exclua ou renomeie outras classes para atender aos seus requisitos.

## <a name="patterns-for-defining-a-dsl"></a><a name="patterns"></a>Padrões para definir uma DSL
 Recomendamos que você desenvolva uma DSL adicionando ou ajustando um ou dois recursos por vez. Adicione um recurso, execute a DSL e teste-a, em seguida, adicione um ou dois recursos adicionais. Um recurso típico de sua DSL pode ser:

- Uma classe de domínio, a relação de incorporação que conecta o elemento ao modelo, a forma necessária para exibir elementos dessa classe no diagrama e a ferramenta do elemento que permite aos usuários criar elementos.

- As propriedades de domínio de uma classe de domínio e os decoradores que as exibem em uma forma.

- Uma relação de referência e o conector que a exibe no diagrama, bem como a ferramenta de conector que permite aos usuários criar vínculos.

- Uma personalização que exige código do programa, tal como uma restrição de validação ou um comando de menu.

  As seções a seguir descrevem como construir os tipos mais úteis de recursos DSL. Há vários outros padrões com os quais uma DSL pode ser construída, mas esses são os usados com mais frequência.

> [!NOTE]
> Depois de adicionar um recurso, não se esqueça de clicar em **transformar todos os modelos** na barra de ferramentas de Gerenciador de soluções antes de compilar e executar sua DSL.

 A figura a seguir mostra as classes e relações que fazem parte da DSL usada de exemplo neste tópico.

 ![Incorporação e relações de referência](../modeling/media/music_classes.png)

 A próxima figura é um modelo de exemplo desta DSL:

 ![Modelo de instância da DSL gerada](../modeling/media/music_instance.png)

> [!NOTE]
> "Modelo" refere-se a uma instância de sua DSL que os usuários criam e geralmente é exibida como um diagrama. Este tópico discute o diagrama da Definição de DSL e os diagramas de modelo que aparecem quando sua DSL é usada.

## <a name="defining-domain-classes"></a><a name="classes"></a>Definindo classes de domínio
 As classes de domínio representam os conceitos de sua DSL. As instâncias são *elementos de modelo*. Por exemplo, em uma DSL **MusicLibrary** , você pode ter classes de domínio denominadas **Album** e **Song**.

 Para criar uma classe de domínio, você pode arrastar da ferramenta de **classe de domínio nomeada** para o diagrama e, em seguida, renomear a classe.

 Para obter mais informações, consulte [Propriedades de classes de domínio](../modeling/properties-of-domain-classes.md).

### <a name="create-an-embedding-relationship-for-each-domain-class"></a>Criar uma relação de incorporação para cada classe de domínio
 Cada classe de domínio, exceto a classe raiz, deve ser o destino de pelo menos uma relação incorporada ou ela deve herdar de uma classe que seja o destino de uma relação de incorporação.

 Em um modelo, todo elemento de modelo é um nó em uma única árvore de relações de incorporação. A origem e o destino de uma relação de incorporação são geralmente chamados de pai e filho.

 A seleção de um pai para uma classe de domínio depende de como você deseja que os tempos de vida de seus elementos dependam de outros elementos. Se um nó de uma árvore for excluído, sua subárvore geralmente também será excluída. Classes de elementos que tenham uma existência independente são, portanto, inseridas diretamente na classe raiz.

 Geralmente, ao exibir um elemento dentro de outro elemento, você deseja indicar uma relação de propriedade. Nesse caso, a classe pai mais apropriada é a classe do contêiner. A exceção é quando o item que você vê dentro de um contêiner é, na verdade, apenas um vínculo de referência a um elemento independente. Nesse caso, a exclusão do contêiner exclui a referência, mas não seu destino.

 Nos padrões de definição de DSL descritos neste tópico, assumiremos que os elementos exibidos dentro de um contêiner serão excluídos quando o contêiner for excluído. Esquemas mais complexos são possíveis e podem ser obtidos pela definição de regras.

|Como o elemento é exibido|Classe pai (incorporação)|Exemplo no modelo de solução DSL|
|-|-|-|
|Forma no diagrama.<br /><br /> Raia.|Classe raiz da DSL.|Linguagem Mínima.<br /><br /> Fluxo de Tarefa: classe Ator.|
|Forma na raia.|Classe de domínio de elementos que são exibidos como raias.|Fluxo de Tarefa: classe Tarefa.|
|Item na lista em forma, em que o item será excluído se o contêiner for excluído.<br /><br /> Porta na borda da forma.|Classe de domínio mapeada conforme a forma do contêiner.|Diagrama de classe: classe Atributo.<br /><br /> Diagrama de componente: classe Porta.|
|Item na lista, não excluído se o contêiner for excluído.|Classe raiz da DSL.<br /><br /> A lista exibe vínculos de referência.||
|Não exibido diretamente.|A classe da qual ela forma parte.||

 No exemplo de Biblioteca de Músicas, Álbuns são exibidos como retângulos nos quais os títulos das Canções são listados. Portanto, o pai de Álbum é a classe raiz Música e o pai de Canção é Álbum.

 Para criar uma classe de domínio e sua incorporação ao mesmo tempo, clique na ferramenta de **relação incorporada** , clique na classe pai e, em seguida, clique em uma parte em branco do diagrama.

 Geralmente não é necessário ajustar o nome da relação de incorporação e de suas funções, pois acompanharão os nomes de classes automaticamente.

 Para obter mais informações, consulte [Propriedades de relações de domínio](../modeling/properties-of-domain-relationships.md) e [Propriedades de funções de domínio](../modeling/properties-of-domain-roles.md).

> [!NOTE]
> Incorporação não é o mesmo que herança. Os filhos em uma relação de incorporação não herdam recursos de seus pais.

### <a name="add-domain-properties-to-each-domain-class"></a>Adicionar propriedades de domínio em cada classe de domínio
 As propriedades de domínio armazenam valores. Os exemplos são: Nome, Título, Data de Publicação.

 Clique em **Propriedades de domínio** na classe, pressione a tecla Enter e digite o nome de uma propriedade. O tipo padrão de uma propriedade de domínio é a Cadeia de Caracteres. Se você quiser alterar o tipo, selecione a propriedade de domínio e defina o **tipo** na janela **Propriedades** . Se o tipo desejado não estiver na lista suspensa, consulte [Adicionando tipos de propriedade](#addTypes).

 **Configure uma propriedade de Nome de Elemento.**  Selecione uma propriedade de domínio que possa ser usada para identificar elementos no gerenciador de linguagens. Por exemplo, na classe de domínio Canção que você poderia escolher a propriedade de domínio Título. Na janela **Propriedades** , defina **é o nome do elemento** como `true` .

### <a name="create-derived-domain-classes"></a>Criar classes de domínio derivadas
 Se você deseja que uma classe de domínio tenha variantes que herdam suas propriedades e relações, crie classes que derivam dela. Por exemplo, Álbum pode ter as classes derivadas WMA e MP3.

 Crie a classe derivada usando a ferramenta de **classe de domínio** .

 Clique na ferramenta de **herança** , clique na classe derivada e, em seguida, clique na classe base.

 Considere definir o **modificador de herança** da classe base como **abstract**. Se você acha que talvez precise de instâncias da classe base, considere, em vez disso, criar uma classe derivada separada para elas.

 As classes derivadas herdam as propriedades e funções de suas classes base.

### <a name="tidy-the-dsl-definition-diagram"></a>Organizar o diagrama de Definição de DSL
 Ao adicionar relações, algumas de suas classes aparecerão em mais de um lugar. Para reduzir o número de aparências e tornar o diagrama mais largo, clique com o botão direito do mouse na classe de destino de uma relação e clique em **colocar árvore aqui**. Para o efeito oposto, clique com o botão direito do mouse na classe de destino de uma relação e clique em **dividir árvore**. Se você não vir esses comandos de menu, certifique-se de que apenas a classe de domínio esteja escolhida.

 Use CTRL+Seta para Cima e CTRL+Seta para Baixo para mover as classes de domínio e as classes de forma.

### <a name="test-the-domain-classes"></a>Testar as classes de domínio

##### <a name="to-test-the-new-domain-classes"></a>Para testar as novas classes de domínio

1. **Clique em transformar todos os modelos** na barra de ferramentas de Gerenciador de soluções para gerar o código do designer de DSL. Você pode automatizar esta etapa. Para obter mais informações, consulte [como automatizar a transformação de todos os modelos](/previous-versions/visualstudio/visual-studio-2012/ff521399\(v\=vs.110\)).

2. **Compile e execute a DSL.** Pressione F5 ou CTRL + F5 para executar uma nova instância do Visual Studio no modo experimental. Na instância experimental do Visual Studio, abra ou crie um arquivo que tenha a extensão de nome de arquivo de sua DSL.

3. **Abra o Gerenciador.** No lado do diagrama está a janela Gerenciador de idiomas, que geralmente é chamada de *YourLanguage* Explorer. Se você não vir essa janela, ela pode estar em uma guia no Gerenciador de Soluções. Se você não conseguir encontrá-lo, no menu **Exibir** , aponte para **outras janelas**e clique em *YourLanguage* **Explorer**.

     Seu gerenciador apresentará uma exibição em árvore do modelo.

4. **Crie novos elementos.** Clique com o botão direito do mouse no nó raiz na parte superior e clique em **Adicionar novo**_yourClass_.

     Uma nova instância de sua classe aparecerá no Gerenciador de linguagens.

5. Verifique se cada instância possui um nome diferente ao criar novas instâncias. Isso ocorrerá somente se você tiver definido o sinalizador de **nome do elemento is** em uma propriedade de domínio.

6. **Examine as propriedades do domínio. Com uma instância de sua classe selecionada,** Inspecione o janela Propriedades. Ela deve mostrar as propriedades de domínio definidas nesta classe de domínio.

7. **Salve o arquivo, feche-o e abra-o novamente**. Após a expansão dos nós, todas as instâncias criadas devem estar visíveis no gerenciador.

## <a name="defining-shapes-on-the-diagram"></a><a name="shapes"></a>Definindo formas no diagrama
 Você pode definir as classes de elementos que aparecem em um diagrama como retângulos, elipses ou ícones.

#### <a name="to-define-a-class-of-elements-that-appear-as-shapes-on-a-diagram"></a>Para definir uma classe de elementos que aparece como formas em um diagrama

1. **Defina e teste uma classe de domínio conforme descrito em**  [definindo classes de domínio](#classes) **.**

   - O pai da classe deve ser a classe raiz. Ou seja, deve haver uma relação de incorporação entre a classe raiz e a nova classe de domínio.

   - Se o seu diagrama tiver raias, o pai pode ser a classe de domínio que é mapeada para uma raia. Antes de continuar com esse procedimento, consulte [definindo uma DSL que tem raias](#swimlanes).

2. **Adicione uma classe de forma** para representar os elementos no diagrama de modelo. Arraste de uma das seguintes ferramentas para o diagrama de Definição de DSL:

   - A **forma Geometry** fornece um retângulo ou uma elipse.

   - **Forma de imagem** exibe uma imagem que você fornece.

   - **Forma de compartimento** é um retângulo que contém uma ou mais listas de itens.

     Renomeie a classe de formas, a qual aparecerá no lado direito do diagrama de Definição de DSL, em Formas e Conectores.

3. **Defina uma imagem, se você tiver criado uma forma de imagem**.

   1. Crie um arquivo de imagem de qualquer tamanho. Os formatos BMP, JPEG, GIF e EMF são compatíveis.

   2. No Gerenciador de Soluções, adicione o arquivo à solução em Dsl\Resources.

   3. Retorne ao diagrama de Definição de DSL e selecione a nova classe de forma de imagem.

   4. Na janela Propriedades, clique na propriedade **imagem** .

   5. Na caixa de diálogo **selecionar imagem** , clique no menu suspenso em nome do **arquivo**e selecione a imagem.

4. **Adicione decoradores de texto à forma para exibir as propriedades do domínio.**

    Para exibir o nome ou o título do elemento de modelo, você provavelmente precisará de pelo menos um decorador de texto.

    Clique com o botão direito do mouse no cabeçalho da classe Shape, aponte para **Adicionar**e clique em **decorador de texto**. Defina o nome do decorador e, na janela Propriedades defina sua **posição**.

5. **Conecte cada forma com um elemento de diagrama mapeado para a classe de domínio que deve ser exibida**.

    Clique na ferramenta **mapa de elementos de diagrama** , clique na classe de domínio e, em seguida, clique na classe forma.

6. **Mapeie as propriedades para os decoradores de texto.**

   1. Selecione a linha cinza entre a classe de domínio e a classe de forma que representa o mapa de elemento do diagrama.

   2. Na janela **detalhes de DSL** , clique na guia **mapas de decoradores** . Se você não vir a janela **de detalhes de DSL** , no menu **Exibir** , aponte para **outras janelas** e clique em **detalhes de DSL**. Normalmente é necessário aumentar a parte superior desta janela para ver todo o seu conteúdo.

   3. Escolha o nome de um decorador. Em **Exibir Propriedade**, selecione o nome de uma propriedade da classe de domínio. Repita isso para cada decorador.

       Se você quiser exibir uma propriedade de um elemento relacionado, clique no navegador de árvore suspenso em **caminho para exibir a propriedade**.

   4. Certifique-se de que haja uma marca de seleção ao lado de cada nome de decorador.

      ![Mapeamentos de forma e janela de detalhes de DSL](../modeling/media/dsldetailswindow.png)

7. **Crie um item da caixa de ferramentas para criar elementos da classe de domínio.**

   1. No **Gerenciador de DSL**, expanda o nó do **Editor** e todos os seus subnós.

   2. Clique com o botão direito do mouse no nó em **guias da caixa de ferramentas** que tem o mesmo nome que a sua DSL, por exemplo, MusicLibrary. Clique em **Adicionar elemento ferramenta**.

       > [!NOTE]
       > Se você clicar com o botão direito do mouse no nó **ferramentas** , não verá a **ferramenta Adicionar elemento**. Em vez disso, clique no nó acima dele.

   3. Na janela Propriedades com a ferramenta novo elemento selecionada, defina **classe** como a classe de domínio que você adicionou recentemente.

   4. Defina a **legenda** e a **dica de ferramenta**.

   5. Defina o **ícone da caixa de ferramentas** como um ícone que será exibido na caixa de ferramentas. Você pode configurá-lo como um novo ícone ou um ícone já usado por outra ferramenta.

        Para criar um novo ícone, abra Dsl\Resources em **Gerenciador de soluções**. Copie e cole um dos arquivos BMP da ferramenta de elemento existente. Renomeie a cópia colada e clique duas vezes para editá-la.

        Retorne ao diagrama de definição de DSL, selecione a ferramenta e, na janela Propriedades clique em **[...]** no **ícone da caixa de ferramentas**. Na caixa de diálogo **selecionar bitmap** , selecione seu. Arquivo BMP no menu suspenso.

   Para obter mais informações, consulte [Propriedades de formas de geometria](../modeling/properties-of-geometry-shapes.md) e [Propriedades de formas de imagem](../modeling/properties-of-image-shapes.md).

#### <a name="to-test-shapes"></a>Para testar as formas

1. **Clique em transformar todos os modelos** na barra de ferramentas de Gerenciador de soluções para gerar o código do designer de DSL.

2. **Compile e execute a DSL.** Pressione F5 ou CTRL + F5 para executar uma nova instância do Visual Studio no modo experimental. Na instância experimental do Visual Studio, abra ou crie um arquivo que tenha a extensão de nome de arquivo de sua DSL.

3. **Verifique se as ferramentas de elemento aparecem na caixa de ferramentas.**

4. **Crie formas** arrastando de uma ferramenta para o diagrama de modelo.

5. **Verifique se cada decorador de texto é exibido** e se:

   1. Você pode editá-lo, a menos que tenha definido o sinalizador **is somente leitura da interface do usuário** na Propriedade Domain.

   2. Quando você edita a propriedade na janela Propriedades ou no decorador, a outra exibição é atualizada.

   Depois de testar inicialmente uma forma, talvez você queira ajustar algumas de suas propriedades e adicionar outros recursos mais avançados. Para obter mais informações, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="defining-reference-relationships"></a><a name="references"></a>Definindo relações de referência
 Você pode definir uma relação de referência entre qualquer classe de domínio de origem e qualquer classe de domínio de destino. As relações de referência são geralmente exibidas em um diagrama como conectores, que são linhas entre formas.

 Por exemplo, se Álbuns de música e Artistas forem exibidos como formas no diagrama, será possível definir um relação chamada ArtistsAppearedOnAlbums, a qual vincula os Artistas aos Álbuns nos quais eles trabalharam. Veja o exemplo na figura.

 ![Modelo de instância da DSL gerada](../modeling/media/music_instance.png)

 As relações de referência também podem vincular elementos do mesmo tipo. Por exemplo, em uma DSL que representa uma árvore genealógica, a relação entre pais e seus filhos é uma relação de referência de Pessoa a Pessoa.

### <a name="define-a-reference-relationship"></a>Definir uma relação de referência
 Clique na ferramenta Relação de Referência, na classe de domínio de origem da relação e na classe de domínio de destino. A classe de destino pode ser a mesma que a classe de origem.

 Cada relação possui duas funções, representadas pela linha de cada lado da caixa de relação. Você pode selecionar cada função e configurar suas propriedades na janela Propriedades.

 **Considere renomear as funções**. Por exemplo, em uma relação entre Pessoa e Pessoa, talvez você queira alterar os nomes padrão para Pais e Filhos, Gerente e Subordinados, Professor e Aluno, etc.

 **Ajuste as multiplicidades de cada função**, se necessário. Se você deseja que cada Pessoa tenha no máximo um Gerente, configure a multiplicidade que aparece abaixo do rótulo Gerente no diagrama como 0..1.

 **Adicione propriedades de domínio à relação.**  Na figura, a relação Artista-Álbum tem uma propriedade de função.

 **Defina a propriedade permitir duplicatas da relação,** se mais de um link da mesma classe puder existir entre o mesmo par de elementos de modelo. Por exemplo, você poderia permitir que um Professor ensinasse mais de uma Matéria para o mesmo Aluno.

 ![Mapas de formas para conectores](../modeling/media/music_connector.png)

 Para obter mais informações, consulte [Propriedades de relações de domínio](../modeling/properties-of-domain-relationships.md) e [Propriedades de funções de domínio](../modeling/properties-of-domain-roles.md).

### <a name="define-a-connector-to-display-the-relationship"></a>Definir um conector para exibir a relação
 Um conector exibe uma linha entre duas formas no diagrama do modelo.

 Arraste a ferramenta **conector** para o diagrama de definição de DSL.

 Adicione decoradores de texto se desejar exibir rótulos no conector. Configure suas posições. Para permitir que o usuário mova um decorador de texto, defina sua propriedade **Moveable** .

 Use a ferramenta **mapa de elementos de diagrama** para vincular o conector à relação de referência.

 Com o mapa de elementos de diagrama selecionado, abra a janela **detalhes de DSL** e abra a guia **mapas de decoradores** .

 Selecione cada **decorador** e defina a **propriedade Display** como a propriedade de domínio correta.

 Verifique se uma marca de seleção aparece ao lado de cada item na lista **decoradores** .

### <a name="define-a-connection-builder-tool"></a>Definir uma ferramenta do construtor de conexões
 Na janela **Gerenciador de DSL** , expanda o nó do **Editor** e todos os seus subnós.

 Clique com o botão direito do mouse no nó que tem o mesmo nome que a sua DSL e clique em **Adicionar nova ferramenta de conexão**.

 Enquanto a nova ferramenta estiver selecionada, na janela Propriedades:

- Defina a **legenda** e a **dica de ferramenta**.

- Clique em **Construtor de conexões** e selecione o construtor apropriado para a nova relação.

- Defina o **ícone da caixa de ferramentas** como o ícone que você deseja que apareça na caixa de ferramentas. Você pode configurá-lo como um novo ícone ou um ícone já usado por outra ferramenta.

     Para criar um novo ícone, abra Dsl\Resources em **Gerenciador de soluções**. Copie e cole um dos arquivos BMP da ferramenta de elemento existente. Renomeie a cópia colada e clique duas vezes para editá-la.

     Retorne ao diagrama de definição de DSL, selecione a ferramenta e, na janela Propriedades clique em **[...]** no **ícone da caixa de ferramentas**. Na caixa de diálogo **selecionar bitmap** , selecione seu. Arquivo BMP no menu suspenso.

##### <a name="to-test-a-reference-relationship-and-connector"></a>Para Testar um relação de Referência e um Conector

1. **Clique em transformar todos os modelos** na barra de ferramentas de Gerenciador de soluções para gerar o código do designer de DSL.

2. **Compile e execute a DSL.** Pressione F5 ou CTRL + F5 para executar uma nova instância do Visual Studio no modo experimental. Na instância experimental do Visual Studio, abra ou crie um arquivo que tenha a extensão de nome de arquivo de sua DSL.

3. **Verifique se a ferramenta de conexão aparece na caixa de ferramentas.**

4. **Crie formas** arrastando de uma ferramenta para o diagrama de modelo.

5. **Crie conexões** entre as formas. Clique na ferramenta do conector, em uma forma e em outra forma.

6. **Verifique se você não pode criar conexões entre classes inadequadas.**  Por exemplo, se a sua relação for entre Álbuns e Artistas, verifique se não é possível vincular Artistas a Artistas.

7. **Verifique se as multiplicidades estão corretas. Por exemplo, verifique se você não pode conectar uma pessoa a mais de um gerente.**

8. **Verifique se cada decorador de texto é exibido** e se:

   1. Você pode editá-lo, a menos que tenha definido o sinalizador **is somente leitura da interface do usuário** na Propriedade Domain.

   2. Quando você edita a propriedade na janela Propriedades ou no decorador, a outra exibição é atualizada.

   Depois de testar inicialmente um conector, talvez você queira ajustar algumas de suas propriedades e adicionar outros recursos mais avançados. Para obter mais informações, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="defining-shapes-that-contain-lists-compartment-shapes"></a><a name="compartments"></a>Definindo formas que contêm listas: formas de compartimento
 Uma forma do compartimento contém uma ou mais listas de itens. Por exemplo, em uma DSL de Biblioteca de Músicas, você poderia usar formas do compartimento para representar os Álbuns de música. Em cada Álbum, há uma lista de Canções.

 ![Forma de compartimento](../modeling/media/compartmentshape.png)

 No método mais simples de obter esse efeito em uma definição de DSL, você define uma classe de domínio para o contêiner e uma classe de domínio para cada lista. A classe de contêiner é mapeada para a forma do compartimento.

 ![Mapa de formas](../modeling/media/music_mapcomp.png)

 Para obter mais informações, consulte [Propriedades de formas de compartimento](../modeling/properties-of-compartment-shapes.md).

#### <a name="to-define-a-compartment-shape"></a>Para definir uma forma do compartimento

1. **Crie a classe de domínio do contêiner**. Clique na ferramenta de **relação incorporada** , clique na classe raiz do modelo e, em seguida, clique em uma parte em branco do diagrama de definição de DSL. Com isso, você cria a classe de domínio chamada Álbum na figura de exemplo.

     Como alternativa, em vez de incorporar na classe raiz, você pode incorporar o contêiner em uma classe de domínio que seja mapeada para uma raia.

     Adicione uma propriedade de domínio, como nome à classe, e defina seu sinalizador de **nome de elemento** no janela Propriedades.

2. **Crie a classe de domínio do item de lista**. Clique na ferramenta de **relação incorporada** , clique na classe de contêiner (álbum) e, em seguida, clique em uma parte em branco do diagrama. Com isso, você cria a classe de domínio chamada Canção na figura de exemplo.

     Adicione uma propriedade de domínio, como título à classe, e defina seu sinalizador de **nome de elemento** .

     Adicione outras propriedades de domínio.

     Adicione outra classe de domínio do item de lista que você deseja exibir.

3. **Para misturar vários tipos de item na lista**, crie classes que herdam da classe List. Torne a classe de lista abstrata definindo seu **modificador de herança**.

     Por exemplo, se você desejar que música clássica seja classificada por compositor em vez de por artista, é possível criar duas subclasses de Canção, ClassicalSong e NonClassicalSong.

4. **Crie a forma de compartimento**. Arraste da ferramenta **forma de compartimento** até o diagrama de definição de DSL.

     Adicione um decorador de texto e defina seu nome.

     Adicione um compartimento e defina seu nome.

5. Para permitir que o usuário oculte os compartimentos de lista, clique com o botão direito do mouse na classe de forma do compartimento, aponte para **Adicionar**e clique em **expandir/recolher decorador**. Na janela Propriedades, configure a posição do decorador.

6. Clique na ferramenta **mapa de elementos de diagrama** , clique na classe de domínio de contêiner e, em seguida, clique na forma de compartimento.

7. Selecione o vínculo de mapa do elemento do diagrama entre a classe de domínio e a forma. Na janela **detalhes de DSL** :

    1. Clique na guia **decoradores** . Clique no nome do decorador e selecione o item apropriado em **Exibir Propriedade**. Certifique-se de que exista uma marca de seleção ao lado do nome do decorador.

    2. Clique na guia **mapas de compartimentos** .

         Clique no nome do compartimento.

         Em **caminho da coleção de elementos exibidos**, navegue até a classe de elemento de lista (música). Clique na seta suspensa para usar a ferramenta de navegador.

         Em **Exibir Propriedade**, selecione a propriedade que deve ser exibida na lista. No exemplo, será Título.

> [!NOTE]
> Usando os campos Caminho nos campos de Mapa do Decorador e Mapa de Compartimento, é possível tornar as relações entre as classes de domínio e a forma do compartimento mais complexas.

#### <a name="to-define-a-tool-for-creating-the-shape"></a>Para definir uma ferramenta para criar a forma

1. **Crie um item da caixa de ferramentas para criar elementos da classe de domínio.**

2. No **Gerenciador de DSL**, expanda o nó do **Editor** e todos os seus subnós.

3. Clique com o botão direito do mouse no nó em **guias da caixa de ferramentas** que tem o mesmo nome que a sua DSL, por exemplo, MusicLibrary. Clique em **Adicionar elemento ferramenta**.

    > [!NOTE]
    > Se você clicar com o botão direito do mouse no nó **ferramentas** , não verá a **ferramenta Adicionar elemento**. Em vez disso, clique no nó acima dele.

4. Na janela Propriedades com a ferramenta novo elemento selecionada, defina **classe** como a classe de domínio que você adicionou recentemente.

5. Defina a **legenda** e a **dica de ferramenta**.

6. Defina o **ícone da caixa de ferramentas** como um ícone que será exibido na caixa de ferramentas. Você pode configurá-lo como um novo ícone ou um ícone já usado por outra ferramenta.

     Para criar um novo ícone, abra Dsl\Resources em **Gerenciador de soluções**. Copie e cole um dos arquivos .BMP da ferramenta de elemento existente. Renomeie a cópia colada e clique duas vezes para editá-la.

     Retorne ao diagrama de definição de DSL, selecione a ferramenta e, na janela Propriedades clique em **[...]** no **ícone da caixa de ferramentas**. Na caixa de diálogo **selecionar bitmap** , selecione o arquivo BMP no menu suspenso.

#### <a name="to-test-a-compartment-shape"></a>Para testar uma forma do compartimento

1. **Clique em transformar todos os modelos** na barra de ferramentas de Gerenciador de soluções para gerar o código do designer de DSL.

2. **Compile e execute a DSL.** Pressione F5 ou CTRL + F5 para executar uma nova instância do Visual Studio no modo experimental. Na instância experimental do Visual Studio, abra ou crie um arquivo que tenha a extensão de nome de arquivo de sua DSL.

3. **Verifique se a ferramenta aparece na caixa de ferramentas.**

4. Arraste a ferramenta para o diagrama de modelo. Com isso, uma forma é criada.

    Verifique se o nome do elemento aparece e é configurado automaticamente como um valor padrão.

5. Clique com o botão direito do mouse no cabeçalho da nova forma e clique em Adicionar *seu item de lista.* No exemplo, o comando é Adicionar Canção.

    Verifique se aparece um item na lista e se ele tem um novo nome.

6. Clique em um dos itens da lista e examine a janela Propriedades. Você deve ver as propriedades dos itens da lista.

7. Abra o Gerenciador de linguagens. Verifique se você pode ver os nós do contêiner com os nós do item de lista dentro.

   ![Gerenciador de DSL gerado](../modeling/media/music_explorer.png)

   Depois de testar inicialmente uma forma do compartimento, talvez você queira ajustar algumas de suas propriedades e adicionar outros recursos mais avançados. Para obter mais informações, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

### <a name="displaying-a-reference-link-in-a-compartment"></a>Exibindo um vínculo de referência em um compartimento
 Geralmente, um elemento que você exibe em um compartimento é um filho do elemento que é representado pela forma do compartimento. No entanto, algumas vezes, você pode desejar exibir um elemento que esteja vinculado a ele com uma relação de referência.

 Por exemplo, podemos adicionar um segundo compartimento a AlbumShape que exibe uma lista dos Artistas que estão vinculados ao Álbum.

 Nesse caso, o compartimento deve exibir o vínculo, e não o elemento referenciado. Isso ocorre porque quando o usuário seleciona o item no compartimento e pressiona DELETE, ele deseja que o link seja excluído, e não o elemento referenciado.

 Entretanto, é possível fazer com que o nome do elemento referenciado apareça no compartimento.

 O procedimento a seguir pressupõe que você já tenha criado a classe de domínio, a relação de referência, a forma do compartimento e o mapa de elemento de diagrama, conforme descrito anteriormente nesta seção.

##### <a name="to-display-a-reference-link-in-a-compartment"></a>Para exibir um vínculo de referência em um compartimento

1. **Adicione um compartimento à forma de compartimento**. No diagrama de definição de DSL, clique com o botão direito do mouse na classe forma do compartimento, aponte para **Adicionar**e clique em **compartimento**.

2. Defina o **caminho da coleção de elementos exibidos** para navegar até o link, em vez de seu elemento de destino. Clique no menu suspenso e use a exibição em árvore para selecionar a relação de referência em vez de seu destino. No exemplo, a relação é **ArtistAppearedOnAlbums**.

3. Defina **caminho para exibir a propriedade** para navegar do link para o elemento de destino. No exemplo, isso é **artista**.

4. Defina a **propriedade de exibição** como a propriedade apropriada do elemento de destino, por exemplo, **nome**.

5. **Transforme todos os modelos**, compile e execute a DSL e abra um modelo de teste.

6. No diagrama de modelo, crie as classes de forma apropriadas, defina seus nomes e crie um vínculo entre eles. Na forma do compartimento, devem aparecer os nomes dos elementos vinculados.

7. Selecione o vínculo ou o item na forma do compartimento. O vínculo e o item devem desaparecer.

## <a name="defining-ports-on-the-boundary-of-another-shape"></a><a name="ports"></a>Definindo portas no limite de outra forma
 Uma porta é uma forma que está localizada no limite de outra forma.

 As portas também podem ser usadas para fornecer um ponto de conexão fixo em outra forma, no qual o usuário pode desenhar conectores. Nesse caso, você pode tornar a forma da porta transparente.

 Para ver um exemplo que usa portas, selecione o modelo de **diagrama de componente** ao criar uma nova solução de DSL. Este exemplo mostra os pontos principais que você pode considerar ao definir as portas:

- Há uma classe de domínio que representa o contêiner das portas, `Component`.

- Há uma classe de domínio que representa portas. no exemplo, é `ComponentPort`.

- Há uma relação de incorporação da classe de domínio de contêiner à classe de domínio de porta. Para obter mais informações, consulte [definindo classes de domínio](#classes).

- Se você deseja combinar tipos diferentes de portas no mesmo contêiner, é possível criar subclasses da classe de domínio da porta. No exemplo, `InPort` e `OutPort` são herdados de `ComponentPort`.

- A classe de domínio de contêiner pode ser mapeada para qualquer tipo de forma. No exemplo, ela é `ComponentShape`. Para obter mais informações, consulte [definindo formas](#shapes).

- As classes de domínio de porta são mapeadas para formas de porta. Você pode mapear as classes derivadas para classes de forma de porta separadas ou mapear a classe base para uma classe de forma de porta.

  Em outros aspectos, as formas de porta se comportam conforme descrito em [definindo formas](#shapes).

  Para obter mais informações, consulte [Propriedades de formas de porta](../modeling/properties-of-port-shapes.md).

## <a name="defining-a-dsl-that-has-swimlanes"></a><a name="swimlanes"></a>Definindo uma DSL que tem raias
 As raias são uma partição horizontal ou vertical de um diagrama. Cada raia corresponde a um elemento de modelo. Sua definição de DSL requer uma classe de domínio para os elementos de raia.

 A melhor maneira de criar uma DSL com raias é criar uma nova solução DSL e escolher o modelo de solução Fluxo de Tarefa. Na Definição de DSL, a classe Ator é a classe de domínio mapeada para a raia. Renomeie essa e as outras classes da forma adequada ao seu projeto.

 Para adicionar uma classe que será exibida como uma forma dentro de uma raia, crie uma Relação de Incorporação entre a classe de raia e sua nova classe. Os usuários poderão arrastar elementos de uma raia para outra, mas cada elemento estará sempre dentro de uma raia específica. No modelo de solução Fluxo de Tarefa, FlowElement é um filho da classe de raia.

 Para adicionar uma classe que será exibida como uma forma independentemente de raias, crie uma Relação de Incorporação entre a classe raiz e sua nova classe. Os usuários poderão colocar essas formas em qualquer lugar no diagrama, inclusive nos limites de raias e fora das raias. No modelo de solução Fluxo de Tarefa, Comment é um filho da classe raiz.

 Para obter mais informações, consulte [Propriedades de raias](../modeling/properties-of-swimlanes.md).

## <a name="adding-property-types"></a><a name="addTypes"></a>Adicionando tipos de propriedade

### <a name="domain-enumerations-and-literals"></a>Enumerações e literais de domínio
 Uma enumeração de domínio é um tipo com vários valores de literais.

 Para adicionar uma enumeração de domínio, clique com o botão direito do mouse na raiz do modelo no **Gerenciador de DSL** e clique em **Adicionar nova enumeração de domínio**. O elemento aparecerá no **Gerenciador de DSL** no nó **tipos de domínio** . Esse elemento não aparece no diagrama.

 Para adicionar literais de enumeração à enumeração de domínio, clique com o botão direito do mouse na enumeração de domínio no **Gerenciador de DSL** e clique em **Adicionar novo literal de enumeração**.

 Por padrão, uma propriedade que possui um tipo de enumeração pode ser configurada para somente um valor de enumeração por vez. Se você quiser que os usuários e programadores possam definir qualquer combinação de valores – um "campo de bits"-defina a propriedade **IsFlags** da enumeração.

### <a name="external-types"></a>Tipos externos
 Ao definir o tipo de uma propriedade de domínio, se você não encontrar o tipo desejado na lista suspensa **tipo** , poderá adicionar um tipo externo. Por exemplo, você pode adicionar o tipo de **sistema. Drawing. Color** à lista.

 Para adicionar um tipo, clique com o botão direito do mouse na raiz do modelo no Gerenciador de DSL e clique em **Adicionar novo tipo externo**. Na janela Propriedades, defina o nome como **cor** e o namespace como **System. Drawing**. Esse tipo agora aparece no Gerenciador de DSL em **tipos de domínio**. Você pode escolhê-lo sempre que definir o tipo de uma propriedade de domínio.

## <a name="customizing-the-dsl"></a><a name="custom"></a>Personalizando a DSL
 Usando as técnicas descritas neste tópico, é possível criar com rapidez uma DSL com uma notação diagramática, uma forma XML legível e as ferramentas básicas necessárias para gerar código e outros artefatos.

 Há dois métodos de extensão da definição de DSL:

1. Ajuste a DSL usando mais recursos da Definição de DSL. Por exemplo, você pode criar uma única ferramenta de conector capaz de criar vários tipos de conectores e você pode controlar as regras com as quais a exclusão de um elemento também exclui elementos relacionados. Essas técnicas são obtidas, em sua maioria, ao configurar valores na Definição de DSL, e alguns deles necessitam de algumas linhas do código do programa.

     Para obter mais informações, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

2. Estenda suas ferramentas de modelagem usando o código do programa para obter efeitos mais avançados. Por exemplo, você pode criar comandos de menu que alteram o modelo e você pode criar ferramentas que integram duas ou mais DSLs. O VMSDK foi projetado especificamente para facilitar a integração de suas extensões com o código gerado a partir da Definição de DSL.  Para obter mais informações, consulte [escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md).

### <a name="changing-the-dsl-definition"></a>Alterando a definição de DSL
 Ao criar qualquer item em uma definição de DSL, diversos valores padrão são configurados automaticamente. Depois de configurados, você poderá alterá-los. Isso simplifica o desenvolvimento de uma DSL e ainda permite personalizações avançadas.

 Por exemplo, quando você mapeia uma forma para um elemento, o Caminho do Elemento Pai do mapeamento é configurado automaticamente, de acordo com a relação de incorporação da classe de domínio. Entretanto, se posteriormente você alterar a relação de incorporação, o caminho do elemento pai não é alterado automaticamente.

 Você deve, portanto, estar ciente de que ao alterar algumas relações em sua Definição de DSL, não é incomum que erros sejam relatados ao salvar a definição ou ao Transformar Todos os Modelos. A maioria dos erros é fácil de corrigir. Clique duas vezes no relatório de erros para ver o local do erro.

 Consulte também [como: alterar o namespace de uma linguagem específica de domínio](../modeling/how-to-change-the-namespace-of-a-domain-specific-language.md).

## <a name="troubleshooting"></a><a name="trouble"></a> Solução de problemas
 A tabela a seguir lista alguns dos problemas mais comuns encontrados ao projetar uma DSL, junto com as sugestões para sua solução. Mais conselhos estão disponíveis no [Fórum de extensibilidade das ferramentas de visualização](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=dslvsarchx).

| Problema | Sugestão |
|-|-|
| As alterações feitas no arquivo de Definição de DSL não surtiram efeito. | Clique em **transformar todos os modelos** na barra de ferramentas acima Gerenciador de soluções e recompile a solução. |
| As formas mostram o nome de um decorador em vez do valor de propriedade. | Configure o mapeamento do decorador. No diagrama de Definição de DSL, clique no mapa do elemento do diagrama, que é a linha cinza entre a classe de domínio e a classe de forma.<br /><br /> Abra a janela **detalhes de DSL** . Se você não puder vê-lo, no menu Exibir, aponte para **outras janelas**e clique em **detalhes de DSL**.<br /><br /> Clique na guia **mapas de decoradores** . Selecione o nome do decorador. Certifique-se de que a caixa ao lado esteja marcada. Em **Exibir Propriedade**, selecione o nome de uma propriedade de domínio.<br /><br /> Para obter mais informações, consulte [formas no diagrama](#shapes). |
| Não consigo adicionar uma coleção no Gerenciador de DSL. Por exemplo, quando clico com o botão direito do mouse em Ferramentas, não encontro o comando "Adicionar Ferramenta" no menu.<br /><br /> No gerenciador de minha DSL, não consigo adicionar um elemento à lista. | Clique com o botão direito do mouse no item acima do nó ao qual você está tentando adicionar elementos. Quando desejar adicionar elementos a uma lista, o comando Adicionar não estará no nó da lista, mas em seu proprietário. |
| Criei uma classe de domínio, mas não consigo criar instâncias no gerenciador de linguagens. | Cada classe de domínio, exceto a raiz, deve ser o destino de uma relação de incorporação. |
| No gerenciador de minha DSL, os elementos são mostrados somente com seus nomes de tipos. | Na definição de DSL, selecione uma propriedade de domínio da classe e, na janela Propriedades, defina **é o nome do elemento** como verdadeiro. |
| Minha DSL sempre é aberta no editor XML. | Isso pode ocorrer em função de um erro durante a leitura do arquivo. No entanto, mesmo após a correção desse erro, você deve redefinir explicitamente o editor para que seja o designer de DSL.<br /><br /> Clique com o botão direito do mouse no item de projeto, clique em **abrir com** e selecione * YourLanguage ***Designer (padrão)**. |
| A caixa de ferramentas de minha DSL não aparece após a mudança de nomes do assembly. | Inspecione e atualize o **DslPackage\GeneratedCode\Package.tt** para obter mais informações, consulte [como alterar o namespace de uma linguagem específica de domínio](../modeling/how-to-change-the-namespace-of-a-domain-specific-language.md). |
| A caixa de ferramentas de minha DSL não aparece, mas não alterei o nome do assembly.<br /><br /> Ou, uma caixa de mensagens aparece relatando a falha ao carregar uma extensão. | Redefina a instância experimental e recompile sua solução.<br /><br /> 1. no menu Iniciar do Windows, em **todos os programas**, expanda [!INCLUDE[vssdk_current_long](../misc/includes/vssdk_current_long_md.md)] , depois em **ferramentas**e clique em **redefinir a instância experimental Microsoft Visual Studio**.<br />2. no menu **Compilar** , clique em **Recompilar solução**. |

## <a name="see-also"></a>Confira também

- [Introdução às linguagens específicas do domínio](../modeling/getting-started-with-domain-specific-languages.md)
- [Criando uma linguagem específica do domínio baseada no Windows Forms](../modeling/creating-a-windows-forms-based-domain-specific-language.md)
- [Criando uma linguagem específica de domínio baseada no WPF](../modeling/creating-a-wpf-based-domain-specific-language.md)
