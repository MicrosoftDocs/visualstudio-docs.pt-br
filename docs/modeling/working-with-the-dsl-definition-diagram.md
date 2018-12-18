---
title: Trabalhando com o diagrama de definição de DSL
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.diagram
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language Tools, diagram
- Domain-Specific Language Tools, Split Tree
- Domain-Specific Language Tools, Show Map Lines
- Domain-Specific Language Tools, Show As Class
- Domain-Specific Language Tools, Bring Tree Here
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: d7e052f64e931769b1fedde7e184bfeefa43a77d
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967396"
---
# <a name="working-with-the-dsl-definition-diagram"></a>Trabalhando com o diagrama de definição de DSL
O diagrama de um [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] definição é uma ferramenta importante para definir a linguagem específica do domínio. É possível adicionar elementos ao seu modelo de domínio e definir as relações no diagrama e é possível modificar o layout do diagrama para torná-lo mais legível.

## <a name="the-layout-of-the-diagram"></a>O layout do diagrama
 O [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] tem duas partições, o diagrama de definição de **Classes e relações** partição e o **elementos de diagrama** partição. O **Classes e relacionamentos** partição exibe as classes de domínio, relações de domínio e herança. O **elementos de diagrama** partition exibe as classes de forma, as classes de conector, classes de Raia e o diagrama gerado pelo designer.

 Classes de domínio podem aparecer em vários locais na **Classes e relacionamentos** partições. Uma definição de classe de domínio exibe uma árvore de herança se esta for a classe base para outras classes de domínio e uma árvore de relações se for a fonte de relações de incorporação ou de referência. Espaços reservados de classe de domínio aparecem como alvos de relações de incorporação ou de referência. Por padrão, os elementos de espaço reservado são exibidos com o **propriedades do domínio** compartimento recolhido. Eles não mostram a herança ou as relações de incorporação ou referência.

 Quando você adiciona uma classe de domínio, ele aparece na parte inferior a **Classes e relacionamentos** partição. Ao adicionar uma relação de incorporação ou referência, ela é desenhada abaixo e à direita da classe de domínio da fonte.

 À medida que adicionar classes de domínio e relações, pode tornar-se difícil localizar uma classe de domínio específica. Você pode encontrar uma classe de domínio clicando na **Gerenciador de DSL** e, em seguida, clicando em **localizar no diagrama**.

 As seções a seguir descrevem como é possível alterar a aparência do diagrama para facilitar a leitura.

## <a name="copying-elements"></a>Copiando elementos
 É possível usar copiar, cortar e colar em elementos no diagrama de definição DSL.

## <a name="zooming-in-or-out-on-the-diagram"></a>Aumentar ou diminuir o zoom no diagrama
 Você pode ampliar ou reduzir o diagrama usando o **Designer de DSL** barra de ferramentas para definir o nível de zoom.

## <a name="hiding-map-lines"></a>Ocultando linhas do mapa
 As linhas do mapa são linhas desenhadas entre uma relação de classe ou do domínio e a forma ou o conector ao qual ela está mapeada. Você pode ocultar as linhas do mapa clicando o **Mostrar linhas de mapa** botão a **Designer de DSL** barra de ferramentas. Para mostrar as linhas, clique no botão novamente.

## <a name="changing-the-diagram-layout"></a>Alterar o layout do diagrama
 Você pode alterar o layout do **Classes e relacionamentos** de partição da seguinte maneira.

### <a name="expandcollapse"></a>Expandir/Recolher
 Você pode reduzir o tamanho de um elemento de forma do compartimento que representa uma classe de domínio ou uma forma de direito do mouse e, em seguida, clicando em **recolher**. Isso oculta o **propriedades do domínio** compartimento da forma. Para mostrar o **propriedades do domínio** compartimento novamente, clique com botão direito na forma e, em seguida, clique em **expandir**.

### <a name="move-updown"></a>Mover para Cima/para Baixo
 Você pode mover uma classe ou diagrama de elemento de domínio para cima ou para baixo na partição clicando duas vezes no elemento e, em seguida, clicando em **mover para cima** ou **mover para baixo**. Se você mover um elemento do espaço reservado que está exibido como um alvo de uma relação de incorporação ou referência, a relação será movida com ele.

### <a name="expandcollapse-relationships-tree"></a>Árvore de relações de expandir/recolher
 Se uma classe de domínio desempenha a função de origem em relações de incorporação ou referência com outras classes de domínio, você pode ocultar as relações clicando duas vezes na definição de classe de domínio e, em seguida, clicando em **Recolher árvore de relacionamentos**. Para mostrar as relações, clique com botão direito no elemento de definição e, em seguida, clique em **Expandir árvore de relacionamentos**.

### <a name="expandcollapse-inheritance-tree"></a>Expandir/Recolher Árvore de Relacionamentos
 Se uma classe de domínio é a classe base de outras classes de domínio, você pode ocultar a árvore de herança clicando duas vezes na definição de classe de domínio e, em seguida, clicando em **Recolher árvore de herança**. Para mostrar a árvore de herança, clique com botão direito no elemento de definição e, em seguida, clique em **Expandir árvore de herança**.

### <a name="bring-tree-here"></a>Bring Tree Here
 Você pode consolidar o diagrama clicando duas vezes uma classe de domínio de espaço reservado e, em seguida, clicando em **trazer árvore aqui**. A classe de domínio do espaço reservado torna-se um elemento de definição e exibe as árvores de herança e relações. O elemento de definição anterior torna-se um elemento do espaço reservado, se este for o alvo de uma relação ou o filho em uma relação de herança; caso contrário, ele desaparece.

### <a name="split-tree"></a>Split Tree
 É possível fragmentar árvores de herança ou as relações clicando duas vezes na definição de classe de domínio que exibe-os e, em seguida, clicando em **dividir árvore**. O elemento de definição torna-se um elemento de espaço reservado e a classe de domínio de definição, juntamente com suas árvores de herança e relações, agora é exibida na parte inferior da partição.

### <a name="show-as-class"></a>Show As Class
 Se uma relação de domínio foi derivada de relações, ou se ele tiver relações de incorporação ou referência com outras relações de domínio, você pode exibir a relação como uma classe clicando duas vezes a relação e, em seguida, clicando em **mostrar como classe** . A relação será exibida com uma **propriedades do domínio** do compartimento e mostrará as árvores de herança e relações.

## <a name="see-also"></a>Consulte também

- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)