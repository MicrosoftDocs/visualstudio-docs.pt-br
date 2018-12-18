---
title: Propriedades das propriedades de domínio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, domain properties
ms.assetid: a9471562-d6f2-46bf-9872-e0d66ba03150
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 977594493279d52154de3cb5ef7bce56d4d8f985
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836834"
---
# <a name="properties-of-domain-properties"></a>Propriedades de propriedades de domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um *propriedade de domínio* é um recurso de um elemento de modelo que pode conter um valor. Por exemplo, a classe de domínio `Person` poderia ter as propriedades `Name` e `BirthDate`. Em Definição de DSL, as propriedades de domínio são listadas na caixa de classe de domínio no diagrama e sob a classe de domínio no Gerenciador de DSL. Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md).  
  
> [!NOTE]
>  A palavra "propriedade" possui dois usos. Um *propriedade de domínio* é um recurso que você define em uma classe de domínio. Por outro lado, muitos elementos de uma DSL têm *propriedades*, que são listadas na **propriedades** janela na definição de DSL. Por exemplo, cada propriedade de domínio tem um conjunto de propriedades, que são descritas neste tópico.  
  
 No momento da execução, quando um usuário cria instâncias da classe de domínio, os valores das propriedades de domínio podem ser vistos na janela Propriedades e exibidos nas formas.  
  
 A maioria das propriedades de domínio é implementada como propriedades CLR comuns. No entanto, do ponto de vista da programação, as propriedades de domínio têm funcionalidade mais rica do que as propriedades de programa comuns:  
  
- Você pode definir regras e eventos que monitoram o estado de uma propriedade. Para obter mais informações, consulte [respondendo a e propagando alterações](../modeling/responding-to-and-propagating-changes.md).  
  
- As transações ajudam a impedir estados inconsistentes. Para obter mais informações, consulte [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md).  
  
  Quando você seleciona uma Propriedade de Domínio em um diagrama ou no Gerenciador de DSL, pode ver os itens a seguir na janela Propriedades. Para obter mais informações sobre como usar esses itens, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).  
  
|Propriedade|Descrição|Valor padrão|  
|--------------|-----------------|-------------------|  
|**Descrição**|A descrição usada para documentar a interface do usuário (IU) do designer gerado.|\<Nenhum >|  
|**Nome de exibição**|O nome que será exibido no designer gerado para essa propriedade de domínio. Ele pode conter espaços e pontuação, por exemplo "Título da Música".|\<Nenhum >|  
|**Nome do provedor de elemento**|Só será aplicável se você tiver configurado `Is Element Name` como `true`. Você pode escrever código que fornece um nome para um novo elemento de uma classe de domínio, substituindo o comportamento padrão.<br /><br /> Em um arquivo de código no projeto DSL, crie uma classe derivada de <xref:Microsoft.VisualStudio.Modeling.ElementNameProvider>.<br /><br /> Depois, no Gerenciador de DSL, clique com o botão direito do mouse na raiz do DSL e clique em Adicionar Tipo Externo. Insira o nome da sua classe.<br /><br /> Escolha essa propriedade de domínio novamente e escolha o nome da classe na lista suspensa.|\<Nenhum >|  
|**Modificador de acesso getter**|O nível de acesso da classe de domínio (`public` ou `internal`). Controla o escopo no qual o código do programa pode acessar a propriedade.|`public`|  
|**Palavra-chave ajuda**|A palavra-chave opcional usada para indexar a ajuda F1 desta propriedade de domínio.|\<Nenhum >|  
|**É navegável**|Se `True`, a propriedade de domínio será exibida para o usuário na janela de propriedades quando modelos deste DSL forem abertos.<br /><br /> Se `False`, a propriedade de domínio ficará oculta na interface do usuário.<br /><br /> Se você quiser tornar a propriedade de domínio visível, mas somente leitura, defina **é IU somente leitura**.|`True`|  
|**É o nome do elemento**|Se `True`, esta propriedade de domínio será exibida como o nome do seu elemento modelo no Gerenciador de DSL.<br /><br /> Novos elementos do modelo receberão um valor padrão único para esta propriedade. Se você quiser controlar como esses valores são gerados, defina **provedor de nomes de elemento**.|`False`|  
|**É IU somente leitura**|Se `True`, o valor da propriedade de domínio não poderá ser alterada usando a IU. Ele ainda pode ser definido por programas e estará visível na janela Propriedades.<br /><br /> Se você quiser ocultar a propriedade de domínio do usuário, defina **é navegável**. Se você quiser controlar o acesso por programas, defina **modificador de acesso Setter**.|`False`|  
|**Tipo**|O tipo da propriedade de domínio (`Normal`, `Calculated` ou `CustomStorage`). Para obter mais informações, consulte [Calculated e propriedades de armazenamento personalizado](../modeling/calculated-and-custom-storage-properties.md).|`Normal`|  
|**Nome**|O nome da propriedade do domínio. Ele deve ser um identificador válido, por exemplo **SongTitle**.|\<Nenhum >|  
|**Observações**|Notas informais associadas a esta propriedade de domínio.|\<Nenhum >|  
|**Modificador de acesso setter**|O modificador de acesso do setter. Controla o escopo no qual o código do programa pode definir a propriedade.|`public`|  
|**Tipo**|O tipo de propriedade. Para adicionar à lista de tipos disponíveis, clique com botão direito a raiz do DSL no Gerenciador de DSL e clique em **Adicionar tipo externo**.|`String`|  
  
## <a name="see-also"></a>Consulte também  
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



