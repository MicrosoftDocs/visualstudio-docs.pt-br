---
title: Respondendo a alterações e propagando-as
description: Saiba que quando um elemento é criado, excluído ou atualizado, você pode escrever código que propaga a alteração para outras partes do modelo ou para recursos externos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d6fc8345ca90414f410dde9a089d9529ed19536b
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387574"
---
# <a name="respond-to-and-propagate-changes"></a>Responder e propagar alterações

Quando um elemento é criado, excluído ou atualizado, você pode escrever código que propaga a alteração para outras partes do modelo ou para recursos externos, como arquivos, bancos de dados ou outros componentes.

## <a name="reference"></a>Referência

Como diretriz, considere essas técnicas na seguinte ordem:

|Técnica|Cenários|Para obter mais informações|
|-|-|-|
|Defina uma propriedade de domínio Calculated.|Uma propriedade de domínio cujo valor é calculado de outras propriedades no modelo. Por exemplo, um preço que é a soma dos preços dos elementos relacionados.|[Propriedades calculadas e de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md)|
|Defina uma propriedade de domínio de Armazenamento Personalizado.|Uma propriedade de domínio armazenada em outras partes do modelo ou externamente. Por exemplo, você pode analisar uma cadeia de caracteres de expressão em uma árvore no modelo.|[Propriedades calculadas e de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md)|
|Substituir manipuladores de alterações, como OnValueChanging e OnDeleting|Mantenha elementos diferentes em sincronia e mantenha valores externos em sincronia com o modelo.<br /><br /> Restringir valores a intervalos definidos.<br /><br /> Chamado imediatamente antes e depois do valor da propriedade e outras alterações. Você pode encerrar a alteração lançando uma exceção.|[Manipuladores de alterações nos valores da propriedade de domínio](../modeling/domain-property-value-change-handlers.md)|
|Regras|Você pode definir regras que estão na fila para execução logo antes do final de uma transação na qual ocorreu uma alteração. Eles não são executados em Desfazer ou Refazer. Use-os para manter uma parte do armazenamento em sincronia com outra.|[Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md)|
|Eventos da Loja|O armazenamento de modelagem fornece notificações de eventos como adicionar ou excluir um elemento ou link ou alterar o valor de uma propriedade. O evento também é executado em Desfazer e Refazer. Use eventos de armazenamento para atualizar valores que não estão no armazenamento.|[Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md)|
|Eventos do .NET|As formas têm manipuladores de eventos que respondem a cliques do mouse e outros gestos. Você precisa se registrar para esses eventos para cada objeto. O registro normalmente é feito em uma substituição de InitializeInstanceResources e deve ser feito para cada elemento.<br /><br /> Esses eventos geralmente ocorrem fora de uma transação.|[Como interceptar um clique em uma forma ou um decorador](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|
|Regras de limites|Uma regra de limites é usada especificamente para restringir os limites de uma forma.|[BoundsRules restringem o local e o tamanho de uma forma](/previous-versions/visualstudio/visual-studio-2015/modeling/boundsrules-constrain-shape-location-and-size?preserve-view=true&view=vs-2015)|
|Regras de seleção|As regras de seleção restringem especificamente o que o usuário pode selecionar.|[Como acessar e restringir a seleção atual](../modeling/how-to-access-and-constrain-the-current-selection.md)|
|OnAssocatedPropertyChanged|Indique os estados dos elementos de modelo usando recursos de formas e conectores, como sombra, setas, cor e larguras de linha e estilo.|[Atualizando formas e conectores para refletir o modelo](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|

## <a name="compare-rules-and-store-events"></a>Comparar regras e armazenar eventos

Os notificadores de alteração, as regras e os eventos são executados quando ocorrem alterações em um modelo.

As regras geralmente são aplicadas na transação final em que a alteração ocorreu e os eventos são aplicados depois que as alterações em uma transação são confirmados.

Use eventos de armazenamento para sincronizar o modelo com objetos fora do Store e regras para manter a consistência dentro do Store.

- **Criando regras personalizadas** Você cria uma regra personalizada como uma classe derivada de uma regra abstrata. Você também deve notificar a estrutura sobre a regra personalizada. Para obter mais informações, consulte [Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md).

- **Assinando eventos** Antes de assinar um evento, crie um manipulador de eventos e um delegado. Em seguida, <xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A> use a propriedade para assinar o evento. Para obter mais informações, consulte [Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

- **Desfazer alterações** Quando você desfaz uma transação, os eventos são gerados, mas as regras não são aplicadas. Se uma regra alterar um valor e você desfazer essa alteração, o valor será redefinido para o valor original durante a ação de desfazer. Quando um evento é gerado, você deve alterar manualmente o valor de volta para seu valor original. Para saber mais sobre transações e desfazer, [consulte Como usar transações para atualizar o modelo.](../modeling/how-to-use-transactions-to-update-the-model.md)

- **Passando argumentos de evento para regras e eventos** Ambos os eventos e regras são passados `EventArgs` um parâmetro que tem informações sobre como o modelo foi alterado.

## <a name="see-also"></a>Confira também

- [Como interceptar um clique em uma forma ou um decorador](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)
- [Escrevendo código para personalizar uma linguagem Domain-Specific linguagem](../modeling/writing-code-to-customise-a-domain-specific-language.md)