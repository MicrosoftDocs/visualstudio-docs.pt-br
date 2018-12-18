---
title: Integrar modelos UML a outros modelos e ferramentas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML - extending, references to models
ms.assetid: 9e75e7d1-93cf-4196-baa3-bd10b9af16d3
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: d1cc5a26a9c2febb0dd1dff3c0d14ba3786dde9f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764134"
---
# <a name="integrate-uml-models-with-other-models-and-tools"></a>Integrar modelos UML a outros modelos e ferramentas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Modelos de UML podem ser integrados com outros modelos e linguagens específicas de domínio.  
  
 Você pode integrar modelos das seguintes maneiras, escrevendo o código de extensão para executar uma variedade de funções:  
  
 Anexe as referências de qualquer elemento para outros itens como arquivos ou elementos em outros modelos.  
 Em um elemento UML, você pode armazenar links para outros elementos UML, arquivos ou outros objetos por suas identidades como cadeias de caracteres de codificação.  
  
 Por exemplo, você poderia escrever uma extensão que pode vincular qualquer ação de UML (ou seja, um elemento em um diagrama de atividade) para outro diagrama de atividade. Quando o usuário clica duas vezes a ação, o outro diagrama é aberto. Isso permite que o usuário forneça uma exibição mais detalhada da ação.  
  
 Há duas maneiras em que você pode armazenar cadeias de caracteres e outros dados em qualquer elemento:  
  
- **Propriedades de estereótipo.** Você pode definir um perfil UML, em que você define um estereótipo que adiciona propriedades a tipos especificados do elemento UML. Por exemplo, você pode definir um perfil que adiciona uma propriedade chamada **MoreDetail** a uma ação de UML. Você pode escrever o código de extensão que lojas vinculem dados em uma ação aplicando o estereótipo para a ação e, em seguida, armazenar os dados na propriedade.  
  
   O estereótipo e suas propriedades são visíveis para o usuário na janela Propriedades.  
  
   Para implantar essa extensão, você deve empacotar a definição de perfil e o código de extensão em uma única [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensão.  
  
   Para obter mais informações, consulte [definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md).  
  
   Para um projeto de exemplo no qual um perfil é implantado junto com os comandos de menu e manipuladores de gestos, consulte [exemplo: perfis UML](http://go.microsoft.com/fwlink/?LinkID=213811).  
  
- **Referências.** Você pode anexar um conjunto de cadeias de caracteres a qualquer elemento UML. Você pode escrever código que armazena as informações como um nome de arquivo ou o GUID de outro elemento. Isso pode ser feito sem fornecer definições adicionais. Referências não são diretamente visíveis para o usuário.  
  
   Para obter mais informações, consulte [elementos de modelo de anexar cadeias de caracteres de referência para UML](../modeling/attach-reference-strings-to-uml-model-elements.md). Para obter um exemplo, consulte [elementos UML de Link de diagramas ou outros arquivos](http://go.microsoft.com/fwlink/?LinkId=213813).  
  
  Há duas maneiras de codificar as referências a elementos de modelo:  
  
- **GUID e nome de arquivo** do elemento de modelo de destino e o modelo que o contém ou um diagrama específico que a exibe.  
  
   Por exemplo, consulte [elementos UML de Link de diagramas ou outros arquivos](http://go.microsoft.com/fwlink/?LinkId=213813).  
  
- **Referências do ModelBus.** ModelBus é uma estrutura para criar e resolver referências entre os modelos. Ele inclui o seletor do ModelBus, que permite que o usuário selecione um elemento em um modelo. Ele também ajuda o usuário para resolver as referências que são perdidas devido a alterações no modelo de destino.  
  
   Para obter mais informações, consulte [integrando modelos por meio do Visual Studio Modelbus](../modeling/integrating-models-by-using-visual-studio-modelbus.md).  
  
  Propaga alterações de um modelo para outro.  
  Por exemplo, você pode sincronizar o nome de um elemento com o nome do diagrama vinculado, para que se o usuário altera uma, o outro também será alterado. Há dois mecanismos para fazer isso:  
  
1. **Regras de VMSDK** pode ser usado para propagar alterações dentro do mesmo modelo.  
  
    Por exemplo, consulte [elementos UML de Link de diagramas ou outros arquivos](http://go.microsoft.com/fwlink/?LinkId=213813).  
  
2. **Eventos de VMSDK** pode ser usado para propagar alterações fora do modelo – por exemplo, para alterar o nome do arquivo de um documento vinculado ou para alterar um elemento em outro modelo.  
  
   Para obter informações sobre os dois desses mecanismos, consulte [como: responder a alterações em um modelo UML](../misc/how-to-respond-to-changes-in-a-uml-model.md).  
  
   Arrastar elementos para copiá-los de um modelo para outro  
   Você pode permitir que o usuário criar elementos arrastando itens para um diagrama UML. O elemento criado não tem uma cópia do original. Por exemplo, você pode permitir que o usuário arrastar um diagrama de atividade do Gerenciador de soluções para outro diagrama de atividade, para criar uma nova ação.  
  
   Para obter mais informações, consulte [definir um manipulador de gesto em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md) e [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md).  
  
## <a name="samples"></a>Exemplos  
 Consulte o exemplo de código [elementos UML de Link de diagramas ou outros arquivos](http://go.microsoft.com/fwlink/?LinkId=213813). O exemplo permite aos usuários arrastar um arquivo para qualquer elemento UML e abri-lo mais tarde clicando duas vezes no elemento. Por exemplo, você pode vincular um diagrama de atividade a um elemento de casos de uso. Um ícone mostra quais elementos têm links.  
  
 Este exemplo de código demonstra as seguintes técnicas:  
  
- [Anexar cadeias de caracteres de referência a elementos de modelo UML](../modeling/attach-reference-strings-to-uml-model-elements.md)  
  
   O código de exemplo armazena os caminhos de arquivo e o elemento GUIDs em cadeias de caracteres de referência que estão associadas ao elemento.  
  
- Como adicionar os decoradores aos elementos UML. Para obter informações gerais sobre os decoradores, consulte [personalizando campos de texto e imagem](../modeling/customizing-text-and-image-fields.md).  
  
   O exemplo adiciona um decorador de imagem às formas UML.  
  
- [Como responder a alterações em um modelo UML](../misc/how-to-respond-to-changes-in-a-uml-model.md)  
  
   O exemplo demonstra como definir uma regra que responde às novas formas que aparecem em um diagrama.  
  
- [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)  
  
- [Definir um manipulador de gestos em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)  
  
   O exemplo demonstra como manipular itens arrastados do Windows Explorer (ou Explorador de arquivos), Gerenciador de soluções e outros elementos UML.  
  
  Para um exemplo em que um modelo UML é ser lidos por uma DSL, consulte [como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md).  
  
## <a name="see-also"></a>Consulte também  
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [Definir um manipulador de gesto em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)   
 [Como: adicionar um manipulador de arrastar e soltar](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [Como: responder a alterações em um modelo UML](../misc/how-to-respond-to-changes-in-a-uml-model.md)   
 [Amostra: Perfis UML](http://go.microsoft.com/fwlink/?LinkID=213811)   
 [Elementos UML de link de diagramas ou outros arquivos](http://go.microsoft.com/fwlink/?LinkId=213813)



