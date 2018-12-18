---
title: Noções básicas sobre modelos, Classes e relações | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, models
ms.assetid: 2ecd569c-b369-41ea-b78e-a61b62e2e4e9
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: b86e9bd2aa11f098b26edf90f3ed415c66b874a1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49271785"
---
# <a name="understanding-models-classes-and-relationships"></a>Noções básicas sobre modelos, classes e relações
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma linguagem específica de domínio (DSL) é definida por seu arquivo de definição de DSL, junto com qualquer código de programa personalizado você pode escrever. A maioria do código do programa na solução DSL é gerada a partir desse arquivo.  
  
 Este tópico explica os recursos centrais da definição de DSL.  
  
## <a name="the-dsl-definition"></a>A definição de DSL  
 Quando você abre `Dsl\DslDefinition.dsl`, seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela se parece com a imagem a seguir.  
  
 ![designer de DSL](../modeling/media/dsl-designer.png "dsl_designer")  
  
 As informações mais importantes na definição de DSL são exibidas no diagrama de definição de DSL. Informações adicionais, que também é parte do Dsldefinition, são exibidas no Gerenciador de DSL, que geralmente aparece no lado do diagrama. Você trabalha com o diagrama para as tarefas mais frequentes e com o Gerenciador de DSL para personalizações mais avançadas.  
  
 O diagrama de definição de DSL mostra as classes de domínio que definem os elementos de modelo e as relações que definem links entre elementos de modelo. Ele também mostra as formas e conectores que são usados para exibir os elementos de modelo para o usuário.  
  
 ![designer de DSL com raias](../modeling/media/dsl-desinger.png "dsl_desinger")  
  
 Quando você seleciona um item na definição de DSL, no diagrama ou no Gerenciador de DSL, informações sobre ele são exibidas na janela Propriedades. Informações adicionais podem ser exibidas na janela de detalhes de DSL.  
  
### <a name="models-are-instances-of-dsls"></a>Os modelos são instâncias de DSLs  
 Um *modelo* é uma instância de sua DSL criado por um usuário. Um modelo contém os elementos de modelo, que são instâncias de classes de domínio que você define e links entre os elementos, que são instâncias dos relacionamentos de domínio que você definir. Um modelo também pode ter formas e conectores, que exibem os elementos de modelo e os links em um diagrama. A definição de DSL inclui as classes de forma, conector classes e uma classe para o diagrama.  
  
 Uma definição de DSL é também conhecido como um *modelo de domínio*. Um modelo de definição de DSL ou de domínio é a representação de tempo de design de linguagem específica de domínio, enquanto o modelo é a instanciação de tempo de execução da linguagem específica do domínio.  
  
## <a name="domain-classes-define-model-elements"></a>Classes de domínio definem elementos de modelo  
 Classes de domínio são usadas para criar os vários elementos no domínio e as relações de domínio estão os links entre os elementos. Eles são a representação de tempo de design dos elementos e links que será instanciado pelos usuários da linguagem de design específicas ao criarem seus modelos.  
  
 Esta ilustração mostra um modelo que foi criado pelo usuário de uma DSL de biblioteca de música. Álbuns de música são representadas por caixas que contêm listas de músicas. Artistas são representadas por caixas com cantos arredondados e estão conectadas aos álbuns ao qual eles contribuíram.  
  
 ![Modelo de instância da DSL gerada](../modeling/media/music-instance.png "Music_Instance")  
  
 A definição de DSL separa os dois aspectos. A aparência dos elementos de modelo no diagrama do modelo é definida por meio de classes de forma e conector. A informação transferida no modelo é definida usando as classes de domínio e relações de domínio.  
  
 A ilustração a seguir mostra as classes de domínio e as relações na definição de DSL da biblioteca de música.  
  
 ![Relações de referência e incorporação](../modeling/media/music-classes.png "Music_Classes")  
  
 A ilustração mostra quatro classes de domínio: música, álbum, artista e música. As classes de domínio definem propriedades de domínio, como nome, título e assim por diante. No modelo de instância, os valores de algumas dessas propriedades são exibidos no diagrama.  
  
 Entre as classes são relações de domínio: MusicHasAlbums, MusicHasArtists, AlbumbHasSongs e ArtistAppearedOnAlbums. As relações tiverem multiplicidades como 1..1, 0.. *. Por exemplo, todas as músicas devem estar relacionadas a exatamente um álbum por meio do relacionamento AlbumHasSongs. Cada álbum pode ter qualquer número de músicas.  
  
### <a name="rearranging-the-dsl-definition-diagram"></a>Reorganizar o diagrama de definição de DSL  
 Observe que uma classe de domínio pode aparecer várias vezes no diagrama de definição de DSL, como o álbum nesta imagem. Sempre há um modo de exibição principal, e pode haver alguns *referência* modos de exibição.  
  
 Para reorganizar o diagrama de definição de DSL, você pode:  
  
-   Troque principal e fazer referência a modos de exibição usando o **trazer árvore aqui** e **dividir árvore** comandos. Clique em uma classe de domínio único para ver esses comandos.  
  
-   Reordene as classes de domínio e forma, pressionando Ctrl + seta para cima e Ctrl + seta para baixo.  
  
-   Recolher ou expandir classes usando o ícone no canto superior direito de cada forma.  
  
-   Recolher partes da árvore clicando no sinal de subtração (-) na parte inferior de uma classe de domínio.  
  
## <a name="inheritance"></a>Herança  
 Classes de domínio podem ser definidas usando a herança. Para criar uma derivação de herança, clique na ferramenta de herança, clique na classe derivada e, em seguida, clique na classe base. Um elemento de modelo tem todas as propriedades que são definidas em sua própria classe de domínio, juntamente com todas as propriedades herdadas da classe base. Ele também herda suas funções em relações.  
  
 Herança também pode ser usada entre relações, formas e conectores. Herança deve manter dentro do mesmo grupo. Uma forma não pode herdar de uma classe de domínio.  
  
## <a name="domain-relationships"></a>Relações de domínio  
 Elementos de modelo podem ser vinculados por relações. Links sempre são binários; vinculam exatamente dois elementos. No entanto, qualquer elemento pode ter muitos links para outros objetos, e pode até mesmo haver mais de um link entre o mesmo par de elementos.  
  
 Assim como você pode definir classes diferentes de elementos, você pode definir classes diferentes de links. A classe de um link é chamada uma *relação de domínio*. Uma relação de domínio especifica quais classes de elemento de suas instâncias podem se conectar. Cada extremidade de uma relação é chamada um *função*, e a relação de domínio define nomes para as duas funções, bem como para a própria relação.  
  
 Há dois tipos de relações de domínio: Inserir relações e relações de referência. No diagrama de definição de DSL, relações de incorporação possuem linhas sólidas em cada função e as relações de referência tiveram linhas tracejadas.  
  
### <a name="embedding-relationships"></a>Relações de incorporação  
 Todos os elementos em um modelo, exceto para sua raiz é o destino de um link de inserção. Portanto, o modelo inteiro forma uma única árvore de inserção de links. Uma relação de incorporação representa confinamento ou propriedade. Dois elementos de modelo que estão relacionados dessa maneira são também conhecidos como pai e filho. O filho deve ser inserido no pai.  
  
 Incorporação de links não são normalmente mostradas explicitamente como conectores em um diagrama. Em vez disso, eles geralmente são representados por confinamento. A raiz do modelo é representado pelo diagrama e elementos incorporados são exibidos como formas no diagrama.  
  
 No exemplo, a classe raiz música tem uma relação de incorporação MusicHasAlbums álbum, que tem um AlbumHasSongs incorporação para música. Músicas são exibidas como itens em uma lista dentro de cada álbum. Música também tem uma inserção MusicHasArtists à classe artista, cujas instâncias também aparecem como formas no diagrama.  
  
 Por padrão, os elementos incorporados são automaticamente excluídos quando os seus pais são excluídos.  
  
 Quando um modelo é salvo para o arquivo no formato XML, os elementos incorporados estão aninhados dentro de seus pais, a menos que você personalizou a serialização.  
  
> [!NOTE]
>  Incorporação não é o mesmo que herança. Filhos em uma relação de incorporação não herdam as propriedades do pai. Uma inserção é um tipo de link entre os elementos de modelo. Herança é uma relação entre classes e não criar links entre elementos de modelo.  
  
### <a name="embedding-rules"></a>Regras de incorporação  
 Todos os elementos em um modelo de instância devem ser o destino de exatamente um link de incorporação, exceto para a raiz do modelo.  
  
 Portanto, cada classe de domínio não-abstrata, exceto a classe raiz, deve ser o destino de pelo menos uma relação de incorporação ou ela deve herdar de incorporação de uma classe base. Uma classe pode ser o destino de duas ou mais objetos incorporados, mas seus elementos de modelo de instância só podem ter um pai de cada vez. A multiplicidade de destino para origem deve ser entre 0 e 1. 1 ou 1.  
  
### <a name="the-explorer-displays-the-embedding-tree"></a>O Explorer exibe a árvore de incorporação  
 Sua definição de DSL também cria um gerenciador, o que os usuários veem junto com seu diagrama de modelo.  
  
 ![Gerado Gerenciador de DSL](../modeling/media/music-explorer.png "Music_Explorer")  
  
 O explorer mostra todos os elementos no modelo, mesmo aqueles para os quais você não definiu qualquer forma. Ele mostra elementos e relações de incorporação, mas não relações de referência.  
  
 Para ver os valores das propriedades de domínio de um elemento, o usuário seleciona um elemento no diagrama de modelo ou no Gerenciador de modelos e abre a janela Propriedades. Ele exibe todas as propriedades de domínio, incluindo aqueles que não são exibidos no diagrama. No exemplo, cada música tem um título e um gênero, mas apenas o valor do título é mostrado no diagrama.  
  
## <a name="reference-relationships"></a>Relações de referência  
 Uma relação de referência representa qualquer tipo de relação que não está inserindo.  
  
 Relações de referência normalmente são exibidas em um diagrama como conectores entre formas.  
  
 Na representação XML do modelo, um link de referência entre dois elementos é representado usando *monikers.* Ou seja, monikers são nomes que identificam exclusivamente cada elemento no modelo. O nó XML para cada elemento de modelo contém um nó que especifica o nome da relação e o moniker do elemento.  
  
## <a name="roles"></a>Funções  
 Todo relacionamento de domínio possui duas funções, uma função de origem e uma função de destino.  
  
 Na imagem a seguir, a linha entre o **Publisher** classe de domínio e o **PublisherCatalog** relacionamento de domínio é a função de origem. A linha entre a relação de domínio e o **álbum** classe de domínio é a função de destino.  
  
 ![As funções e propriedades. ](../modeling/media/propertycode.png "PropertyCode")  
  
 Os nomes associados a uma relação são especialmente importantes quando você escreve o código do programa que atravessa o modelo. Por exemplo, quando você compila a solução DSL, o publicador de classe gerada tem uma propriedade de catálogo que é uma coleção de álbuns. A classe álbum tem uma propriedade de publicador é uma única instância da classe publicador.  
  
 Quando você cria uma relação em uma definição de DSL, os nomes de propriedade e relação recebem valores padrão. No entanto, você pode alterá-los.  
  
## <a name="multiplicities"></a>Multiplicidades  
 Multiplicidades especificam quantos elementos pode ter a mesma função em uma relação de domínio. No exemplo, zero-para-muitos (0...\*) configuração de multiplicidade na **catálogo** função especifica que qualquer instância da **Publisher** classe de domínio pode ter quantos  **PublisherCatalog** relação links que você deseja dar a ele.  
  
 Configure a multiplicidade de uma função digitando-se no diagrama ou modificando o `Multiplicity` propriedade em de **propriedades** janela. A tabela a seguir descreve as configurações para essa propriedade.  
  
|Tipo de multiplicidade|Descrição|  
|-----------------------|-----------------|  
|0.. * (zero para muitos)|Cada instância da classe de domínio pode ter várias instâncias do relacionamento ou nenhuma instância da relação.|  
|Entre 0 e 1 (zero para um)|Cada instância da classe de domínio pode ter não mais de uma instância da relação ou nenhuma instância da relação.|  
|1..1 (um)|Cada instância da classe de domínio pode ter uma instância da relação. É possível criar mais de uma instância desse relacionamento de qualquer instância da classe de função. Se a validação estiver habilitada, um erro de validação aparecerá quando qualquer instância da classe de função não tem nenhuma instância da relação.|  
|1.. * (um para muitos)|Cada instância da classe na função que tem essa multiplicidade pode ter várias instâncias do relacionamento, e cada instância deve ter pelo menos uma instância da relação. Se a validação estiver habilitada, um erro de validação aparecerá quando qualquer instância da classe de função não tem nenhuma instância da relação.|  
  
## <a name="domain-relationships-as-classes"></a>Relações de domínio como Classes  
 Um link é representado na Store como uma instância de LinkElement, que é uma classe derivada de ModelElement. Você pode definir essas propriedades no diagrama de modelo de domínio em relações de domínio.  
  
 Você também pode fazer uma relação de origem ou destino de outras relações. No diagrama de modelo de domínio, a relação de domínio com o botão direito e, em seguida, clique em **mostrar como classe**. Será exibida uma caixa de classe adicional. Em seguida, você pode conectar relações a ela.  
  
 Você pode definir uma relação em parte por herança, exatamente como é possível com classes de domínio. Selecione o relacionamento derivado e defina **relacionamento Base** na janela Propriedades.  
  
 Uma relação derivada é especialista em seu relacionamento base. Classes de domínio que ele links deve ser derivados de ou para o mesmo que as classes vinculadas pela relação de base. Quando um link da relação derivada é criado em um modelo, ele é uma instância de derivado e as relações base. No código do programa, você pode navegar para a outra ponta do link usando as propriedades geradas com a base ou pela classe derivada.  
  
## <a name="see-also"></a>Consulte também  
 [Relações de domínio na API gerada](../misc/domain-relationships-in-the-generated-api.md)   
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



