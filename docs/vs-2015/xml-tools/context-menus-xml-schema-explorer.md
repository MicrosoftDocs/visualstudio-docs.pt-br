---
title: Menus de contexto (XML Schema Explorer) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42ab17ca-b8c1-40d7-beda-d033f66fe874
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 854ea473f2f606b28052b093978253372b4fec59
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49294602"
---
# <a name="context-menus-xml-schema-explorer"></a>Menus de contexto (XML Schema Explorer)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Os seguintes itens de menu de contexto são usados para executar pesquisas esquema- específicas e outras operações.  
  
## <a name="node-type-schema-set"></a>Tipo de nó: Conjunto de esquema  
 A tabela a seguir descreve as opções que estão disponíveis para um nó do esquema.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar elementos raiz mais prováveis**|Localiza e realça todos os elementos globais não são referenciados de elementos globais diferentes de se.|  
|**Mostrar tipos globais**|Os localiza e realça todos globais no conjunto de esquema.|  
|**Mostrar elementos globais**|Localiza e realces todos elementos globais no conjunto de esquema.|  
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|  
  
## <a name="node-type-namespace"></a>Tipo de nó: Namespace  
 A tabela a seguir descreve as opções que estão disponíveis para um nó de namespace.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar todas as referências de entrada**|Localiza e ressalta os arquivos que importar o namespace selecionada.|  
|**Mostrar todas as referências de saída**|Para cada arquivo no namespace selecionado, localiza e ressalta o seguinte:<br /><br /> -Todos os namespaces referenciados em instruções de importação sem um `schemaLocation` atributo.<br />-Todos os arquivos em namespaces diferentes de selecionada que são especificados no `schemaLocation` de atributo na importação e incluem instruções.|  
|**Mostrar tipos globais**|Os localiza e realça todos globais no namespace selecionada.|  
|**Mostrar elementos globais**|Localiza e realces todos elementos globais no namespace selecionado.|  
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|  
  
## <a name="node-type-file"></a>Tipo de nó: Arquivo  
 A tabela a seguir descreve as opções que estão disponíveis para um nó de arquivo.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar todas as referências de entrada**|Localiza e realça todos os arquivos que especificam o arquivo selecionado em atributos de `schemaLocation` do incluem e importar instruções.|  
|**Mostrar todas as referências de saída**|Localiza e realces o seguinte:<br /><br /> -Todos os namespaces especificados nos atributos de namespace de todas as instruções que não têm de importar o `schemaLocation` atributo.<br />-Todos os arquivos especificados no `schemaLocation` de todos os atributos de importação e incluem instruções.|  
|**Mostrar tipos globais**|Os localiza e realça todos globais neste arquivo.|  
|**Mostrar elementos globais**|Os localiza e realça todos os elementos globais neste arquivo.|  
|**Exibir Código**|Abre o arquivo que contém o nó selecionado no editor XML. O item selecionado em XML Schema Explorer também será selecionado no editor XML.|  
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|  
  
## <a name="all-global-node-types"></a>Todos os tipos de nós globais  
 A tabela a seguir descreve as opções que estão disponíveis para todos os nós globais.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar na exibição de gráfico**|Abre a exibição do gráfico. Se o nó selecionado não está no espaço de trabalho, adicione-o ao espaço de trabalho e selecione o nó.|  
|**Mostrar no modo de exibição do modelo de conteúdo**|Abre a exibição do modelo de conteúdo. Se o nó selecionado não está no espaço de trabalho, adicione-o ao espaço de trabalho e selecione o nó.|  
|**Exibir Código**|Abre o arquivo que contém o nó selecionado no editor XML. O item selecionado em XML Schema Explorer também será selecionado no editor XML.|  
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|  
  
## <a name="node-type-element"></a>Tipo de nó: Elemento  
 Além das opções do nó globais descritos acima, o menu de contexto para nós do elemento tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Ir para definição de tipo**|Navega para a definição de tipo do elemento selecionado. Isso é aplicável quando o tipo que é usado para o elemento é um tipo global.|  
|**Vá para o elemento Original**|Para referências de elemento, navega para a definição real do elemento.|  
|**Mostrar todas as referências**|Para elementos globais, localiza e realça todas as referências (elementos que têm `ref="selectedElement"`) ao elemento selecionado.|  
|**Mostrar membros de grupo de substituição**|Para os cabeçotes de um grupo de substituição, localiza e realça todos os elementos que são membros do grupo de substituição de que o elemento selecionado é um membro. Isso mostra participantes diretos e indiretos.|  
|**Cabeçalhos de grupo de substituição**|Para elementos globais que são membros de um grupo de substituição, localiza e ressalta os cabeçotes qualquer diretos e indiretos para o elemento selecionado, como o seguinte:<br /><br /> -Um chefe de grupo de substituição especificado no elemento selecionado.<br />-Um chefe de grupo de substituição especificado no elemento principal.|  
|**Gerar XML de exemplo**|Disponível somente para os elementos globais. Gerencia um arquivo XML de exemplo para o elemento global.|  
  
## <a name="node-type-global-types"></a>Tipo de nó: Tipos globais  
 Além das opções do nó globais descritos acima, o menu de contexto para nós globais do tipo tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar tipo Base**|Se o tipo selecionado é derivado de um tipo global, navega para o tipo de base do tipo selecionado.|  
|**Mostrar todas as referências**|Localiza e realces todas as referências para o tipo selecionado. Isso inclui os elementos e atributos de tipo e tipos derivados selecionados do tipo selecionado.|  
|**Mostrar todos os tipos derivados**|Localiza e realça todos os tipos que direta e indiretamente são derivados do tipo selecionado.|  
|**Mostrar todos os ancestrais**|Mostrar todos os tipos de base pai ().|  
  
## <a name="node-type-attribute"></a>Tipo de nó: Atributo  
 Além das opções do nó globais descritos acima, o menu de contexto para nós de atributo tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Ir para definição de tipo**|Quando o tipo que é usado para o atributo é um tipo global, navega para a definição de tipo do atributo selecionado.|  
|**Vá para o atributo Original**|Para referências de atributo, navega para a definição real do atributo.|  
|**Mostrar todas as referências**|Para atributos globais, localiza e realça todas as referências (outros atributos que têm `ref="selectedAttribute"`) para o atributo selecionado.|  
  
## <a name="node-type-attribute-group"></a>Tipo de nó: Grupo de atributo  
 Além das opções do nó globais descritos acima, o menu de contexto para nós do grupo de atributo tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Ir para Definição**|Para referências, navega para a definição real do atributo.|  
|**Mostrar todos os membros**|Localiza e realces todos os membros do grupo de atributo.|  
|**Mostrar todas as referências**|Localiza e realça todas as referências (grupos de atributo que têm `ref="selectedAttributeGroup"`) para o grupo selecionado de atributo.|  
  
## <a name="node-type-named-group"></a>Tipo de nó: Grupo nomeado  
 Além das opções do nó globais descritos acima, o menu de contexto para nós nome de grupo tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Ir para Definição**|Para referências, navega para a definição real do atributo.|  
|**Mostrar todos os membros**|Localiza e realces todos os membros do grupo chamado.|  
|**Mostrar todas as referências**|Localiza e realça todas as referências (grupos que têm `ref="selectedGroup"`) para o grupo selecionado.|  
  
## <a name="see-also"></a>Consulte também  
 [XML Schema Explorer](../xml-tools/xml-schema-explorer.md)   
 [Pesquisando pelo conjunto de esquema](../xml-tools/searching-the-schema-set.md)



