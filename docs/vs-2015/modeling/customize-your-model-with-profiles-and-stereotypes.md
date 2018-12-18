---
title: Personalizar o modelo com perfis e estereótipos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML model, profiles
- UML model, stereotypes
- UML model, customizing
ms.assetid: fd607157-0d3a-4583-a84e-427a4b2a5acb
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 33e887764c535083c2449a7d333868b2ccd9c4c5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727699"
---
# <a name="customize-your-model-with-profiles-and-stereotypes"></a>Personalizar o modelo com perfis e estereótipos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode adaptar os elementos de modelo UML padrão, como classes e componentes, personalizá-los para fins específicos. Você pode aplicar uma *estereótipo* a um elemento de modelo que pode alterar a lista do elemento de propriedades. Estereótipos são definidos dentro de coleções chamadas *perfis*.  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Para usar um estereótipo, você pode vincular um pacote a um perfil. Isso permite aplicar os estereótipos que são definidos no perfil para os elementos no pacote. Alguns perfis são instaladas junto com o Visual Studio. Além disso, você pode definir seus próprios perfis.  
  
 Estereótipos podem ser definidos na lista de propriedades de um elemento. Para os tipos principais de forma em um diagrama, os estereótipos aplicados também são exibidos na forma, conforme mostrado no exemplo.  
  
 ![Uma classe UML com um estereótipo. ](../modeling/media/uml-class-stereotype.png "UML_class_stereotype")  
  
> [!NOTE]
>  Se você usar um perfil para criar um modelo e, em seguida, compartilhar o modelo com outra pessoa, eles poderão ver os estereótipos, a menos que eles instalaram o mesmo perfil em seu computador.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Adicionar estereótipos a elementos de modelo UML](../modeling/add-stereotypes-to-uml-model-elements.md)|Colocar um elemento de modelo em um pacote, o pacote de vinculação a um perfil e aplicação de um estereótipo para o elemento.|  
|[Estereótipos padrão para modelos UML](../modeling/standard-stereotypes-for-uml-models.md)|O UML padrão perfis de L2 e L3 são instalados com o Visual Studio, e cada modelo está vinculado a eles por padrão. Eles fornecem os estereótipos que você pode usar para fazer anotações em seus modelos.<br /><br /> Por exemplo, você pode aplicar o estereótipo «especificação» a uma classe para indicar que ele destina-se somente para definir o comportamento visível externamente de suas instâncias|  
|[Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)|Você pode definir seus próprios estereótipos e ferramentas que são adaptadas à sua própria área do aplicativo.<br /><br /> Por exemplo, se você desenvolver software bancário, você pode definir um estereótipo «Conta» que pode ser aplicado às classes. Você pode usar diagramas de classe para descrever diferentes tipos de conta e suas relações.|  
|[Instalar um perfil UML](../modeling/install-a-uml-profile.md)|Se alguém tenha dado a você um perfil UML, você pode instalá-lo em seu computador.|  
|[Definir um item de caixa de ferramentas de modelagem personalizada](../modeling/define-a-custom-modeling-toolbox-item.md)|Um item de caixa de ferramentas personalizado evita que você definir repetidamente um estereótipo em novos elementos.|  
|[Classes UML de cor por estereótipo](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)|Esse código de exemplo estende os diagramas UML. Ela configura automaticamente a cor de uma forma UML de acordo com o estereótipo do elemento.|



