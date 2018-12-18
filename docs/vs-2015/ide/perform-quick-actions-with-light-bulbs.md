---
title: Realizar ações rápidas com lâmpadas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 990ee487-cf9a-4b89-9784-e7b47c220e8c
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3eff05df37dd1d15774fb059396f3f94b0fff2a8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49883452"
---
# <a name="perform-quick-actions-with-light-bulbs"></a>Realizar ações rápidas com lâmpadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As lâmpadas são um novo recurso de produtividade no Visual Studio 2015. Eles são ícones que aparecem no editor do Visual Studio e que você pode clicar para realizar ações rápidas, incluindo a refatoração e correção de erros. As lâmpadas levam a assistência de correção de erros e refatoração para um único ponto focal, em geral, exatamente na linha em que você está digitando.  
  
 ![Ícone de lâmpada pequeno](../ide/media/vs2015-lightbulbsmall.png "VS2015_LightBulbSmall")  
  
 No C# e no Visual Basic, você verá uma lâmpada se houver um rabisco vermelho e o Visual Studio tiver uma sugestão para corrigir o problema. Por exemplo se você tiver um erro indicado por um rabisco vermelho, uma lâmpada aparecerá quando correções estiverem disponíveis para esse erro. No C++, ao adicionar uma nova função a um arquivo de cabeçalho, você verá uma lâmpada que se oferece para criar uma implementação de stub dessa função. Para qualquer idioma, terceiros podem oferecer diagnóstico e sugestões personalizados, por exemplo, como parte de um SDK, e as lâmpadas do Visual Studio serão acesas de acordo com essas regras.  
  
## <a name="to-see-a-light-bulb"></a>Para ver uma lâmpada  
  
1. Em muitos casos, as lâmpadas aparecem espontaneamente ao focalizar o mouse no ponto de um erro ou na margem esquerda do editor ao mover o cursor em uma linha que contém um erro. Quando você vir um rabisco vermelho, poderá focalizar o mouse sobre ele para exibir a lâmpada. Você também poderá fazer com que uma lâmpada seja exibida ao usar o mouse ou o teclado para ir para qualquer lugar da linha em que ocorre o problema.  
  
2. Pressione **Ctrl + .** em qualquer lugar de uma linha para invocar a lâmpada e ir diretamente para a lista de possíveis correções.  
  
   ![Lâmpada com o mouse focalizando](../ide/media/vs2015-lightbulb-hover.png "VS2015_LightBulb_Hover")  
  
## <a name="to-see-potential-fixes"></a>Para ver as possíveis correções  
 Clique na seta para baixo ou no link Mostrar possíveis correções para exibir uma lista de ações rápidas que a lâmpada pode executar para você.  
  
 ![Lâmpada expandida](../ide/media/vs2015-lightbulb-hover-expanded.png "VS2015_LightBulb_hover_expanded")  
  
## <a name="to-do-a-refactoring"></a>Para fazer uma refatoração  
 Você ainda poderá executar refatorações clicando com o botão direito do mouse para abrir o menu de contexto, mas também poderá pressionar Ctrl + . para exibir opções de refatoração. Na ilustração a seguir, a refatoração Extrair Método é oferecida depois de pressionar Ctrl + . em algum lugar da linha que contém a chamada `Math.Abs`:  
  
 ![Lâmpada mostrando opções de refatoração](../ide/media/vs2015-lightbulbs-refactor.png "VS2015_LightBulbs_refactor")



