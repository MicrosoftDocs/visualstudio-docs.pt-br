---
title: Editar modelos e diagramas UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.modelingproject
- vs.teamarch.UMLModelExplorer
- vs.teamarch.UMLModelExplorer.rootnode
helpviewer_keywords:
- diagrams - modeling
- UML, copy and paste
- UML, models
- UML model
- UML, element properties
- UML
- UML, diagrams
ms.assetid: 87affd40-8127-4ee9-9d3a-ad977abe2ed6
caps.latest.revision: 86
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 92d2be3abfb849b0b5cf5c1c820040b658e2240c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803429"
---
# <a name="edit-uml-models-and-diagrams"></a>Editar modelos e diagramas UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode criar e editar um modelo UML por meio de modos de exibição fornecidos por vários tipos diferentes de diagrama. Fornecendo diferentes perspectivas em seu sistema, esses diagramas ajudarão-lo a entender e discutir aspectos diferentes de seus requisitos e design. O Visual Studio fornece modelos para cinco dos mais usados com frequência os tipos de diagrama UML.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Este tópico descreve técnicas para editar o modelo que são comuns entre os tipos de diagramas diferentes. Para obter mais informações específicas a determinados tipos de diagramas, consulte [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md).  
  
## <a name="in-this-topic"></a>Neste tópico  
  
-   [Diagramas de UML são exibições de um modelo UML](#Views)  
  
-   [Criar diagramas de modelagem UML](#Creating)  
  
-   [Desenhar diagramas de modelagem UML](#Drawing)  
  
-   [Edição de formas e conectores](#Editing)  
  
-   [Desfazendo alterações ao modelo](#Undo)  
  
-   [Compartilhamento de elementos entre diagramas](#Sharing)  
  
-   [Copiando elementos e grupos de elementos relacionados](#Copying)  
  
-   [A exclusão de um elemento de modelo ou seus modos de exibição](#Deleting)  
  
-   [Pesquisando texto em um diagrama](#Searching)  
  
-   [Preparando um diagrama para apresentação](#presentation)  
  
-   [Estendendo os Designers UML](#extensions)  
  
##  <a name="Views"></a> Diagramas de UML são exibições de um modelo UML  
 Você pode criar e usar diagramas de UML apenas em projetos de modelagem. Para obter mais informações sobre como criar diagramas e projetos, consulte [diagramas e projetos de modelagem UML criar](../modeling/create-uml-modeling-projects-and-diagrams.md).  
  
-   Um projeto de modelagem contém um único modelo UML. Cada diagrama UML no projeto é um modo de exibição de modelo UML.  
  
-   Você pode ver o modelo no **Gerenciador de modelos UML**. Sobre o **arquitetura** , aponte para **Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
-   Cada forma em um diagrama é um modo de exibição de um elemento no modelo. Quando você coloca uma nova forma em um diagrama, você está criando um novo elemento no modelo.  
  
-   Quando você salvar qualquer diagrama, o Visual Studio salva o modelo inteiro, todos os seus diagramas e a modelagem de arquivo de projeto.  
  
##  <a name="Creating"></a> Criar diagramas de modelagem UML  
  
1. Sobre o **arquitetura** menu no Visual Studio, clique em **UML novo ou diagrama de camada**.  
  
2. Selecione e nomeie seu diagrama.  
  
3. Na **adicionar ao projeto de modelagem**, selecione um projeto de modelagem existente ou selecione **criar um novo projeto de modelagem**.  
  
   > [!NOTE]
   >  Um diagrama de modelagem deve estar dentro de um projeto de modelagem.  
  
   Você também pode adicionar um diagrama em um projeto de modelagem existente no Gerenciador de soluções. Clique com botão direito no projeto de modelagem, aponte para **Add**e, em seguida, clique em **Novo Item**.  
  
#### <a name="to-create-an-empty-uml-modeling-project"></a>Para criar um projeto de modelagem UML vazio  
  
- No **arquivo** , aponte para **New**, clique em **projeto**e, no **novo projeto** caixa de diálogo, clique duas vezes em **de modelagem Projetos**.  
  
  Para obter mais informações sobre como gerenciar projetos de modelagem, consulte [diagramas e projetos de modelagem UML criar](../modeling/create-uml-modeling-projects-and-diagrams.md).  
  
##  <a name="Drawing"></a> Desenhar diagramas de modelagem UML  
 Um diagrama de modelagem exibe uma coleção de elementos de modelo vinculada por relações. Cada elemento é exibido como uma forma e cada relação é exibida como um conector entre duas formas.  
  
 Há dois tipos de ferramentas, para elementos de um para relações. Por exemplo, no diagrama de classe UML caixa de ferramentas **classe** é uma ferramenta de elemento, e **associação** é uma ferramenta de relação.  
  
> [!NOTE]
>  Se você quiser obter informações específicas para tipos de diagrama específico, consulte [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md).  
  
#### <a name="to-create-elements-and-relationships-in-a-uml-modeling-diagram"></a>Para criar elementos e relações em um diagrama de modelagem UML  
  
1. Para criar um elemento de modelo, clique em uma ferramenta de elemento na caixa de ferramentas e, em seguida, clique no diagrama de onde você deseja que ele apareça. Depois de criar o elemento, ajuste seu tamanho e forma arrastando suas alças.  
  
    Em alguns casos, você pode colocar um novo elemento dentro de outro elemento. Por exemplo, em um diagrama de classe UML, você pode colocar uma classe dentro de um pacote.  
  
   > [!NOTE]
   >  Se você não conseguir ver a caixa de ferramentas, clique em **caixa de ferramentas** sobre o **exibição** menu.  
  
2. Para criar uma relação, clique em uma ferramenta de relação, clique no elemento onde você deseja que a relação para iniciar e, em seguida, clique no elemento de onde você deseja que ele termine.  
  
    Diferentes tipos de relações podem iniciar ou terminar em diferentes tipos de elementos. Por exemplo, em um diagrama de classe UML, uma relação de associação não pode iniciar ou terminar em um elemento de comentário.  
  
   > [!NOTE]
   >  Para usar a mesma ferramenta várias vezes, clique duas vezes a ferramenta. Quando você tiver terminado, clique o **ponteiro** ferramenta.  
  
   Alguns tipos de diagramas, você também pode desenhar formas simples. Essas formas não são parte do modelo, mas você pode usá-los para chamar atenção para partes do diagrama ou dividi-la em áreas diferentes.  
  
##  <a name="Editing"></a> Edição de formas e conectores  
 Quando você redimensiona uma forma de cor ou redirecionar um conector, não há nenhum efeito sobre o modelo subjacente. No entanto, quando você renomeia uma forma no diagrama ou no Gerenciador de modelos UML, o elemento correspondente é renomeado no Gerenciador de modelos UML e em outros diagramas que apresentam esse elemento.  
  
> [!NOTE]
>  Há uma maneira simples de fazer novos itens de caixa de ferramentas da qual você pode criar grupos de elementos ou elementos com sua própria escolha Propriedades. Para obter mais informações, consulte [definir um personalizado item de caixa de ferramentas de modelagem](../modeling/define-a-custom-modeling-toolbox-item.md).  
  
 A figura a seguir mostra como alterar o tamanho de uma forma ou seu nome.  
  
 ![Ajustando um elemento de modelo](../modeling/media/uml-drawadjust1.png "UML_DrawAdjust1")  
  
> [!TIP]
>  Os comandos internos não incluem um comando para organizadamente alinhar formas. No entanto, você pode criar facilmente seu próprio comando de alinhamento, copiando o código no exemplo na [exibir um modelo UML em diagramas](../modeling/display-a-uml-model-on-diagrams.md).  
  
 A figura a seguir mostra como ajustar a rota e a posição de um conector ou seus rótulos.  
  
 ![Ajustando um conector](../modeling/media/uml-drawadjust2.png "UML_DrawAdjust2")  
  
#### <a name="to-move-one-end-of-a-connector-to-another-shape"></a>Para mover uma extremidade de um conector para outra forma  
  
1. Siga um destes procedimentos:  
  
   - Pressione **CTRL** e move a extremidade.  
  
     \- ou -  
  
   - O conector com o botão direito e, em seguida, clique em **reconectar**.  
  
2. Clique no final do conector que você deseja mover.  
  
3. Clique na forma que você deseja mover para o conector.  
  
#### <a name="to-change-color-or-other-properties-of-an-element-relationship-or-diagram"></a>Para alterar a cor ou outras propriedades de um elemento, relação, ou de diagrama  
  
-   Clique no elemento e defina os campos na **propriedades** janela.  
  
     Se você não conseguir ver a **propriedades** , clique com botão direito do elemento e, em seguida, clique em **propriedades.**  
  
#### <a name="to-zoom-in-and-out-on-a-modeling-diagram"></a>Para ampliar e reduzir em um diagrama de modelagem  
  
-   Pressione e segure a **CTRL** pressionada ao girar a roda do mouse.  
  
     \- ou -  
  
-   Pressione e segure **CTRL + SHIFT**e, em seguida, clique no botão esquerdo ou direito do mouse.  
  
     \- ou -  
  
-   Sobre o **Designers de arquitetura** barra de ferramentas, clique no sinal de adição (**+**) ou sinal de subtração (**-**), ou escolha um nível de zoom.  
  
##  <a name="Searching"></a> Pesquisando em um diagrama  
 A função Localizar rápido encontrará itens em um diagrama. Você deve definir **xaminar:** à **documento atual**.  
  
#### <a name="to-search-for-text-in-a-modeling-diagram"></a>Para pesquisar texto em um diagrama de modelagem  
  
1.  Pressione **CTRL + F**.  
  
     \- ou -  
  
     Sobre o **edite** , aponte para **localizar e substituir**e, em seguida, clique em **localização rápida**.  
  
    > [!NOTE]
    >  No **localizar e substituir** caixa de diálogo, você deve deixar o **examinar** campo definido como **documento atual**. Não há suporte para as outras opções.  
  
2.  Digite o texto que você deseja localizar e, em seguida, clique em **Localizar próximo**.  
  
    > [!NOTE]
    >  Se o texto que você deseja localizar estiver dentro de uma forma recolhida, a forma será realçada. Expandir a forma e, em seguida, clique em **Localizar próximo** novamente.  
  
##  <a name="Undo"></a> Desfazendo alterações ao modelo  
 Você pode desfazer e refazer alterações que você fez para o modelo e os diagramas usando o **desfazer** e **Refazer** os comandos no **editar** menu.  
  
 **Cada projeto de modelagem tem uma única pilha de alterações.** Todas as alterações feitas no modelo e os diagramas são mantidas nessa pilha. A pilha também inclui alterações de foco de um diagrama para outro. O comando Desfazer reverte as alterações nessa pilha.  
  
 Por exemplo, digamos que você executar essas operações: faça uma alteração diagrama1; Altere o foco para o diagrama 2; Altere Diagram2. Quando você desfaz as alterações, o primeiro desfazer reverterá a última alteração; o próximo desfazer mudar o foco volta para o diagrama 1; e o terceiro desfazer reverterá a alteração ao diagrama 1.  
  
 **Um diagrama de fechamento trunca a pilha de alterações.** Se você fechar um diagrama, você não pode desfazer as alterações que você executou no diagrama, e você não pode desfazer as alterações anteriores para o modelo ou qualquer um dos seus diagramas.  
  
 **Você não pode desfazer enquanto você estiver editando uma propriedade.** Enquanto você estiver editando uma propriedade na janela Propriedades, ou em um diagrama de um rótulo, só é possível desfazer as alterações feitas nessa propriedade. Concluir a alteração na propriedade pressionando ENTER ou cancelá-la pressionando ESC. Em seguida, você poderá desfazer as alterações no modelo e diagramas.  
  
 **Fechar um diagrama sem salvar pode não ter o efeito esperado.** Se você fazer algumas alterações e, em seguida, fecha um diagrama sem salvá-lo, suas alterações ainda serão preservadas no modelo. É recomendável fechar o modelo inteiro, se você quiser fazer isso sem salvá-lo.  
  
##  <a name="Sharing"></a> Compartilhamento de elementos entre diagramas  
 Você pode fazer com que uma instância específica de um elemento de modelo aparecer mais de uma vez em seus diagramas. Isso se aplica a classes, interfaces, componentes, casos de uso e atores.  
  
 Isso é útil se você quiser mostrar grupos diferentes de relações em diagramas diferentes. Por exemplo, em um diagrama, você poderia mostrar as associações entre as classes de cliente e o endereço. Em outro diagrama, você poderia mostrar novamente, a classe de endereço com sua associação à área Postal.  
  
 Você pode alterar as propriedades de um elemento de modelo, como seu nome, selecionando qualquer um dos seus modos de exibição em qualquer diagrama, ou selecionando-o no Gerenciador de modelos UML.  
  
 Cada tipo de diagrama pode mostrar apenas alguns tipos de elemento de modelo. Por exemplo, você não pode mostrar um caso de uso em um diagrama de componente. Portanto, os procedimentos a seguir funcionará apenas para algumas combinações de elemento de modelo e o diagrama.  
  
#### <a name="to-add-a-new-view-of-a-model-element-by-using-uml-model-explorer"></a>Para adicionar uma nova exibição de um elemento de modelo usando o Gerenciador de modelos UML  
  
1.  Para abrir **Gerenciador de modelos UML**diante de **arquitetura** , aponte para **Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
2.  Arraste o elemento de modelo da **Gerenciador de modelos UML** a um diagrama compatível no mesmo projeto.  
  
     Uma forma de fornecer que uma exibição do elemento de modelo é exibida, que pode ser além das exibições em outros diagramas ou no mesmo diagrama.  
  
    > [!NOTE]
    >  O efeito é diferente quando você arrasta uma classe ou um componente para um diagrama de sequência. Nesse caso, uma nova linha da vida é criada cujo tipo é a classe ou componente. Para obter mais informações, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).  
  
#### <a name="to-add-a-new-view-of-a-model-element-by-using-paste-reference"></a>Para adicionar uma nova exibição de um elemento de modelo usando Colar referência  
  
1.  Um elemento existente com o botão direito e, em seguida, clique em **cópia**.  
  
    -   Você pode copiar vários elementos ao mesmo tempo. Mantenha pressionada a tecla CTRL enquanto clica em cada elemento, clique em um deles e, em seguida, clique em **cópia**.  
  
2.  Uma parte vazia de um diagrama de compatível com o botão direito e, em seguida, clique em **Colar referência**.  
  
     Outro modo de exibição do mesmo elemento aparece.  
  
    > [!NOTE]
    >  Isso difere de **colar** comando, que cria um novo elemento no modelo. Para obter mais informações, consulte [copiando elementos e grupos de elementos relacionados](#Copying).  
  
> [!NOTE]
>  Se você adicionar um modos de exibição de diagrama de dois elementos de modelo que já estão conectados por uma relação, uma exibição da relação também aparecerão no diagrama. Você pode excluir este modo de exibição somente, removendo um dos elementos do diagrama ou excluindo a relação do modelo.  
  
##  <a name="Copying"></a> Copiando elementos e grupos de elementos relacionados  
 Você pode copiar e colar os elementos de modelo, e você pode copiar e colar os grupos de elementos junto com as relações entre eles.  
  
> [!NOTE]
>  O **colar** e **Colar referência** comandos têm efeitos diferentes. **Colar** cria novos elementos cujas propriedades serão semelhantes dos elementos copiados. **Colar referência** cria novos modos de exibição os mesmos elementos.  
  
#### <a name="to-copy-elements-and-their-relationships"></a>Para copiar elementos e suas relações  
  
1.  No diagrama com os elementos que você deseja copiar, selecione um ou mais elementos.  
  
    > [!NOTE]
    >  É possível copiar as relações, exceto como parte de um grupo de elementos.  
  
2.  Sobre o **edite** menu, clique em **cópia**.  
  
3.  Se você quiser copiar os elementos para outro diagrama, crie o novo diagrama ou abra o diagrama existente.  
  
4.  Sobre o **edite** menu, clique em **colar**.  
  
    -   Cópias dos elementos são exibidas, junto com cópias de todas as relações que vinculam entre eles.  
  
    -   Cada novo elemento terá um novo nome gerado automaticamente.  
  
5.  Ajuste as posições, nomes e outras propriedades dos novos elementos e relações.  
  
> [!NOTE]
>  É possível copiar um elemento de modelo de um modelo para outro, por exemplo, se você tiver dois modelos na mesma solução. Mas você pode copiar elementos de um diagrama para outro.  
  
#### <a name="to-copy-an-entire-diagram"></a>Para copiar o diagrama inteiro  
  
1. Crie um novo diagrama.  
  
2. Selecione todos os elementos em um diagrama existente, copiá-los e colá-los em um novo.  
  
   Você não pode replicar um diagrama, copiando e colando no Gerenciador de soluções.  
  
##  <a name="Deleting"></a> A exclusão de um elemento de modelo ou seus modos de exibição  
 Alguns tipos de elementos, especificamente os classificadores, podem ser removidos de um diagrama sem excluí-las do modelo. Classificadores são os elementos principais que são exibidos em diagramas de classe, diagramas de componente e usam diagramas de caso. Eles podem aparecer em mais de um diagrama. Para esses tipos de elementos, há dois comandos separados: **remover do diagrama** e **excluir do modelo**.  
  
 Por outro lado, quando você exclui uma relação de um diagrama, você sempre é excluí-lo do modelo.  
  
> [!NOTE]
>  Determinados tipos de elementos em um diagrama UML têm rótulos. Quando você seleciona a esses elementos ao desenhar um retângulo ao redor deles, é possível selecionar os rótulos, mas não os elementos que possuem esses rótulos. Não há suporte para a exclusão de um subconjunto de elementos que são selecionadas dessa maneira. Para selecionar um subconjunto desses elementos, pressione e segure a **CTRL** pressionada enquanto você clica em cada elemento.  
  
#### <a name="to-remove-a-classifiers-view-from-a-diagram"></a>Para remover o modo de exibição do classificador de um diagrama  
  
- O elemento no diagrama com o botão direito e, em seguida, clique em **remover do diagrama**.  
  
  \- ou -  
  
- Clique no elemento no diagrama e, em seguida, pressione a **excluir** chave.  
  
  -   Este modo de exibição do elemento desaparece. No entanto, o elemento permanece no modelo, e você ainda pode encontrá-lo no **Gerenciador de modelos UML**. Outros modos de exibição do mesmo elemento também permanecem.  
  
  -   Cada conector que termina nessa forma é removida do diagrama, mas a relação que ele representa permanece no modelo. Você pode ver a relação na **Gerenciador de modelos UML** sob **relações**, em cada elemento que ele se conecta.  
  
#### <a name="to-delete-an-element-from-the-model"></a>Para excluir um elemento do modelo  
  
-   Clique com botão direito do elemento ou em **Gerenciador de modelos UML** ou em um diagrama e clique **excluir do modelo**.  
  
    -   O elemento é excluído de todos os diagramas no qual ele aparece.  
  
    -   Todo relacionamento que termina nesse elemento também é excluído do modelo.  
  
#### <a name="to-delete-a-relationship-from-the-model"></a>Para excluir uma relação do modelo  
  
-   Clique com botão direito na relação em um diagrama ou no **Gerenciador de modelos UML**e, em seguida, clique em **excluir do modelo**.  
  
    > [!CAUTION]
    >  É possível remover uma relação de um diagrama sem removê-lo do modelo.  
  
     A relação é excluída do modelo e é excluída de todos os diagramas no qual ele aparece.  
  
##  <a name="presentation"></a> Preparando um diagrama para apresentação  
 Os seguintes recursos ajudam você a chamar a atenção para determinados partes de seu diagrama, adicionar explicações ou dividir um diagrama em diferentes áreas de interesse.  
  
-   Você pode copiar qualquer parte de um diagrama em uma palavra, PowerPoint ou outro documento. Selecione as formas e conectores desejado, clique com botão direito e, em seguida, clique em **cópia**.  
  
-   A cor de qualquer forma ou conector pode ser alterada. Selecione uma ou mais formas e altere o **cor** propriedade. Se você não conseguir ver a janela **Propriedades**, pressione **F4**.  
  
-   Diagramas de alguns tipos, você pode desenhar linhas, retângulos e elipses do **formas simples** seção da caixa de ferramentas. Essas formas não fazem parte do modelo de UML.  
  
-   Para rotular uma área, você pode arrastar um comentário na caixa de ferramentas e, em seguida, defina suas **Transparent** propriedade **verdadeiro**. Como formas simples, os comentários não fazem parte do modelo de UML e não aparecem no Gerenciador de modelos UML.  
  
-   Para adicionar anotações e explicações para elementos de modelo, você pode criar comentários e, em seguida, vinculá-los para os elementos.  
  
-   Para alinhar claramente uma coluna ou linha o formas no diagrama, você pode instalar o comando Alinhar formas. Isso está disponível como uma extensão UML de exemplo: [UML: comando para alinhar formas](http://code.msdn.microsoft.com/UML-command-to-Align-4139c0d7)  
  
### <a name="to-export-a-diagram-as-an-image"></a>Para exportar um diagrama como uma imagem  
 Para obter mais informações, consulte [exportar diagramas como imagens](../modeling/export-diagrams-as-images.md).  
  
##  <a name="extensions"></a> Estendendo os Designers UML  
 Você pode adicionar uma nova funcionalidade para as ferramentas UML e se adaptar a notação de diagrama com suas necessidades. Para obter mais informações, consulte [modelos e diagramas UML estender](../modeling/extend-uml-models-and-diagrams.md).  
  
 Há várias extensões de exemplo disponíveis. Você apenas pode instalar e usá-los, ou você pode usar o código-fonte como base para suas próprias extensões. Os exemplos incluem:  
  
|||  
|-|-|  
|[Alinhar formas](http://code.msdn.microsoft.com/UML-command-to-Align-4139c0d7)|Comando de menu que ajuda você a organizar um diagrama.|  
|[Vincular ao docs](http://code.msdn.microsoft.com/Link-UML-elements-to-0adbf5a8)|Vincule a qualquer elemento UML títulos do Word, slides do PowerPoint, arquivos de qualquer tipo, diagramas de UML ou outros elementos UML. O link pode ser feito simplesmente arrastando. Posteriormente, você pode clicar duas vezes no elemento para ver o item vinculado. Por exemplo, você poderia vincular casos de uso de ações de storyboard slides ou diagramas de atividade detalhados e especificações do Word.|  
|[Entrada rápida](http://code.msdn.microsoft.com/UML-Rapid-Entry-using-Text-0813ad8a)|Crie um modelo rapidamente usando a entrada de texto. Útil para capturar ideias em reuniões.|  
|[Cor por estereótipo](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)|Classes de acordo com o estereótipo de cores. Você pode estender facilmente o código funcione para seus próprios estereótipos.|  
|[Modelagem de domínio](http://code.msdn.microsoft.com/UML-Domain-Modeling-6df6f7f4)|Padrões convenientes para modelos de negócios. Associações são mostradas sem setas por padrão, e as operações não aparecem em classes.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar diagramas e projetos de modelagem UML](../modeling/create-uml-modeling-projects-and-diagrams.md)   
 [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)   
 [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)



