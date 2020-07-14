---
title: Propriedades de propriedades de domínio
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain properties
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0342146f604d86dd93ce25ed20e6ab393c581ea9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544164"
---
# <a name="properties-of-domain-properties"></a>Propriedades de propriedades de domínio
Uma *propriedade de domínio* é um recurso de um elemento de modelo que pode conter um valor. Por exemplo, a classe de domínio `Person` poderia ter as propriedades `Name` e `BirthDate`. Em Definição de DSL, as propriedades de domínio são listadas na caixa de classe de domínio no diagrama e sob a classe de domínio no Gerenciador de DSL. Para obter mais informações, consulte [como definir uma linguagem específica de domínio](../modeling/how-to-define-a-domain-specific-language.md).

> [!NOTE]
> A palavra "propriedade" possui dois usos. Uma *propriedade de domínio* é um recurso que você define em uma classe de domínio. Por outro lado, muitos elementos de uma DSL têm *Propriedades*, que são listadas na janela **Propriedades** na definição de DSL. Por exemplo, cada propriedade de domínio tem um conjunto de propriedades, que são descritas neste tópico.

 No momento da execução, quando um usuário cria instâncias da classe de domínio, os valores das propriedades de domínio podem ser vistos na janela Propriedades e exibidos nas formas.

 A maioria das propriedades de domínio é implementada como propriedades CLR comuns. No entanto, do ponto de vista da programação, as propriedades de domínio têm funcionalidade mais rica do que as propriedades de programa comuns:

- Você pode definir regras e eventos que monitoram o estado de uma propriedade. Para obter mais informações, consulte [respondendo e propagando alterações](../modeling/responding-to-and-propagating-changes.md).

- As transações ajudam a impedir estados inconsistentes. Para obter mais informações, consulte [navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).

  Quando você seleciona uma Propriedade de Domínio em um diagrama ou no Gerenciador de DSL, pode ver os itens a seguir na janela Propriedades. Para obter mais informações sobre como usar esses itens, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

|Propriedade|Descrição|Valor Padrão|
|-|-|-|
|**Descrição**|A descrição usada para documentar a interface do usuário (IU) do designer gerado.|\<none>|
|**Nome de exibição**|O nome que será exibido no designer gerado para essa propriedade de domínio. Ele pode conter espaços e pontuação, por exemplo "Título da Música".|\<none>|
|**Provedor de nome de elemento**|Só será aplicável se você tiver configurado `Is Element Name` como `true`. Você pode escrever código que fornece um nome para um novo elemento de uma classe de domínio, substituindo o comportamento padrão.<br /><br /> Em um arquivo de código no projeto DSL, crie uma classe derivada de <xref:Microsoft.VisualStudio.Modeling.ElementNameProvider>.<br /><br /> Depois, no Gerenciador de DSL, clique com o botão direito do mouse na raiz do DSL e clique em Adicionar Tipo Externo. Insira o nome da sua classe.<br /><br /> Escolha essa propriedade de domínio novamente e escolha o nome da classe na lista suspensa.|\<none>|
|**Modificador de acesso getter**|O nível de acesso da classe de domínio (`public` ou `internal`). Controla o escopo no qual o código do programa pode acessar a propriedade.|`public`|
|**Palavra-chave de ajuda**|A palavra-chave opcional usada para indexar a ajuda F1 desta propriedade de domínio.|\<none>|
|**É navegável**|Se `True`, a propriedade de domínio será exibida para o usuário na janela de propriedades quando modelos deste DSL forem abertos.<br /><br /> Se `False`, a propriedade de domínio ficará oculta na interface do usuário.<br /><br /> Se você quiser tornar a propriedade de domínio visível, mas somente leitura, definir **é somente leitura da interface do usuário**.|`True`|
|**É nome de elemento**|Se `True`, esta propriedade de domínio será exibida como o nome do seu elemento modelo no Gerenciador de DSL.<br /><br /> Novos elementos do modelo receberão um valor padrão único para esta propriedade. Se você quiser controlar como esses valores são gerados, defina **provedor de nome de elemento**.|`False`|
|**É IU Somente leitura**|Se `True`, o valor da propriedade de domínio não poderá ser alterada usando a IU. Ele ainda pode ser definido por programas e estará visível na janela Propriedades.<br /><br /> Se você quiser ocultar a propriedade de domínio do usuário, defina **é navegável**. Se você quiser controlar o acesso por programas, defina **modificador de acesso setter**.|`False`|
|**Tipo**|O tipo da propriedade de domínio (`Normal`, `Calculated` ou `CustomStorage`). Para obter mais informações, consulte [Propriedades de armazenamento calculadas e personalizadas](../modeling/calculated-and-custom-storage-properties.md).|`Normal`|
|**Nome**|O nome da propriedade do domínio. Ele deve ser um identificador válido, por exemplo, **SongTitle**.|\<none>|
|**Observações**|Notas informais associadas a esta propriedade de domínio.|\<none>|
|**Modificador de acesso setter**|O modificador de acesso do setter. Controla o escopo no qual o código do programa pode definir a propriedade.|`public`|
|**Tipo**|O tipo de propriedade. Para adicionar à lista de tipos disponíveis, clique com o botão direito do mouse na raiz da DSL no Gerenciador de DSL e clique em **Adicionar tipo externo**.|`String`|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)