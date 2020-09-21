---
title: Implementando visualizadores de tipo e personalizados | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b780f2115400fd43e8915a5109c960cab99bf131
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "90838740"
---
# <a name="implementing-type-visualizers-and-custom-viewers"></a>Implementando visualizadores de tipo e visualizadores personalizados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).  
  
 Visualizeres de tipo e visualizadores personalizados permitem que um usuário exiba dados de um tipo específico de uma maneira mais significativa do que um simples despejo hexadecimal de números. Um avaliador de expressão (EE) pode associar visualizadores personalizados a tipos específicos de dados ou variáveis. Esses visualizadores personalizados são implementados pelo EE. O EE também pode oferecer suporte a visualizadores de tipo externo, que podem vir de outro fornecedor de terceiros ou até mesmo do usuário final.  
  
## <a name="discussion"></a>Discussão  
  
### <a name="type-visualizers"></a>Visualizadores de tipo  
 O Visual Studio solicita uma lista de visualizadores de tipo e visualizadores personalizados para cada objeto a ser exibido em uma janela de inspeção. Um avaliador de expressão (EE) fornece uma lista desse tipo para todos os tipos para os quais deseja dar suporte a visualizadores de tipo e visualizadores personalizados. Chamadas para [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) e [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) iniciam todo o processo de acesso a visualizadores de tipos e visualizadores personalizados (consulte visualizando [e exibindo dados](../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes sobre a sequência de chamada).  
  
### <a name="custom-viewers"></a>Visualizadores personalizados  
 Os visualizadores personalizados são implementados no EE para um tipo de dados específico e são representados pela interface [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) . Um visualizador personalizado não é tão flexível quanto um visualizador de tipo, pois está disponível somente quando o EE que implementa esse visualizador personalizado específico está em execução. A implementação de um visualizador personalizado é mais simples do que a implementação de suporte para visualizadores de tipos. No entanto, os visualizadores de tipo de suporte dão o máximo de flexibilidade ao usuário final para visualizar seus dados. O restante desta discussão só diz respeito a visualizadores de tipos.  
  
## <a name="interfaces"></a>Interfaces  
 O EE implementa as seguintes interfaces para dar suporte a visualizadores de tipos, para ser consumido pelo Visual Studio:  
  
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)  
  
- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)  
  
- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)  
  
- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)  
  
- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)  
  
- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)  
  
  O EE consome as seguintes interfaces para dar suporte a visualizadores de tipo:  
  
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)  
  
- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)  
  
- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Escrevendo um avaliador de expressão CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [Visualizando e exibindo dados](../../extensibility/debugger/visualizing-and-viewing-data.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
