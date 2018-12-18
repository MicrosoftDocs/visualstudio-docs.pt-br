---
title: Estado gráfico | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.graphics.statewindow
ms.assetid: 97e7757e-c372-4626-8149-99a81367a0e1
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2b45e5d922a5f2ed5a2ba15086c708c734d25e95
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31476374"
---
# <a name="graphics-state"></a>Estado gráfico
A janela de estado no diagnóstico de gráficos do Visual Studio ajuda a entender o estado dos gráficos que está ativo no momento do evento atual como uma chamada de desenho.  
  
## <a name="understanding-the-state-window"></a>Noções básicas sobre a janela de estado  
 A janela de estado juntos coleta o estado que afeta o processamento e a apresenta hierarquicamente, em um único local. Dependendo da versão do Direct3D seu aplicativo usa, as informações apresentadas na janela de estado podem ter diferenças.  
  
### <a name="state-views"></a>Exibições de estado  
 Você pode exibir a tabela de estado de várias maneiras diferentes:  
  
|Exibir|Descrição|  
|----------|-----------------|  
|Exibição de estado de entrada de API|Essa exibição apresenta o estado em um layout semelhante aos objetos Direct3D que compõem o estado.|  
|Modo de exibição lógico de estado de entrada|Essa exibição apresenta o estado em uma exibição lógica que não refletem o layout dos objetos Direct3D que compõem o estado.|  
|Exibição de estado de fixado|Em vez de uma hierarquia, o modo de exibição de estado fixos apresenta os itens fixados estado em uma lista simples com nomes totalmente qualificados. Este modo de exibição faz é possível exibir muitos itens de estado de diferentes pacotes de estado em um pequeno número de linhas.|  
  
##### <a name="to-change-the-state-view"></a>Para alterar a exibição de estado  
  
-   Na janela de estado, no canto superior esquerdo logo abaixo do título, escolha o botão que corresponde ao estilo de exibição de estado que deseja usar.  
  
    -   **Mostrar exibição de estado de entrada de API**  
  
    -   **Mostrar exibição do estado lógico**  
  
    -   **Mostrar exibição do estado fixos**  
  
> [!IMPORTANT]
>  Deve fixar o estado no **API mostrar o estado de entrada** ou **estado lógico Mostrar** modos de exibição para que ele seja exibido no **fixado Mostrar exibição de estado**.  
  
### <a name="state-table-format"></a>Formato de tabela de estado  
 A janela de estado apresenta várias colunas de informações.  
  
|Column|Descrição|  
|------------|-----------------|  
|Nome|O nome do item de estado. Se este item representa um pacote do estado, o item pode ser expandido para exibi-la.<br /><br /> No **exibição de estado de entrada da API** e **exibição de estado lógico** estados, nomes são recuados para mostrar a relação hierárquica entre estados.<br /><br /> No **fixado exibição de estado** estado, nomes totalmente qualificados são exibidos em uma lista simples.|  
|Valor|O valor do item de estado.|  
|Tipo|O tipo do item de estado.|  
  
### <a name="changed-state"></a>Estado de alteração  
 Estado gráfico normalmente alterações de forma incremental entre as chamadas subsequentes de desenho e muitos tipos de problemas de processamento são causados quando o estado é alterado de forma incorreta. Para ajudá-lo a localizar qual estado foi alterado desde que a chamada de desenhar anterior, estado que tiver sido alterado é marcado com um asterisco e exibido em vermelho — isso se aplica não apenas o estado em si, mas seu item de estado do pai, para que você pode facilmente detectar o estado de alteração no nível mais alto e, em seguida, drill-down até os detalhes.  
  
### <a name="pinning-state"></a>Estado de fixação  
 Como muitos aplicativos processam objetos semelhantes em sequência, a alteração de um conjunto conhecido de estado, às vezes é útil fixar os estados de alteração no local para que você pode assistir como ela muda conforme você mover da chamada de desenho para desenhar a chamada.  
  
 Isso também pode ser útil se você tiver isolado a origem de um problema ao ser devido a uma alteração em um estado específico.  
  
##### <a name="to-pin-state-in-place"></a>Para fixar o estado em vigor  
  
1.  Na janela de estado, localize o estado que você está interessado. Talvez você precise expandir o estado de nível superior para localizar os detalhes que você está interessado.  
  
2.  Posicione o cursor sobre o estado que você está interessado. Um ícone de pino aparece à esquerda do item de estado.  
  
3.  Escolha o ícone de pino para fixar o item de estado em vigor.