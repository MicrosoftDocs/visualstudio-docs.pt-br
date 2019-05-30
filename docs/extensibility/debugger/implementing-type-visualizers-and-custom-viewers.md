---
title: Implementar visualizadores de tipo e visualizadores personalizados | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f7e977df6236ea8c3310312114ba4fa30d5003a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344198"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>Implementar visualizadores de tipo e visualizadores personalizados
> [!IMPORTANT]
> No Visual Studio 2015, essa forma de implementar os avaliadores de expressão foi preterida. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte [avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Visualizadores de tipo e visualizadores personalizados permitem que um usuário exibir dados de um tipo específico de forma que seja mais significativa do que um despejo hexadecimal simple de números. Um avaliador de expressão (EE) pode associar os visualizadores personalizados com tipos específicos de dados ou variáveis. Esses visualizadores personalizados são implementados com o EE. O EE também pode dar suporte a visualizadores de tipo externo, que podem vir de outro fornecedor de terceiros ou até mesmo o usuário final.

## <a name="discussion"></a>Discussão

### <a name="type-visualizers"></a>Visualizadores de tipo
 Visual Studio solicita uma lista de visualizadores de tipo e visualizadores personalizados para cada objeto a ser exibido em uma janela inspeção. Um avaliador de expressão (EE) fornece essa lista para todos os tipos para os quais deseja dar suporte a visualizadores de tipo e visualizadores personalizados. Chamadas para [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) e [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) iniciar todo o processo de acessar os visualizadores de tipo e visualizadores personalizados (consulte [visualização e exibindo os dados](../../extensibility/debugger/visualizing-and-viewing-data.md)para obter detalhes sobre a sequência de chamada).

### <a name="custom-viewers"></a>Visualizadores personalizados
 Visualizadores personalizados são implementados no EE para um tipo de dados específico e são representados pela [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) interface. Um visualizador personalizado não é tão flexível quanto um visualizador de tipo, uma vez que ele está disponível apenas quando o EE que implementa esse visualizador personalizado específico está em execução. A implementação de um visualizador personalizado é mais simples do que a implementação de suporte para visualizadores de tipo. No entanto, que dão suporte a visualizadores de tipo fornece máxima flexibilidade para o usuário final para visualizar seus dados. O restante desta discussão diz respeito apenas visualizadores de tipo.

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
- [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [Visualizar e exibir dados](../../extensibility/debugger/visualizing-and-viewing-data.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)