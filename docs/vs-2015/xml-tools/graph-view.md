---
title: Exibição de gráfico | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5881afde-3f24-4eb9-bff8-6cb3fc8aade7
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: d1c0bbe55f2e63c1d86d71556392d57d1330c6b4
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49813616"
---
# <a name="graph-view"></a>Exibição de gráfico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A exibição do gráfico fornece uma representação gráfica de nós globais do esquema e relações entre os nós. Observe que a exibição do gráfico não permite que você alterar o layout do esquema definido na superfície de design. A exibição do gráfico também inclui a barra de ferramentas do designer de esquema XML e a barra de rastreamento.  
  
 A imagem a seguir mostra a visualização de gráfico com seis nós globais na superfície de design.  
  
 ![Modo de exibição de gráfico do Designer de esquema XML](../xml-tools/media/xsddesigner-graphview.gif "XSDDesigner_GraphView")  
  
## <a name="design-surface"></a>A superfície de design  
 A superfície de design do modo de gráfico exibe o conteúdo do [espaço de trabalho de Designer de esquema XML](../xml-tools/xml-schema-designer-workspace.md). Se o workspace contém quaisquer nós globais do conjunto de esquema, os nós são mostrados na superfície de design do modo de gráfico e as setas são desenhadas entre os nós que possuem relações.  
  
 Clique duas vezes em um nó no modo de gráfico trará anterior o editor XML.  
  
 Para excluir selecionou nós de workspace, usa a barra de ferramentas do designer XSD ou a tecla DELETE.  
  
 Se a superfície de design está em branco, o editor XML, XML Schema Explorer, e a marca de agua são mostrados. O *marca d'água* é uma lista de links para todas as exibições de Designer XSD.  
  
 ![Designer XSD; Exibição de gráfico](../xml-tools/media/xsdgraphviewwatermark.gif "XSDGraphViewWatermark")  
  
 Se o esquema tem erros, o seguinte texto é exibido no fim da lista: “Use Lista de erros para exibir e corrigir erros no conjunto.”  
  
## <a name="breadcrumb-bar"></a>Barra de rastreamento  
 A barra de rastreamento na parte inferior do modo de figura a seguir mostra onde o nó selecionado é localizado no conjunto de esquema. Se vários itens são selecionados, a barra de rastreamento será em branco.  
  
## <a name="context-menu"></a>O menu de contexto  
 A tabela a seguir descreve as opções que estão disponíveis para todos os nós na superfície de design do modo de gráfico.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar em XML Schema Explorer**|Coloca o foco no esquema Explorer e ressalta o nó do esquema.|  
|**Mostrar na exibição de gráfico**|Alterna para o modo de exibição gráfico (desativada).|  
|**Gerar XML de exemplo**|Disponível somente para os elementos globais. Gerencia um arquivo XML de exemplo para o elemento global.|  
|**Limpar o espaço de trabalho**|Limpa o workspace e a superfície de design.|  
|**Remover espaço de trabalho**|Removes selecionou nós de workspace e da superfície de design.|  
|**Remover tudo, exceto a seleção do espaço de trabalho**|Remove os nós que não são selecionados de workspace e da superfície de design.|  
|**Exporte diagrama como imagem...**|Salva a superfície de design para um arquivo XPS.|  
|**Selecionar tudo**|Selecionar todos os nós na superfície de design.|  
|**Exibir Código**|Abre o arquivo que contém o nó selecionado no editor XML. O item selecionado em XML Schema Explorer também será selecionado no editor XML.|  
|**Janela Propriedades**|Abre o **propriedades** janela (se não ainda estiver aberto). Esta janela exibe informações sobre o nó.|  
  
 Além das opções comuns descritas anterior, o menu de contexto para elementos globais também tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Adicionar definição de tipo**|Adiciona o tipo base no diagrama.|  
|**Adicionar todas as referências**|Adiciona todos os nós que se referem ao elemento e desenha setas para indicar relações entre eles.|  
|**Adicionar membros do grupo de substituição**|Adiciona todos os membros do grupo de substituição. Essa opção aparece na exibição se o elemento é o início ou membro de um grupo de substituição.|  
|**Gerar XML de exemplo**|Gerencia um arquivo XML de exemplo para o elemento global.|  
  
 Além das opções comuns descritas anterior, o menu de contexto para tipos complexos simples e globais globais também tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Adicione o tipo Base**|Se o tipo selecionado é derivado de um tipo global, adiciona o tipo base do tipo selecionado.|  
|**Adicionar todas as referências**|Adiciona todas as referências de tipo selecionado. Isso inclui os elementos e atributos do tipo selecionado, e tipos derivados do tipo selecionado.|  
|**Adicionar todos os tipos derivados**|Adiciona todos os tipos que direta e indiretamente são derivados do tipo selecionado.|  
|**Adicionar todos os ancestrais**|Adiciona todos os tipos de base pai ().|  
  
 Além das opções comuns descritas anterior, o menu de contexto para grupos globais e grupos de atributo também tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Adicionar todas as referências**|Adiciona todos os nós que se referem ao grupo e desenha setas para indicar relações entre eles.|  
|**Adicionar todos os membros**|Adiciona todos os membros do grupo e desenha setas para indicar relações entre eles.|  
  
 No addtion em padrões comuns descritas anterior, o menu de contexto para atributos globais também tem as seguintes opções:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Adicionar todas as referências**|Adiciona todos os nós que se referem ao grupo e desenha setas para indicar relações entre eles.|  
  
## <a name="properties-window"></a>Janela Propriedades  
 Use o menu de contexto para abrir inicialmente a **propriedades** janela. Por padrão, o **propriedades** janela é exibida no canto inferior direito do Visual Studio. Quando você clica em um nó que é renderizado no modo de modelo de conteúdo, as propriedades do nó serão exibidas na **propriedades** janela.  
  
## <a name="xsd-toolbar"></a>Barra de ferramentas XSD  
 Os seguintes botões da barra de ferramentas XSD são ativados quando a exibição do gráfico está ativo.  
  
 ![Barra de ferramentas Designer de esquema XML](../xml-tools/media/xsdgraphviewtoolbar.gif "XSDGraphViewToolbar")  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Mostrar exibição inicial**|Alterna para o [Iniciar modo de exibição](../xml-tools/start-view.md). Este modo de exibição pode ser acessado por meio do atalho de teclado: **CTRL + 1**.|  
|**Mostrar modo de exibição do modelo de conteúdo**|Alterna para o [exibição de modelo de conteúdo](../xml-tools/content-model-view.md). Este modo de exibição pode ser acessado por meio do atalho de teclado: **CTRL + 2**.|  
|**Mostrar exibição de gráfico**|Alterna para o [exibição de gráfico](../xml-tools/graph-view.md). Este modo de exibição pode ser acessado por meio do atalho de teclado: **CTRL + 3**.|  
|**Limpar o espaço de trabalho**|Limpa o workspace e a superfície de design.|  
|**Remover espaço de trabalho**|Removes selecionou nós de workspace e serface de design.|  
|**Remover tudo, exceto a seleção do espaço de trabalho**|Remove os nós que não são selecionados de workspace e serface de design. Essa opção é ativada no modo do modelo de conteúdo e no modo de gráfico.|  
|**Esquerda para a direita**|Altera o layout no modo de gráfico a uma representação hierárquica esquerda para a direita de nós. Essa opção pode ser acessada por meio do atalho de teclado: **Alt + seta para a direita**.|  
|**Direita para a esquerda**|Altera o layout no modo de gráfico a uma representação hierárquica da direita para a esquerda de nós. Essa opção pode ser acessada por meio do atalho de teclado: **Alt + seta para a esquerda**.|  
|**Cima para baixo**|Altera o layout no modo de gráfico a uma representação hierárquica de cima para baixo de nós. Essa opção pode ser acessada por meio do atalho de teclado: **Alt + seta para baixo**.|  
|**Baixo para cima**|Altera o layout no modo de gráfico a uma representação hierárquica de parte inferior-à- parte superior dos nós. Essa opção pode ser acessada por meio do atalho de teclado: **Alt + seta para cima**.|  
  
## <a name="panscroll"></a>Bandeja/rolagem  
 Você pode filtrar a superfície de design usando barras de rolagem ou mantendo a tecla CTRL quando você clique e arraste o mouse. Quando você filtra a superfície de design usando o clique e o arrastar, o cursor será alterado a quatro setas cruzadas apontando em quatro direções.  
  
## <a name="undoredo"></a>Desfazer/refazer  
 Desfazer/refaz o recurso é habilitado no modo de gráfico para as seguintes ações:  
  
-   Adicionando um único nó arrastando e soltando-se.  
  
-   Adicionando mais nós da janela de resultados de pesquisa no esquema Explorer ou em consultas de exibição de Início.  
  
-   Excluindo única ou mais nós.  
  
## <a name="zoom"></a>Aplicar Zoom  
 O zoom está disponível no canto inferior direito do modo de gráfico.  
  
 O zoom pode ser controlado das seguintes maneiras:  
  
- Mantendo a tecla CTRL e girar o mouse rode quando o mouse está sobre a superfície de exibição de gráfico.  
  
- Usando o controle deslizante. O controle deslizante mostra o nível atual de zoom.  
  
  O controle deslizante de zoom é opaco ao selecionar, o passa sobre ele, ou utiliza o CTRL com a roda do mouse para aplicar zoom; em quaisquer outros vezes, é transparente.  
  
## <a name="xml-editor-integration"></a>Integração de editor XML  
 Você pode alternar para frente e para trás entre o modo de gráfico e o editor XML clicando em um nó e usando o menu de contexto de código de exibição.  
  
 Se você alterar o esquema definido no editor XML, as alterações serão sincronizadas no modo de gráfico. Para obter mais informações, consulte [integração com Editor XML](../xml-tools/integration-with-xml-editor.md).  
  
## <a name="see-also"></a>Consulte também  
 [Superfície de design](../xml-tools/xml-schema-designer-workspace.md)



