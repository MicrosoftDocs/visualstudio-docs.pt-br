---
title: Definir pacotes e namespaces | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML model, namespaces
- UML, namespaces
- UML, packages
- UML model, packages
ms.assetid: 79147068-02d5-4b70-933d-f647c1da3829
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: b9295b5af83270069df11e6460ee85dfe0fd9c73
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741901"
---
# <a name="define-packages-and-namespaces"></a>Definir pacotes e namespaces
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, uma *pacote* é um contêiner para as definições dos elementos UML, como classes, casos de uso e componentes. Um pacote também pode conter outros pacotes.  
  
 No Gerenciador de modelos UML, todas as definições de dentro de um pacote são aninhadas sob o pacote. O modelo UML é um tipo de pacote e forma a raiz da árvore.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="in-this-topic"></a>Neste tópico  
 [Namespaces](#Namespaces)  
  
 [Criar e exibir pacotes](#Packages)  
  
 [Criar elementos de modelo dentro de pacotes](#Elements)  
  
 [Movendo elementos dentro ou fora de um pacote](#Moving)  
  
 [Colar elementos em um pacote](#Pasting)  
  
 [Importar relações entre os pacotes](#Import)  
  
 [Referências de um Namespace para outra](#References)  
  
 [Propriedades de pacotes](#Properties)  
  
##  <a name="Namespaces"></a> Namespaces  
 Os pacotes são úteis para separar o trabalho em áreas diferentes. Cada pacote define um namespace para que os nomes que são definidos em pacotes diferentes não entram em conflito uns com os outros.  
  
 A propriedade de nome qualificado de cada elemento é o nome qualificado do pacote ao qual ele pertence, seguido do nome do elemento. Por exemplo, se o pacote é chamado `MyPackage`, uma classe dentro do pacote terá um nome qualificado, como `MyPackage::MyClass`. Como cada elemento está contido dentro de um modelo, cada nome qualificado começa com o nome do modelo.  
  
 Um modelo também define um namespace, para que o nome qualificado de cada elemento em um modelo começa com o nome do modelo.  
  
 Outros elementos de modelo também definem namespaces. Por exemplo, uma operação pertence ao namespace definido por sua classe pai, para que seu nome qualificado é como `MyModel ::MyPackage ::MyClass ::MyOperation`. Da mesma maneira, uma ação pertence ao namespace definido pela sua atividade pai.  
  
 Os pacotes são contêineres. Se você mover ou excluir um pacote, as classes, pacotes e outras coisas definidas dentro dele são também movidas ou excluídas. O mesmo é verdadeiro para outros elementos que definem os namespaces.  
  
##  <a name="Packages"></a> Criar e exibir pacotes  
 Você pode criar um pacote em um diagrama de classe UML ou no Gerenciador de modelos UML.  
  
#### <a name="to-create-a-package-in-a-uml-class-diagram"></a>Para criar um pacote em um diagrama de classe UML  
  
1.  Abra um diagrama de classe UML ou criar um novo.  
  
2.  Clique o **pacote** ferramenta.  
  
3.  Clique em qualquer lugar no diagrama. Uma nova forma de pacote será exibido.  
  
     Você pode clicar dentro de um pacote existente para aninhar um pacote em outro.  
  
4.  Digite um novo nome para o pacote.  
  
#### <a name="to-create-a-package-in-uml-model-explorer"></a>Para criar um pacote no Gerenciador de modelos UML  
  
1. Abra **Gerenciador de modelos UML**. Sobre o **arquitetura** , aponte para **Windows**e, em seguida, clique no **Gerenciador de modelos UML**.  
  
2. Clique com botão direito um pacote ou um modelo ao qual você deseja adicionar um novo pacote.  
  
   > [!NOTE]
   >  Você pode aninhar um pacote dentro de outro pacote.  
  
3. Aponte para **Add** e, em seguida, clique em **pacote**.  
  
    Um novo pacote é exibido no modelo.  
  
4. Digite um novo nome para o pacote.  
  
   Se você tiver criado um pacote no Gerenciador de modelos UML, você pode exibi-lo em um diagrama de classe UML. Você também pode exibir um pacote em mais de um diagrama de classes UML.  
  
#### <a name="to-show-an-existing-package-on-a-uml-class-diagram"></a>Para mostrar um pacote existente em um diagrama de classe UML  
  
-   Arraste o pacote do Gerenciador de modelos UML para o diagrama de classe.  
  
    > [!NOTE]
    >  Isso cria um modo de exibição do pacote neste diagrama. Ele não necessariamente mostrará todos os elementos que o pacote contém. Para certificar-se de que você vê que todo o conteúdo do pacote, exibi-lo no Gerenciador de modelos UML.  
  
##  <a name="Elements"></a> Criar elementos de modelo dentro de pacotes  
 Há quatro maneiras em que você pode colocar os elementos de modelo dentro de um pacote:  
  
- Adicione um novo elemento a um pacote no Gerenciador de modelos UML.  
  
- Adicione classes e outros tipos de pacotes em um diagrama de classe UML.  
  
- Defina as **LinkedPackage** propriedade de um diagrama para que novos elementos criados no diagrama são colocados dentro do pacote que você especificar. Diagramas de classe, diagramas de componente e diagramas de caso de uso podem ser vinculados a um pacote dessa maneira.  
  
- Mova elementos para dentro ou fora de um pacote no Gerenciador de modelos UML.  
  
  Um elemento em um pacote é exibido sob o pacote no Gerenciador de modelos UML e seu nome qualificado começa com o nome qualificado do pacote. Para ver o nome qualificado de qualquer elemento, o elemento com o botão direito e, em seguida, clique em **propriedades**. O **nome qualificado** propriedade aparece na **propriedades** janela.  
  
#### <a name="to-create-an-element-in-a-package-in-uml-model-explorer"></a>Para criar um elemento em um pacote no Gerenciador de modelos UML  
  
1.  Abra **Gerenciador de modelos UML**. Sobre o **modo de exibição** , aponte para **Other Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
2.  Clique com botão direito um pacote ou um modelo ao qual você deseja adicionar um novo elemento.  
  
3.  Aponte para **adicionar**e, em seguida, clique no tipo de elemento que você deseja adicionar.  
  
     O novo elemento aparece sob o pacote.  
  
4.  Digite um nome para o novo elemento.  
  
    > [!NOTE]
    >  O novo elemento não aparece em qualquer diagrama. Para criar um modo de exibição do novo elemento, você pode arrastá-lo do Gerenciador de modelos UML para um diagrama. O diagrama deve ser um tipo que exibirá esse tipo de elemento.  
  
#### <a name="to-create-an-element-in-a-package-on-a-uml-class-diagram"></a>Para criar um elemento em um pacote em um diagrama de classe UML  
  
1.  Abra um diagrama de classe na qual o pacote é exibida.  
  
    -   Crie um novo pacote, se você ainda não tiver feito isso.  
  
    -   Para fazer com que um pacote existente aparecer em um diagrama de classe, você pode arrastar o pacote a partir **Gerenciador de modelos UML** para o diagrama de classe.  
  
2.  Clique na ferramenta para uma classe, interface ou enumeração ou pacote.  
  
3.  Clique no pacote no qual você deseja colocar o novo elemento.  
  
     O novo elemento é exibido dentro do pacote.  
  
#### <a name="to-create-all-the-elements-of-a-diagram-in-a-specified-package"></a>Para criar todos os elementos de um diagrama em um pacote especificado  
  
1.  Crie o pacote, se você ainda não tiver feito isso.  
  
2.  Abra um diagrama de componente, o diagrama de caso de uso ou o diagrama de classe UML.  
  
3.  Abra as propriedades do diagrama. Clique com botão direito em uma parte em branco do diagrama e, em seguida, clique em **propriedades**.  
  
4.  No **pacote vinculado** propriedade, escolha o pacote que você deseja que contenha o conteúdo do diagrama.  
  
5.  Crie novos elementos no diagrama. Eles serão colocados no pacote.  
  
    -   O **nome qualificado** de cada elemento começará com o nome do pacote qualificado.  
  
    -   Na **Gerenciador de modelos UML**, cada elemento será exibido sob o pacote.  
  
##  <a name="Moving"></a> Movendo elementos dentro e fora de pacotes  
 Você pode mover um ou mais elementos dentro ou fora de um pacote.  
  
 Se você mover um pacote, tudo dentro dele será movido com ele.  
  
#### <a name="to-move-an-element-into-or-out-of-a-package"></a>Para mover um elemento dentro ou fora de um pacote  
  
-   No Gerenciador de modelos UML, arraste o elemento dentro ou fora da árvore cuja raiz é o pacote.  
  
     O nome qualificado do elemento será alterado para mostrar seu novo pacote de proprietário ou o modelo.  
  
     \- ou -  
  
-   Em um diagrama de classe, arraste o elemento em uma forma de pacote.  
  
     O nome qualificado do elemento será alterado para mostrar o novo pacote de proprietário.  
  
    > [!NOTE]
    >  Se você arrastar um elemento fora de um pacote em uma parte em branco do diagrama, seu pacote proprietário não é alterado. Isso permite que você faça um diagrama que mostra os elementos de vários pacotes sem a necessidade de mostrar os pacotes em si.  
  
##  <a name="Pasting"></a> Colar elementos em um pacote  
 Você pode colar um elemento em um pacote. Se você colar um grupo de elementos relacionados em um pacote, as relações entre elas também serão coladas.  
  
#### <a name="to-paste-elements-into-a-package-on-a-uml-class-diagram"></a>Para colar elementos em um pacote em um diagrama de classe UML  
  
1.  Em um diagrama de classe UML, selecione todos os elementos que você deseja copiar. Clique em um deles e, em seguida, clique em **cópia**.  
  
2.  O pacote com o botão direito e, em seguida, clique em **colar**.  
  
    > [!NOTE]
    >  O pacote pode estar em um diagrama de diferente.  
  
##  <a name="Import"></a> Importar relações entre os pacotes  
 Você pode definir uma relação de importação entre pacotes, usando o **importação** ferramenta.  
  
 Importação significa que os elementos definidos no pacote importado, que são os elementos na extremidade da seta da relação, efetivamente são definidos também no pacote de importação. Todos os elementos cuja visibilidade está definida como **pacote** estarão visíveis também no pacote de importação.  
  
 Evite criar loops em relações de importação.  
  
##  <a name="References"></a> Referências de um Namespace para outra  
 Se você quiser se referir a um elemento de um pacote de outra, você deve usar o nome qualificado do elemento.  
  
 Por exemplo, suponha que o pacote `SalesCommon` define o tipo `CustomerAddress`. Em outro pacote `RestaurantSales`, você deseja definir um tipo `MealOrder`, que tem um atributo de tipo de endereço do cliente. Você tem duas opções:  
  
-   Especifique o tipo de atributo usando o nome totalmente qualificado `SalesCommon::CustomerAddress`. Você deve fazer isso pode apenas se `CustomerAddress` tem sua **visibilidade** propriedade definida como **público**.  
  
-   Criar uma relação de importação do `RestaurantSales` de pacote para o `SalesCommon` pacote. Em seguida, você pode usar `CustomerAddress` sem usar o nome qualificado.  
  
##  <a name="Properties"></a> Propriedades de pacotes  
 Cada pacote tem as seguintes propriedades. Para ver as propriedades, o pacote em um diagrama ou no Gerenciador de modelos UML, com o botão direito e, em seguida, clique em **propriedades**.  
  
|Propriedade|Valor padrão|Descrição|  
|--------------|-------------------|-----------------|  
|**Nome**|(um novo nome)|O nome do pacote. Você pode alterá-lo no diagrama ou na janela Propriedades.|  
|**Nome qualificado**|*Recipiente* :: *nome do pacote*|O nome completo, prefixado pelo nome do pacote ou modelo que contém esse pacote. Para obter mais informações, consulte [Namespaces](#Namespaces).|  
|**Perfis**|(vazio)|Uma lista dos perfis vinculado a este pacote. Esses perfis fornecem os estereótipos que podem ser aplicados aos elementos dentro do pacote. Para obter mais informações, consulte [personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md).|  
|**Visibilidade**|**Público**|A visibilidade do pacote fora do seu pacote pai.|  
|**Itens de trabalho**|(vazio)|Uma lista de itens de trabalho vinculados. Para obter mais informações, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).|  
|**Local da definição**|(um nome)|O nome do arquivo onde os detalhes do pacote são armazenados. Os arquivos estão dentro de **ModelDefinition** pasta do projeto. Essa informação pode ser útil para fins de controle do código-fonte.|  
|**Descrição**|(vazio)|Uma descrição do pacote.|  
|**Estereótipos**|(vazio)|Estereótipos que são aplicados a este pacote. A lista de estereótipos disponíveis é determinada pelos perfis que você escolheu para este pacote e os pacotes que contêm a ele. Para obter mais informações, consulte [personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md).|  
  
## <a name="how-packages-are-stored"></a>Como os pacotes são armazenados  
 Quando você cria um novo pacote, um novo **. UML** arquivo é criado na **ModelDefinition** pasta do projeto. O modelo de raiz, que também é um pacote, também é armazenado em uma **. UML** arquivo.  
  
 Além disso, cada diagrama é armazenado em dois arquivos, um que representa as formas do diagrama, e um **. layout** arquivo que registra as posições das formas.  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)   
 [Gerenciar modelos e diagramas com controle de versão](../modeling/manage-models-and-diagrams-under-version-control.md)



