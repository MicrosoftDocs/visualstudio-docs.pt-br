---
title: 'Como: obter uma visão geral de um conjunto de esquema usando o modo de exibição de gráfico | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c0df4b0d-52ef-4a6c-9676-1d8311aad7c7
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3722af4aef2f56d6da1c2a79840c05edd2a87b65
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49181357"
---
# <a name="how-to-get-an-overview-of-a-schema-set-using-the-graph-view"></a>Como: Obter uma visão geral de um conjunto de esquema usando a exibição do gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este tópico descreve como usar o [modo de exibição gráfico](../xml-tools/graph-view.md) para ver uma exibição de alto nível de nós em um conjunto de esquema e as relações entre os nós.  
  
### <a name="to-create-a-new-xsd-file-and-display-the-root-element-in-the-content-model-view"></a>Para criar um novo arquivo XSD e exibir o elemento raiz no modo do modelo de conteúdo  
  
1.  Crie um novo arquivo de esquema XML e salve o arquivo como Relationships.xsd.  
  
2.  Clique o **Use o Editor de XML para exibir e editar o arquivo de esquema XML subjacente** link no modo de início.  
  
3.  Copie o código de exemplo de esquema XML do [esquema XML de exemplo: relações](../xml-tools/sample-xsd-file-relationships.md) e cole-o para substituir o código que foi adicionado ao novo arquivo XSD por padrão.  
  
4.  Clique com botão direito em qualquer lugar no Editor de XML e selecione **Designer de exibição**.  
  
5.  Selecione o modo de gráfico da barra de ferramentas XSD.  
  
6.  Selecione **do conjunto de esquema** nó no XML Schema Explorer e arraste o nó para criar o suface do modo de gráfico. Você deve ver todos os nós globais, e as setas que conectam os nós que possuem relações.  
  
     ![Exibição de gráfico](../xml-tools/media/relationshipingraphview.gif "RelationshipInGraphView")  
  
7.  Clique em qualquer nó na superfície de design e examine a barra de rastreamento para ver onde o nó selecionado é localizado no conjunto de esquema.  
  
8.  Rick-clique em qualquer nó de elemento na superfície desing e selecione **gerar XML de exemplo** para ver o documento de instância XML.



