---
title: Noções básicas sobre modelos, classes e relações
description: Saiba como uma DSL (linguagem específica de domínio) é definida por seu arquivo de definição de DSL e que a maior parte do código do programa na solução de DSL é gerada a partir desse arquivo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, models
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b086f21b466863c3498ce15c15f7077b358c6d39
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388614"
---
# <a name="understanding-models-classes-and-relationships"></a>Noções básicas sobre modelos, classes e relações
Uma DSL (linguagem específica de domínio) é definida por seu arquivo de definição de DSL, junto com qualquer código de programa personalizado que você possa escrever. A maior parte do código do programa na solução de DSL é gerada a partir desse arquivo.

 Este tópico explica os recursos centrais da definição de DSL.

## <a name="the-dsl-definition"></a>A definição de DSL
 Quando você abre `Dsl\DslDefinition.dsl` , sua janela do Visual Studio é semelhante à imagem a seguir.

 ![Designer de DSL](../modeling/media/dsl_designer.png)

 As informações mais importantes na definição de DSL são exibidas no diagrama de definição de DSL. Informações adicionais, que também fazem parte de DslDefinition. DSL, são exibidas no Gerenciador de DSL, que geralmente aparece no lado do diagrama. Você trabalha com o diagrama para as tarefas mais frequentes e com o Gerenciador de DSL para personalizações mais avançadas.

 O diagrama de definição de DSL mostra as classes de domínio que definem elementos de modelo e as relações que definem links entre elementos de modelo. Ele também mostra as formas e os conectores que são usados para exibir os elementos do modelo para o usuário.

 ![Designer de DSL com raia](../modeling/media/dsl_desinger.png)

 Quando você seleciona um item na definição de DSL, seja no diagrama ou no Gerenciador de DSL, as informações sobre ele são exibidas no janela Propriedades. Informações adicionais podem ser exibidas na janela detalhes de DSL.

### <a name="models-are-instances-of-dsls"></a>Modelos são instâncias de DSLs
 Um *modelo* é uma instância de sua DSL criada por um usuário. Um modelo contém elementos de modelo, que são instâncias das classes de domínio que você define e links entre os elementos, que são instâncias das relações de domínio que você define. Um modelo também pode ter formas e conectores, que exibem os elementos de modelo e links em um diagrama. A definição de DSL inclui as classes de forma, as classes de conector e uma classe para o diagrama.

 Uma definição de DSL também é conhecida como um *modelo de domínio*. Uma definição de DSL ou modelo de domínio é a representação de tempo de design da linguagem específica do domínio, enquanto o modelo é a instanciação de tempo de execução da linguagem específica do domínio.

## <a name="domain-classes-define-model-elements"></a>Classes de domínio definem elementos de modelo
 As classes de domínio são usadas para criar os vários elementos no domínio, e as relações de domínio são os links entre os elementos. Eles são a representação de tempo de design dos elementos e links que serão instanciados pelos usuários da linguagem específica do design quando criarem seus modelos.

 Esta ilustração mostra um modelo que foi criado pelo usuário de um DSL da biblioteca de música. Os álbuns de música são representados por caixas que contêm listas de músicas. Os artistas são representados por caixas com cantos arredondados e estão conectados aos álbuns aos quais eles contribuíram.

 ![Modelo de instância da DSL gerada](../modeling/media/music_instance.png)

 A definição de DSL separa dois aspectos. A aparência dos elementos de modelo no diagrama de modelo é definida usando classes de forma e de conector. As informações transportadas no modelo são definidas usando classes de domínio e relações de domínio.

 A ilustração a seguir mostra as classes de domínio e relações na definição de DSL da biblioteca de músicas.

 ![Incorporação e relações de referência](../modeling/media/music_classes.png)

 A ilustração mostra quatro classes de domínio: música, álbum, artista e música. As classes de domínio definem propriedades de domínio, como nome, título e assim por diante. No modelo de instância, os valores de algumas dessas propriedades são exibidos no diagrama.

 Entre as classes estão relações de domínio: MusicHasAlbums, MusicHasArtists, AlbumbHasSongs e ArtistAppearedOnAlbums. As relações têm multiplicidades como 1.. 1, 0.. *. Por exemplo, cada música deve estar relacionada a exatamente um álbum por meio da relação AlbumHasSongs. Cada álbum pode ter qualquer número de músicas.

### <a name="rearranging-the-dsl-definition-diagram"></a>Reorganizando o diagrama de definição de DSL
 Observe que uma classe de domínio pode aparecer várias vezes no diagrama de definição de DSL, como o álbum faz nesta imagem. Há sempre uma exibição principal e pode haver algumas exibições de *referência* .

 Para reorganizar o diagrama de definição de DSL, você pode:

- Permutar exibições principais e de referência usando os comandos **colocar árvore aqui** e **dividir árvore** . Clique com o botão direito do mouse em uma única classe de domínio para ver esses comandos.

- Reordene as classes de domínio e as classes de forma pressionando Ctrl + Up e Ctrl + Down.

- Recolha ou expanda classes usando o ícone na parte superior direita de cada forma.

- Recolha partes da árvore clicando no sinal de subtração (-) na parte inferior de uma classe de domínio.

## <a name="inheritance"></a>Herança
 As classes de domínio podem ser definidas usando a herança. Para criar uma derivação de herança, clique na ferramenta de herança, clique na classe derivada e, em seguida, clique na classe base. Um elemento de modelo tem todas as propriedades que são definidas em sua própria classe de domínio, junto com todas as propriedades herdadas da classe base. Ele também herda suas funções em relações.

 A herança também pode ser usada entre relações, formas e conectores. A herança deve ser mantida dentro do mesmo grupo. Uma forma não pode herdar de uma classe de domínio.

## <a name="domain-relationships"></a>Relações de domínio
 Elementos de modelo podem ser vinculados por relações. Os links são sempre binários; Eles vinculam exatamente dois elementos. No entanto, qualquer elemento pode ter muitos links para outros objetos e pode até mesmo ser mais de um link entre o mesmo par de elementos.

 Assim como você pode definir diferentes classes de elementos, você pode definir diferentes classes de links. A classe de um link é chamada de *relação de domínio*. Um relacionamento de domínio especifica quais classes de elemento suas instâncias podem se conectar. Cada extremidade de uma relação é chamada de *função* e o relacionamento de domínio define nomes para as duas funções, bem como para a própria relação.

 Há dois tipos de relações de domínio: inserindo relações e relações de referência. No diagrama de definição de DSL, as relações de inserção têm linhas sólidas em cada função e as relações de referência têm linhas tracejadas.

### <a name="embedding-relationships"></a>Inserindo relações
 Cada elemento em um modelo, exceto para sua raiz, é o destino de um link de incorporação. Portanto, todo o modelo forma uma única árvore de links de inserção. Uma relação incorporada representa a contenção ou a propriedade. Dois elementos de modelo que são relacionados dessa maneira também são conhecidos como pai e filho. O filho é considerado inserido no pai.

 Os links de inserção geralmente não são mostrados explicitamente como conectores em um diagrama. Em vez disso, eles geralmente são representados por confinamento. A raiz do modelo é representada pelo diagrama e os elementos inseridos nela são exibidos como formas no diagrama.

 No exemplo, a classe raiz Music tem uma relação incorporada MusicHasAlbums ao álbum, que tem um AlbumHasSongs de inserção para a música. As músicas são exibidas como itens em uma lista dentro de cada álbum. Music também tem um MusicHasArtists de incorporação para a classe artista, cujas instâncias também aparecem como formas no diagrama.

 Por padrão, os elementos inseridos são excluídos automaticamente quando seus pais são excluídos.

 Quando um modelo é salvo no formato de arquivo em XML, os elementos inseridos são aninhados dentro de seus pais, a menos que você tenha personalizado a serialização.

> [!NOTE]
> Incorporação não é o mesmo que herança. Os filhos em uma relação incorporada não herdam as propriedades do pai. Uma incorporação é um tipo de link entre elementos de modelo. A herança é uma relação entre classes e não cria links entre elementos de modelo.

### <a name="embedding-rules"></a>Regras de incorporação
 Cada elemento em um modelo de instância deve ser o destino de exatamente um link de incorporação, exceto para a raiz do modelo.

 Portanto, toda classe de domínio não abstrata, exceto a classe raiz, deve ser o destino de pelo menos uma relação de incorporação ou deve herdar uma incorporação de uma classe base. Uma classe pode ser o destino de duas ou mais incorporações, mas seus elementos de modelo de instância só podem ter um pai por vez. A multiplicidade do destino para a origem deve ser 0.. 1 ou 1.. 1.

### <a name="the-explorer-displays-the-embedding-tree"></a>O Gerenciador exibe a árvore de incorporação
 Sua definição de DSL também cria um Gerenciador, que os usuários veem junto com seu diagrama de modelo.

 ![Gerenciador de DSL gerado](../modeling/media/music_explorer.png)

 O Explorer mostra todos os elementos no modelo, mesmo aqueles para os quais você não definiu nenhuma forma. Ele mostra os elementos e as relações de incorporação, mas não as relações de referência.

 Para ver os valores das propriedades de domínio de um elemento, o usuário seleciona um elemento, seja no diagrama de modelo ou no Gerenciador de modelos, e abre o janela Propriedades. Ele exibe todas as propriedades de domínio, incluindo aquelas que não são exibidas no diagrama. No exemplo, cada música tem um título e um gênero, mas apenas o valor do título é mostrado no diagrama.

## <a name="reference-relationships"></a>Relações de referência
 Uma relação de referência representa qualquer tipo de relação que não esteja incorporando.

 As relações de referência são geralmente exibidas em um diagrama como conectores entre as formas.

 Na representação XML do modelo, um link de referência entre dois elementos é representado usando *moniker.* Ou seja, os monikers são nomes que identificam exclusivamente cada elemento no modelo. O nó XML para cada elemento de modelo contém um nó que especifica o nome da relação e o moniker do outro elemento.

## <a name="roles"></a>Funções
 Cada relação de domínio tem duas funções, uma função de origem e uma função de destino.

 Na figura a seguir, a linha entre a classe de domínio do **Publicador** e a relação de domínio **PublisherCatalog** é a função de origem. A linha entre a relação de domínio e a classe de domínio de **álbum** é a função de destino.

 ![Funções e propriedades.](../modeling/media/propertycode.png)

 Os nomes associados a uma relação são especialmente importantes quando você escreve o código do programa que percorre o modelo. Por exemplo, quando você cria a solução de DSL, o editor de classe gerado tem um catálogo de propriedades que é uma coleção de álbuns. O álbum de classe tem um editor de propriedade que é uma única instância do editor de classe.

 Quando você cria uma relação em uma definição de DSL, os nomes de propriedade e relação recebem valores padrão. No entanto, você pode alterá-las.

## <a name="multiplicities"></a>Multiplicidades
 As multiplicidades especificam quantos elementos podem ter a mesma função em um relacionamento de domínio. No exemplo, a configuração de multiplicidade de zero para muitos (0.. \* ) na função de **Catálogo** especifica que qualquer instância da classe de domínio do **Publicador** pode ter tantos links de relações **PublisherCatalog** quanto você deseja dar.

 Configure a multiplicidade de uma função digitando no diagrama ou modificando a `Multiplicity` Propriedade na janela **Propriedades** . A tabela a seguir descreve as configurações dessa propriedade.

|Tipo de multiplicidade|Descrição|
|-|-|
|0.. * (zero a muitos)|Cada instância da classe de domínio pode ter várias instâncias da relação ou nenhuma instância da relação.|
|0.. 1 (zero a um)|Cada instância da classe de domínio não pode ter mais de uma instância da relação ou nenhuma das instâncias da relação.|
|1.. 1 (um)|Cada instância da classe de domínio pode ter uma instância da relação. Você não pode criar mais de uma instância dessa relação de qualquer instância da classe de função. Se a validação estiver habilitada, um erro de validação será exibido quando qualquer instância da classe de função não tiver nenhuma instância da relação.|
|1.. * (um para muitos)|Cada instância da classe na função que tem essa multiplicidade pode ter várias instâncias da relação, e cada instância deve ter pelo menos uma instância da relação. Se a validação estiver habilitada, um erro de validação será exibido quando qualquer instância da classe de função não tiver nenhuma instância da relação.|

## <a name="domain-relationships-as-classes"></a>Relações de domínio como classes
 Um link é representado no repositório como uma instância de Linkelement, que é uma classe derivada de ModelElement. Você pode definir essas propriedades no diagrama de modelo de domínio em relações de domínio.

 Você também pode fazer uma relação entre a origem ou o destino de outras relações. No diagrama de modelo de domínio, clique com o botão direito do mouse na relação de domínio e clique em **mostrar como classe**. Uma caixa de classe adicional será exibida. Em seguida, você pode conectar relações a ele.

 Você pode definir uma relação parcialmente por herança, assim como é possível com as classes de domínio. Selecione a relação derivada e defina a **relação base** no janela Propriedades.

 Uma relação derivada especializa sua relação de base. As classes de domínio para as quais ele se vincula devem ser derivadas ou iguais às classes vinculadas pela relação base. Quando um link da relação derivada é criado em um modelo, ele é uma instância de relações derivadas e base. No código do programa, você pode navegar até a extremidade oposta do link usando as propriedades geradas pelo base ou pela classe derivada.

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))