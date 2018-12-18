---
title: Adicionar estereótipos a elementos de modelo UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML model, stereotypes
ms.assetid: 82545252-83ce-4e11-a419-61373be75d16
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: dbd5f4288833a29bdfef2df97ee71ac765ae168f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725383"
---
# <a name="add-stereotypes-to-uml-model-elements"></a>Adicionar estereótipos a elementos de modelo UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode adicionar um estereótipo para um elemento de modelo UML anotá-lo e fornecê-los com propriedades especializadas. Para adicionar um estereótipo para um elemento de modelo, o estereótipo deve ser definido em um perfil, e você deve vincular o perfil a um pacote ou para o modelo que contém o elemento de modelo. Cada estereótipo pode ser adicionado somente a determinados tipos de elemento de modelo, como classes UML, casos de uso ou componentes.  
  
 Por exemplo, se você quiser definir uma classe UML com o estereótipo «especificação», você deve criá-lo dentro de um pacote ou um modelo que esteja vinculado à L2 de perfil padrão.  
  
 Por padrão, cada modelo é por vinculado ao UML padrão perfis L2 e L3.  
  
### <a name="to-link-a-profile-to-a-model-or-a-package"></a>Para vincular a um perfil para um modelo ou um pacote  
  
1.  Abra **Gerenciador de modelos UML**. Sobre o **arquitetura** , aponte para **Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
2.  Localize um pacote ou um modelo que contém todos os elementos para o qual você deseja aplicar os estereótipos no perfil.  
  
3.  Clique com botão direito do pacote ou o modelo e, em seguida, clique em **propriedades**.  
  
4.  No **propriedades** janela, defina as **perfis** propriedade para os perfis que contêm os estereótipos que você deseja usar.  
  
     Os estereótipos do perfil agora estará disponíveis em todos os elementos dentro do modelo ou pacote. Se o pacote contiver outros pacotes, os estereótipos também estará disponíveis nos elementos dentro deles.  
  
### <a name="to-add-stereotypes-to-model-elements-or-relationships"></a>Adicionar estereótipos a elementos de modelo ou relações  
  
1.  Clique com botão direito do elemento de modelo ou relação, em um diagrama ou no **Gerenciador de modelos UML**e, em seguida, clique em **propriedades**.  
  
    > [!NOTE]
    >  Para adicionar os estereótipos mesmos a vários elementos, você pode selecionar vários elementos e, em seguida, clique em um deles.  
  
2.  Clique o **estereótipos** propriedade e selecione os estereótipos que você deseja aplicar.  
  
     Os estereótipos selecionados aparecem em «divisas» no elemento de modelo, para a maioria dos tipos de relação e de elemento.  
  
    > [!NOTE]
    >  Se você não conseguir ver a **estereótipos** propriedade, ou se o estereótipo desejado não aparecer, verifique se o elemento de modelo está dentro de um pacote ou um modelo ao qual o perfil apropriado foi vinculado.  
  
3.  Alguns estereótipos permitem que você defina os valores das propriedades adicionais para o elemento de modelo. Para ver essas propriedades, expanda o **estereótipos** propriedade.  
  
### <a name="to-create-model-elements-within-a-package"></a>Para criar elementos de modelo dentro de um pacote  
  
1.  Criar um pacote em um diagrama de classe UML ou em **Gerenciador de modelos UML**.  
  
2.  Adicione elementos de modelo para o pacote de uma das seguintes maneiras:  
  
    -   Em um diagrama de classe UML, clique na ferramenta para um elemento e, em seguida, clique dentro do pacote no diagrama.  
  
         \- ou -  
  
    -   No Gerenciador de modelos UML, o pacote de direito do mouse, aponte para **adicionar**e, em seguida, clique em um tipo de elemento.  
  
         \- ou -  
  
    -   No Gerenciador de modelos UML, arraste um elemento existente para o pacote.  
  
         \- ou -  
  
    -   Vincular um diagrama para o pacote e, em seguida, criar elementos do diagrama.  
  
         Para fazer isso, clique em uma parte em branco do diagrama e, em seguida, clique em **propriedades**. No **propriedades** janela, defina **pacote vinculado** para o pacote desejado.  
  
         Todos os elementos de novo que você cria no diagrama serão definidos dentro desse pacote.  
  
         Você pode fazer isso apenas com alguns tipos de diagrama.  
  
## <a name="see-also"></a>Consulte também  
 [Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)   
 [Personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md)   
 [Definir pacotes e namespaces](../modeling/define-packages-and-namespaces.md)   
 [Classes UML de cor por estereótipo](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)



