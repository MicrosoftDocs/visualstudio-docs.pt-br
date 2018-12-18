---
title: Tipo de visualizador e o visualizador personalizado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: f5cf2cc9c8f89ed0ecc7935f9afa8e096f05a840
ms.sourcegitcommit: 8d38d5d2f2b75fc1563952c0d6de0fe43af12766
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/26/2018
ms.locfileid: "39276488"
---
# <a name="type-visualizer-and-custom-viewer"></a>Visualizador de tipo e visualizador personalizado
Um visualizador de tipo é um componente que exibe uma parte dos dados em um formato específico. O formato é totalmente até que implementa o visualizador, seja o usuário final ou um fornecedor de terceiros dos visualizadores.  
  
 Um visualizador personalizado é a parte de um avaliador de expressão personalizado que exibe uma parte dos dados em um formato específico. Esse formato é inteiramente a cargo do implementador do visualizador personalizado, o que significa que o formato cabe ao implementador do avaliador de expressão (EE).  
  
## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>Suporte para os visualizadores de tipo em um avaliador de expressão  
 Um EE dá suporte a visualizadores de tipo, oferecendo suporte a um conjunto de interfaces acessíveis para os visualizadores: interfaces, como [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) e [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md). No entanto, não é responsável por implementar o Visualizador de tipo em si o EE: o EE simplesmente permite visualizadores externos acessem as informações de tipo. Esses visualizadores podem ser enviados juntamente com o EE e instalados no local apropriado no Visual Studio, fornecido por outro fornecedor de terceiros ou até mesmo pelo usuário final.  
  
## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>Suporte para visualizadores personalizados em um avaliador de expressão  
 Um EE também pode dar suporte a visualizadores personalizados na qual o EE em si fornece o código para exibir o tipo de dados. Um visualizador personalizado implementa o [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) interface, que lida com todas as tarefas de mostrar os dados em qualquer formato que é desejado; o visualizador tem controle total sobre a exibição e pode até mesmo permitir que os dados de ser modificado. Qualquer visualizadores personalizados fornecidos pelo EE vêm com o EE quando a entrega do produto.  
  
## <a name="see-also"></a>Consulte também  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)   
 [Avaliador de expressão](../../extensibility/debugger/expression-evaluator.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)