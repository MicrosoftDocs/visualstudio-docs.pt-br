---
title: Atalhos de teclado e do mouse do Designer de Classe
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.classdetails.window
helpviewer_keywords:
- class diagrams, keyboard shortcuts
- class diagrams, mouse shortcuts
ms.assetid: c12d8dac-9902-4fde-b721-2a8116da53b7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 30932a6c94bc6104aeea0244f06f471d0a639b21
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533660"
---
# <a name="keyboard-and-mouse-shortcuts-in-the-class-diagram-and-class-details-window"></a>Atalhos de teclado e do mouse no Diagrama de Classe e na janela Detalhes da Classe

É possível usar o teclado, além do mouse, para executar ações de navegação no **Designer de Classe** e na janela **Detalhes da Classe**.

## <a name="use-the-mouse-in-class-designer"></a>Usar o mouse no Designer de Classe

As seguintes ações do mouse têm suporte em diagramas de classe:

|Combinação do mouse|Contexto|Descrição|
| - |-------------|-----------------|
|Clicar duas vezes|Elementos de forma|Abre o editor de códigos.|
|Clicar duas vezes|Conector de pirulito|Expande/recolhe o pirulito.|
|Clicar duas vezes|Rótulo do conector de pirulito|Invoca o comando **Mostrar Interface**.|
|Botão de rolagem do mouse|Diagrama de classe|Rolar verticalmente.|
|**Shift** + botão de rolagem do mouse|Diagrama de classe|Rolar horizontalmente.|
|**Ctrl** + botão de rolagem do mouse|Diagrama de classe|Zoom.|
|**Ctrl** + **Shift** + clique|Diagrama de classe|Zoom.|

## <a name="use-the-mouse-in-the-class-details-window"></a>Usar o mouse na janela Detalhes da Classe

Usando um mouse, você pode alterar a aparência da janela de **detalhes da classe** e os dados exibidos das seguintes maneiras:

- Clicar em qualquer célula editável permite editar o conteúdo da célula. As alterações são refletidas em todos os locais em que dados são armazenados ou exibidos, incluindo na janela **Propriedades** e no código-fonte.

- Clicar em qualquer célula de uma linha faz com que a janela **Propriedades** exiba as propriedades do elemento representado pela linha.

- Para alterar a largura de uma coluna, arraste o limite do lado direito do título de coluna até que a coluna tenha a largura desejada.

- É possível expandir ou recolher nós de propriedade ou compartimento clicando nos símbolos de direção à esquerda da linha.

- A janela **Detalhes da Classe** oferece vários botões para a criação de novos membros na classe atual e para navegar entre os compartimentos dos membros na grade da janela **Detalhes da Classe**.

## <a name="use-the-keyboard-in-class-designer"></a>Usar o teclado do Designer de Classe

As seguintes ações do teclado têm suporte em diagramas de classe:

|Chave|Contexto|Descrição|
|---------|-------------|-----------------|
|**Teclas de direção**|Dentro das formas de tipo|Navegação em estilo de árvore pelo conteúdo da forma (há suporte para o encapsulamento da forma). As teclas para a esquerda e para a direita expandem/recolhem o item atual se ele for expansível e navegam até o pai se ele não for (consulte a navegação do modo de exibição em árvore para ver o comportamento detalhado).|
|**Teclas de direção**|Formas de nível superior|Mover formas no diagrama.|
|**Shift** + **teclas de direção**|Dentro das formas de tipo|Criar uma seleção contínua que consiste em elementos de forma, como membros, tipos aninhados ou compartimentos. Esses atalhos não dão suporte ao encapsulamento.|
|**Início**|Dentro das formas de tipo|Navegue até o título de forma de nível superior.|
|**Início**|Formas de nível superior|Navegue até a primeira forma no diagrama.|
|**End**|Dentro das formas de tipo|Navegue até o último elemento visível dentro da forma.|
|**End**|Formas de nível superior|Navegue até a última forma no diagrama.|
|**Shift** + **Página inicial**|Dentro da forma de tipo|Seleciona elementos dentro da forma, começando pelo item atual e terminando com o item superior na mesma forma.|
|**Shift** + **Fim**|Dentro da forma de tipo|O mesmo que **Shift** + **Home** , mas na direção de cima para baixo.|
|**Digita**|Todos os contextos|Invoca a ação padrão na forma, o que também está disponível por meio de um clique duplo. Na maioria dos casos, essa ação é Exibir Código, mas alguns elementos a definem de maneira diferente (pirulitos, cabeçalhos de compartimento, rótulos de pirulito).|
|**+** e**-**|Todos os contextos|Se o elemento em foco no momento for expansível, essas chaves expandirão ou recolherão o elemento.|
|**>**|Todos os contextos|Em elementos com filhos, isso expande o elemento se ele estiver recolhido e navega até o primeiro filho.|
|**<**|Todos os contextos|Navega até o elemento pai.|
|**ALT** + **Shift** + **L**|Dentro de formas de tipo + em formas de tipo.|Navega para o pirulito da forma selecionada atualmente, se ele estiver presente.|
|**ALT** + **Shift** + **B**|Dentro de formas de tipo + em formas de tipo.|Se lista de tipos base for mostrada na forma de tipo e tiver mais de um item, isso alternará o estado de expansão da lista (expandir/recolher).|
|**Excluir**|Em formas de tipo e de comentário|Invoca o comando **Remover do Diagrama**.|
|**Excluir**|Em todo o resto.|Invoca o comando **Excluir do Código** (membros, parâmetros, associações, herança, rótulos de pirulito).|
|**Ctrl** + **Excluir**|Todos os contextos|Invoca o comando **Excluir do Código** na seleção.|
|**Tab**|Todos os contextos|Navega até o próximo filho dentro do mesmo pai (dá suporte a encapsulamento).|
|**Shift** + **Guia**|Todos os contextos|Navega até o filho anterior dentro do mesmo pai (dá suporte a encapsulamento).|
|**Barra de espaços**|Todos os contextos|Alterna a seleção no elemento atual.|

## <a name="use-the-keyboard-in-the-class-details-window"></a>Usar o teclado na janela Detalhes da Classe

> [!NOTE]
> As seguintes associações de teclas foram escolhidas para reproduzir especificamente a experiência de digitar código.

Usar as chaves a seguir para navegar na janela **Detalhes da Classe**:

|Chave|Result|
|-|-|
|**,** (vírgula)|Se o cursor estiver em uma linha de parâmetro, digitar uma vírgula move o cursor para o campo Nome do parâmetro seguinte. Se o cursor estiver na linha do último parâmetro de um método, ele moverá o cursor para o \<add parameter> campo, que você pode usar para criar um novo parâmetro.<br /><br /> Se o cursor estiver em outro lugar na janela **Detalhes da Classe**, digitar uma vírgula adicionará literalmente uma vírgula ao campo atual.|
|**;** (ponto e vírgula) ou **)** (parênteses de fechamento)|Mova o cursor para o campo Nome da próxima linha de membro na grade da janela **Detalhes da Classe**.|
|**Tab**|Move o cursor para o campo seguinte, se movendo primeiro da esquerda para a direita e, depois, de cima para baixo. Se o cursor estiver saindo de um campo no qual você digitou texto, a janela **Detalhes da Classe** processará o texto e o armazenará se ele não produzir um erro.<br /><br /> Se o cursor estiver em um campo vazio, como \<add parameter> , Tab o move para o primeiro campo da próxima linha.|
|**Barra de espaços**|Move o cursor para o campo seguinte, se movendo primeiro da esquerda para a direita e, depois, de cima para baixo. Se o cursor estiver em um campo vazio, como \<add parameter> , ele será movido para o primeiro campo da próxima linha. Observe que \<space> é digitado imediatamente após uma vírgula ser ignorada.<br /><br /> Se o cursor estiver no campo Resumo, digitar um espaço adiciona um caractere de espaço.<br /><br /> Se o cursor estiver na coluna Ocultar de uma determinada linha, digitar um espaço alterna o valor da caixa de seleção Ocultar.|
|**Ctrl** + **Guia**|Mude para outra janela do documento. Por exemplo, mude da janela **Detalhes da Classe** para um arquivo de código aberto.|
|**Esc**|Se você tiver começado a digitar texto em um campo, pressionar ESC atua como uma tecla de desfazer, revertendo o conteúdo do campo para o valor anterior. Se a janela Detalhes da Classe tiver o foco geral, mas nenhuma célula específica estiver em foco, pressionar ESC removerá o foco da janela **Detalhes da Classe**.|
|Seta para **cima** e **seta para baixo**|Essas chaves movem o cursor de uma linha para outra, verticalmente, na grade da janela **Detalhes da Classe**.|
|**Seta para a esquerda**|Se o cursor estiver na coluna Nome, pressionar a seta para a esquerda recolhe o nó atual da hierarquia (se ele estiver aberto).|
|**Seta para a direita**|Se o cursor estiver na coluna Nome, pressionar a seta para a direita expande o nó atual da hierarquia (se ele estiver recolhido).|

## <a name="see-also"></a>Confira também

- [Criar e configurar membros do tipo](creating-and-configuring-type-members.md)
- [Como usar exclusivamente o teclado](../reference/how-to-use-the-keyboard-exclusively.md)
- [Atalhos de teclado padrão no Visual Studio](../default-keyboard-shortcuts-in-visual-studio.md)
- [Atalhos de teclado no Blend](../../xaml-tools/keyboard-shortcuts-in-blend.md)
