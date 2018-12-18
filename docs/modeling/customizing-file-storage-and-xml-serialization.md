---
title: Personalizando o armazenamento de arquivos e a serialização XML
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.xmlbehavior
helpviewer_keywords:
- Domain-Specific Language, serialization
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 8a21067eab6e55f3fb031e57fa2257b0d40a7eb6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49886455"
---
# <a name="customize-file-storage-and-xml-serialization"></a>Personalizar o armazenamento de arquivos e a serialização XML

Quando o usuário salva uma instância, ou *modelo*, de uma linguagem específica de domínio (DSL) no Visual Studio, um arquivo XML é criado ou atualizado. O arquivo pode ser recarregado para recriar o modelo na Store.

Você pode personalizar o esquema de serialização ajustando as configurações sob **comportamento da serialização Xml** no Gerenciador de DSL. Há um nó sob **comportamento da serialização Xml** para cada classe de domínio, a propriedade e a relação. As relações estão localizadas em suas classes de origem. Também há nós correspondentes para a forma, conector e classes de diagrama.

Você também pode escrever código de programa para personalização mais avançado.

> [!NOTE]
> Se você deseja salvar o modelo em um formato específico, mas não é necessário recarregá-lo a partir desse formulário, considere o uso de modelos de texto para gerar a saída do modelo, em vez de um esquema de serialização personalizada. Para obter mais informações, consulte [código de geração de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md).

## <a name="model-and-diagram-files"></a>Arquivos de modelo e diagrama

Geralmente, cada modelo é salvo em dois arquivos:

-   O arquivo de modelo tem um nome, como **Model1.mydsl**. Ele armazena os elementos de modelo e as relações e suas propriedades. A extensão de arquivo, como **.mydsl** é determinado pelo **FileExtension** propriedade do **Editor** nó na definição de DSL.

-   O arquivo de diagrama tem um nome, como **Model1.mydsl.diagram**. Ele armazena as formas, conectores e suas posições, cores, espessuras de linha e outros detalhes da aparência do diagrama. Se o usuário exclui um **. Diagram** arquivo, as informações essenciais no modelo não são perdidas. Apenas o layout do diagrama será perdido. Quando o arquivo de modelo é aberto, um padrão definido de formas e conectores serão criados.

### <a name="to-change-the-file-extension-of-a-dsl"></a>Para alterar a extensão de arquivo de uma DSL

1.  Abra a definição de DSL. No Gerenciador de DSL, clique no nó de Editor.

2.  Na janela Propriedades, edite o **FileExtension** propriedade. Não inclua inicial "." da extensão de nome do arquivo.

3.  No Solution Explorer, altere o nome dos arquivos de modelo de dois itens na **DslPackage\ProjectItemTemplates**. Esses arquivos têm nomes que seguem este formato:

     `myDsl.diagram`

     `myDsl.myDsl`

## <a name="the-default-serialization-scheme"></a>O esquema de serialização padrão

Para criar um exemplo deste tópico, a seguinte definição de DSL foi usada.

![Diagrama de definição de DSL &#45; modelo de árvore genealógica](../modeling/media/familyt_person.png)

Essa DSL foi usado para criar um modelo que tem a aparência a seguir na tela.

![Explorer, a caixa de ferramentas e diagrama de árvore genealógica](../modeling/media/familyt_instance.png)

Esse modelo foi salvo e aberto novamente no editor de texto XML:

```xml
<?xml version="1.0" encoding="utf-8"?>
<familyTreeModel xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="f817b728-e920-458e-bb99-98edc469d78f" xmlns="http://schemas.microsoft.com/dsltools/FamilyTree">
  <people>
    <person name="Henry VIII" birthYear="1491" deathYear="1547" age="519">
      <children>
        <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
        <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Mary" />
      </children>
    </person>
    <person name="Elizabeth I" birthYear="1533" deathYear="1603" age="477" />
    <person name="Mary" birthYear="1515" deathYear="1558" age="495" />
  </people>
</familyTreeModel>
```

Observe os seguintes pontos sobre o modelo serializado:

-   Cada nó XML tem um nome que é o mesmo que um nome de classe de domínio, exceto que a primeira letra é minúscula. Por exemplo, `familyTreeModel` e `person`.

-   Propriedades do domínio, como nome e BirthYear são serializadas como atributos em nós de XML. Novamente, o caractere inicial do nome da propriedade é convertido em minúsculas.

-   Cada relação é serializada como um nó XML aninhado dentro de extremidade de origem da relação. O nó tem o mesmo nome que a propriedade da função de origem, mas com um caractere inicial de letras minúsculas.

     Por exemplo, na definição de DSL, uma função que é denominada **pessoas** é originado na **FamilyTree** classe.  No XML, isso é representado pelo nó chamado `people` aninhada dentro de `familyTreeModel` nó.

-   A extremidade de destino de cada relação de incorporação é serializada como um nó aninhado sob o relacionamento. Por exemplo, o `people` nó contém vários `person` nós.

-   A extremidade de destino de cada relação de referência é serializada como um *moniker*, que codifica uma referência ao elemento de destino.

     Por exemplo, em um `person` nó, pode haver um `children` relação. Esse nó contém identificadores de origem, como:

    ```xml
    <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
    ```

## <a name="understand-monikers"></a>Entender os Monikers

Monikers são usados para representar referências cruzadas entre diferentes partes dos arquivos de modelo e o diagrama. Eles também são usados no `.diagram` arquivo para referir-se a nós no arquivo de modelo. Há duas formas de moniker:

-   *Monikers ID* citar o GUID do elemento de destino. Por exemplo:

    ```xml
    <personShapeMoniker Id="f79734c0-3da1-4d72-9514-848fa9e75157" />
    ```

-   *Qualificado monikers chave* identificar o elemento de destino pelo valor de uma propriedade de domínio designado, chamado da chave do moniker. O moniker do elemento de destino é prefixado pelo moniker do seu elemento pai na árvore de relações inseridas.

     Os exemplos a seguir são obtidos de uma DSL no qual existe é uma classe de domínio chamada álbum, que tem uma relação de incorporação em um domínio canção nomeada de classe:

    ```xml
    <albumMoniker title="/My Favorites/Jazz after Teatime" />
    <songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
    ```

     Qualificado monikers chave serão usadas se a classe de destino tem uma propriedade de domínio para o qual a opção **é a chave do Moniker** é definido como `true` na **comportamento da serialização Xml**. No exemplo, essa opção é definida para as propriedades de domínio denominadas "Título" nas classes de domínio "Álbum" e "Música".

Qualificado monikers de chave são mais fáceis de ler do que monikers de ID. Se você pretende que o XML de seus arquivos de modelo a ser lido por pessoas, considere o uso de monikers chave qualificados. No entanto, é possível que o usuário definir mais de um elemento para ter a mesma chave do moniker. Chaves duplicadas pode causar o recarregamento do arquivo não corretamente. Portanto, se você definir uma classe de domínio que é referenciada usando monikers chave qualificados, você deve considerar maneiras de impedir que o usuário salvar um arquivo que tem identificadores duplicados.

### <a name="to-set-a-domain-class-to-be-referenced-by-id-monikers"></a>Para definir uma classe de domínio sejam referenciadas pelo monikers de ID

1.  Certifique-se de que **é a chave do Moniker** é `false` para cada propriedade de domínio na classe e suas classes base.

    1.  No DSL Explorer, expanda **dados da serialização Xml Behavior\Class\\\<a classe de domínio > \Element dados**.

    2.  Verifique **é a chave do Moniker** é `false` para cada propriedade de domínio.

    3.  Se a classe de domínio tem uma classe base, repita o procedimento dessa classe.

2.  Definir **serializar Id**  =  `true` para a classe de domínio.

     Essa propriedade pode ser encontrada na **comportamento da serialização Xml**.

### <a name="to-set-a-domain-class-to-be-referenced-by-qualified-key-monikers"></a>Para definir uma classe de domínio para ser referenciado por identificadores de chave qualificados

-   Definir **é a chave do Moniker** para uma propriedade de domínio de uma classe de domínio existente. O tipo da propriedade deve ser `string`.

    1.  No DSL Explorer, expanda **dados da serialização Xml Behavior\Class\\\<a classe de domínio > \Element dados**e, em seguida, selecione a propriedade de domínio.

    2.  Na janela Propriedades, defina **é a chave do Moniker** para `true`.

-   \- ou -

     Criar um novo domínio classe usando o **classe de domínio chamado** ferramenta.

     Essa ferramenta cria uma nova classe que tem uma propriedade de domínio denominada nome. O **é o nome do elemento** e **é a chave do Moniker** as propriedades dessa propriedade de domínio são inicializadas para `true`.

-   \- ou -

     Crie uma relação de herança da classe de domínio para outra classe que tem uma propriedade de chave do moniker.

### <a name="avoid-duplicate-monikers"></a>Evite Monikers duplicados

Se você usar monikers chave qualificados, é possível que dois elementos no modelo de um usuário pode ter o mesmo valor na propriedade de chave. Por exemplo, se a sua DSL tem uma pessoa que tem uma propriedade de nome de classe, o usuário pode definir os nomes dos dois elementos a ser o mesmo. Embora o modelo pode ser salvo em um arquivo, ele seria não recarregar corretamente.

Há vários métodos que ajudam a evitar essa situação:

-   Definir **é o nome do elemento**  =  `true` para a propriedade de chave do domínio. Selecione a propriedade de domínio no diagrama de definição de DSL e, em seguida, defina o valor na janela Propriedades.

     Quando o usuário cria uma nova instância da classe, esse valor faz com que a propriedade de domínio a ser atribuído automaticamente um valor diferente. O comportamento padrão adiciona um número ao final do nome da classe. Isso não impede que o usuário alterar o nome para uma duplicata, mas ajuda no caso de quando o usuário não define o valor antes de salvar o modelo.

-   Habilite a validação para a DSL. No Gerenciador de DSL, selecione Editor \ validação e defina o **usa...**  propriedades a serem `true`.

     Há um método de validação gerada automaticamente que verifica as ambiguidades. O método está entre o `Load` categoria de validação. Isso garante que o usuário será avisado que pode não ser possível abrir o arquivo novamente.

     Para obter mais informações, consulte [validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md).

### <a name="moniker-paths-and-qualifiers"></a>Qualificadores e caminhos de moniker

Um moniker de chave qualificado termina com a chave de moniker e é prefixado com o moniker de seu pai na árvore de incorporação. Por exemplo, se o moniker de um álbum é:

```xml
<albumMoniker title="/My Favorites/Jazz after Teatime" />
```

Em seguida, uma das músicas desse álbum poderia ser:

```xml
<songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
```

No entanto, se álbuns são referenciados por ID em vez disso, em seguida, os monikers seria da seguinte maneira:

```xml
<albumMoniker Id="77472c3a-9bf9-4085-976a-d97a4745237c" />
<songMoniker title="/77472c3a-9bf9-4085-976a-d97a4745237c/Hot tea" />
```

Observe que como um GUID é exclusivo, ele é nunca prefixado pelo moniker de seu pai.

Se você souber que uma propriedade de domínio específico sempre terá um valor exclusivo dentro de um modelo, você pode definir **é o qualificador de Moniker** para `true` para essa propriedade. Isso fará com que ele seja usado como um qualificador, sem usar o moniker do pai. Por exemplo, se você definir ambos **é o qualificador de Moniker** e **é a chave do Moniker** para a propriedade de domínio do título da classe álbum, nome ou o identificador do modelo não é usado nos monikers para álbum e seu incorporado filhos:

```xml
<albumMoniker name="Jazz after Teatime" />
<songMoniker title="/Jazz after Teatime/Hot tea" />
```

## <a name="customize-the-structure-of-the-xml"></a>Personalizar a estrutura do XML

Para fazer as seguintes personalizações, expanda o **comportamento da serialização Xml** nó no Gerenciador de DSL. Em uma classe de domínio, expanda o nó de elemento de dados para ver a lista de propriedades e relações que têm origem em que essa classe. Selecione uma relação e ajustar suas opções na janela Propriedades.

-   Definir **omitir o elemento** como true para omitir o nó de função de origem, deixando apenas a lista de elementos de destino. Você não deve definir essa opção se não houver mais de uma relação entre as classes de origem e destino.

    ```xml
    <familyTreeModel ...>
      <!-- The following node is omitted by using Omit Element: -->
      <!-- <people> -->
        <person name="Henry VIII" .../>
        <person name="Elizabeth I" .../>
      <!-- </people> -->
    </familyTreeModel>
    ```

-   Definir **usar o formulário completo** para inserir os nós de destino em nós que representam as instâncias de relação. Essa opção é definida automaticamente quando você adiciona as propriedades do domínio a uma relação de domínio.

    ```xml
    <familyTreeModel ...>
      <people>
        <!-- The following node is inserted by using Use Full Form: -->
        <familyTreeModelHasPeople myRelationshipProperty="x1">
          <person name="Henry VIII" .../>
        </familyTreeModelHasPeople>
        <familyTreeModelHasPeople myRelationshipProperty="x2">
          <person name="Elizabeth I" .../>
        </familyTreeModelHasPeople>
      </people>
    </familyTreeModel>
    ```

-   Definir **representação** = **elemento** ter uma propriedade de domínio salva como elemento, em vez de como um valor de atributo.

    ```xml
    <person name="Elizabeth I" birthYear="1533">
      <deathYear>1603</deathYear>
    </person>
    ```

-   Para alterar a ordem na qual os atributos e relações são serializadas, um item de dados do elemento com o botão direito e usar o **mover para cima** ou **mover para baixo** comandos de menu.

## <a name="major-customization-using-program-code"></a>Principais personalização usando um código de programa

Você pode substituir partes ou todos os algoritmos de serialização.

Recomendamos que você estude o código na **Dsl\Generated Code\Serializer.cs** e **SerializationHelper.cs**.

### <a name="to-customize-the-serialization-of-a-particular-class"></a>Para personalizar a serialização de uma classe específica

1.  Definir **é personalizada** no nó para essa classe sob **comportamento da serialização Xml**.

2.  Transformar todos os modelos, compile a solução e investigue os erros de compilação resultante. Comentários perto de cada erro explicam o que o código que você precisa fornecer.

### <a name="to-provide-your-own-serialization-for-the-whole-model"></a>Para fornecer sua própria serialização para todo o modelo

1.  Substituir métodos em Dsl\GeneratedCode\SerializationHelper.cs

## <a name="options-in-xml-serialization-behavior"></a>Opções de comportamento de serialização de Xml

No Gerenciador de DSL, o nó de comportamento da serialização Xml contém um nó filho para cada classe de domínio, relação, forma, conector e classe de diagrama. Em cada um de nós é uma lista de propriedades e relações originadas no elemento. As relações são representadas por si mesmos e em suas classes de origem.

A tabela a seguir resume as opções que podem ser definidas nesta seção da definição de DSL. Em cada caso, selecione um elemento no Gerenciador de DSL e definir as opções na janela Propriedades.

### <a name="xml-class-data"></a>Dados da classe XML

Esses elementos são encontrados no Gerenciador de DSL sob **dados Behavior\Class da serialização Xml**.

|||
|-|-|
|Propriedade|Descrição|
|Tem o esquema de elemento personalizado|Se for True, indica que a classe de domínio tem um esquema de elemento personalizado|
|É personalizado|Defina isso como **verdadeira** se você deseja escrever seu próprio código de serialização e desserialização para essa classe de domínio.<br /><br /> Compile a solução e investigue os erros para obter instruções detalhadas de descobrir.|
|Classe de domínio|Classe de domínio ao qual se aplica a este nó de dados de classe. Somente leitura.|
|Nome de elementos|Nome do nó XML para elementos dessa classe. O valor padrão é uma versão em minúsculas do nome da classe de domínio.|
|Nome do atributo de identificador de origem|Nome do atributo usado nos elementos de moniker para conter a referência. Se estiver vazio, o nome da propriedade de chave ou id é usado.<br /><br /> Neste exemplo, é "name":  `<personMoniker name="/Mike Nash"/>`|
|Nome de elemento do identificador de origem|Nome do elemento xml usado para monikers que se referem a elementos dessa classe.<br /><br /> O valor padrão é uma versão em letra minúscula do nome da classe, o sufixo "Moniker". Por exemplo, `personMoniker`.|
|Nome do tipo de identificador de origem|Nome do tipo xsd gerado para monikers aos elementos dessa classe. O XSD está na **código Dsl\Generated\\\*XSD**|
|Serializar Id|Se for True, o GUID de elemento é incluído no arquivo. Isso deve ser verdadeiro se não houver nenhuma propriedade que é marcada **é a chave do Moniker** e DSL define as relações de referência a essa classe.|
|Nome do tipo|Nome do tipo xml gerado no xsd de classe de domínio designada.|
|Observações|Observações informais associadas a este elemento|

### <a name="xml-property-data"></a>Propriedade XML de dados

Nós de propriedade XML estão localizadas sob os nós de classe.

|||
|-|-|
|Propriedade|Descrição|
|Propriedade de domínio|Propriedade à qual se aplica os dados de configuração de serialização de xml. Somente leitura.|
|É a chave do Moniker|Se for True, a propriedade é usada como a chave para a criação de identificadores de origem que referenciam as instâncias dessa classe de domínio.|
|É o qualificador de Moniker|Se for True, a propriedade é usada para criar o qualificador nos monikers. Se for false, e se SerializeId não é válido para essa classe de domínio, monikers são qualificados pelo moniker do elemento pai na árvore de incorporação.|
|Representação|Se o atributo, a propriedade é serializado como um atributo xml; Se o elemento, ele é serializado como um elemento. Se ignorar, ele não será serializado.|
|Nome XML|Nome usado para o elemento que representa a propriedade ou atributo xml. Por padrão, esta é uma versão em minúsculas do nome da propriedade de domínio.|
|Observações|Observações informais associadas a este elemento|

### <a name="xml-role-data"></a>Dados XML de função

Nós de dados de função são encontradas sob os nós de classe de origem.

|Propriedade|Descrição|
|-|-|
|Tem o Moniker personalizado|Defina como verdadeiro se desejar fornecer seu próprio código para gerar e resolvendo monikers que atravessam a essa relação.<br /><br /> Para obter instruções detalhadas, compile a solução e, em seguida, clique duas vezes as mensagens de erro.|
|Relacionamento de domínio|Especifica a relação ao qual essas opções se aplicam. Somente leitura.|
|Omitir um elemento|Se for true, o nó XML que corresponde à função de origem é omitido do esquema.<br /><br /> Se houver mais de uma relação entre as classes de origem e destino, este nó de função faz distinção entre os links que pertencem a duas relações. Portanto, recomendamos que você não defina essa opção nesse caso.|
|Nome do elemento de função|Especifica o nome do elemento XML que é derivado da função de origem. O valor padrão é o nome da propriedade de função.|
|Use o formulário completo|Se for true, cada elemento de destino ou o identificador de origem está contido em um nó XML que representa a relação. Isso deve ser definido como true se o relacionamento tem suas próprias propriedades de domínio.|

## <a name="see-also"></a>Consulte também

- [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)