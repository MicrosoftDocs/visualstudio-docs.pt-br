---
title: Respondendo a alterações e propagando | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, events
ms.assetid: fc2e9ac5-7a84-44ed-9945-94e45f89c227
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a9838e934421e619c85f348052fbe589288391c1
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60104714"
---
# <a name="responding-to-and-propagating-changes"></a>Respondendo a alterações e propagando-as
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando um elemento é criado, excluído ou atualizado, você pode escrever código que propaga a alteração para outras partes do modelo ou a recursos externos como arquivos, bancos de dados ou outros componentes.  
  
## <a name="in-this-section"></a>Nesta seção  
 Como diretriz, considere estas técnicas na seguinte ordem:  
  
|Técnica|Cenários|Para obter mais informações|  
|---------------|---------------|--------------------------|  
|Defina uma propriedade de domínio Calculated.|Uma propriedade de domínio cujo valor é calculado de outras propriedades no modelo. Por exemplo, um preço que é a soma dos preços dos elementos relacionados.|[Propriedades calculadas e de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md)|  
|Defina uma propriedade de domínio personalizado de armazenamento.|Uma propriedade de domínio armazenada em outras partes do modelo ou externamente. Por exemplo, você poderia analisar uma cadeia de caracteres de expressão em uma árvore no modelo.|[Propriedades calculadas e de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md)|  
|Substituir os manipuladores de alteração como OnValueChanging e OnDeleting|Mantenha os elementos diferentes em sincronia e valores externos em sincronia com o modelo.<br /><br /> Restringir os valores em intervalos definidos.<br /><br /> Chamado imediatamente antes e depois o valor da propriedade e outras alterações. Você pode encerrar a alteração lançando uma exceção.|[Manipuladores de alterações nos valores da propriedade de domínio](../modeling/domain-property-value-change-handlers.md)|  
|Regras|Você pode definir regras que estão na fila para execução antes do final de uma transação em que uma alteração tiver ocorrido. Eles não são executados em Desfazer ou refazer. Usá-los para manter uma parte do armazenamento em sincronia com o outro.|[Regras propagam alterações dentro do modelo](../modeling/rules-propagate-changes-within-the-model.md)|  
|Eventos de Store|O repositório de modelagem fornece notificações de eventos, como adicionar ou excluir um elemento ou um link ou alterando o valor de uma propriedade. O evento também é executado em Desfazer e refazer. Use eventos de armazenamento para atualizar os valores que não estão no repositório.|[Manipuladores de eventos propagam alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md)|  
|Eventos do .NET|Formas têm manipuladores de eventos que respondem a cliques do mouse e outros gestos. Você deve registrar esses eventos para cada objeto. O registro normalmente é feito em uma substituição de InitializeInstanceResources e deve ser feito para cada elemento.<br /><br /> Esses eventos geralmente ocorrem fora de uma transação.|[Como: Interceptar um clique em uma forma ou um decorador](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)|  
|Regras de limites|Uma regra é usada especificamente para restringir os limites de uma forma.|[BoundsRules restringem o local e o tamanho de uma forma](../modeling/boundsrules-constrain-shape-location-and-size.md)|  
|Regras de seleção|Regras de seleção restringem especificamente o que o usuário pode selecionar.|[Como: Acessar e restringir a seleção atual](../modeling/how-to-access-and-constrain-the-current-selection.md)|  
|OnAssocatedPropertyChanged|Indica estados dos elementos de modelo usando os recursos de formas e conectores, como sombra, setas, cor e larguras de linha e estilo.|[Atualizando formas e conectores para refletir o modelo](../modeling/updating-shapes-and-connectors-to-reflect-the-model.md)|  
  
## <a name="comparing-rules-and-store-events"></a>**Comparando as regras e eventos da Store**  
 Alteração notifiers, regras e eventos são executados quando ocorrem alterações em um modelo.  
  
 Geralmente, as regras são aplicadas na transação final em que a alteração ocorreu e eventos são aplicados depois que as alterações em uma transação sejam confirmadas.  
  
 Use eventos de armazenamento para sincronizar o modelo com objetos fora da Store e regras para manter a consistência dentro de Store.  
  
- **Criação de regras personalizadas** criar uma regra personalizada como uma classe derivada de uma regra de abstrata. Você também deve notificar o framework sobre a regra personalizada. Para obter mais informações, consulte [propagam alterações dentro do modelo de regras](../modeling/rules-propagate-changes-within-the-model.md).  
  
- **Assinando eventos** antes de assinar um evento, crie um manipulador de eventos e o delegado. Em seguida, use o <xref:Microsoft.VisualStudio.Modeling.Store.EventManagerDirectory%2A>propriedade para assinar o evento. Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md).  
  
- **Desfazendo alterações** ao desfazer uma transação, os eventos são gerados, mas não são aplicadas as regras. Se um valor é alterado de uma regra e desfazer essa alteração, o valor será redefinido para o valor original durante a ação de desfazer. Quando um evento é gerado, você deve alterar manualmente o valor para seu valor original. Para saber mais sobre transactons e desfazer, consulte [como: Usar transações para atualizar o modelo](../modeling/how-to-use-transactions-to-update-the-model.md).  
  
- **Passando argumentos de evento para eventos e regras** ambos os eventos e as regras são transmitidas uma `EventArgs` parâmetro que tem informações sobre como o modelo foi alterado.  
  
## <a name="see-also"></a>Consulte também  
 [Como: Interceptar um clique em uma forma ou um decorador](../modeling/how-to-intercept-a-click-on-a-shape-or-decorator.md)   
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
