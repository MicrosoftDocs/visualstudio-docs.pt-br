---
title: Implementar visualizadores de tipo e visualizadores personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 11d047904e932646eedc974a50590dbe0a9ea99e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791274"
---
# <a name="implementing-type-visualizers-and-custom-viewers"></a>Implementando visualizadores de tipo e visualizadores personalizados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
>  No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Visualizadores de tipo e visualizadores personalizados permitem que um usuário exibir dados de um tipo específico de forma que seja mais significativa do que um despejo hexadecimal simple de números. Um avaliador de expressão (EE) pode associar os visualizadores personalizados com tipos específicos de dados ou variáveis. Esses visualizadores personalizados são implementados com o EE. O EE também pode dar suporte a visualizadores de tipo externo, que podem vir de outro fornecedor de terceiros ou até mesmo o usuário final.  
  
## <a name="discussion"></a>Discussão  
  
### <a name="type-visualizers"></a>Visualizadores de tipo  
 Visual Studio solicita uma lista de visualizadores de tipo e visualizadores personalizados para cada objeto a ser exibido em uma janela inspeção. Um avaliador de expressão (EE) fornece essa lista para todos os tipos para os quais deseja dar suporte a visualizadores de tipo e visualizadores personalizados. Chamadas para [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) e [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) iniciar todo o processo de acessar os visualizadores de tipo e visualizadores personalizados (consulte [visualização e exibindo os dados](../../extensibility/debugger/visualizing-and-viewing-data.md)para obter detalhes sobre a sequência de chamada).  
  
### <a name="custom-viewers"></a>Visualizadores personalizados  
 Visualizadores personalizados são implementados no EE para um tipo de dados específico e são representados pela [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) interface. Um visualizador personalizado não é tão flexível quanto um visualizador de tipo, uma vez que ele está disponível apenas quando o EE que implementa esse visualizador personalizado específico está em execução. A implementação de um visualizador personalizado é mais simples do que a implementação de suporte para visualizadores de tipo. No entanto, que dão suporte a visualizadores de tipo fornece máxima flexibilidade para o usuário final para visualizar dados de suas respectiva. O restante desta discussão diz respeito apenas visualizadores de tipo.  
  
## <a name="interfaces"></a>Interfaces  
 O EE implementa as interfaces a seguir para dar suporte a visualizadores de tipo a ser consumido pelo Visual Studio:  
  
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)  
  
- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)  
  
- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)  
  
- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)  
  
- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)  
  
- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)  
  
  O EE consome as interfaces a seguir para dar suporte a visualizadores de tipo:  
  
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)  
  
- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)  
  
- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)  
  
## <a name="see-also"></a>Consulte também  
 [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [Visualizar e exibir dados](../../extensibility/debugger/visualizing-and-viewing-data.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)

