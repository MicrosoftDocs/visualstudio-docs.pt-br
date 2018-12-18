---
title: Interface de usuário do depurador (XSLT)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: reference
ms.assetid: 846fdabd-e5c3-4688-9b0d-a93fbeea1b96
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6c2cedf1a07307b8494e6a6b810e9590f347c9f1
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847377"
---
# <a name="debugger-user-interface-xslt"></a>Interface de usuário do depurador (XSLT)

Este tópico descreve as janelas e caixas de diálogo do depurador. Discute somente as partes da interface do usuário que têm o comportamento XSLT- específico de depuração.

Para obter mais informações, consulte o [referência de interface do usuário de depuração](../debugger/debugging-user-interface-reference.md).

## <a name="locals-window"></a>Janela Locais
 A janela locais exibe informações sobre todas as variáveis definidos na folha de estilos. A janela locais contém três colunas de informações:

 **Nome**

 Esta coluna contém os nomes de todos as variáveis locais no escopo atual. Conjuntos de nó têm um controle de árvore que você possa fazer pesquisa detalhadas para consultar suas subpastas.

 **Valor**

 Esta coluna mostra o valor contido por cada variável. O atributo, a instrução de processamento, o comentário, texto, e os nós CDATA exibem o valor de texto do nó. Os nós de namespace exibem URI de namespace.

 **Tipo**

 Essa coluna identifica o tipo de dados de cada variável listado na **nome** coluna.

 A janela locais também exibe as variáveis predefinidos de contexto que acompanham o contexto de transformação XSLT. A tabela a seguir descreve as variáveis predefinidos de contexto usados pelo depurador XSLT.

|Nome|Descrição|
|-|-----------------|
|`last()`|O tamanho do contexto.|
|`position()`|A posição, ou número de índice, o nó de contexto, relativo ao tamanho do contexto.|
|`self::node()`|O valor do nó de contexto.|

## <a name="output-window"></a>janela Saída
 A janela de saída mostra todas as mensagens de erro ou exceções de segurança que ocorrem durante a depuração.

 O depurador XSLT usa uma janela separada para exibir a saída do depurador. Isso é a mesma janela usada para exibir a saída de um **saída XSL de apresentação** comando.

## <a name="task-list"></a>Lista de Tarefas
 O **lista de tarefas** lista todos os erros de compilação na folha de estilos. Clique duas vezes no erro leva o cursor para a linha com o erro.

 O **lista de tarefas** inclui todos os erros que ocorrem nos blocos de script no arquivo XSLT.

> [!NOTE]
> O depurador XSLT não tem nenhum aviso, portanto, eles nunca aparecerão na **lista de tarefas**.

## <a name="breakpoints-window"></a>Janela Pontos de Interrupção
 A janela de pontos de interrupção mostra os pontos de interrupção definidos no projeto atual. Se um ponto de interrupção é adicionado quando a janela está em modo de exibição, a janela é atualizado automaticamente para mostrar o novo ponto de interrupção.

 A janela de pontos de interrupção deve se comportar da mesma maneira que outros depuradores do Visual Studio.

## <a name="command-windowimmediate-window"></a>Janela imediato/janela de comando
 Não implementado nesta versão do depurador XSLT.

## <a name="watch-window"></a>Janela Inspecionar
 A janela de observação é usada para avaliar as variáveis. Você também pode alterar os valores das variáveis.

 Variáveis exibidos na janela de observação são para o contexto atual (o item top-most na pilha de chamadas). Se você alterar o contexto, a janela de observação atualiza e exibe as variáveis definidas para esse contexto.

## <a name="call-stack-window"></a>janela de Pilha de Chamadas
 O **pilha de chamadas** janela é usada para exibir os nomes das funções na pilha de chamadas, tipos de parâmetro e valores de parâmetro. Informações de pilha de chamadas é mostrada somente quando o programa que está sendo depurado está em um estado de interrupção.

 A pilha de chamadas representa os vários contextos que a execução de fonte está atravessando. Por exemplo, se houver uma chamada de modelo "a" modelo "b", o modelo "a" e o modelo "b" aparecem na **pilha de chamadas** janela com o contexto atual na parte superior da lista. O usuário pode ver a consulta que está em execução atualmente.

 Se os modelos não têm um nome para o arquivo XSLT, os nomes gerados pelo processador XSLT são usados.

 Clique em um item diferente de aquele na parte superior da lista indica ao visualizador onde a ramificação de execução XSLT ocorreu usando realce padrão de verde e setas verde.

## <a name="quickwatch-dialog-box"></a>QuickWatch (caixa de diálogo)
 O **QuickWatch** caixa de diálogo é usada para avaliar expressões XPath 1.0. O nó de contexto (o nó de `self::node()` da janela locais) fornece o contexto para a execução da expressão XPath. O resultado de executar a expressão XPath é exibido na janela de observação.

 A lista a seguir descreve algumas restrições na avaliação de expressão XPath.

-   Somente as funções internas XPath são permitidas.

-   XSLT interno funciona como `document()`, `key()`, não é permitido, e assim por diante.

-   As funções definidas pelo usuário não são permitidas.

Para obter mais informações, consulte [como: avaliar uma expressão XPath](../xml-tools/how-to-evaluate-an-xpath-expression.md).

## <a name="disassembly-window"></a>janela de Desmontagem
 A janela de desmontagem mostra o código do assembly que é gerado pelo compilador XSLT. Esta janela pode ser usada da mesma forma como quaisquer outras janelas de desmontagem do Visual Studio.

 Para obter mais informações, [como: usar a janela de desmontagem](../debugger/how-to-use-the-disassembly-window.md).

## <a name="see-also"></a>Consulte também

- [Depuração de XSLT](../xml-tools/debugging-xslt.md)
- [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)
- [Inspecionar variáveis nas janelas autos e locais no Visual Studio](../debugger/autos-and-locals-windows.md)