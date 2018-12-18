---
title: Visual C# IntelliSense | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IntelliSense [J#]
- Visual C#, IntelliSense
- IntelliSense [C#]
ms.assetid: 79ca304d-dc1e-4dc9-a2a6-7808df2e588e
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 0d094a0272e5c90afa1a83a42543dd464f219a17
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862197"
---
# <a name="visual-c-intellisense"></a>Visual C# IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Visual C# IntelliSense fica disponível durante a codificação no editor e durante a depuração na janela Comando [Modo Imediato](../ide/reference/immediate-window.md).  
  
## <a name="completion-lists"></a>Listas de Conclusão  
 As listas de preenchimento do IntelliSense no Visual C# contêm tokens de Listar Membros, Completar Palavra e muito mais. Ele fornece acesso rápido a:  
  
- Membros de um tipo ou namespace,  
  
- Variáveis, comandos e nomes de funções,  
  
- [Snippets de código](#CodeSnippets),  
  
- [Palavras-chave de linguagem](#Keywords),  
  
- [Métodos de Extensão](#ExtensionMethods)  
  
  A Lista de Conclusão no C# também é inteligente o suficiente para filtrar tokens irrelevantes e pré-selecionar um token com base no contexto. Para obter mais informações, consulte [Listas de preenchimento filtradas no C#](../misc/filtered-completion-lists-in-csharp.md) e [Itens pré-selecionados da lista de preenchimento no C#](../misc/pre-selected-completion-list-items-in-csharp.md).  
  
###  <a name="CodeSnippets"></a> Snippets de código em listas de preenchimento  
 No Visual C#, a lista de preenchimento inclui snippets de código para ajudá-lo a inserir com facilidade corpos de código predefinidos no programa. Os snippets de código são exibidos na lista de preenchimento como o [Elemento de atalho (snippets de código do IntelliSense)](http://msdn.microsoft.com/en-us/052cc97a-5c70-42f8-b398-4c3adf670cfa) do snippet.  Para obter mais informações sobre os snippets de código disponíveis no Visual C# por padrão, consulte [Snippets de código do Visual C#](../ide/visual-csharp-code-snippets.md).  
  
###  <a name="Keywords"></a> Palavras-chave de linguagem em listas de preenchimento  
 No Visual C#, a lista de preenchimento também inclui palavras-chave. Para obter mais informações sobre palavras-chave de linguagem do C#, consulte [Palavras-chave do C#](http://msdn.microsoft.com/library/e929b0f2-4b92-4d37-8060-23d323b098ad).  
  
###  <a name="ExtensionMethods"></a> Métodos de extensão em listas de preenchimento  
 No Visual C#, a lista de preenchimento inclui Métodos de Extensão que estão no escopo.  
  
> [!NOTE]
>  A lista de conclusão não exibe todos os métodos de extensão para objetos <xref:System.String>.  
  
 Os métodos de extensão usam um ícone diferente dos métodos de instância. Para obter uma listagem de ícones de lista, consulte [Modo de Exibição de Classe e ícones do Pesquisador de Objetos](../ide/class-view-and-object-browser-icons.md). Quando um método de instância e um método de extensão com o mesmo nome estão no escopo, a lista de preenchimento exibe o ícone do método de extensão.  
  
### <a name="filtered-completion-lists"></a>Listas de preenchimento filtradas  
 O IntelliSense remove membros desnecessários da lista de preenchimento usando filtros.  
  
 O Visual C# filtra as listas de preenchimento exibidas para estes itens:  
  
-   **Interfaces e classes base.** O IntelliSense remove automaticamente itens das listas de preenchimento de interface e de classe base nas listas de base de declaração de classe e de interface e nas listas de restrição. Por exemplo, enumerações não aparecem na lista de preenchimento nas classes base, pois enumerações não podem ser usadas para as classes base. A lista de preenchimento de classes base contém apenas interfaces e namespaces. Se você selecionar um item na lista e, em seguida, digitar uma vírgula, o IntelliSense removerá as classes base da lista de preenchimento, pois o Visual C# não dá suporte à herança múltipla. O mesmo comportamento também ocorre em cláusulas de restrição.  
  
-   **Atributos**: ao aplicar um atributo a um tipo, a lista de conclusão é filtrada para que ela tenha somente os tipos que descendem dos namespaces que contêm esses tipos, como <xref:System.Attribute>.  
  
-   Operadores `as` e `is`.  
  
-   **Cláusulas catch.**  
  
-   **Inicializadores de objeto:** somente os membros que podem ser inicializados serão exibidos na lista de preenchimento.  
  
-   **Nova palavra-chave**: ao digitar `new` e pressionar a BARRA DE ESPAÇOS, é exibida uma lista de preenchimento. Um item é selecionado na lista automaticamente, de acordo com o contexto no código. Por exemplo, os itens são selecionados automaticamente na lista de preenchimento em busca de declarações e instruções de retorno nos métodos.  
  
-   **Operadores as e is:** uma lista de preenchimento filtrada é exibida automaticamente ao pressionar a BARRA DE ESPAÇOS depois de digitar a palavra-chave `as` ou `is`.  
  
-   Eventos: ao digitar a palavra-chave `event`, a lista de preenchimento conterá apenas os tipos de delegado.  
  
-   A ajuda do parâmetro classifica automaticamente para a primeira sobrecarga de método que corresponde aos parâmetros, conforme eles são inseridos. Se houver várias sobrecargas de método disponíveis, será possível usar as setas para cima e para baixo para navegar para a próxima sobrecarga possível na lista.  
  
## <a name="most-recently-used-members"></a>Membros usados mais recentemente  
 O IntelliSense lembra os membros selecionados recentemente na caixa pop-up [Listar Membros](../ide/using-intellisense.md) quanto à conclusão automática de nome de objeto. Na próxima vez que você usar a Lista de Membros, os membros usados mais recentemente serão mostrados na parte superior. O histórico dos membros mais usados recentemente é limpo entre cada sessão no IDE.  
  
## <a name="override"></a>override  
 Ao digitar [override](http://msdn.microsoft.com/library/dd1907a8-acf8-46d3-80b9-c2ca4febada8) e, em seguida, pressionar a BARRA DE ESPAÇOS, o IntelliSense exibirá todos os membros da classe base válidos que podem ser substituídos em uma caixa de listagem pop-up. Digitar o tipo de retorno do método após `override` solicitará ao IntelliSense para mostrar apenas os métodos que retornam o mesmo tipo. Quando o IntelliSense não conseguir encontrar nenhuma correspondência, ele exibirá todos os membros da classe base.  
  
## <a name="automatic-code-generation"></a>Geração automática de códigos  
  
### <a name="add-using"></a>Adicionar usando  
 A operação Adicionar usando o IntelliSense permite que você mantenha o foco no código que está sendo escrito, em vez de precisar mudar o foco para outra parte do código.  
  
 Para iniciar a operação Adicionar usando, posicione o cursor em uma referência de tipo que não pode ser resolvida. Por exemplo, ao criar um aplicativo de console e, em seguida, adicionar `XmlTextReader` ao corpo do método `Main`, uma marcação inteligente será exibida abaixo do caractere mais à direita de `XmlTextReader`, pois ele aparece como uma referência de tipo que não pode ser resolvida.  
  
 ![Adicionar usando a imagem de marcação inteligente](../ide/media/addusesmart.gif "AddUseSmart")  
  
 Em seguida, é possível invocar a operação Adicionar usando selecionando-a no submenu **Resolver** do menu **IntelliSense** ou do menu de contexto, ou invocando Adicionar usando por meio da marcação inteligente. A marcação inteligente fica visível apenas quando o cursor está posicionado no tipo não associado ou adjacente a ele.  
  
 ![Adicionar usando, imagem expandida da marcação inteligente](../ide/media/addusesmartexp.gif "AddUseSmartExp")  
  
### <a name="organize-usings"></a>Organizar usos  
 As opções **Organizar Usos** classificam e removem as declarações `using` e `extern` sem alterar o comportamento do código-fonte. Ao longo do tempo, os arquivos de origem poderão ficar sobrecarregados e ser difíceis de serem lidos devido a diretivas `using` desnecessárias e desorganizadas. As opções **Organizar Usos** compactam o código-fonte removendo diretivas `using` não utilizadas e melhoram a legibilidade com sua classificação.  
  
 Para ver as opções disponíveis no IDE do Visual Studio, no menu **Editar**, aponte para **IntelliSense** e, em seguida, para **Organizar Usos**. O IDE fornece as seguintes opções para organizar e remover as diretivas `usings`:  
  
### <a name="implement-interface"></a>Implementar interface  
 O IntelliSense fornece uma opção para ajudá-lo a implementar uma [interface](http://msdn.microsoft.com/library/7da38e81-4f99-4bc5-b07d-c986b687eeba) enquanto estiver trabalhando no Editor de Código. Normalmente, para implementar uma interface corretamente, é necessário criar uma declaração de método para cada membro da interface na classe. Usando o IntelliSense, depois de digitar o nome de uma interface em uma declaração de classe, uma marcação inteligente é exibida. A marcação inteligente oferece a opção de implementar a interface automaticamente, usando a nomenclatura explícita ou implícita. Na nomenclatura explícita, as declarações de método levam o nome da interface; na nomenclatura implícita, as declarações de método não indicam a interface à qual pertencem. Um método de interface explicitamente nomeado só pode ser acessado por meio de uma instância de interface, e não por meio de uma instância de classe. Para obter mais informações, consulte [Implementação explícita da interface](http://msdn.microsoft.com/library/181c901f-0d4c-4f29-97fc-895079617bf2).  
  
 A implementação da interface gerará o número mínimo de stubs de método necessários para atender à interface. Se uma classe base implementar partes da interface, os stubs não serão regenerados.  
  
### <a name="implement-abstract-base-class"></a>Implementar classe base abstrata  
 O IntelliSense fornece uma opção para ajudá-lo a implementar membros de uma classe base abstrata automaticamente enquanto estiver trabalhando no Editor de Código. Normalmente, para implementar membros de uma classe base abstrata, é necessário criar uma nova definição de método para cada método da classe base abstrata na classe derivada. Usando o IntelliSense, depois de digitar o nome de uma classe base abstrata em uma declaração de classe, uma marcação inteligente é exibida. A marcação inteligente oferece a opção de implementar os métodos de classe base automaticamente.  
  
 Os stubs de método gerados pelo recurso Implementar Classe Base Abstrata são modelados pelo trecho de código definido no arquivo MethodStub.snippet. Os snippets de código são modificáveis. Para obter mais informações, consulte [Passo a passo: criando um snippet de código](../ide/walkthrough-creating-a-code-snippet.md).  
  
### <a name="generate-from-usage"></a>Gerar com base no uso  
 O recurso **Gerar com Base no Uso** permite usar classes e membros antes de defini-los. É possível gerar um stub para qualquer classe, construtor, método, propriedade, campo ou enumeração que você deseja usar, mas que ainda não foi definido. É possível gerar novos tipos e membros sem sair do local atual no código. Isso minimiza a interrupção do fluxo de trabalho.  
  
 Um sublinhado ondulado é exibido em cada identificador indefinido. Ao posicionar o ponteiro do mouse sobre o identificador, uma mensagem de erro é exibida em uma dica de ferramenta.  
  
 Para exibir as opções apropriadas, é possível usar um dos seguintes procedimentos:  
  
- Clique no identificador indefinido. Um sublinhado curto é exibido abaixo do caractere mais à esquerda. Posicione o ponteiro do mouse sobre o sublinhado curto e uma marcação inteligente (um ícone) será exibida. Clique na marcação inteligente.  
  
- Clique no identificador indefinido e pressione CTRL+. (ponto).  
  
- Clique com o botão direito do mouse no identificador indefinido e clique em **Gerar**.  
  
  As opções exibidas podem incluir as seguintes:  
  
- **Gerar stub de propriedade**  
  
- **Gerar stub de campo**  
  
- **Gerar stub de método**  
  
- **Gerar classe**  
  
- **Gerar novo tipo** (para uma classe, um struct, uma interface ou enumeração)  
  
## <a name="generate-event-handlers"></a>Gerar manipuladores de eventos  
 No Editor de Código, o IntelliSense pode ajudá-lo a vincular métodos (manipuladores de eventos) a campos de evento.  
  
 Ao digitar o operador `+=` após um campo de evento em um arquivo .cs, o IntelliSense mostra a opção de pressionar a tecla TAB. Isso insere uma nova instância de um delegado que aponta para o método que manipula o evento.  
  
 ![Botão Vínculo Automático](../ide/media/vxautohookup.gif "vxAutoHookUp")  
  
 Se você pressionar TAB, o IntelliSense concluirá a instrução para você automaticamente e exibirá a referência de manipulador de eventos como um texto selecionado no Editor de Código. Para concluir o vínculo automático de evento, o IntelliSense solicita que você pressione a tecla TAB novamente para criar um stub vazio para o manipulador de eventos.  
  
 ![Gerar manipulador de eventos](../ide/media/vxgenerateeventhandler.gif "vxGenerateEventHandler")  
  
> [!NOTE]
>  Se um novo delegado criado pelo IntelliSense referenciar um manipulador de eventos existente, o IntelliSense comunicará essas informações na dica de ferramenta. Depois, é possível modificar essa referência; o texto já está selecionado no Editor de Código. Caso contrário, o vínculo automático de evento será concluído nesse ponto.  
  
 Se você pressionar TAB, o IntelliSense criará um stub de um método com a assinatura correta e colocará o cursor no corpo do manipulador de eventos.  
  
> [!NOTE]
>  Use o comando **Navegação Regressiva** no menu **Exibir** (CTRL+-) para retornar à declaração de vínculo de evento.  
  
 A tarefa a seguir mostra como o IntelliSense vincula automaticamente um manipulador de eventos chamado `button1_Click` a um campo de evento chamado `button1.Click`.  
  
## <a name="see-also"></a>Consulte também  
 [Visual Studio IDE](../ide/visual-studio-ide.md)



