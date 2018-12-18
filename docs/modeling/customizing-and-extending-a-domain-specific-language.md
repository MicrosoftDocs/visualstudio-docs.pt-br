---
title: Personalizando e estendendo uma linguagem específica do domínio
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, creating solutions
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: a49d9998aa319e66c22baa345864bc473f733c87
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816683"
---
# <a name="customizing-and-extending-a-domain-specific-language"></a>Personalizando e estendendo uma linguagem específica do domínio
O Visual Studio de modelagem e o SDK de visualização (VMSDK) oferece vários níveis na qual você pode definir as ferramentas de modelagem:

1.  Defina uma linguagem específica de domínio (DSL) usando o diagrama de definição de DSL. Você pode criar rapidamente uma DSL com uma notação diagramática, uma forma XML legível e as ferramentas básicas necessárias para gerar o código e outros artefatos.

     Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md).

2.  Ajuste a DSL usando os recursos mais avançados de definição de DSL. Por exemplo, você pode fazer com que os links adicionais aparecem quando o usuário cria um elemento. Essas técnicas são obtidas principalmente na definição de DSL, e alguns exigem algumas linhas de código do programa.

3.  Estenda suas ferramentas de modelagem usando o código do programa. O VMSDK foi projetado especificamente para facilitar a integração de suas extensões com o código gerado a partir da Definição de DSL.  Para obter mais informações, consulte [escrevendo código para personalizar uma linguagem específica do domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md).

> [!NOTE]
>  Quando você atualizou o arquivo de definições de DSL, não se esqueça de clicar **transformar todos os modelos** na barra de ferramentas do Gerenciador de soluções antes de recompilar sua solução.

## <a name="customShapes"></a> Nesta seção

|Para obter esse efeito|Consulte este tópico|
|-|-|
|Permitir que o usuário definir as propriedades de cor e estilo de uma forma.|A classe de forma ou conector com o botão direito, aponte para **adicionar exposto**e clique em um item.<br /><br /> Ver [Personalizando a apresentação no diagrama](../modeling/customizing-presentation-on-the-diagram.md).|
|No diagrama, as propriedades como altura inicial e a largura, cor, dicas de ferramenta de compartilhamento semelhante diferentes classes de elemento de modelo.|Use a herança entre classes de conector ou formas. Mapeamentos entre as formas derivadas e classes de domínio derivadas herdam os detalhes do mapeamento dos pais.<br /><br /> Ou então, mapear as classes de domínio diferentes para a mesma classe de forma.|
|Uma classe de elemento de modelo é exibida por contextos de formas diferentes.|Mapear mais de uma classe de forma para a mesma classe de domínio. Quando você compila a solução, execute o relatório de erros e forneça o código solicitado para decidir qual forma a ser usado.|
|Cor da forma ou outros recursos, como de fonte indicam o estado atual.|Ver [atualizando formas e conectores para refletir o modelo](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md).<br /><br /> Crie uma regra que atualiza as propriedades expostas. Ver [regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).<br /><br /> Ou use OnAssociatedPropertyChanged() para atualizar os recursos não expostos como setas de link ou da fonte.|
|Ícone nas alterações de forma para indicar o estado.|Defina a visibilidade do decorador mapeamento na janela de detalhes de DSL. Localize vários decoradores de imagem na mesma posição. Ver [atualizando formas e conectores para refletir o modelo](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md).<br /><br /> Ou, substituir `ImageField.GetDisplayImage()`. Consulte o exemplo <xref:Microsoft.VisualStudio.Modeling.Diagrams.ImageField>.|
|Definir uma imagem de plano de fundo em qualquer forma|Substitua InitializeInstanceResources() para adicionar um ImageField ancorado. Ver [Personalizando a apresentação no diagrama](../modeling/customizing-presentation-on-the-diagram.md).|
|Aninhar formas em qualquer profundidade|Configure uma recursiva a inserção de árvore. Defina BoundsRules para conter as formas. Ver [Personalizando a apresentação no diagrama](../modeling/customizing-presentation-on-the-diagram.md).|
|Anexe conectores em pontos fixos em limites de um elemento.|Defina elementos incorporados de terminal, representados por portas pequeno no diagrama. Use BoundsRules para corrigir as portas em vigor. Consulte o exemplo de diagrama de circuito em [SDK de visualização e modelagem](http://go.microsoft.com/fwlink/?LinkID=186128).|
|Campo de texto exibe um valor derivado de outros valores.|Mapear o decorador de texto para uma propriedade de domínio Calculated ou armazenamento personalizado. Para obter mais informações, consulte [Calculated e propriedades de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md).|
|Propagar alterações entre os elementos de modelo, ou entre formas|Ver [validação em uma linguagem específica do domínio](../modeling/validation-in-a-domain-specific-language.md).|
|Propaga alterações aos recursos, como outras extensões do Visual Studio fora do repositório.|Ver [manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).|
|Janela Propriedades exibe as propriedades de um elemento relacionado.|Configure o encaminhamento de propriedade. Ver [Personalizando a janela propriedades](../modeling/customizing-the-properties-window.md).|
|Categorias de propriedades|A janela Propriedades é dividida em seções chamadas categorias. Defina as **categoria** de suas propriedades de domínio. Propriedades com o mesmo nome de categoria aparecerá na mesma seção. Você também pode definir as **categoria** de uma função de relação.|
|Controlar o acesso do usuário para propriedades de domínio|Definir **é navegável** false para impedir que uma propriedade de domínio que aparecem na janela Propriedades em tempo de execução. Você ainda pode mapeá-lo para decoradores de texto.<br /><br /> **É IU somente leitura** impede usuários de alterar uma propriedade de domínio.<br /><br /> Acesso a programas para a propriedade de domínio não é afetado.|
|Altere o nome, ícone e visibilidade de nós no Gerenciador de modelos da sua DSL.|Ver [Personalizando o Gerenciador de modelos](../modeling/customizing-the-model-explorer.md).|
|Habilitar copiar, recortar e colar|Defina as **habilitar copiar e colar** propriedade da **Editor** nó no Gerenciador de DSL.|
|Copie suas metas e links de referência sempre que um elemento é copiado. Por exemplo, copie os comentários anexados a um item.|Defina as **propaga cópia** propriedade da função de origem (representada pela linha em um dos lados da relação de domínio no diagrama de definição de DSL).<br /><br /> Escreva código para substituir ProcessOnCopy para atingir efeitos mais complexos.<br /><br /> Ver [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).|
|Excluir, reassociar ou vincular novamente os elementos relacionados quando um elemento é excluído.|Defina as **propaga exclusão** valor de uma função de relação. Para obter efeitos mais complexos, substituir `ShouldVisitRelationship` e `ShouldVisitRolePlayer` métodos na `MyDslDeleteClosure` classe, definida em **DomainModel.cs**<br /><br /> Consulte [Personalizando o comportamento de exclusão](../modeling/customizing-deletion-behavior.md)|
|Preserve o layout da forma e a aparência em cópia e arraste e solte.|Adicionar as formas e conectores para copiado `ElementGroupPrototype`. É o método mais conveniente para substituir `ElementOperations.CreateElementGroupPrototype()`<br /><br /> Ver [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md).|
|Cole formas em um local escolhido, como a posição atual do cursor.|Substituir `ClipboardCommandSet.ProcessOnCopy()` para usar a versão específica do local de `ElementOperations.Merge().` consulte [personalizar o comportamento de cópia](../modeling/customizing-copy-behavior.md).|
|Criar links adicionais ao colar|Override ClipboardCommandSet.ProcessOnPasteCommand()|
|Permitir arrastar e soltar este diagrama para outras DSLs e Windows elementos|Consulte [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md)|
|Permitir que uma forma ou a ferramenta a ser arrastado para uma forma de filho, como uma porta, como se ele foi arrastado para o pai.|Defina uma diretiva Element Merge na classe de objeto de destino para encaminhar o objeto solto ao pai. Ver [Personalizando a criação de elemento e movimentação](../modeling/customizing-element-creation-and-movement.md).|
|Permitir que uma forma ou a ferramenta a ser arrastado para uma forma e têm links adicionais ou objetos criados. Por exemplo, para permitir que um comentário a ser solto em um item ao qual ele deve ser vinculado.|Definir uma diretiva Element Merge na classe de domínio de destino e definir os links a ser gerado. Em casos complexos, você pode adicionar código personalizado. Ver [Personalizando a criação de elemento e movimentação](../modeling/customizing-element-creation-and-movement.md).|
|Crie um grupo de elementos com uma ferramenta. Por exemplo, um componente com um conjunto fixo de portas.|Substitua o método de inicialização da caixa de ferramentas no ToolboxHelper.cs. Crie um protótipo de grupo de elemento (EGP) que contém os elementos e seus vínculos de relação. Ver [personalizando ferramentas e a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md).<br /><br /> Inclua as formas de entidade de segurança e a porta em que o EGP ou definir BoundsRules para posicionar as formas de porta, quando o EGP é instanciado. Ver [BoundsRules restringem o local de forma e tamanho](../modeling/boundsrules-constrain-shape-location-and-size.md).|
|Use uma ferramenta de conexão para criar uma instância de vários tipos de relação.|Adicione diretivas de conectar-se de Link (LCD) para o construtor de Conexão que é invocado pela ferramenta. Os LCDs determinam o tipo da relação entre os tipos dos dois elementos. Para fazer isso dependem dos estados dos elementos, você pode adicionar código personalizado. Ver [personalizando ferramentas e a caixa de ferramentas](../modeling/customizing-tools-and-the-toolbox.md).|
|Ferramentas de adesivas - o usuário pode clicar duas vezes qualquer ferramenta para criar muitas formas ou conectores em sucessão.|No Gerenciador de DSL, selecione o `Editor` nó. Na janela Propriedades, defina **usa itens de caixa de ferramentas adesivo**.|
|Definir comandos de menu|Consulte [como: modificar um comando de Menu padrão](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)|
|Restringir o modelo com as regras de validação|Consulte [validação em uma linguagem específica de domínio](../modeling/validation-in-a-domain-specific-language.md)|
|Gere código, arquivos de configuração ou documentos de uma DSL.|[Gerando código com base em uma linguagem específica de domínio](../modeling/generating-code-from-a-domain-specific-language.md)|
|Personalizar como os modelos são salvos ao arquivo.|Consulte [Personalizando o armazenamento de arquivos e a serialização de XML](../modeling/customizing-file-storage-and-xml-serialization.md)|
|Salve modelos de bancos de dados ou outras mídias.|Substituir *YourLanguage*DocData<br /><br /> Consulte [Personalizando o armazenamento de arquivos e a serialização de XML](../modeling/customizing-file-storage-and-xml-serialization.md)|
|Integre diversas DSLs, de modo que eles funcionam como parte de um aplicativo.|Ver [integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).|
|Permitir que a sua DSL seja estendida por terceiros e controlar a extensão.|[Estender a DSL usando MEF](../modeling/extend-your-dsl-by-using-mef.md)<br /><br /> [Compartilhando classes entre DSLs por meio de uma biblioteca de DSLs](../modeling/sharing-classes-between-dsls-by-using-a-dsl-library.md)<br /><br /> [Definindo uma política de bloqueio para criar segmentos somente leitura](../modeling/defining-a-locking-policy-to-create-read-only-segments.md)|

## <a name="see-also"></a>Consulte também

- [Como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
- [SDK de Modelagem para Visual Studio – linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]