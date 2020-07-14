---
title: Personalizando o armazenamento de arquivos e a serialização XML
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.xmlbehavior
helpviewer_keywords:
- Domain-Specific Language, serialization
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 07592247e0afb870f3c4774c6f2023a6e8141cd1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542734"
---
# <a name="customize-file-storage-and-xml-serialization"></a>Personalizar o armazenamento de arquivos e a serialização XML

Quando o usuário salva uma instância, ou *modelo*, de uma DSL (linguagem específica de domínio) no Visual Studio, um arquivo XML é criado ou atualizado. O arquivo pode ser recarregado para recriar o modelo no repositório.

Você pode personalizar o esquema de serialização ajustando as configurações em **comportamento de serialização XML** no Gerenciador de DSL. Há um nó sob **comportamento de serialização XML** para cada classe de domínio, propriedade e relação. As relações estão localizadas sob suas classes de origem. Também há nós correspondentes às classes Shape, Connector e diagram.

Você também pode escrever o código do programa para personalização mais avançada.

> [!NOTE]
> Se você quiser salvar o modelo em um formato específico, mas não precisar recarregá-lo a partir desse formulário, considere usar modelos de texto para gerar a saída do modelo, em vez de um esquema de serialização personalizado. Para obter mais informações, consulte [gerando código de uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md).

## <a name="model-and-diagram-files"></a>Arquivos de modelo e diagrama

Cada modelo é geralmente salvo em dois arquivos:

- O arquivo de modelo tem um nome como **Model1. MyDSL**. Ele armazena os elementos de modelo e as relações e suas propriedades. A extensão de arquivo, como **. MyDSL** , é determinada pela propriedade **FileExtension** do nó do **Editor** na definição de DSL.

- O arquivo de diagrama tem um nome como **Model1. MyDSL. Diagram**. Ele armazena as formas, os conectores e suas posições, cores, espessuras de linha e outros detalhes da aparência do diagrama. Se o usuário excluir um arquivo **. Diagram** , as informações essenciais no modelo não serão perdidas. Somente o layout do diagrama é perdido. Quando o arquivo de modelo for aberto, um conjunto padrão de formas e conectores será criado.

### <a name="to-change-the-file-extension-of-a-dsl"></a>Para alterar a extensão de arquivo de uma DSL

1. Abra a definição de DSL. No Gerenciador de DSL, clique no nó do editor.

2. Na janela Propriedades, edite a propriedade **FileExtension** . Não inclua o "." inicial da extensão de nome de arquivo.

3. Em Gerenciador de Soluções, altere o nome dos dois arquivos de modelo de item em **DslPackage\ProjectItemTemplates**. Esses arquivos têm nomes que seguem este formato:

     `myDsl.diagram`

     `myDsl.myDsl`

## <a name="the-default-serialization-scheme"></a>O esquema de serialização padrão

Para criar um exemplo para este tópico, a definição de DSL a seguir foi usada.

![Diagrama de definição de DSL &#45; modelo de árvore da família](../modeling/media/familyt_person.png)

Essa DSL foi usada para criar um modelo com a seguinte aparência na tela.

![Diagrama de árvore da família, caixa de ferramentas e Explorer](../modeling/media/familyt_instance.png)

Esse modelo foi salvo e, em seguida, reaberto no editor de texto XML:

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

- Cada nó XML tem um nome que é igual a um nome de classe de domínio, exceto que a letra inicial é minúscula. Por exemplo, `familyTreeModel` e `person`.

- As propriedades de domínio, como Name e nascimento, são serializadas como atributos nos nós XML. Novamente, o caractere inicial do nome da propriedade é convertido em minúsculas.

- Cada relação é serializada como um nó XML aninhado dentro da extremidade de origem da relação. O nó tem o mesmo nome que a propriedade da função de origem, mas com um caractere inicial de minúsculas.

     Por exemplo, na definição de DSL, uma função nomeada **pessoas** é originada na classe **FamilyTree** .  No XML, isso é representado pelo nó nomeado `people` aninhado dentro do `familyTreeModel` nó.

- A extremidade de destino de cada relação de incorporação é serializada como um nó aninhado na relação. Por exemplo, o `people` nó contém vários `person` nós.

- A extremidade de destino de cada relação de referência é serializada como um *moniker*, que codifica uma referência ao elemento de destino.

     Por exemplo, em um `person` nó, pode haver uma `children` relação. Este nó contém monikers, como:

    ```xml
    <personMoniker name="/f817b728-e920-458e-bb99-98edc469d78f/Elizabeth I" />
    ```

## <a name="understand-monikers"></a>Entender os monikers

Os monikers são usados para representar referências cruzadas entre diferentes partes do modelo e dos arquivos de diagrama. Eles também são usados no `.diagram` arquivo para se referir a nós no arquivo de modelo. Há duas formas de moniker:

- *Monikers de ID* citam o GUID do elemento de destino. Por exemplo:

    ```xml
    <personShapeMoniker Id="f79734c0-3da1-4d72-9514-848fa9e75157" />
    ```

- Os *identificadores de chave qualificados* identificam o elemento de destino pelo valor de uma propriedade de domínio designada chamada de chave de moniker. O moniker do elemento de destino é prefixado pelo moniker de seu elemento pai na árvore de relações de incorporação.

     Os exemplos a seguir são obtidos de uma DSL em que há uma classe de domínio denominada Album, que tem uma relação de incorporação com uma classe de domínio chamada Song:

    ```xml
    <albumMoniker title="/My Favorites/Jazz after Teatime" />
    <songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
    ```

     Os monikers de chave qualificados serão usados se a classe de destino tiver uma propriedade de domínio para a qual a opção **é a chave de moniker** esteja definida como `true` em **comportamento de serialização XML**. No exemplo, essa opção é definida para propriedades de domínio chamadas "title" nas classes de domínio "Album" e "Song".

Os moniker de chave qualificados são mais fáceis de ler do que os monikers de ID. Se você pretende que o XML de seus arquivos de modelo seja lido por pessoas, considere o uso de moniker de chave qualificados. No entanto, é possível que o usuário defina mais de um elemento para ter a mesma chave de moniker. Chaves duplicadas podem fazer com que o arquivo não recarregue corretamente. Portanto, se você definir uma classe de domínio que é referenciada usando moniker de chave qualificados, deverá considerar as maneiras de impedir que o usuário salve um arquivo com monikers duplicados.

### <a name="to-set-a-domain-class-to-be-referenced-by-id-monikers"></a>Para definir uma classe de domínio a ser referenciada por monikers de ID

1. Certifique-se de que a **chave de moniker** seja `false` para cada propriedade de domínio na classe e suas classes base.

    1. No Gerenciador de DSL, expanda **XML serialização Behavior\Class data \\ \<the domain class> \Element data**.

    2. Verifique se a **chave de moniker** é `false` para cada propriedade de domínio.

    3. Se a classe de domínio tiver uma classe base, repita o procedimento nessa classe.

2. Defina **Serialize ID**  =  `true` para a classe de domínio.

     Essa propriedade pode ser encontrada em **comportamento de serialização XML**.

### <a name="to-set-a-domain-class-to-be-referenced-by-qualified-key-monikers"></a>Para definir uma classe de domínio a ser referenciada por moniker de chave qualificados

- Set **é a chave do moniker** para uma propriedade de domínio de uma classe de domínio existente. O tipo da propriedade deve ser `string` .

    1. No Gerenciador de DSL, expanda **XML serialização Behavior\Class data \\ \<the domain class> \Element data**e, em seguida, selecione a propriedade domínio.

    2. Na janela Propriedades, defina **é a chave do moniker** para `true` .

- \- ou –

     Crie uma nova classe de domínio usando a ferramenta de **classe de domínio nomeada** .

     Essa ferramenta cria uma nova classe que tem uma propriedade de domínio chamada nome. O **nome do elemento is** e as propriedades de **chave do moniker** dessa propriedade de domínio são inicializadas como `true` .

- \- ou –

     Crie uma relação de herança da classe de domínio para outra classe que tenha uma propriedade de chave de moniker.

### <a name="avoid-duplicate-monikers"></a>Evite monikers duplicados

Se você usar moniker de chave qualificados, é possível que dois elementos no modelo de um usuário tenham o mesmo valor na propriedade de chave. Por exemplo, se a sua DSL tiver uma pessoa que tenha um nome de propriedade, o usuário poderá definir os nomes de dois elementos como o mesmo. Embora o modelo possa ser salvo no arquivo, ele não recarregará corretamente.

Há vários métodos que ajudam a evitar essa situação:

- Defina **é**  =  `true` o nome do elemento para a propriedade de domínio de chave. Selecione a propriedade Domain no diagrama de definição de DSL e defina o valor na janela Propriedades.

     Quando o usuário cria uma nova instância da classe, esse valor faz com que a propriedade de domínio seja atribuída automaticamente a um valor diferente. O comportamento padrão adiciona um número ao final do nome da classe. Isso não impede que o usuário altere o nome para uma duplicata, mas ajuda no caso em que o usuário não define o valor antes de salvar o modelo.

- Habilite a validação para a DSL. No Gerenciador de DSL, selecione Editor\Validation e defina as propriedades **uses...** como `true` .

     Há um método de validação gerado automaticamente que verifica se há ambiguidades. O método está na `Load` categoria validação. Isso garante que o usuário será avisado de que talvez não seja possível reabrir o arquivo.

     Para obter mais informações, consulte [validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md).

### <a name="moniker-paths-and-qualifiers"></a>Caminhos e qualificadores do moniker

Um moniker de chave qualificado termina com a chave de moniker e é prefixado com o moniker de seu pai na árvore de incorporação. Por exemplo, se o moniker de um álbum for:

```xml
<albumMoniker title="/My Favorites/Jazz after Teatime" />
```

Em seguida, uma das músicas nesse álbum poderia ser:

```xml
<songMoniker title="/My Favorites/Jazz after Teatime/Hot tea" />
```

No entanto, se os álbuns forem referenciados por ID, em vez disso, os monikers serão os seguintes:

```xml
<albumMoniker Id="77472c3a-9bf9-4085-976a-d97a4745237c" />
<songMoniker title="/77472c3a-9bf9-4085-976a-d97a4745237c/Hot tea" />
```

Observe que, como um GUID é exclusivo, ele nunca é prefixado pelo moniker de seu pai.

Se você souber que uma determinada propriedade de domínio sempre terá um valor exclusivo dentro de um modelo, você poderá definir o **qualificador de moniker** como `true` para essa propriedade. Isso fará com que ele seja usado como um qualificador, sem usar o moniker do pai. Por exemplo, se você definir ambos como um **qualificador de moniker** e **for a chave de moniker** para a propriedade de domínio title da classe Album, o nome ou o identificador do modelo não será usado em monikers para o álbum e seus filhos incorporados:

```xml
<albumMoniker name="Jazz after Teatime" />
<songMoniker title="/Jazz after Teatime/Hot tea" />
```

## <a name="customize-the-structure-of-the-xml"></a>Personalizar a estrutura do XML

Para fazer as personalizações a seguir, expanda o nó **comportamento de serialização XML** no Gerenciador de DSL. Em uma classe de domínio, expanda o nó dados do elemento para ver a lista de propriedades e relações que são originadas nessa classe. Selecione uma relação e ajuste suas opções na janela Propriedades.

- Defina o **elemento omita** como true para omitir o nó da função de origem, deixando apenas a lista de elementos de destino. Você não deve definir essa opção se houver mais de uma relação entre as classes de origem e de destino.

    ```xml
    <familyTreeModel ...>
      <!-- The following node is omitted by using Omit Element: -->
      <!-- <people> -->
        <person name="Henry VIII" .../>
        <person name="Elizabeth I" .../>
      <!-- </people> -->
    </familyTreeModel>
    ```

- Defina **usar formulário completo** para inserir os nós de destino em nós que representam as instâncias de relacionamento. Essa opção é definida automaticamente quando você adiciona propriedades de domínio a uma relação de domínio.

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

- Defina **Representation**  =  o**elemento** de representação para ter uma propriedade de domínio salva como um elemento em vez de como um valor de atributo.

    ```xml
    <person name="Elizabeth I" birthYear="1533">
      <deathYear>1603</deathYear>
    </person>
    ```

- Para alterar a ordem na qual os atributos e as relações são serializados, clique com o botão direito do mouse em um item em dados do elemento e use os comandos do menu **mover para cima** ou **mover para baixo** .

## <a name="major-customization-using-program-code"></a>Personalização principal usando o código do programa

Você pode substituir partes ou todos os algoritmos de serialização.

Recomendamos que você estude o código em **Dsl\Generated Code\Serializer.cs** e **SerializationHelper.cs**.

### <a name="to-customize-the-serialization-of-a-particular-class"></a>Para personalizar a serialização de uma classe específica

1. Set **é personalizado** no nó para essa classe em **comportamento de serialização XML**.

2. Transforme todos os modelos, Compile a solução e investigue os erros de compilação resultantes. Os comentários próximos a cada erro explicam o código que você precisa fornecer.

### <a name="to-provide-your-own-serialization-for-the-whole-model"></a>Para fornecer sua própria serialização para todo o modelo

1. Métodos de substituição em Dsl\GeneratedCode\SerializationHelper.cs

## <a name="options-in-xml-serialization-behavior"></a>Opções no comportamento de serialização XML

No Gerenciador de DSL, o nó de comportamento de serialização XML contém um nó filho para cada classe de domínio, relação, forma, conector e classe de diagrama. Em cada um desses nós há uma lista de propriedades e relações originadas nesse elemento. As relações são representadas em suas próprias e em suas classes de origem.

A tabela a seguir resume as opções que você pode definir nesta seção da definição de DSL. Em cada caso, selecione um elemento no Gerenciador de DSL e defina as opções na janela Propriedades.

### <a name="xml-class-data"></a>Dados da classe XML

Esses elementos são encontrados no Gerenciador de DSL em **dados de Behavior\Class de serialização XML**.

|Propriedade|Descrição|
|-|-|
|Tem Esquema de elemento personalizado|Se for true, indica que a classe de domínio tem um esquema de elemento personalizado|
|É personalizado|Defina como **true** se você quiser escrever seu próprio código de serialização e desserialização para essa classe de domínio.<br /><br /> Compile a solução e investigue os erros para descobrir instruções detalhadas.|
|Classe de domínio|Classe de domínio à qual este nó de dados de classe se aplica. Somente leitura.|
|Nome do elemento|Nome do nó XML para elementos desta classe. O valor padrão é uma versão em minúsculas do nome da classe de domínio.|
|Nome do atributo do moniker|Nome do atributo usado nos elementos do moniker para conter a referência. Se estiver em branco, o nome da propriedade ou da ID de chave será usado.<br /><br /> Neste exemplo, é "Name":`<personMoniker name="/Mike Nash"/>`|
|Nome do elemento do moniker|Nome do elemento XML usado para monikers que se referem a elementos dessa classe.<br /><br /> O valor padrão é uma versão em minúsculas do nome de classe sufixos por "moniker". Por exemplo, `personMoniker`.|
|Nome do tipo de moniker|Nome do tipo XSD gerado para os monikers para elementos desta classe. O XSD está no **Dsl\Generated de esquema de código \\ \* . xsd**|
|Serializar ID|Se for true, o elemento GUID será incluído no arquivo. Isso deve ser verdadeiro se não houver nenhuma propriedade marcada como **moniker chave** e a DSL definir relações de referência para essa classe.|
|Nome do Tipo|Nome do tipo XML gerado no XSD a partir da classe de domínio designada.|
|Observações|Notas informais associadas a este elemento|

### <a name="xml-property-data"></a>Dados de propriedade XML

Nós de propriedade XML são encontrados sob os nós de classe.

|Propriedade|Descrição|
|-|-|
|Propriedade de domínio|Propriedade à qual se aplica os dados de configuração de serialização XML. Somente leitura.|
|É chave de moniker|Se for true, a propriedade será usada como a chave para criar monikers que referenciam instâncias dessa classe de domínio.|
|É qualificador de moniker|Se for true, a propriedade será usada para criar o qualificador em moniker. Se for false, e se Serializeid não for verdadeiro para essa classe de domínio, os monikers serão qualificados pelo moniker do elemento pai na árvore de incorporação.|
|Representação|Se for o atributo, a propriedade será serializada como um atributo XML; Se for o elemento, ele será serializado como um elemento; Se ignorar, ele não será serializado.|
|Nome do XML|Nome usado para o atributo ou elemento XML que representa a propriedade. Por padrão, essa é uma versão em minúsculas do nome da propriedade de domínio.|
|Observações|Notas informais associadas a este elemento|

### <a name="xml-role-data"></a>Dados da função XML

Nós de dados de função são encontrados nos nós de classe de origem.

|Propriedade|Descrição|
|-|-|
|Tem moniker personalizado|Defina como true se você quiser fornecer seu próprio código para gerar e resolver monikers que atravessam essa relação.<br /><br /> Para obter instruções detalhadas, crie a solução e clique duas vezes nas mensagens de erro.|
|Relacionamento de domínio|Especifica a relação à qual essas opções se aplicam. Somente leitura.|
|Omitir elemento|Se for true, o nó XML que corresponde à função de origem será omitido do esquema.<br /><br /> Se houver mais de uma relação entre as classes de origem e de destino, esse nó de função diferenciará os links que pertencem às duas relações. Portanto, recomendamos que você não defina essa opção nesse caso.|
|Nome do elemento de função|Especifica o nome do elemento XML que é derivado da função de origem. O valor padrão é o nome da propriedade de função.|
|Usar forma completa|Se for true, cada elemento de destino ou moniker será colocado em um nó XML que representa a relação. Isso deve ser definido como true se a relação tiver suas próprias propriedades de domínio.|

## <a name="see-also"></a>Confira também

- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Gerando código a partir de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md)
