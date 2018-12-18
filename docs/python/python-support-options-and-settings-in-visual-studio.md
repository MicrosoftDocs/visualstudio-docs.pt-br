---
title: Opções e configurações para Python
description: Uma referência para as várias configurações no Visual Studio que se relacionam ao código e projetos Python.
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-python
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Python_Tools
- VS.ToolsOptionsPages.Python_Tools.General
- VS.ToolsOptionsPages.Python_Tools.Debugging
- VS.ToolsOptionsPages.Python_Tools.Diagnostics
- VS.ToolsOptionsPages.Python_Tools.Experimental
- VS.ToolsOptionsPages.Python_Tools.Interactive_Windows
- VS.ToolsOptionsPages.Text_Editor.Python.Advanced
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- python
- data-science
ms.openlocfilehash: f5b8c6b3860641dafccac28b24a4be141d90eae5
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220050"
---
# <a name="options-for-python-in-visual-studio"></a>Opções para o Python no Visual Studio

Para exibir as opções do Python, use o comando de menu **Ferramentas** > **Opções**, verifique se **Mostrar todas as configurações** está marcado e navegue até **Ferramentas Python**:

![Caixa de diálogo de opções do Python, guia Geral](media/options-general.png)

Também há opções adicionais específicas do Python na guia **Editor de Texto** > **Python** > **Avançado** e na guia **Ambiente** > **Fontes e Cores** dentro do grupo **Editor de Texto**.

> [!Note]
> O grupo **Experimental** contém opções para recursos que ainda estão em desenvolvimento e não estão documentados aqui. Geralmente eles são discutidos em postagens no [blog Python engineering at Microsoft (Engenharia Python na Microsoft)](https://blogs.msdn.microsoft.com/pythonengineering/).

## <a name="general-options"></a>Opções gerais

(Guia **Ferramentas** > **Opções** > **Python**.)

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **Mostrar a Janela de Saída ao criar ambientes virtuais**| On | Desmarque essa opção para impedir que a janela **Saída** seja exibida. |
| **Mostrar a Janela de Saída ao instalar ou remover pacotes** | On | Desmarque essa opção para impedir que a janela **Saída** seja exibida. |
| **Sempre executar pip como administrador** | Off | Sempre eleva as operações `pip install` para todos os ambientes. Ao instalar pacotes, o Visual Studio solicitará privilégios de administrador se o ambiente estiver localizado em uma área protegida do sistema de arquivos como *c:\Program Files*. Nesse prompt, você pode optar por sempre elevar `pip install` apenas para esse ambiente específico. Confira [guia Pacotes](python-environments-window-tab-reference.md#packages-tab). |
| **Gerar automaticamente o BD de conclusão no primeiro uso** | On | *Aplica-se ao Visual Studio 2017 versão 15.5 e anteriores e a versões posteriores ao usar um banco de dados do IntelliSense.* Prioriza a conclusão do banco de dados para uma biblioteca quando você escreve código que a usa. Confira mais informações na [guia IntelliSense](python-environments-window-tab-reference.md#intellisense-tab). |
| **Ignorar variáveis PYTHONPATH de todo o sistema** | On | PYTHONPATH é ignorado por padrão porque o Visual Studio fornece um meio mais direto para especificar caminhos de pesquisa em projetos e ambientes. Confira [Caminhos de pesquisa](search-paths.md) para obter detalhes. |
| **Atualizar os caminhos de pesquisa ao adicionar arquivos vinculados** | On | Quando definido, adicionar um [arquivo vinculado](managing-python-projects-in-visual-studio.md#linked-files) a um projeto atualiza os [caminhos de pesquisa](search-paths.md) para que o IntelliSense possa incluir o conteúdo da pasta do arquivo vinculado em seu banco de dados de conclusão. Desmarque esta opção para excluir o conteúdo do banco de dados de conclusão. |
| **Avisar quando o módulo importado não puder ser encontrado** | On | Desmarque esta opção para suprimir avisos quando você sabe que um módulo importado não está disponível no momento, mas não afeta a operação do código de outra forma. |
| **Relatar recuo divergente como** | **Avisos** | Como o interpretador do Python depende muito do recuo adequado para determinar o escopo, o Visual Studio por padrão emite avisos quando detecta recuos inconsistentes que podem indicar erros de codificação. Definir como **Erros** para ser ainda mais estrito, o que faz com que o programa saia nesses casos. Para desabilitar esse comportamento completamente, selecione **Não**. |
| **Verificar se há pesquisa/notícias** | **Uma vez por semana** | Define a frequência com que você permite que o Visual Studio abra uma janela contendo uma página da Web com itens de notícias e pesquisas relacionados ao Python, se disponível. As opções são **Nunca**, **Uma vez por dia**, **Uma vez por semana** e **Uma vez por mês**. |
| Botão **Redefinir todas as caixas de diálogo permanentemente ocultas** | N/D | Caixas de diálogo diferentes fornecem opções como **Não mostrar novamente**. Use esse botão para limpar essas opções e fazer com que as caixas de diálogo sejam exibidas novamente. |

![Caixa de diálogo de opções do Python, guia Geral](media/options-general.png)

## <a name="debugging-options"></a>Opções de depuração

(Guia **Ferramentas** > **Opções** > **Python** > **Depuração**.)

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **Perguntar antes de executar quando houver erros** | On | Quando definido, solicita que você confirme que deseja executar o código que contém erros. Desmarque esta opção para desabilitar o aviso. |
| **Aguardar pela entrada quando o processo for encerrado de forma anormal**<br/><br/>**Aguardar pela entrada quando o processo for encerrado normalmente** | Ativo (para os dois) | Um programa de Python iniciado no Visual Studio é executado em sua própria janela de console. Por padrão, a janela espera que você pressione uma tecla antes de fechá-la, independentemente de como o programa é encerrado. Para remover este prompt e fechar a janela automaticamente, desmarque uma ou ambas as opções. |
| **A saída do programa para Depurar a janela de Saída** | On | Exibe a saída do programa em uma janela separada do console e na janela de **Saída** do Visual Studio. Desmarque esta opção para mostrar a saída somente na janela do console separado. |
| **Interromper a exceção SystemExit com código de saída zero** | Off | Se definido, interrompe o depurador nessa exceção. Quando desmarcado, o depurador sai sem interromper. |
| **Habilitar a depuração da biblioteca padrão do Python** | Off | Torna possível intervir no código-fonte da biblioteca padrão durante a depuração, mas aumenta o tempo necessário para iniciar o depurador.|

![Caixa de diálogo de opções do Python, guia Depuração](media/options-debugging.png)

## <a name="diagnostics-options"></a>Opções de diagnóstico

(Guia **Ferramentas** > **Opções** > **Python** > **Diagnóstico**.)

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **Incluir logs de análise** | On | Inclui logs detalhados relacionados à análise de ambientes do Python instalados ao salvar o diagnóstico em um arquivo ou copiá-los na área de transferência usando os botões. Essa opção pode aumentar significativamente o tamanho do arquivo gerado, mas costuma ser necessária para diagnosticar problemas do IntelliSense. |
| Botão **Salvar o diagnóstico no arquivo** | N/D | Solicita um nome de arquivo e salva o log em um arquivo de texto. |
| Botão **Copiar diagnóstico na área de transferência** | N/D | Coloca a totalidade do log na área de transferência; essa operação pode levar algum tempo, dependendo do tamanho do log. |

![Caixa de diálogo de opções do Python, guia Diagnóstico](media/options-diagnostics.png)

## <a name="interactive-windows-options"></a>Opções da Janela Interativa

(Guia **Ferramentas** > **Opções** > **Python** > **Janelas Interativas**.)

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **Scripts** | N/D | Especifica uma pasta geral para scripts de inicialização que serão aplicados às janelas **Interativas** de todos os ambientes. Consulte [Scripts de inicialização](python-environments-window-tab-reference.md#startup-scripts). No entanto, observe que esse recurso não funciona no momento. |
| **As setas para cima e para baixo navegam o histórico** | On | Usa as teclas de direção para navegar no histórico na janela **Interativa**. Desmarque essa configuração para usar as teclas de direção para navegar na saída da janela **Interativa**. |
| **Modo de Conclusão** | **Avaliar somente expressões sem chamadas de função** | O processo de determinar os membros disponíveis em uma expressão na janela **Interativa** pode exigir a avaliação da expressão incompleta atual, que pode resultar em efeitos colaterais ou funções sendo chamadas várias vezes. A configuração padrão **Avaliar somente expressões sem função chamadas** exclui expressões que aparecem para chamar uma função, mas avaliada outras expressões. Por exemplo, ele avalia `a.b`, mas não `a().b`.  **Nunca avaliar expressões** impede todos os efeitos colaterais, usando apenas o mecanismo IntelliSense normal para obter sugestões. **Avaliar todas as expressões** avalia a expressão completa para obter sugestões, independentemente de efeitos colaterais. |
| **Ocultar sugestões de análise estática** | Off | Quando definido, exibe apenas sugestões que são obtidas avaliando a expressão. Se combinado com o valor do **Modo de Conclusão** **Nunca avaliar expressões**, nenhuma conclusão útil será exibida na janela **Interativa**. |

![Caixa de diálogo de opções do Python, guia Janelas Interativas](media/options-interactive-windows.png)

## <a name="advanced-python-editor-options"></a>Opções avançadas de editor de Python

(Guia **Ferramentas** > **Opções** > **Editor de Texto** > **Python** > **Avançado**.)

### <a name="completion-results"></a>Resultados de Conclusão

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **A conclusão de membros exibe a interseção de membros** | Off | Quando definido, mostra apenas conclusões que têm suporte por todos os tipos possíveis. |
| **Lista de filtro com base na cadeia de pesquisa** | On | Aplica a filtragem de sugestões de preenchimento conforme você digita (o padrão é marcado). |
| **Mostrar automaticamente conclusões para todos os identificadores** | On | Desmarque esta opção para desabilitar as conclusões no editor e nas janelas **Interativas**. |

### <a name="selection-in-completion-list"></a>Seleção em listas de conclusão

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **Confirmado pela digitação dos seguintes caracteres** | **{}\[\]().,:;+-*/%&&#124;^~=<>#@\\** | Esses caracteres normalmente seguem um identificador que pode ser selecionado em uma lista de conclusão, portanto, é conveniente confirmar a conclusão digitando um caractere. Você pode remover ou adicionar caracteres específicos à lista conforme desejado.  |
| **Inserir a conclusão atual de confirmação** | On | Quando definido, a tecla **Enter** escolhe e aplica a conclusão escolhida no momento, assim como acontece com os caracteres acima (mas obviamente, não há um caractere para **Enter** portanto, ele não pode entrar diretamente para essa lista!). |
| **Adicionar uma nova linha ao pressionar Enter após o fim da palavra totalmente digitada** | Off | Por padrão, se você digitar a palavra inteira que aparece no pop-up de conclusão e pressionar **Enter**, você confirmará a conclusão. Ao definir essa opção, você realmente confirma as conclusões quando termina de digitar o identificador, de modo que **Enter** insere uma nova linha. |

### <a name="miscellaneous-options"></a>Opções diversas

| Opção | Padrão | Descrição |
| --- | --- | --- |
| **Entrar no modo de estrutura de tópicos na abertura dos arquivos** | On | Ative automaticamente o recurso de estrutura de tópicos do Visual Studio no editor ao abrir o arquivo de código do Python. |
| **Colar prompts REPL removidos** | On | Remove **>>>** e **...** do texto colado, permitindo a transferência fácil do código da janela **Interativa** para o editor. Desmarque essa opção se você precisar manter esses caracteres ao colar de outras fontes. |
| **Nomes de cores com base em tipos** | On | Habilita as cores de sintaxe no código do Python. |

![Caixa de diálogo de opções do editor do Python, guia Avançado](media/options-editor-advanced.png)

## <a name="fonts-and-colors-options"></a>Opções de Fontes e Cores

(Guia **Ambiente** > **Fontes e Cores** no grupo **Editor de Texto**.)

Os nomes das opções do Python são prefixadas com **Python** e são autoexplicativas. A fonte padrão para todos os temas de cores do Visual Studio é 10pt Consolas regular (não está em negrito). As cores padrão variam de acordo com o tema. Normalmente, você altera uma fonte ou a cor se tiver dificuldade para ler texto com as configurações padrão.

![Opções de fonte e cor do Python](media/options-fonts-and-colors.png)
