---
title: Exibição do modelo de conteúdo do Designer de Esquema XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: reference
ms.assetid: e8db7c7d-31cf-479e-9dcc-299759891795
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0a151daa4419c24464aeeafd9a3b58d202a6e82b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942569"
---
# <a name="content-model-view"></a>O modo do modelo de conteúdo

A exibição do modelo de conteúdo fornece uma representação gráfica de nós locais e globais de esquema e seus componentes, de incluir simples e tipos complexos, de elementos, grupos de modelo, de atributos, e de grupos de atributo. Comentários e instruções de processamento XML não podem ser exibidos no modo do modelo de conteúdo. O modo de exibição do modelo de conteúdo contém dois painéis: um **espaço de trabalho** que contém uma lista de nós no painel a [espaço de trabalho designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md)e a superfície de design onde você pode ver o modelo de conteúdo do esquema nós que são selecionados na **espaço de trabalho** painel. A exibição do modelo de conteúdo também inclui a barra de ferramentas do designer de esquema XML e a barra de rastreamento.

 Na imagem a seguir, o **espaço de trabalho** painel contém seis nós de esquema. O `purchaseOrder` nó é selecionado na **espaço de trabalho** painel e é exibido na superfície de design.

 ![Exibição do modelo de conteúdo do Designer de Esquema XML](../xml-tools/media/xsddesigner_contentmodelview.gif)

## <a name="workspace-panel"></a>Painel de espaço de trabalho

 Depois de adicionar nós ao espaço de trabalho, a lista de nós aparecerá na **espaço de trabalho** painel da exibição de modelo de conteúdo. Quando você seleciona nós na **espaço de trabalho** do painel, eles aparecem na superfície de design de exibição do modelo de conteúdo. Para excluir nós de espaço de trabalho, use a barra de ferramentas do Designer XSD, o **espaço de trabalho** menu de contexto do painel, ou o **excluir** chave.

 Para obter informações sobre como adicionar nós, consulte a seção "Adicionando nós para o espaço de trabalho" em [espaço de trabalho designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md).

## <a name="design-surface"></a>Superfície de design

 Quando um nó é selecionado na **espaço de trabalho** painel, ele é adicionado à superfície de design de exibição do modelo de conteúdo onde você pode exibir os detalhes do nó.

 O modelo de conteúdo de um nó é representado por uma árvore gráfico expansível com elementos e atributos que aparecem como nós de árvore. Por padrão, somente um nível é expandido. Outras informações, como compositores, nomes de tipo, grupos, e outros contêineres é colocada em uma barra vertical (quando expandido) ao longo de elementos e atributos que incluem. Quando você clica duas vezes em uma barra vertical, transformações horizontal e recolhe de árvore. Quando você clica duas vezes em uma barra horizontal e vertical, transformações a árvore expande. Selecione a barra vertical seleciona todos os nós no contêiner. Os expansores são exibidos à direita de um nó se um elemento pode ser expandido ou recolhido.

 Se a superfície de design fica em branco, o Editor de XML, o **XML Schema Explorer**, e a marca d'água são mostradas. O *marca d'água* é uma lista de links para todas as exibições de Designer XSD. Se o esquema tem erros, o seguinte texto é exibido no fim da lista: “Use Lista de erros para exibir e corrigir erros no conjunto.”

## <a name="breadcrumb-bar"></a>Barra de navegação estrutural

 A barra de rastreamento na parte inferior do modo de modelo de conteúdo mostra onde o nó selecionado é localizado no conjunto de esquema.

## <a name="context-menus"></a>Menus de contexto

 Quando você clique com botão direito um item na superfície de design ou **espaço de trabalho** do painel, será exibido um menu de contexto. A tabela a seguir descreve as opções que estão disponíveis para a superfície de design do modo de modelo de conteúdo.

|Opção|Descrição|
|-|-----------------|
|**Mostrar em XML Schema Explorer**|Coloca o foco no esquema Explorer e ressalta o nó do esquema.|
|**Mostrar na exibição de gráfico**|Alterna a O modo de gráfico.|
|**Gerar XML de exemplo**|Disponível somente para os elementos globais. Gerencia um arquivo XML de exemplo para o elemento global.|
|**Exibir documentação**|Mostra ou de anotação/documentação de oculta conteúdo do nó.|
|**Exportar diagrama como imagem**|Salva a superfície de design para um arquivo XPS.|
|**Exibir Código**|Abre o arquivo que contém o nó selecionado no editor XML. O item selecionado na **XML Schema Explorer** também está selecionado no Editor de XML.|
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|

 A tabela a seguir descreve as opções que estão disponíveis para o **espaço de trabalho** painel.

|Opção|Descrição|
|-|-----------------|
|**Mostrar em XML Schema Explorer**|Coloca o foco no esquema Explorer e ressalta o nó do esquema.|
|**Mostrar na exibição de gráfico**|Alterna para representar graficamente a exibição.|
|**Limpar o espaço de trabalho**|Limpa o workspace e a superfície de design.|
|**Remover espaço de trabalho**|Removes selecionou nós de workspace e da superfície de design.|
|**Remover tudo, exceto a seleção do espaço de trabalho**|Remove os nós que não são selecionados de workspace e da superfície de design.|
|**Gerar XML de exemplo**|Disponível somente para os elementos globais. Gerencia um arquivo XML de exemplo para o elemento global.|
|**Selecionar tudo**|Seleciona todos os nós a **espaço de trabalho** painel.|
|**Exibir Código**|Abre o arquivo que contém o nó selecionado no editor XML. O item selecionado na **XML Schema Explorer** também está selecionado no Editor de XML.|
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|

## <a name="properties-window"></a>Janela de Propriedades

 Use o menu de contexto para abrir inicialmente a **propriedades** janela. Por padrão, o **propriedades** janela é exibida no canto inferior direito do Visual Studio. Quando você clica em um nó que é renderizado no modo de modelo de conteúdo, as propriedades de nó são exibidas na **propriedades** janela.

## <a name="xsd-designer-toolbar"></a>Barra de ferramentas do designer XSD

 Os seguintes botões da barra de ferramentas do designer XSD são ativados quando a exibição do modelo de conteúdo está ativo.

 ![Barra de ferramentas do Designer de Esquema XML](../xml-tools/media/xsdcontentmodelviewtoolbar.gif)

|Opção|Descrição|
|-|-----------------|
|**Mostrar exibição inicial**|Alterna para o [Iniciar modo de exibição](../xml-tools/start-view.md). Este modo de exibição pode ser acessado por meio do atalho de teclado: **Ctrl**+**1**.|
|**Mostrar modo de exibição do modelo de conteúdo**|Alterna para o [exibição de modelo de conteúdo](../xml-tools/content-model-view.md). Este modo de exibição pode ser acessado por meio do atalho de teclado: **Ctrl**+**2**.|
|**Mostrar exibição de gráfico**|Alterna para o [exibição de gráfico](../xml-tools/graph-view.md). Este modo de exibição pode ser acessado por meio do atalho de teclado: **Ctrl**+**3**.|
|**Limpar o espaço de trabalho**|Limpa o workspace e a superfície de design.|
|**Remover espaço de trabalho**|Removes selecionou nós de workspace e da superfície de design.|
|**Remover tudo, exceto a seleção do espaço de trabalho**|Remove os nós que não são selecionados de workspace e da superfície de design.|
|**Exibir documentação**|Mostra ou de anotação/documentação de oculta conteúdo do nó.|

## <a name="panscroll"></a>Bandeja/rolagem

 Você pode filtrar a superfície de design usando barras de rolagem ou mantendo a **Ctrl** pressionada enquanto você clica e arrasta o mouse. Quando você filtra a superfície de design usando clicar e arrastar, o cursor muda para quatro setas cruzadas apontando em quatro direções.

## <a name="undoredo"></a>Desfazer/refazer

 Desfazer/refaz o recurso é habilitado no modo de modelo de conteúdo para as seguintes ações:

-   Adicionando um único nó arrastando e soltando-se.

-   Adicionando mais nós da janela de resultados de pesquisa no esquema Explorer.

-   Adicionando a exibição de nós do início.

-   Excluindo única ou mais nós.

## <a name="zoom"></a>Aplicar Zoom

 Zoom está disponível no canto inferior direito da exibição de modelo de conteúdo.

 O zoom pode ser controlado das seguintes maneiras:

-   Mantendo os **Ctrl** wheel de chave e girar o mouse quando o mouse está sobre a superfície de exibição do modelo de conteúdo.

-   Usando o controle deslizante. O controle deslizante mostra o nível atual de zoom.

O controle deslizante de Zoom é opaco ao selecioná-la, passe o mouse sobre ele ou usar **Ctrl** com a roda do mouse para aplicar zoom; em todos os outros momentos, é transparente.

## <a name="xml-editor-integration"></a>Integração do editor de XML

 Você pode alternar entre o **Designer XSD** e o Editor de XML usando o menu de contexto.

 Se você fizer alterações no esquema definido no Editor XML as alterações serão sincronizadas no modo de modelo de conteúdo. Para obter mais informações, consulte [integração com o editor de XML](../xml-tools/integration-with-xml-editor.md).

## <a name="see-also"></a>Consulte também

- [O workspace do designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md)