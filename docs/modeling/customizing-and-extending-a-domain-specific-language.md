---
title: Personalizando e estendendo uma linguagem específica do domínio
description: Saiba como o Visual Studio Modeling VMSDK (SDK de modelagem e visualização) fornece vários níveis nos quais você pode definir ferramentas de modelagem.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, creating solutions
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 04180b1fc8930b58c2d78635c794c8a614db5ed5
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112389378"
---
# <a name="customize-and-extend-a-domain-specific-language"></a>Personalizar e estender uma linguagem específica de domínio

O Visual Studio Modeling VMSDK (SDK de modelagem e visualização) fornece vários níveis nos quais você pode definir ferramentas de modelagem:

1. Defina uma linguagem de domínio específico (DSL) usando o diagrama de definição de DSL. Você pode criar rapidamente uma DSL com uma notação diagramáticas, um formulário XML legível e as ferramentas básicas que são necessárias para gerar código e outros artefatos. Para obter mais informações, consulte [como definir um idioma de Domain-Specific](../modeling/how-to-define-a-domain-specific-language.md).

2. Ajuste a DSL usando recursos mais avançados da definição de DSL. Por exemplo, você pode fazer os links adicionais aparecerem quando o usuário criar um elemento. Essas técnicas são mais obtidas na definição de DSL e algumas exigem algumas linhas de código de programa.

3. Estenda suas ferramentas de modelagem usando o código do programa. O VMSDK foi projetado especificamente para facilitar a integração de suas extensões com o código gerado a partir da Definição de DSL. Para obter mais informações, consulte [escrevendo código para personalizar um idioma de Domain-Specific](../modeling/writing-code-to-customise-a-domain-specific-language.md).

> [!NOTE]
> Quando você tiver atualizado o arquivo de definições de DSL, não se esqueça de clicar em **transformar todos os modelos** na barra de ferramentas de **Gerenciador de soluções** antes de recompilar sua solução.

## <a name="article-reference"></a>Referência do artigo

|Para obter esse efeito|Consulte este tópico|
|-|-|
|Permite que o usuário defina as propriedades de cor e estilo de uma forma.|Clique com o botão direito do mouse na classe de forma ou conector, aponte para **Adicionar exposto** e clique em um item.|
|Classes diferentes de elementos de modelo são semelhantes no diagrama, compartilhando propriedades como altura inicial e largura, cor, dicas de ferramenta.|Use a herança entre formas ou classes de conector. Mapeamentos entre formas derivadas e classes de domínio derivadas herdam os detalhes de mapeamento dos pais.<br /><br /> Ou mapear classes de domínio diferentes para a mesma classe de forma.|
|Uma classe de elemento de modelo é exibida por contextos de formas diferentes.|Mapeie mais de uma classe de forma para a mesma classe de domínio. Ao criar a solução, siga o relatório de erros e forneça o código solicitado para decidir qual forma usar.|
|Cor da forma ou outros recursos como fonte indicam o estado atual.|Consulte [atualizando formas e conectores para refletir o modelo](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md).<br /><br /> Crie uma regra que atualize as propriedades expostas. Consulte [regras propagar alterações no modelo](../modeling/rules-propagate-changes-within-the-model.md).<br /><br /> Ou use OnAssociatedPropertyChanged () para atualizar recursos não expostos, como setas de link ou fonte.|
|Ícone de alterações de forma para indicar estado.|Defina a visibilidade do mapeamento de decorador na janela detalhes de DSL. Localize vários decoradores de imagem na mesma posição. Consulte  [atualizando formas e conectores para refletir o modelo](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md).<br /><br /> Ou, substitua `ImageField.GetDisplayImage()` . Consulte o exemplo em <xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField> .|
|Definir uma imagem de plano de fundo em qualquer forma|Substitua InitializeInstanceResources () para adicionar um ImageField ancorado.|
|Aninhe formas em qualquer profundidade|Configure uma árvore de incorporação recursiva. Defina BoundsRules para conter as formas.|
|Anexe conectores em pontos fixos no limite de um elemento.|Defina elementos de terminal inseridos, representados por portas pequenas no diagrama. Use BoundsRules para corrigir as portas em vigor. Consulte o exemplo de diagrama de circuito na [visualização e no SDK de modelagem](https://code.msdn.microsoft.com/Visualization-and-Modeling-313535db).|
|O campo de texto exibe um valor derivado de outros valores.|Mapeie o decorador de texto para uma propriedade de domínio de armazenamento calculada ou personalizada. Para obter mais informações, consulte [Propriedades de armazenamento calculadas e personalizadas](../modeling/calculated-and-custom-storage-properties.md).|
|Propagar alterações entre elementos de modelo ou entre formas|Consulte [validação em um idioma Domain-Specific](../modeling/validation-in-a-domain-specific-language.md).|
|Propague alterações para recursos como outras extensões do Visual Studio fora da loja.|Consulte [manipuladores de eventos propagar alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).|
|Janela de Propriedades exibe as propriedades de um elemento relacionado.|Configure o encaminhamento de propriedade. Consulte [Personalizando a janela Propriedades](../modeling/customizing-the-properties-window.md).|
|Categorias de propriedade|A janela Propriedades é dividida em seções chamadas categorias. Defina a **categoria** de suas propriedades de domínio. As propriedades com o mesmo nome de categoria serão exibidas na mesma seção. Você também pode definir a **categoria** de uma função de relação.|
|Controlar o acesso do usuário às propriedades do domínio|Set **é navegável** false para impedir que uma propriedade de domínio apareça no janela Propriedades em tempo de execução. Você ainda pode mapeá-lo para decoradores de texto.<br /><br /> A **interface do usuário é somente leitura** impede que os usuários alterem uma propriedade de domínio.<br /><br /> O acesso do programa à propriedade de domínio não é afetado.|
|Altere o nome, o ícone e a visibilidade dos nós no Gerenciador de modelos de sua DSL.|Consulte [Personalizando o Gerenciador de modelos](../modeling/customizing-the-model-explorer.md).|
|Habilitar copiar, recortar e colar|Defina a propriedade **habilitar copiar colar** do nó do **Editor** no Gerenciador de DSL.|
|Copie links de referência e seus destinos sempre que um elemento for copiado. Por exemplo, copie os comentários anexados a um item.|Defina a propriedade de **cópia propagada** da função de origem (representada pela linha em um lado da relação de domínio no diagrama de definição de DSL).<br /><br /> Escreva o código para substituir ProcessOnCopy para obter efeitos mais complexos.<br /><br /> Consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).|
|Excluir, repai ou vincular novamente os elementos relacionados quando um elemento é excluído.|Defina o valor de **exclusão de propagações** de uma função de relação. Para efeitos mais complexos, substitua `ShouldVisitRelationship` e `ShouldVisitRolePlayer` métodos na `MyDslDeleteClosure` classe, definidos em **DomainModel. cs**.|
|Preserve o layout de forma e a aparência em copiar e arrastar e soltar.|Adicione as formas e os conectores aos copiados `ElementGroupPrototype` . O método mais conveniente para substituir é `ElementOperations.CreateElementGroupPrototype()`<br /><br /> Consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).|
|Cole formas em um local escolhido, como a posição atual do cursor.|Substitua `ClipboardCommandSet.ProcessOnCopy()` para usar a versão específica de local do `ElementOperations.Merge().` consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).|
|Criar links adicionais ao colar|Substituir ClipboardCommandSet. ProcessOnPasteCommand ()|
|Habilitar arrastar e soltar deste diagrama, outras DSLs e elementos do Windows|Consulte [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md)|
|Permite que uma forma ou ferramenta seja arrastada para uma forma filho, como uma porta, como se ela fosse arrastada para o pai.|Defina uma diretiva de mesclagem de elementos na classe de objeto de destino para encaminhar o objeto Descartado para o pai. Consulte [Personalizando a criação e movimentação de elementos](../modeling/customizing-element-creation-and-movement.md).|
|Permite que uma forma ou ferramenta seja arrastada para uma forma e tenha links ou objetos adicionais criados. Por exemplo, para permitir que um comentário seja descartado em um item ao qual ele será vinculado.|Defina uma diretiva de mesclagem de elementos na classe de domínio de destino e defina os links a serem gerados. Em casos complexos, você pode adicionar código personalizado. Consulte [Personalizando a criação e movimentação de elementos](../modeling/customizing-element-creation-and-movement.md).|
|Crie um grupo de elementos com uma ferramenta. Por exemplo, um componente com um conjunto fixo de portas.|Substitua o método de inicialização da caixa de ferramentas em ToolboxHelper. cs. Crie um protótipo de grupo de elementos (EGP) contendo os elementos e seus links de relacionamento. Consulte [Personalizando ferramentas e a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md).<br /><br /> Inclua as formas de entidade e de porta no EGP, ou defina BoundsRules para posicionar as formas de porta quando o EGP for instanciado.|
|Use uma ferramenta de conexão para criar uma instância de vários tipos de relação.|Adicione as diretivas de conexão de link (LCD) ao construtor de conexões que é invocado pela ferramenta. Os LCDs determinam o tipo da relação dos tipos dos dois elementos. Para fazer isso depender dos Estados dos elementos, você pode adicionar código personalizado. Consulte [Personalizando ferramentas e a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md).|
|Ferramentas adesivas – o usuário pode clicar duas vezes em qualquer ferramenta para criar muitas formas ou conectores sucessivamente.|No Gerenciador de DSL, selecione o `Editor` nó. Na janela Propriedades, Set **usa itens de caixa de ferramentas adesivas**.|
|Definir comandos de menu|Consulte [como: modificar um comando de menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)|
|Restringir o modelo com regras de validação|Consulte [validação em um idioma Domain-Specific](../modeling/validation-in-a-domain-specific-language.md)|
|Gere código, arquivos de configuração ou documentos de uma DSL.|[Gerando código a partir de uma linguagem específica do domínio](../modeling/generating-code-from-a-domain-specific-language.md)|
|Personalize como os modelos são salvos no arquivo.|Consulte [Personalizando o armazenamento de arquivos e a serialização de XML](../modeling/customizing-file-storage-and-xml-serialization.md)|
|Salve modelos em bancos de dados ou em outras mídias.|Substituir DocData *YourLanguage*<br /><br /> Consulte [Personalizando o armazenamento de arquivos e a serialização de XML](../modeling/customizing-file-storage-and-xml-serialization.md)|
|Integre várias DSLs para que elas funcionem como parte de um aplicativo.|Consulte [integrando modelos usando o Visual Studio ModelBus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).|
|Permita que sua DSL seja estendida por terceiros e controle a extensão.|[Estender a DSL usando MEF](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [Compartilhando classes entre DSLs por meio de uma biblioteca de DSLs](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [Definindo uma política de bloqueio para criar segmentos somente leitura](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>Confira também

- [Como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Escrevendo código para personalizar um idioma Domain-Specific](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [SDK de Modelagem para Visual Studio - linguagens específicas ao domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
