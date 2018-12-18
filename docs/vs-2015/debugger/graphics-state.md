---
title: Estado gráfico | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics.statewindow
ms.assetid: 97e7757e-c372-4626-8149-99a81367a0e1
caps.latest.revision: 5
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c5100f32a7a706f0d61e3b0ac006c8168e1ee553
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750365"
---
# <a name="graphics-state"></a>Estado gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A janela de estado no diagnóstico de gráficos do Visual Studio ajuda a entender o estado dos gráficos que está ativo no momento do evento atual, como uma chamada de desenho.  
  
## <a name="understanding-the-state-window"></a>Noções básicas sobre a janela de estado  
 A janela de estado juntos coleta o estado que afeta a renderização e a apresenta hierarquicamente, em um só lugar. Dependendo da versão do Direct3D seu aplicativo usa, as informações apresentadas na janela de estado podem ter diferenças.  
  
### <a name="state-views"></a>Exibições de estado  
 Você pode exibir a tabela de estado de várias maneiras diferentes:  
  
|Exibir|Descrição|  
|----------|-----------------|  
|Modo de exibição de estado de entrada de API|Essa exibição apresenta o estado em um layout semelhante aos objetos Direct3D que compõem o estado.|  
|Modo de exibição de estado lógico de entrada|Essa exibição apresenta o estado em uma exibição lógica que não refletem o layout dos objetos Direct3D que compõem o estado.|  
|Fixado a exibição de estado|Em vez de uma hierarquia, o modo de exibição de estado fixos apresenta estado fixado itens em uma lista simples com nomes totalmente qualificados. Essa exibição faz é possível exibir muitos itens de estado de diferentes pacotes de estado em um pequeno número de linhas.|  
  
##### <a name="to-change-the-state-view"></a>Para alterar a exibição de estado  
  
-   Na janela de estado, no canto superior esquerdo logo abaixo a barra de título, escolha o botão que corresponde ao estilo de exibição de estado que deseja usar.  
  
    -   **Mostrar exibição de estado de entrada de API**  
  
    -   **Mostrar exibição de estado lógico**  
  
    -   **Mostrar modo de exibição de estado fixos**  
  
> [!IMPORTANT]
>  Você deve fixar estado na **API mostrar o estado de entrada** ou **estado lógico mostram** modos de exibição para que ele seja exibido no **fixado Mostrar modo de exibição de estado**.  
  
### <a name="state-table-format"></a>Formato de tabela de estado  
 A janela de estado apresenta várias colunas de informações.  
  
|Column|Descrição|  
|------------|-----------------|  
|Nome|O nome do item de estado. Se esse item representa um pacote do estado, o item pode ser expandido para exibi-la.<br /><br /> No **exibição de estado de entrada da API** e **exibição de estado lógico** afirma, nomes são recuados para mostrar a relação hierárquica entre estados.<br /><br /> No **fixado a exibição de estado** de estado, nomes totalmente qualificados são exibidos em uma lista simples.|  
|Valor|O valor do item de estado.|  
|Tipo|O tipo de item de estado.|  
  
### <a name="changed-state"></a>Estado alterado  
 Estado dos gráficos geralmente altera incrementalmente entre chamadas de desenho subsequentes, e muitos tipos de problemas de renderização são causados quando o estado é alterado incorretamente. Para ajudá-lo a localizar qual estado foi alterado desde que a chamada de desenho anterior, estado que tiver sido alterado é marcado com um asterisco e exibido em vermelho — isso se aplica não apenas o estado em si, mas seu item de estado do pai, para que você possa identificar facilmente o estado alterado no nível mais alto e, em seguida, drill-down até os detalhes.  
  
### <a name="pinning-state"></a>Fixar estado  
 Porque muitos aplicativos renderizam objetos semelhantes em sequência, a alteração de um conjunto conhecido de estado, às vezes é útil fixar os estados de alteração em vigor para que você pode observar como ele é alterado à medida que você move da chamada de desenho para a chamada de desenho.  
  
 Isso também pode ser útil se você tiver isolado a origem de um problema ao ser devido a uma alteração em um estado específico.  
  
##### <a name="to-pin-state-in-place"></a>Para fixar o estado em vigor  
  
1.  Na janela de estado, localize o estado em que você está interessado. Você talvez precise expandir o estado de nível superior para localizar os detalhes que você está interessado.  
  
2.  Coloque o cursor sobre o estado em que você está interessado. Um ícone de alfinete aparece à esquerda do item de estado.  
  
3.  Escolha o ícone de pino para fixar o item de estado em vigor.



