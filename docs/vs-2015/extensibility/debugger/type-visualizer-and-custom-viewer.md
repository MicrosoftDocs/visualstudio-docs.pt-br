---
title: Tipo de visualizador e o visualizador personalizado | Microsoft Docs
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
ms.assetid: fd3691e6-9c78-4767-846f-43f85ada4375
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5319721d57212f4fc853ca99c1544a51d4af878c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51732126"
---
# <a name="type-visualizer-and-custom-viewer"></a>Visualizador de tipo e visualizador personalizado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um visualizador de tipo é um componente que exibe uma parte dos dados em um formato muito específico. Esse formato é inteiramente a cargo do implementador do visualizador, seja o usuário final ou um fornecedor de terceiros dos visualizadores.  
  
 Um visualizador personalizado é a parte de um avaliador de expressão personalizado que exibe uma parte dos dados em um formato muito específico. Esse formato é inteiramente a cargo do implementador do visualizador personalizado, o que significa que o formato cabe ao implementador do avaliador de expressão (EE).  
  
## <a name="support-for-type-visualizers-in-an-expression-evaluator"></a>Suporte para os visualizadores de tipo em um avaliador de expressão  
 Um EE pode dar suporte a visualizadores de tipo que dão suporte a um conjunto de interfaces acessíveis para os visualizadores: interfaces, como [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) e [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md). No entanto, observe que o EE não é responsável por implementar o Visualizador de tipo em si: o EE simplesmente permite visualizadores externos acessem as informações de tipo. Esses visualizadores podem ser enviados juntamente com o EE e instalados no local apropriado no Visual Studio, fornecido por outro fornecedor de terceiros ou até mesmo pelo usuário final.  
  
## <a name="support-for-custom-viewers-in-an-expression-evaluator"></a>Suporte para visualizadores personalizados em um avaliador de expressão  
 Um EE também pode dar suporte a visualizadores personalizados na qual o EE em si fornece o código para exibir o tipo de dados. Um visualizador personalizado implementa o [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) interface, que lida com todas as tarefas de mostrar os dados em qualquer formato que é desejado; o visualizador tem controle total sobre a exibição e pode até permitir que os dados a ser modificado. Qualquer visualizadores personalizados fornecidos pelo EE vêm com o EE quando a entrega do produto.  
  
## <a name="see-also"></a>Consulte também  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)   
 [Avaliador de expressão](../../extensibility/debugger/expression-evaluator.md)   
 [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)   
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

