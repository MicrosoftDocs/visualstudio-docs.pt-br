---
title: Visualizar e exibir dados | Microsoft Docs
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
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f26ed20eccbff52afdc4f8b5060ad426cc100b71
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737418"
---
# <a name="visualizing-and-viewing-data"></a>Visualizando e exibindo dados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visualizadores de tipo e apresentar dados visualizadores personalizados de forma que seja significativo rapidamente para um desenvolvedor. O avaliador de expressão (EE) pode dar suporte a visualizadores de tipo de terceiros bem como fornecer seus próprios visualizadores personalizados.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Determina o número de visualizadores de tipo e visualizadores personalizados estão associados com o tipo do objeto chamando o [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) método. Se houver Visualizador de pelo menos um tipo ou o visualizador personalizado disponível, o Visual Studio chama o [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) método para recuperar uma lista desses visualizadores e visualizadores (na verdade, uma lista de `CLSID`s que implementam o visualizadores e visualizadores) e os apresenta ao usuário.  
  
## <a name="supporting-type-visualizers"></a>Suporte a visualizadores de tipo  
 Há um número de interfaces que o EE deve implementar para dar suporte a visualizadores de tipo. Essas interfaces podem ser divididas em duas amplas categorias: aqueles que lista os visualizadores de tipo e aqueles que acessam os dados de propriedade.  
  
### <a name="listing-type-visualizers"></a>Visualizadores de tipo de listagem  
 O EE suporta a lista visualizadores de tipo em sua implementação de `IDebugProperty3::GetCustomViewerCount` e `IDebugProperty3::GetCustomViewerList`. Esses métodos passam a chamada para os métodos correspondentes [GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) e [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md).  
  
 O [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md) é obtida chamando [CreateVisualizerService](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md). Esse método requer que o [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md) interface, que é obtida a [IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md) interface é passada para [EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md). `IEEVisualizerServiceProvider::CreateVisualizerService` também requer o [IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md) e [IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md) interfaces que foram passados para `IDebugParsedExpression::EvaluateSync`. A interface final necessária para criar o `IEEVisualizerService` interface é o [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md) interface, que implementa o EE. Essa interface permite que alterações sejam feitas para a propriedade que está sendo visualizada. Todos os dados de propriedade é encapsulado em um [IDebugObject](../../extensibility/debugger/reference/idebugobject.md) interface, que também é implementado pelo EE.  
  
### <a name="accessing-property-data"></a>Acessando dados de propriedade  
 Acessando dados de propriedade é feito por meio de [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md) interface. Para obter essa interface, o Visual Studio chama [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) no objeto de propriedade para obter o [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md) interface (implementado no mesmo objeto que implementa o [ IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md) interface) e, em seguida, chama o [GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md) método para obter o `IPropertyProxyEESide` interface.  
  
 Todos os dados passados dentro e fora das `IPropertyProxyEESide` interface é encapsulado em de [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md) interface. Essa interface representa uma matriz de bytes e é implementada pelo Visual Studio e o EE. Quando dados uma propriedade dos deve ser alterado, o Visual Studio cria um `IEEDataStorage` objeto que contém os novos dados e chamadas [CreateReplacementObject](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md) com esse objeto de dados para obter um novo `IEEDataStorage` objeto que, por sua vez, é passado para [InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md) para atualizar dados a propriedade dos. `IPropertyProxyEESide::CreateReplacementObject` permite que o EE criar uma instância de sua própria classe que implementa o `IEEDataStorage` interface.  
  
## <a name="supporting-custom-viewers"></a>Suporte a visualizadores personalizados  
 O sinalizador `DBG_ATTRIB_VALUE_CUSTOM_VIEWER` é definido na `dwAttrib` campo da [DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md) estrutura (retornado por uma chamada para [GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)) para indicar que o objeto tem um visualizador personalizado associado com ele. Quando esse sinalizador estiver definido, o Visual Studio obtém os [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md) da interface da [IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md) interface usando [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3).  
  
 Se o usuário seleciona um visualizador personalizado, o Visual Studio cria o visualizador personalizado usando o visualizador `CLSID` fornecido pelo `IDebugProperty3::GetCustomViewerList` método. Visual Studio, em seguida, chama [DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md) para mostrar o valor para o usuário.  
  
 Normalmente, `IDebugCustomViewer::DisplayValue` apresenta uma exibição somente leitura dos dados. Para permitir que as alterações nos dados, o EE deve implementar uma interface personalizada que dá suporte à alteração de dados em um objeto de propriedade. O `IDebugCustomViewer::DisplayValue` método usa essa interface personalizada para dar suporte à alteração dos dados. O método procura a interface personalizada o `IDebugProperty2` interface passado como o `pDebugProperty` argumento.  
  
## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>Suporte a ambos tipo visualizadores e visualizadores personalizados  
 Um EE pode dar suporte a visualizadores de tipo e visualizadores personalizados na [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) e [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) métodos. Primeiro, o EE adiciona o número de visualizadores personalizados que está fornecendo para o valor retornado pela [GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) método. Em segundo lugar, o EE acrescenta a `CLSID`s de seus próprios visualizadores personalizados para a lista retornada pelo [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)   
 [Visualizador de Tipo e Visualizador Personalizado](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)

