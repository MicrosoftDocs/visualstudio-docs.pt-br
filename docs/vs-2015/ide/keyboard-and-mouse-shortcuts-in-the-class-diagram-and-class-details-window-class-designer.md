---
title: Atalhos de teclado e mouse no Diagrama de Classe e na Janela Detalhes da Classe (Designer de Classe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdetails.window
helpviewer_keywords:
- class diagrams, keyboard shortcuts
- class diagrams, mouse shortcuts
ms.assetid: c12d8dac-9902-4fde-b721-2a8116da53b7
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5865059e60907397ae7d69b230676ac63a5c3386
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543111"
---
# <a name="keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer"></a>Atalhos de teclado e mouse no diagrama de classe e janela Detalhes da Classe (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível usar o teclado, além do mouse, para executar ações de navegação no Designer de Classe e na janela **Detalhes da Classe**.

 **Neste tópico**

- [Usando o mouse no Designer de Classe](../ide/keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer.md#MouseClassDesigner)

- [Usando o mouse na Janela Detalhes da Classe](../ide/keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer.md#MouseClassDetails)

- [Usando o teclado no Designer de Classe](../ide/keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer.md#KeyboardClassDesigner)

- [Usando o teclado na Janela Detalhes da Classe](../ide/keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window-class-designer.md#KeyboardClassDetails)

## <a name="using-the-mouse-in-class-designer"></a><a name="MouseClassDesigner"></a>Usando o mouse em Designer de Classe
 As seguintes ações do mouse têm suporte em diagramas de classe:

|Combinação do mouse|Contexto|Descrição|
|-----------------------|-------------|-----------------|
|Clicar duas vezes|Elementos de forma|Abre o editor de códigos.|
||Conector de pirulito|Expande/recolhe o pirulito.|
||Rótulo do conector de pirulito|Invoca o comando **Mostrar Interface**.|
|Botão de rolagem do mouse|Diagrama de classe|Rolar verticalmente.|
|SHIFT + botão de rolagem do mouse|Diagrama de classe|Rolar horizontalmente.|
|CTRL + botão de rolagem do mouse|Diagrama de classe|Zoom.|
|CTRL + Shift + clique|Diagrama de classe|Zoom.|

## <a name="using-the-mouse-in-the-class-details-window"></a><a name="MouseClassDetails"></a> Usando o mouse na Janela Detalhes da Classe
 Usando um mouse, você pode alterar a aparência da Janela Detalhes da Classe e os dados que ela exibe das seguintes maneiras:

- Clicar em qualquer célula editável permite editar o conteúdo da célula. As alterações são refletidas em todos os locais em que dados são armazenados ou exibidos, incluindo na janela Propriedades e no código-fonte.

- Clicar em qualquer célula de uma linha faz com que a janela Propriedades exiba as propriedades do elemento representado pela linha.

- Para alterar a largura de uma coluna, arraste o limite do lado direito do título de coluna até que a coluna tenha a largura desejada.

- É possível expandir ou recolher nós de propriedade ou compartimento clicando nos símbolos de direção à esquerda da linha.

- A Janela Detalhes da Classe oferece vários botões para a criação de novos membros na classe atual e para navegar entre os compartimentos dos membros na grade da Janela Detalhes da Classe. Para obter mais informações, consulte Botões da Janela Detalhes da Classe.

## <a name="using-the-keyboard-in-class-designer"></a><a name="KeyboardClassDesigner"></a>Usando o teclado no Designer de Classe
 As seguintes ações do teclado têm suporte em diagramas de classe:

|Chave|Contexto|Descrição|
|---------|-------------|-----------------|
|Teclas de direção|Dentro das formas de tipo|Navegação em estilo de árvore pelo conteúdo da forma (há suporte para o encapsulamento da forma). As teclas para a esquerda e para a direita expandem/recolhem o item atual se ele for expansível e navegam até o pai se ele não for (consulte a navegação do modo de exibição em árvore para ver o comportamento detalhado).|
||Formas de nível superior|Mover formas no diagrama.|
|SHIFT + teclas de direção|Dentro das formas de tipo|Criar uma seleção contínua que consiste em elementos de forma, como membros, tipos aninhados ou compartimentos. Esses atalhos não dão suporte ao encapsulamento.|
|HOME|Dentro das formas de tipo|Navegue até o título de forma de nível superior.|
||Formas de nível superior|Navegue até a primeira forma no diagrama.|
|END|Dentro das formas de tipo|Navegue até o último elemento visível dentro da forma.|
||Formas de nível superior|Navegue até a última forma no diagrama.|
|SHIFT+HOME|Dentro da forma de tipo|Seleciona elementos dentro da forma, começando pelo item atual e terminando com o item superior na mesma forma.|
|SHIFT+END|Dentro da forma de tipo|O mesmo que SHIFT + HOME, mas na direção de cima para baixo.|
|Enter|Todos os contextos|Invoca a ação padrão na forma, o que também está disponível por meio de um clique duplo. Na maioria dos casos, essa ação é Exibir Código, mas alguns elementos a definem de maneira diferente (pirulitos, cabeçalhos de compartimento, rótulos de pirulito).|
|+/-|Todos os contextos|Se o elemento em foco atualmente for expansível, essas chaves expandem/recolhem o elemento.|
|>|Todos os contextos|Em elementos com filhos, isso expande o elemento se ele estiver recolhido e navega até o primeiro filho.|
|<|Todos os contextos|Navega até o elemento pai.|
|ALT + SHIFT + L|Dentro de formas de tipo + em formas de tipo.|Navega para o pirulito da forma selecionada atualmente, se ele estiver presente.|
|ALT + SHIFT + B|Dentro de formas de tipo + em formas de tipo.|Se lista de tipos base for mostrada na forma de tipo e tiver mais de um item, isso alternará o estado de expansão da lista (expandir/recolher).|
|Delete (excluir)|Em formas de tipo e de comentário|Invoca o comando **Remover do Diagrama**.|
||Em todo o resto.|Invoca o comando **Excluir do Código** (membros, parâmetros, associações, herança, rótulos de pirulito).|
|CTRL+DELETE|Todos os contextos|Invoca o comando **Excluir do Código** na seleção.|
|TAB|Todos os contextos|Navega até o próximo filho dentro do mesmo pai (dá suporte a encapsulamento).|
|SHIFT+TAB|Todos os contextos|Navega até o filho anterior dentro do mesmo pai (dá suporte a encapsulamento).|
|SPACE|Todos os contextos|Alterna a seleção no elemento atual.|

## <a name="using-the-keyboard-in-the-class-details-window"></a><a name="KeyboardClassDetails"></a> Usando o teclado na Janela Detalhes da Classe

> [!NOTE]
> As seguintes associações de teclas foram escolhidas para reproduzir especificamente a experiência de digitar código.

 Use as teclas a seguir para navegar na Janela Detalhes da Classe:

|Chave|Result|
|-|-|
|, (vírgula)|Se o cursor estiver em uma linha de parâmetro, digitar uma vírgula move o cursor para o campo Nome do parâmetro seguinte. Se o cursor estiver na linha do último parâmetro de um método, ele moverá o cursor para o \<add parameter> campo, que você pode usar para criar um novo parâmetro.<br /><br /> Se o cursor estiver em outro lugar na Janela Detalhes da Classe, digitar uma vírgula literalmente adiciona uma vírgula ao campo atual.|
|; (ponto e vírgula)<br /><br /> ou o<br /><br /> ) (parêntese de fechamento)|Mova o cursor para o campo Nome da próxima linha de membro na grade da Janela Detalhes da Classe.|
|Tab|Move o cursor para o campo seguinte, se movendo primeiro da esquerda para a direita e, depois, de cima para baixo. Se o cursor estiver se movendo de um campo no qual você digitou texto, a Janela Detalhes da Classe processa o texto e o armazena se ele não produzir um erro.<br /><br /> Se o cursor estiver em um campo vazio, como \<add parameter> , Tab o move para o primeiro campo da próxima linha.|
|\<space>|Move o cursor para o campo seguinte, se movendo primeiro da esquerda para a direita e, depois, de cima para baixo. Se o cursor estiver em um campo vazio, como \<add parameter> , ele será movido para o primeiro campo da próxima linha. Observe que \<space> é digitado imediatamente após uma vírgula ser ignorada.<br /><br /> Se o cursor estiver no campo Resumo, digitar um espaço adiciona um caractere de espaço.<br /><br /> Se o cursor estiver na coluna Ocultar de uma determinada linha, digitar um espaço alterna o valor da caixa de seleção Ocultar.|
|CTRL + Tab|Mude para outra janela do documento. Por exemplo, mude da Janela Detalhes da Classe para um arquivo de código aberto.|
|ESC (Escape)|Se você tiver começado a digitar texto em um campo, pressionar ESC atua como uma tecla de desfazer, revertendo o conteúdo do campo para o valor anterior. Se a Janela Detalhes da Classe tiver foco geral, mas nenhuma célula específica estiver em foco, pressionar ESC tira o foco da Janela Detalhes da Classe.|
|Seta para cima e seta para baixo|Essas chaves movem o cursor de uma linha para outra, verticalmente, na grade da Janela Detalhes da Classe.|
|Seta para a esquerda|Se o cursor estiver na coluna Nome, pressionar a seta para a esquerda recolhe o nó atual da hierarquia (se ele estiver aberto).|
|Seta para a direita|Se o cursor estiver na coluna Nome, pressionar a seta para a direita expande o nó atual da hierarquia (se ele estiver recolhido).|

## <a name="see-also"></a>Consulte Também
 [Criando e configurando membros de tipo (Designer de Classe)](../ide/creating-and-configuring-type-members-class-designer.md)
