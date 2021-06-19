---
title: Trabalhando com o diagrama de definição de DSL
description: Saiba que o diagrama de uma definição de Ferramentas DSL é uma ferramenta importante para definir uma linguagem específica do domínio.
ms.custom: SEO-VS-2020
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
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f401fe0509fc425fff873a7dc224c69359156861
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388068"
---
# <a name="working-with-the-dsl-definition-diagram"></a>Trabalhando com o diagrama de definição de DSL
O diagrama de uma [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] definição é uma ferramenta importante para definir o idioma específico do domínio. É possível adicionar elementos ao seu modelo de domínio e definir as relações no diagrama e é possível modificar o layout do diagrama para torná-lo mais legível.

## <a name="the-layout-of-the-diagram"></a>O layout do diagrama
 O [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] diagrama de definição tem duas partições, a **partição Classes** e Relações e a **partição Elementos do** Diagrama. A **partição Classes e Relações** exibe classes de domínio, relações de domínio e herança. A **partição Elementos de** Diagrama exibe classes de forma, classes de conector, classes de raias e o diagrama de designer gerado.

 As classes de domínio podem aparecer em vários locais nas **partições Classes** e Relações. Uma definição de classe de domínio exibe uma árvore de herança se esta for a classe base para outras classes de domínio e uma árvore de relações se for a fonte de relações de incorporação ou de referência. Espaços reservados de classe de domínio aparecem como alvos de relações de incorporação ou de referência. Por padrão, os elementos de espaço reservado são exibidos com o compartimento **Propriedades do Domínio** recolhido. Eles não mostram a herança ou as relações de incorporação ou referência.

 Quando você adiciona uma classe de domínio, ela aparece na parte inferior da **partição Classes e** Relações. Ao adicionar uma relação de incorporação ou referência, ela é desenhada abaixo e à direita da classe de domínio da fonte.

 À medida que adicionar classes de domínio e relações, pode tornar-se difícil localizar uma classe de domínio específica. Você pode encontrar uma classe de domínio clicando com o botão direito do mouse no **DSL Explorer** e clicando **em Localizar no Diagrama**.

 As seções a seguir descrevem como é possível alterar a aparência do diagrama para facilitar a leitura.

## <a name="copying-elements"></a>Copiando elementos
 É possível usar copiar, cortar e colar em elementos no diagrama de definição DSL.

## <a name="zooming-in-or-out-on-the-diagram"></a>Aumentar ou diminuir o zoom no diagrama
 Você pode ampliar ou reduzir o diagrama usando a barra **Designer de DSL** de ferramentas para definir o nível de zoom.

## <a name="hiding-map-lines"></a>Ocultando linhas do mapa
 As linhas do mapa são linhas desenhadas entre uma relação de classe ou do domínio e a forma ou o conector ao qual ela está mapeada. Você pode ocultar linhas de mapa clicando no **botão Mostrar Linhas do** Mapa na barra **Designer de DSL** ferramentas. Para mostrar as linhas, clique no botão novamente.

## <a name="changing-the-diagram-layout"></a>Alterar o layout do diagrama
 Você pode alterar o layout da **partição Classes e Relações** da seguinte forma.

### <a name="expandcollapse"></a>Expandir/Recolher
 Você pode reduzir o tamanho de um elemento de forma de compartimento que representa uma classe de domínio ou uma forma clicando com o botão direito do mouse nele e, em seguida, clicando em **Fechar**. Isso oculta o compartimento **Propriedades de** Domínio da forma. Para mostrar o compartimento **Propriedades do** Domínio novamente, clique com o botão direito do mouse na forma e clique em **Expandir**.

### <a name="move-updown"></a>Mover para Cima/para Baixo
 Você pode mover uma classe de domínio ou elemento de diagrama para cima ou para baixo na partição clicando com o botão direito do mouse no elemento e, em seguida, clicando em Mover para **Cima** ou **Mover para Baixo.** Se você mover um elemento do espaço reservado que está exibido como um alvo de uma relação de incorporação ou referência, a relação será movida com ele.

### <a name="expandcollapse-relationships-tree"></a>Árvore de relações de expandir/recolher
 Se uma classe de domínio desempenha a função de origem em relações de incorporação ou referência com outras classes de domínio, você pode ocultar as relações clicando com o botão direito do mouse na definição da classe de domínio e clicando em Recaiar Árvore de **Relações**. Para mostrar as relações, clique com o botão direito do mouse no elemento de definição e clique **em Expandir Árvore de Relações**.

### <a name="expandcollapse-inheritance-tree"></a>Expandir/Recolher Árvore de Relacionamentos
 Se uma classe de domínio for a classe base de outras classes de domínio, você poderá ocultar a árvore de herança clicando com o botão direito do mouse na definição da classe de domínio e clicando em **Recaia de** Árvore de Herança . Para mostrar a árvore de herança, clique com o botão direito do mouse no elemento de definição e clique **em Expandir Árvore de Herança**.

### <a name="bring-tree-here"></a>Bring Tree Here
 Você pode consolidar o diagrama clicando com o botão direito do mouse em uma classe de domínio de espaço reservado e clicando **em Trazer Árvore aqui.** A classe de domínio do espaço reservado torna-se um elemento de definição e exibe as árvores de herança e relações. O elemento de definição anterior torna-se um elemento do espaço reservado, se este for o alvo de uma relação ou o filho em uma relação de herança; caso contrário, ele desaparece.

### <a name="split-tree"></a>Dividir Árvore
 Você pode dividir árvores de herança ou relações clicando com o botão direito do mouse na definição da classe de domínio que as exibe e clicando em **Dividir Árvore**. O elemento de definição torna-se um elemento de espaço reservado e a classe de domínio de definição, juntamente com suas árvores de herança e relações, agora é exibida na parte inferior da partição.

### <a name="show-as-class"></a>Show As Class
 Se uma relação de domínio tiver relações derivadas ou se ela tiver relações de incorporação ou referência com outras relações de domínio, você poderá exibir a relação como uma classe clicando com o botão direito do mouse na relação e clicando em **Mostrar Como Classe**. A relação será exibida com um compartimento **Propriedades de Domínio** e mostrará as árvores de herança e relações.

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))