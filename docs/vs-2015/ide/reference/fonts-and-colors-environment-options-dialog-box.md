---
title: Caixa de diálogo Fontes e Cores, Ambiente, Opções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPag.Environment.Fonts_And_Colors
- VS.ToolsOptionsPages.FontsAndColors
- VS.ToolsOptionsPages.Environment.Fonts_And_Colors
- VS.Environment.Fonts And Colors
helpviewer_keywords:
- colors, customizing IDE
- Query and View Designer, customizing
- fonts, editors
- menus, customizing
- Table Designer, customizing
- Database Designer, customizing environment
- default colors
- accessibility, options
- editors, customizing
- designers, customizing environment
- defaults, colors
- printers, customizing
ms.assetid: c767d302-51ed-47a8-a527-c07bce2aa485
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: dbaaab64a50a918844a8f9060ce80ee8c8e7ae00
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220229"
---
# <a name="fonts-and-colors-environment-options-dialog-box"></a>Caixa de diálogo Fontes e Cores, Ambiente, Opções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

  
A página **Fontes e Cores** da caixa de diálogo **Opções** permite estabelecer um esquema de cores e fontes personalizado para vários elementos da interface do usuário no IDE (ambiente de desenvolvimento integrado). É possível acessar essa caixa de diálogo clicando em **Ferramentas / Opções** e, em seguida, selecionando **Ambiente / Fontes e Cores**. Se essa página não aparecer na lista, selecione **Mostrar todas as configurações** na caixa de diálogo **Opções**.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Alterações do esquema de cores não terão efeito durante a sessão em que foram feitas. É possível avaliar alterações de cores abrindo outra instância do Visual Studio e produzindo as condições nas quais você espera aplicar essas alterações.  
  
 **Mostrar configurações de**  
 Lista todos os elementos da interface do usuário para os quais é possível alterar os esquemas de fontes e cores. Após selecionar um item da lista, você pode personalizar as configurações de cor do item selecionado em **Exibir itens**.  
  
- **Editor de Texto**  
  
   Alterações nas configurações de exibição de cor, tamanho e estilo da fonte do Editor de Texto afetam a aparência do texto no editor de texto padrão. Documentos abertos em um editor de texto fora do IDE não serão afetados por essas configurações.  
  
- **Impressora**  
  
   Alterações nas configurações de exibição de cor, tamanho e estilo da fonte da Impressora afetam a aparência do texto em documentos impressos.  
  
  > [!NOTE]
  >  Conforme for necessário, é possível selecionar uma fonte padrão para impressão diferente daquela usada para exibição no editor de texto. Isso pode ser útil ao imprimir códigos que contêm caracteres de byte único e de caractere duplo.  
  
- **Preenchimento de Declaração**  
  
   Altera o tamanho e o estilo da fonte do texto que aparece no pop-up de preenchimento de declaração no editor.  
  
- **Dica de ferramenta do Editor**  
  
   Altera o tamanho e o estilo da fonte do texto que aparece em ToolTips exibidas no editor.  
  
- **Fonte do ambiente**  
  
   Altera o tamanho e o estilo da fonte de todos os elementos de interface do usuário do IDE que ainda não têm uma opção separada em **Mostrar configurações de**. Por exemplo, essa opção se aplica à **Página Inicial**, mas não afetaria a Janela de **Saída**.  
  
- **[Todas as janelas de ferramentas de texto]**  
  
   Alterações nas configurações de exibição de cor, tamanho e estilo da fonte deste item afetam a aparência do texto nas janelas de ferramentas que têm painéis de saída no IDE. Por exemplo, Janela de Saída, janela Comando, janela Imediato etc.  
  
  > [!NOTE]
  >  Alterações no texto de itens **[Todas as janelas de ferramentas de texto]** não terão efeito durante a sessão em que forem feitas. É possível avaliar tais alterações abrindo outra instância do Visual Studio.  
  
  **Usar Padrões**  
  Redefine os valores de fonte e cor do item de lista selecionado em **Mostrar configurações de**. O botão **Usar** é exibido quando outros esquemas de exibição estão disponíveis para seleção. Por exemplo, é possível escolher entre dois esquemas para a impressora.  
  
  **Fonte (o negrito indica fontes de largura fixa)**  
  Lista todas as fontes instaladas em seu sistema. Quando o menu suspenso aparece pela primeira vez, a fonte atual do elemento selecionado no campo **Mostrar configurações de** é realçada. Fontes fixas – que são mais fáceis de alinhar no editor – aparecem em negrito.  
  
  **Size**  
  Listas tamanhos de pontos disponíveis para a fonte realçada. Alterar o tamanho da fonte afeta todos os **Itens de exibição** para a seleção **Mostrar configurações de**.  
  
  **Exibir itens**  
  Lista os itens cuja cor de primeiro plano e a cor da tela de fundo você pode modificar.  
  
> [!NOTE]
>  **Texto sem Formatação** é o item de exibição padrão. Sendo assim, propriedades atribuídas a **PlainText** serão substituídas por propriedades atribuídas a outros itens de exibição. Por exemplo, se você atribuir a cor azul a **PlainText** e a cor verde a **Identificador**, todos os identificadores serão exibidos em verde. Neste exemplo, as propriedades de **Identificador** substituem as propriedades em **PlainText**.  
  
 Alguns dos itens de exibição incluem:  
  
|Item de exibição|Descrição|  
|------------------|-----------------|  
|**Texto sem Formatação**|Texto no editor.|  
|**Texto Selecionado**|Texto incluído na seleção atual quando o editor está em foco.|  
|**Texto Selecionado Inativo**|Texto incluído na seleção atual quando o editor sai de foco.|  
|**Margem de Indicadores**|A margem à esquerda do Editor de Códigos em que os ícones de indicador e ponto de interrupção são exibidos.|  
|**Números de Linha**|Números opcionais que aparecem ao lado de cada linha de código|  
|**Espaço em branco visível**|Espaços, tabulações e indicadores de quebra automática de linha|  
|**Indicador**|Linhas com indicadores. O **Indicador** só ficará visível se a margem de indicadores estiver desabilitada.|  
|**Correspondência de chaves (Realce)**|Realce que normalmente tem formatação em negrito para chaves correspondentes.|  
|**Correspondência de chaves (Retângulo)**|Realce que normalmente é um retângulo cinza na tela de fundo.|  
|**Ponto de Interrupção (Desabilitado)**|Não usado.|  
|**Ponto de Interrupção (Habilitado)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção simples. Essa opção é aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção (Erro)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção em estado de erro. Aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção (Aviso)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção em estado de aviso. Aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Avançado (Desabilitado)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção condicionais desabilitados ou com contagem de ocorrências. Aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Avançado (Habilitado)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção condicionais ou com contagem de ocorrências. Aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Avançado (Erro)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção condicionais ou com contagem de ocorrências que estão em estado de erro. Aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Avançado (Aviso)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção condicionais ou com contagem de ocorrências que estão em estado de aviso. Aplicável somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Mapeado (Desabilitado)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção mapeados desabilitados. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Mapeado (Habilitado)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção mapeados. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Mapeado (Erro)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção mapeados em estado de erro. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Ponto de Interrupção – Mapeado (Aviso)**|Especifica a cor de realce para instruções ou linhas que contêm pontos de interrupção mapeados em estado de aviso. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Palavras-chave de usuário do C/C++**|Uma constante dentro de um arquivo de código específico definido por meio da diretiva `#define`.|  
|**Retorno de Chamada**|Especifica a cor de realce para instruções ou linhas de origem que indicam pontos de retorno de chamada quando o contexto é alternado para um registro de ativação não superior durante a depuração.|  
|**Campo dependente de snippet de código**|Um campo que será atualizado quando o campo editável atual for modificado.|  
|**Campo de Snippet de Código**|Campo editável quando um snippet de código está ativo.|  
|**Texto Recolhível**|Um bloco de texto ou código que pode ser colocado e removido da exibição no Editor de Código.|  
|**Comentário**|Comentários sobre o código.|  
|**Erro do Compilador**|Rabiscos azuis no editor que indicam um erro do compilador.|  
|**Área Sem Alcance de Cobertura**|Código que não foi coberto por um teste de unidade.|  
|**Área Com Alcance de Cobertura Parcial**|Código que foi coberto parcialmente por um teste de unidade.|  
|**Área de Cobertura Alcançada**|Código que foi coberto completamente por um teste de unidade.|  
|**Comentário CSS**|Um comentário em folhas de estilos em cascata. Por exemplo:<br /><br /> /* comentário \*/|  
|**Palavra-chave CSS**|Palavras-chave na folha de estilos em cascata.|  
|**Nome da Propriedade CSS**|O nome de uma propriedade, como Tela de Fundo.|  
|**Valor da Propriedade CSS**|O valor atribuído a uma propriedade, como azul.|  
|**Seletor de CSS**|Uma cadeia de caracteres que identifica a quais elementos a regra correspondente se aplica. Um seletor pode ser um seletor simples, como "H1", ou um seletor contextual, como "H1 B", que consiste em vários seletores de simples.|  
|**Valor da Cadeia de Caracteres da CSS**|Uma cadeia de caracteres em folhas de estilos em cascata.|  
|**Localização Atual na Lista**|Linha atual acessada em uma janela de ferramentas de lista, como a Janela de Saída ou a janela Localizar Resultados.|  
|**Instrução Atual**|Especifica a cor de realce para a linha ou a instrução de origem que indica a posição da etapa atual durante a depuração.|  
|**Dados Alterados do Depurador**|A cor do texto usado para exibir dados alterados dentro das janelas **Registros** e **Memória**.|  
|**Tela de fundo da janela de Definição**|A cor da tela de fundo da Janela de **Definição de Código**.|  
|**Correspondência atual na janela de Definição**|A definição atual na Janela de **Definição de Código**.|  
|**Nome do Arquivo de Desmontagem**|A cor do texto usado para exibir as quebras de nome de arquivo dentro da janela **Desmontagem**.|  
|**Origem de Desmontagem**|A cor do texto usado para exibir as linhas de origem dentro da janela **Desmontagem**.|  
|**Símbolo de Desmontagem**|A cor do texto usado para exibir nomes de símbolos dentro da janela **Desmontagem**.|  
|**Texto de Desmontagem**|A cor do texto usado para exibir dados e códigos de operação dentro da janela **Desmontagem**.|  
|**Código Excluído**|Código que não deve ser compilado, de acordo com uma diretiva de pré-processador condicional como `#if`.|  
|**Identificador**|Identificadores no código, como nomes de classes, nomes de métodos e nomes de variáveis.|  
|**Palavra-chave**|Palavras-chave da linguagem específica que são reservadas. Por exemplo: classe e namespace.|  
|**Endereço de Memória**|A cor do texto usado para exibir a coluna de endereço dentro da janela **Memória**.|  
|**Memória Alterada**|A cor do texto usado para exibir dados alterados dentro da janela **Memória**.|  
|**Dados da Memória**|A cor do texto usado para exibir dados dentro de **memória** janela.|  
|**Memória Ilegível**|A cor do texto usado para exibir áreas de memória ilegível dentro da janela **Memória**.|  
|**Número**|Um número no código que representa um valor numérico real.|  
|**Operador**|Operadores, como +, - e !=.|  
|**Outro Erro**|Outros tipos de erro que não são cobertos por outros rabiscos de erro. Atualmente, inclui edições rudimentares em Editar e Continuar.|  
|**Palavra-chave do Pré-processador**|Palavras-chave usadas pelo pré-processador, como #include.|  
|**Região Somente Leitura**|Código que não pode ser editado. Por exemplo, código exibido na janela Exibição de Definição de Código ou código que não pode ser modificado durante Editar e Continuar.|  
|**Tela de fundo de refatoração**|Cor da tela de fundo da caixa de diálogo **Visualizar Alterações**.|  
|**Campo atual de refatoração**|Cor da tela de fundo do elemento atual a ser refatorado na caixa de diálogo **Visualizar Alterações**.|  
|**Campo dependente de refatoração**|Cor das referências do elemento a ser refatorado na caixa de diálogo **Visualizar Alterações**.|  
|**Dados do Registro**|A cor do texto usado para exibir dados dentro da janela **Registros**.|  
|**NAT do Registro**|A cor do texto usado para exibir dados e objetos não reconhecidos dentro da janela **Registros**.|  
|**Marcação Inteligente**|Usado para indicar a estrutura de tópicos quando marcações inteligentes são invocadas.|  
|**Marcador DML SQL**|Aplica-se ao editor de Transact-SQL. Por padrão, instruções DML neste editor são marcadas com uma caixa delimitadora azul.|  
|**Código Obsoleto**|Código obsoleto que aguarda atualização. Em alguns casos, Editar e Continuar não pode aplicar alterações de código imediatamente, mas os aplicará mais tarde enquanto você continua a depuração. Isso ocorre se você editar uma função que deve chamar a função que está em execução ou se você adicionar mais de 64 bytes de novas variáveis a uma função em espera na pilha de chamadas. Quando isso acontece, o depurador exibe uma caixa de diálogo "Aviso de Código Obsoleto", e o código obsoleto continua sendo executado até que a função em questão termine e seja chamada novamente. Editar e Continuar aplica as alterações de código nesse momento.|  
|**Cadeia de caracteres**|Literais de cadeia de caracteres.|  
|**Cadeia de caracteres (C# @ Textual)**|Literais de cadeia de caracteres em C# que são interpretadas de forma textual. Por exemplo:<br /><br /> @"x"|  
|**Erro de Sintaxe**|Erros de análise.|  
|**Atalho da Lista de Tarefas**|Se um atalho de **Lista de Tarefas** for adicionado a uma linha e a margem de indicadores for desabilitada, a linha será realçada.|  
|**Tracepoint (Desabilitado)**|Não usado.|  
|**Tracepoint (Habilitado)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints simples. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint (Erro)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints em estado de erro. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint (Aviso)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints em estado de aviso. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Avançado (Desabilitado)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints condicionais desabilitados ou com contagem de ocorrências. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Avançado (Habilitado)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints condicionais ou com contagem de ocorrências. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Avançado (Erro)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints condicionais ou com contagem de ocorrências que estão em estado de erro. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Avançado (Aviso)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints condicionais ou com contagem de ocorrências que estão em estado de aviso. Essa opção é aplicável somente se tracepoints no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Mapeado (Desabilitado)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints mapeados desabilitados. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Mapeado (Habilitado)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints mapeados. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Mapeado (Erro)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints mapeados em estado de erro. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Tracepoint – Mapeado (Aviso)**|Especifica a cor de realce para instruções ou linhas que contêm tracepoints mapeados em estado de aviso. Aplicável para a depuração de ASP ou ASP.NET somente se pontos de interrupção no nível da instrução estiverem ativos ou se a opção **Realçar a linha de origem inteira para pontos de interrupção e a declaração atual** for selecionada em [Geral, Depuração, caixa de diálogo Opções](../../debugger/general-debugging-options-dialog-box.md).|  
|**Marca de controle de alterações depois de salvar**|Linhas de código que foram modificadas desde que o arquivo foi aberto, mas são salvas em disco.|  
|**Marca de controle de alterações antes de salvar**|Linhas de código que foram modificadas desde que o arquivo foi aberto, mas não são salvas em disco.|  
|**Tipos de Usuário**|Tipos definidos pelos usuários.|  
|**Tipos de Usuário (Representantes)**|Cor do tipo para delegados.|  
|**Tipos de Usuário (Enums)**|Cor do tipo usada para enums.|  
|**Tipos de Usuário (Interfaces)**|Cor do tipo para interfaces.|  
|**Tipos de Usuário (Tipos de valor)**|Cor do tipo para tipos de valor, como structs em C#.|  
|**Marcador Somente Leitura do Visual Basic**|Um marcador específico do Visual Basic usado para designar EnC, como regiões de exceção, uma definição de método e quadros de chamada que não são folhas.|  
|**Aviso**|Avisos do compilador.|  
|**Caminho das linhas de aviso**|Usado para linhas de aviso de Análise Estática.|  
|**Atributo XML**|Nomes de atributo.|  
|**Aspas do Atributo XML**|Os caracteres de aspas para atributos XML.|  
|**Valor do Atributo XML**|Conteúdo de atributos XML.|  
|**Seção Cdata XML**|Conteúdo de \<![CDATA[…]]>.|  
|**Comentário XML**|O conteúdo de \<!-- -->.|  
|**Delimitador XML**|Delimitadores da sintaxe XML, incluindo <, <?, <!, \<!--, -->, ?\>, \<![, ]]> e [, ].|  
|**Atributo de Documento XML**|O valor de um atributo de documentação XML, como \<param name="I">, em que o "I" é colorido.|  
|**Comentário da documentação XML**|Os comentários incluídos nos comentários de documentação XML.|  
|**Marcação de Documento XML**|As marcações em comentários de documentos XML, como<br /><br /> /// \<summary>.|  
|**Palavra-Chave XML**|Palavras-chave DTD, como CDATA, IDREF e NDATA.|  
|**Nome XML**|Nomes de elementos e o nome de destino das Instruções de processamento.|  
|**Instrução de Processamento XML**|Conteúdo das Instruções de processamento, sem incluir o nome do destino.|  
|**Texto XML**|Conteúdo do elemento de texto sem formatação.|  
|**Palavra-Chave XSLT**|Nomes de elementos XSLT.|  
  
 **Primeiro plano do item**  
 Lista as cores disponíveis que você pode escolher para o primeiro plano do item selecionado em **Exibir itens**. Como alguns itens estão relacionados e, portanto, devem manter um esquema de exibição consistente, alterar a cor de primeiro plano do texto também altera os padrões para elementos como Erro do Compilador, Palavra-Chave ou Operador.  
  
 Itens **Automáticos** podem herdar a cor de primeiro plano de outros itens de exibição, como **Texto sem Formatação**. Usando essa opção, quando você altera a cor de um item de exibição herdado, a cor dos itens de exibição relacionados também é alterada automaticamente. Por exemplo, se você selecionar o valor **Automático** para **Erro do Compilador** e posteriormente alterar a cor de **Texto sem Formatação** para vermelho, **Erro do Compilador** herdará automaticamente a cor vermelha.  
  
 **Padrão** A cor que aparece para o item na primeira vez que você iniciar o Visual Studio. Clicar no botão **Usar Padrões** redefine para essa cor.  
  
 **Personalizado**  
 Exibe a caixa de diálogo Cor para permitir que você defina uma cor personalizada para o item selecionado na lista de itens de Exibição.  
  
> [!NOTE]
>  Sua capacidade de definir cores personalizadas pode ser limitada pelas configurações de cor de exibição do computador. Por exemplo, se o computador estiver configurado para exibir 256 cores e você selecionar uma cor personalizada na caixa de diálogo **Cor**, o IDE assume como padrão a **Cor básica** mais próxima disponível e exibe a cor preta na caixa de visualização **Cor**.  
  
 **Tela de fundo do item**  
 Fornece uma paleta de cores na qual você pode escolher uma cor da tela de fundo para o item selecionado em **Exibir itens**. Como alguns itens estão relacionados e, portanto, devem manter um esquema de exibição consistente, alterar a cor da tela de fundo do texto também altera os padrões para elementos como Erro do Compilador, Palavra-Chave ou Operador.  
  
 Itens **Automáticos** podem herdar a cor da tela de fundo de outros itens de exibição, como **Texto sem Formatação**. Usando essa opção, quando você altera a cor de um item de exibição herdado, a cor dos itens de exibição relacionados também é alterada automaticamente. Por exemplo, se você selecionar o valor **Automático** para **Erro do Compilador** e posteriormente alterar a cor de **Texto sem Formatação** para vermelho, **Erro do Compilador** herdará automaticamente a cor vermelha.  
  
 **Padrão** A cor que aparece para o item na primeira vez que você iniciar o Visual Studio. Clicar no botão **Usar Padrões** redefine para essa cor.  
  
 **Personalizado**  
 Exibe a caixa de diálogo Cor para permitir que você defina uma cor personalizada para o item selecionado na lista de itens de Exibição.  
  
 **Negrito**  
 Selecione esta opção para exibir o texto de **Itens de exibição** selecionados em negrito. É mais fácil identificar texto em negrito no editor.  
  
 **Amostra**  
 Exibe uma amostra do esquema de cores, tamanho e estilo da fonte de **Mostrar configurações de** e **Itens de exibição** selecionados. É possível usar essa caixa para visualizar os resultados quando você testa diferentes opções de formatação.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo Opções do Ambiente](../../ide/reference/environment-options-dialog-box.md)   
 [Caixa de diálogo Opções](../../ide/reference/options-dialog-box-visual-studio.md)   
 [Como alterar fontes e cores](../../ide/how-to-change-fonts-and-colors-in-visual-studio.md)



