---
title: Como visualizar uma associação de coleção (Designer de Classe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.collectionassociationline
- vs.classdesigner.ShowAssociationException
helpviewer_keywords:
- collection associations
- collections, collection associations
- Class Designer [Visual Studio], collection associations
ms.assetid: 54e39838-2fc9-4dc2-85b6-7e88a743108e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 24dc8b21fbdacb5da2795b215cd8503b08cf3449
ms.sourcegitcommit: 4c0db930d9d5d8b857d3baf2530ae89823799612
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "33995875"
---
# <a name="how-to-visualize-a-collection-association-in-class-designer"></a>Como visualizar uma associação de coleção no Designer de Classe

Propriedades e campos que são coleções de outros tipos podem ser exibidos no diagrama de classe como uma associação de coleção. Diferentemente de uma associação regular, que exibe um campo ou uma propriedade como uma linha que vincula a classe proprietária ao tipo do campo, uma associação de coleção é exibida como uma linha que vincula a classe proprietária ao tipo coletado.

## <a name="to-create-a-collection-association"></a>Para criar uma associação de coleção

1.  No código, crie uma propriedade ou campo cujo tipo seja uma coleção fortemente tipada.

2.  No diagrama de classe, expanda a classe de modo que os campos e as propriedades sejam mostrados.

3.  Na classe, clique com o botão direito do mouse no campo ou propriedade e escolha **Mostrar como Associação de Coleção**.

A propriedade ou o campo é mostrado como uma linha de associação vinculando ao tipo coletado.

## <a name="see-also"></a>Consulte também

- [Como criar associações entre tipos](how-to-create-associations-between-types.md)
- [Projetando classes e tipos](designing-and-viewing-classes-and-types.md)
- [Exibindo tipos e relações](viewing-types-and-relationships.md)
