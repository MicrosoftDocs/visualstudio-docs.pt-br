---
title: Padrões de aplicativo para o Visual Studio | Microsoft Docs
description: Saiba mais sobre a diferença entre janelas de documentos, janelas de ferramentas e caixas de diálogo sem janela restrita, incluindo padrões de uso de janelas para novos recursos para o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: 8ed68602-4e28-46fe-b39f-f41979b308a2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7b19d60294431a08fa26f11bf58606893f392cd1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060231"
---
# <a name="application-patterns-for-visual-studio"></a>Padrões de aplicativo para Visual Studio
## <a name="window-interactions"></a><a name="BKMK_WindowInteractions"></a> Interações com a janela

### <a name="overview"></a>Visão geral
Os dois tipos de janela principais usados no Visual Studio são editores de documentos e janelas de ferramentas. Raras, mas possíveis, são caixas de diálogo sem janela restrita. Embora todos estejam sem janela restrita no Shell, seus padrões são fundamentalmente diferentes. Esta seção aborda a diferença entre janelas de documentos, janelas de ferramentas e caixas de diálogo sem janela restrita. Os padrões de caixa de diálogo modais são abordados em [caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs).

### <a name="comparing-window-usage-patterns"></a>Comparando padrões de uso da janela
As **janelas de documentos** quase sempre são exibidas no documento. Isso dá ao editor de documentos um "estágio central" para organizar as janelas de ferramentas complementares.

Uma **janela de ferramenta** é exibida com mais frequência como uma janela separada e menor recolhida em relação à borda do IDE. Isso pode ser visível, oculto ou oculto automaticamente. No entanto, às vezes, as janelas de ferramentas são apresentadas dentro do documento, desmarcando a propriedade **janela/encaixe** na janela. Isso resulta em mais espaço real, mas também em uma decisão de design comum: ao tentar se integrar ao Visual Studio, você deve decidir se seu recurso deve exibir uma janela de ferramentas ou uma janela de documento.

**Caixas de diálogo sem janela restrita** são desencorajadas no Visual Studio. A maioria das caixas de diálogo sem janela restrita são, por definição, janelas de ferramentas flutuantes e devem ser implementadas dessa maneira. Caixas de diálogo sem janela restrita são permitidas nos casos em que o tamanho de uma janela de ferramentas normal encaixada no lado do Shell estaria muito limitado. Eles também são permitidos em casos em que o usuário provavelmente moveria a caixa de diálogo para um monitor secundário.

Pense atentamente sobre qual tipo de contêiner você precisa. As considerações comuns de padrão de uso para o design de interface do usuário estão na tabela a seguir.

||Janela do documento|Janela de ferramentas|Caixa de diálogo sem janela restrita|
|-|---------------------|-----------------|---------------------|
| **Posição** | Sempre posicionado dentro do documento bem e não se encaixa em todas as bordas do IDE. Pode ser "retirada" para que ele flutue separadamente do Shell principal. | Em geral, é encaixado em volta das bordas do IDE, mas pode ser personalizado para ser flutuante, ocultado automaticamente (não fixado) ou encaixado dentro do compartimento do documento.|Janela flutuante grande separada do IDE. |
| **Confirmar modelo** | *Confirmação atrasada*<br /><br /> Para salvar os dados em um documento, o usuário deve emitir o comando **arquivo &gt; salvar**, **salvar como** ou **salvar todos** . Uma janela de documento tem o conceito dos dados em que ele está sendo "sujos", em seguida, confirmado em um dos comandos Save. Ao fechar uma janela de documento, todo o conteúdo é salvo em disco ou perdido. | *Confirmação imediata*<br /><br /> Não há nenhum modelo de salvamento. Para janelas de ferramenta de inspetor que auxiliam na edição de um arquivo, o arquivo deve ser aberto no editor ou designer ativo, e o editor ou Designer possui a gravação. | *Confirmação atrasada ou imediata*<br /><br /> Geralmente, uma caixa de diálogo com janela restrita grande requer uma ação para confirmar as alterações e permite uma operação "Cancelar", que reverte as alterações feitas na sessão de diálogo.  Isso diferencia uma caixa de diálogo sem-modo de uma janela de ferramentas no que as janelas de ferramentas sempre têm um modelo de confirmação imediata. |
| **Visibilidade** | *Abrir/criar (arquivo) e fechar*<br /><br /> Abrir uma janela de documentos é feito por meio da abertura de um documento existente ou do uso de um modelo para criar um novo documento. Não há nenhum comando "Open \<specific editor> ". | *Ocultar e mostrar*<br /><br /> Janelas de ferramentas de instância única podem ser ocultadas ou mostradas. O conteúdo e os Estados dentro da janela de ferramentas persistem se estão na exibição ou ocultos. As janelas de ferramentas de várias instâncias podem ser fechadas e ocultas. Quando uma janela de ferramenta de várias instâncias é fechada, o conteúdo e o estado dentro da janela de ferramentas são descartados. | *Iniciado a partir de um comando*<br /><br /> As caixas de diálogo são iniciadas de um comando baseado em tarefa. |
| **Instâncias** | *Várias instâncias*<br /><br /> Vários editores podem ser abertos ao mesmo tempo e editar arquivos diferentes, enquanto alguns editores também permitem que o mesmo arquivo seja aberto em mais de um editor (usando o comando **janela &gt; nova janela** ).<br /><br /> Um único editor pode estar editando um ou vários arquivos ao mesmo tempo (Designer de projeto). | *Instância única ou múltipla*<br /><br /> O conteúdo é alterado para refletir o contexto (como no navegador de propriedades) ou o foco/contexto de push para outras janelas (Lista de Tarefas Gerenciador de Soluções).<br /><br /> As janelas de ferramentas de instância única e várias instâncias devem ser associadas à janela do documento ativo, a menos que haja um motivo convincente para não. | *Instância única* |
| **Exemplos** | **Editores de texto**, como o editor de código<br /><br /> **Superfícies de design**, como um designer de formulário ou uma superfície de modelagem<br /><br /> **Layouts de controle semelhantes a caixas de diálogo**, como o designer de manifesto | O **Gerenciador de soluções** fornece uma solução e projetos contidos na solução<br /><br /> O **Gerenciador de servidores** fornece uma exibição hierárquica de servidores e conexões de dados que o usuário escolhe abrir na janela. Abrir um objeto da hierarquia de banco de dados, como uma consulta, abre uma janela de documento e permite que o usuário edite a consulta.<br /><br /> O **navegador de propriedades** exibe as propriedades do objeto selecionado em uma janela de documento ou em outra janela de ferramenta. As propriedades são apresentadas em uma exibição de grade hierárquica ou em controles complexos semelhantes a caixas de diálogo e permitem que o usuário defina os valores para essas propriedades. | |

## <a name="tool-windows"></a><a name="BKMK_ToolWindows"></a> Janelas de ferramentas

### <a name="overview"></a>Visão geral
As janelas de ferramentas dão suporte ao trabalho do usuário que ocorre em janelas de documentos. Eles podem ser usados para exibir uma hierarquia que representa um objeto raiz fundamental que o Visual Studio fornece e pode manipular.

Ao considerar uma nova janela de ferramentas no IDE, os autores devem:

- Use as janelas de ferramentas existentes apropriadas para a tarefa e não crie novas com funcionalidades semelhantes. As novas janelas de ferramentas só devem ser criadas se oferecerem uma "ferramenta" significativamente diferente ou uma funcionalidade que não pode ser integrada em uma janela semelhante ou transformando uma janela existente em um hub dinâmico.

- Use uma barra de comandos padrão, se necessário, na parte superior da janela de ferramentas.

- Seja consistente com padrões já presentes em outras janelas de ferramentas para controlar a apresentação e a navegação por teclado.

- Seja consistente com a apresentação de controle em outras janelas de ferramentas.

- Torne as janelas de ferramentas específicas do documento visíveis automaticamente quando possível, para que elas apareçam somente quando o documento pai for ativado.

- Verifique se o conteúdo da janela é navegável pelo teclado (teclas de seta de suporte).

#### <a name="tool-window-states"></a>Estados da janela de ferramentas
As janelas de ferramentas do Visual Studio têm Estados diferentes, algumas das quais são ativadas pelo usuário (como o recurso de ocultar automaticamente). Outros Estados, como visível automaticamente, permitem que janelas de ferramentas apareçam no contexto correto e se ocultem quando não forem necessárias. Há cinco Estados da janela de ferramentas no total.

- As janelas de ferramentas **encaixadas/fixas** podem ser anexadas a qualquer um dos quatro lados da área do documento. O ícone de pino aparece na barra de título da janela de ferramentas. A janela de ferramentas pode ser encaixada horizontal ou verticalmente ao longo da borda do Shell e de outras janelas de ferramentas, e também pode ser vinculada por guias.

- Janelas **de ferramentas ocultas automaticamente** são desafixadas. A janela pode deslizar de visão, deixando uma tabulação (com o nome da janela de ferramentas e seu ícone) na borda da área do documento. A janela de ferramentas desliza quando um usuário passa o mouse sobre a guia.

- As janelas **de ferramentas visíveis** automaticamente aparecem quando outra parte da interface do usuário, como um editor, é iniciada ou ganha foco.

- Janelas de ferramentas **flutuantes** focalizam fora do IDE. Isso é útil para configurações de vários monitores.

- As janelas de ferramentas de **documentos com guias** também podem ser encaixadas no documento. Isso é útil para janelas de ferramentas grandes, como o pesquisador de objetos, que precisa de mais espaço livre do que o encaixe nas bordas do quadro permite.

![Estados da janela de ferramentas no Visual Studio](../../extensibility/ux-guidelines/media/0702-01_toolwindowstates.png "0702-01_ToolWindowStates")<br />Estados da janela de ferramentas no Visual Studio

#### <a name="single-instance-and-multi-instance"></a>Instância única e várias instâncias
As janelas de ferramentas são de instância única ou várias instâncias. Algumas janelas de ferramentas de instância única podem ser associadas à janela do documento ativo, enquanto as janelas de ferramentas de várias instâncias podem não ser. As janelas de ferramentas de várias instâncias respondem ao comando **janela &gt; nova janela** criando uma nova instância da janela. A imagem a seguir ilustra uma janela de ferramentas que habilita o comando nova janela quando uma instância da janela está ativa:

![Janela de ferramentas habilitando o comando ' nova janela ' quando uma instância da janela estiver ativa](../../extensibility/ux-guidelines/media/0702-02_toolwindowenablingcommand.png "0702-02_ToolWindowEnablingCommand")<br />Janela de ferramentas habilitando o comando ' nova janela ' quando uma instância da janela estiver ativa

As janelas de ferramentas de instância única podem ser ocultadas ou mostradas, enquanto as janelas de ferramentas de várias instâncias podem ser fechadas e ocultas. Todas as janelas de ferramentas podem ser encaixadas, vinculadas à guia, flutuantes ou definidas como uma janela filho de MDI (interface de Multiple-Document) (semelhante a uma janela de documento). Todas as janelas de ferramentas devem responder aos comandos de gerenciamento de janela apropriados no menu janela:

![Comandos de gerenciamento de janelas no menu da janela do Visual Studio](../../extensibility/ux-guidelines/media/0702-03_windowmanagementcontrols.png "0702-03_WindowManagementControls")<br />Comandos de gerenciamento de janelas no menu da janela do Visual Studio

#### <a name="document-specific-tool-windows"></a>Janelas de ferramentas específicas de documento
Algumas janelas de ferramentas são projetadas para serem alteradas com base em um determinado tipo de documento. Essas janelas são continuamente atualizadas para refletir a funcionalidade aplicável à janela do documento ativo no IDE.

Exemplos de janelas de ferramentas cujo conteúdo é alterado para refletir o editor selecionado são a caixa de ferramentas e a estrutura de tópicos do documento. Essas janelas mostram uma marca d' água quando um editor tem foco que não oferece contexto para a janela.

#### <a name="navigable-list-tool-windows"></a>Janelas de ferramentas da lista navegável
Algumas janelas de ferramentas exibem uma lista de itens navegáveis com os quais o usuário pode interagir. Nesse tipo de janela, sempre deve haver comentários para o item atual na lista, mesmo que a janela esteja inativa. A lista deve responder aos comandos **GoToNextLocation** e **GoToPrevLocation** também alterando o item atualmente selecionado na janela

Exemplos de janelas de ferramenta de lista navegável são o Gerenciador de Soluções e a janela Localizar resultados.

### <a name="tool-window-types"></a>Tipos de janela de ferramentas

#### <a name="common-tool-windows-and-their-functions"></a>Janelas de ferramentas comuns e suas funções

**Janelas de ferramentas hierárquicas**

| Janela de ferramentas | Função |
| --- | --- |
| Gerenciador de Soluções | Uma árvore hierárquica que exibe uma lista de documentos contidos em projetos, arquivos diversos e itens de solução. A exibição dos itens dentro de projetos é definida pelo pacote que possui o tipo de projeto (por exemplo, tipos de modo misto ou baseado em referência). |
| Exibição de Classe | Uma árvore hierárquica das classes e de vários elementos no conjunto de trabalho de documentos, independentemente dos próprios arquivos. |
| Gerenciador de Servidores | Uma árvore hierárquica que exibe todos os servidores e conexões de dados na solução. |
| Estrutura de Tópicos do Documento | A estrutura hierárquica do documento ativo. |

**Janelas de ferramentas de grade**

| Janela de ferramentas | Função |
| --- | --- |
| Propriedades | Uma grade que exibe uma lista de propriedades para o objeto selecionado, juntamente com seletores de valor para editar essas propriedades. |
| Lista de Tarefas | Uma grade que permite ao usuário criar/editar/excluir tarefas e comentários. |

**Janelas de ferramentas de conteúdo**

| Janela de ferramentas | Função |
| --- | --- |
| Help | Uma janela que permite aos usuários acessar vários métodos de obter ajuda, de "como faço para?" vídeos para fóruns do MSDN. |
| Ajuda dinâmica | Uma janela de ferramentas que exibe links para tópicos da ajuda aplicáveis à seleção atual. |
| Pesquisador de Objetos | Um conjunto de quadros de duas colunas com uma lista de componentes de objetos hierárquicos no painel esquerdo e as propriedades e os métodos do objeto na coluna à direita. |

**Janelas de ferramentas da caixa de diálogo**

| Janela de ferramentas | Função |
| --- | --- |
| Localizar | Uma caixa de diálogo que permite ao usuário localizar ou localizar e substituir em vários arquivos dentro da solução. |
| Localização Avançada | Uma caixa de diálogo que permite ao usuário localizar ou localizar e substituir em vários arquivos dentro da solução. |

**Outras janelas de ferramentas**

::: moniker range="vs-2017"

| Janela de ferramentas | Função |
| --- | --- |
| Caixa de Ferramentas | A janela de ferramentas usada para armazenar elementos que serão descartados em superfícies de design, fornecendo uma fonte de arrasto consistente para todos os designers. |
| Start Page | O portal do usuário para o Visual Studio, com acesso a feeds de notícias para desenvolvedores, ajuda do Visual Studio e projetos recentes. Os usuários também podem criar páginas iniciais personalizadas copiando o arquivo StartPage. XAML do diretório "Common7\IDE\StartPages \" Visual Studio Program Files para a pasta StartPages no diretório documentos do Visual Studio e editando o XAML manualmente ou abrindo-o no Visual Studio ou em outro editor de código. |

::: moniker-end

::: moniker range=">=vs-2019"

| Janela de ferramentas | Função |
| --- | --- |
| Caixa de Ferramentas | A janela de ferramentas usada para armazenar elementos que serão descartados em superfícies de design, fornecendo uma fonte de arrasto consistente para todos os designers. |

::: moniker-end

**Janelas de ferramentas do depurador**

| Janela de ferramentas | Função |
| --- | --- |
| Autos ||
| Imediata ||
| Saída | A janela de saída pode ser usada sempre que você tiver eventos de texto ou status para declarar. |
| Memória ||
| Pontos de interrupção ||
| Executando ||
| Documentos ||
| Pilha de chamadas ||
| Locais ||
| Relógios ||
| Desmontagem ||
| Registros ||
| Threads ||

## <a name="document-editor-conventions"></a><a name="BKMK_DocumentEditorConventions"></a> Convenções do editor de documento

### <a name="document-interactions"></a>Interações com documentos
O "documento bem" é o maior espaço no IDE e é onde o usuário geralmente se concentrou em sua atenção para concluir suas tarefas, assistidas por janelas de ferramentas complementares. Os editores de documento representam as unidades fundamentais de trabalho que o usuário abre e salva no Visual Studio. Eles retêm uma forte noção de seleção vinculada a Gerenciador de Soluções ou outras janelas de hierarquia ativas. O usuário deve ser capaz de apontar para uma dessas janelas de hierarquia e saber onde o documento está contido e sua relação com a solução, o projeto ou outro objeto raiz fornecido por um pacote do Visual Studio.

A edição de documentos requer uma experiência de usuário consistente. Para permitir que o usuário se concentre na tarefa em vez de em gerenciamento de janelas e localizando comandos, selecione uma estratégia de exibição de documento que melhor atenda às tarefas do usuário para editar esse tipo de documento.

#### <a name="common-interactions-for-the-document-well"></a>Bem como as interações comuns para o documento

- Mantenha um modelo de interação consistente nas experiências comuns de **arquivo novo** e de arquivo **aberto** .

- Atualize a funcionalidade relacionada em janelas e menus relacionados quando a janela do documento for aberta.

- Os comandos de menu são adequadamente integrados a menus comuns, como menus de **edição**, **formatação** e **exibição** . Se uma quantidade significativa de comandos especializados estiver disponível, um novo menu poderá ser criado. Esse novo menu deve ser visível somente quando o documento tiver foco.

- Uma barra de ferramentas incorporada pode ser colocada na parte superior do editor. É preferível ter uma barra de ferramentas separada que aparece fora do editor.

- Sempre mantenha uma seleção na Gerenciador de Soluções ou na janela de hierarquia ativa semelhante.

- Clicar duas vezes em um documento no Gerenciador de Soluções deve executar a mesma ação que **abrir**.

- Se mais de um editor puder ser usado em um tipo de documento, o usuário deverá ser capaz de substituir ou redefinir a ação padrão em um determinado tipo de documento usando a caixa de diálogo **abrir com** clicando com o botão direito do mouse no arquivo e selecionando **abrir com** no menu de atalho.

- Não crie um assistente em um documento bem.

### <a name="user-expectations-for-specific-document-types"></a>Expectativas do usuário para tipos de documento específicos
Há vários tipos básicos diferentes de editores de documento e cada um tem um conjunto de interações que são consistentes com outras pessoas do mesmo tipo.

- **Editor baseado em texto:** editor de código, arquivos de log

- **Superfície de design:** WPF Forms Designer, Windows Forms

- **Editor de estilo de caixa de diálogo:** Designer de manifesto, propriedades do projeto

- **Designer de modelos:** designer de fluxo de trabalho, codemap, diagrama de arquitetura, progressão

Há também vários tipos que não são de editor que usam bem o documento. Embora eles não editem documentos, eles precisam seguir as interações padrão para janelas de documentos.

- **Relatórios:** Relatório do IntelliTrace, relatório do Hyper-V, relatório do criador de perfil

- **Painel:** Hub de diagnóstico

#### <a name="text-based-editors"></a>Editores baseados em texto

- O documento participa do modelo da guia de visualização, permitindo a visualização do documento sem abri-lo.

- A estrutura do documento pode ser representada em uma janela de ferramenta complementar, como uma estrutura de tópicos do documento.

- O IntelliSense (se apropriado) se comportará de forma consistente com outros editores de código.

- Pop-ups ou interface do usuário assistencial seguem estilos e padrões semelhantes para a interface do usuário semelhante existente, como CodeLens.

- As mensagens referentes ao status do documento serão apresentadas em um controle de barra de lista na parte superior do documento ou na barra de status.

- O usuário deve ser capaz de personalizar a aparência de fontes e cores usando uma página **ferramentas > opções** , a página fontes e cores compartilhadas ou uma específica para o editor.

#### <a name="design-surfaces"></a>Superfícies de design

- Um designer vazio deve ter uma marca-d ' água na superfície indicando como começar.

- Os mecanismos de alternância de exibição seguirão padrões existentes, como clique duplo para abrir um editor de código, ou guias na janela do documento, permitindo a interação com ambos os painéis.

- A adição de elementos à superfície de design deve ser feita por meio da caixa de ferramentas, a menos que uma janela de ferramentas altamente específica seja necessária.

- Os itens na superfície seguirão um modelo de seleção consistente.

- As barras de ferramentas inseridas contêm apenas comandos específicos do documento, não comandos comuns, como **salvar**.

#### <a name="dialog-style-editors"></a>Editores de estilo de caixa de diálogo

- O layout de controle deve seguir as convenções normais de layout de diálogo.

- As guias no editor não devem corresponder à aparência das guias de documento, elas devem corresponder a um dos dois estilos de guia interiores permitidos.

- Os usuários devem ser capazes de interagir com os controles usando somente o teclado; Ativando o editor e tabulando por meio de controles ou usando mnemônicos padrão.

- O designer deve usar o modelo de salvamento comum. Nenhum botão de gravação ou confirmação geral deve ser colocado na superfície, embora outros botões possam ser apropriados.

#### <a name="model-designers"></a>Designers de modelos

- Um designer vazio deve ter uma marca-d ' água na superfície indicando como começar.

- A adição de elementos à superfície de design deve ser feita por meio da caixa de ferramentas.

- Os itens na superfície seguirão um modelo de seleção consistente.

- As barras de ferramentas inseridas contêm apenas comandos específicos do documento, não comandos comuns, como **salvar**.

- Uma legenda pode aparecer na superfície, indica ou uma marca d' água.

- O usuário deve ser capaz de personalizar a aparência das fontes/cores usando uma página **ferramentas > opções** , a página fontes e cores compartilhadas ou uma específica para o editor.

#### <a name="reports"></a>Relatórios

- Normalmente, os relatórios são apenas informações e não participam do modelo de salvamento. No entanto, eles podem incluir a interação, como links para outras informações ou seções relevantes que se expandem e recolhem.

- A maioria dos comandos na superfície deve ser hiperlinks, não botões.

- O layout deve incluir um cabeçalho e seguir as diretrizes de layout de relatório padrão.

#### <a name="dashboards"></a>Painéis

- Os painéis não têm um modelo de interação em si, mas servem como meio de oferecer uma variedade de outras ferramentas.

- Eles não participam do modelo de salvamento.

- Os usuários devem ser capazes de interagir com os controles usando somente o teclado, ativando o editor e tabulando por meio de controles ou usando mnemônicos padrão.

## <a name="dialogs"></a><a name="BKMK_Dialogs"></a> Caixas

### <a name="introduction"></a>Introdução
As caixas de diálogo no Visual Studio normalmente devem suportar uma unidade discreta do trabalho do usuário e, em seguida, ser ignoradas.

Se você determinou que precisa de uma caixa de diálogo, tem três opções, em ordem de preferência:

1. Integre seus recursos em uma das caixas de diálogo compartilhadas no Visual Studio.

2. Crie sua própria caixa de diálogo usando um padrão encontrado em uma caixa de diálogo semelhante existente.

3. Crie uma nova caixa de diálogo, seguindo as diretrizes de interação e layout.

Esta seção descreve como escolher o padrão de caixa de diálogo correto dentro dos fluxos de trabalho do Visual Studio e as convenções comuns para o design de diálogo.

### <a name="themes"></a>Temas
As caixas de diálogo no Visual Studio seguem um dos dois estilos básicos:

#### <a name="standard-unthemed"></a>Padrão (não-tem)
A maioria das caixas de diálogo são as caixas de diálogo de utilitário padrão e não devem ser destinadas. Não remodeloe controles comuns ou tente criar botões ou controles "modernos" estilizados. Os controles e a aparência do Chrome seguem as [diretrizes de interação padrão do Windows Desktop para caixas de diálogo](/windows/desktop/uxguide/win-dialog-box).

#### <a name="themed"></a>Com tema
Caixas de diálogo de "assinatura" especiais podem estar com tema. As caixas de diálogo com tema têm uma aparência distinta, que também tem alguns padrões de interação especiais associados ao estilo. Tema sua caixa de diálogo somente se atender a estes requisitos:

- A caixa de diálogo é uma experiência comum que será vista e usada com frequência ou por muitos usuários (por exemplo, a caixa de diálogo **novo projeto** .

- A caixa de diálogo contém elementos proeminentes da marca do produto (por exemplo, a caixa de diálogo **configurações da conta** ).

- A caixa de diálogo aparece como parte integral de um fluxo maior que inclui outras caixas de diálogo (por exemplo, a caixa de diálogo **Adicionar serviço conectado** ).

- A caixa de diálogo é uma parte importante de uma experiência que exerce uma função estratégica na promoção ou diferenciação de uma versão do produto.

Ao criar uma caixa de diálogo com tema, use as cores de ambiente apropriadas e siga os padrões corretos de layout e interação. (Consulte [layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).)

### <a name="dialog-design"></a>Design da caixa de diálogo
As caixas de diálogo bem projetadas levam os seguintes elementos em consideração:

- A tarefa do usuário com suporte

- O estilo, a linguagem e a terminologia do texto da caixa de diálogo

- Opções de controle e convenções de interface do usuário

- Especificação de layout visual e alinhamento de controle

- Acesso pelo teclado

#### <a name="content-organization"></a>Organização de conteúdo
Considere as diferenças entre esses tipos básicos de caixas de diálogo:

- [Caixas de diálogo simples](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_SimpleDialogs) apresentam controles em uma única janela modal. A apresentação pode incluir variações de padrões de controle complexos, incluindo um seletor de campo ou uma barra de ícones.

- As [caixas de diálogo em camadas](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_LayeredDialogs) são usadas para aproveitar ao máximo o espaço da tela quando uma única parte da interface do usuário é composta por vários grupos de controles. Os agrupamentos da caixa de diálogo são "em camadas" por meio de controles de guia, controles de lista de navegação ou botões para que o usuário possa escolher qual Agrupamento verá em um determinado momento.

- Os [assistentes](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Wizards) são úteis para direcionar o usuário por meio de uma sequência lógica de etapas para a conclusão de uma tarefa. Uma série de opções são oferecidas em painéis seqüenciais, às vezes apresentando fluxos de trabalho diferentes ("branches") dependentes de uma escolha feita no painel anterior.

#### <a name="simple-dialogs"></a><a name="BKMK_SimpleDialogs"></a> Caixas de diálogo simples
Uma caixa de diálogo simples é uma apresentação de controles em uma única janela modal. Essa apresentação pode incluir variações de padrões de controle complexos, como um seletor de campo. Para caixas de diálogo simples, siga o layout geral padrão, bem como qualquer layout específico necessário para agrupamentos de controle complexos.

![>criar uma chave de nome forte é um exemplo de uma caixa de diálogo simples no Visual Studio.](../../extensibility/ux-guidelines/media/0704-01_createstrongnamekey.png "0704-01_CreateStrongNameKey")<br />Criar chave de nome forte é um exemplo de uma caixa de diálogo simples no Visual Studio.

#### <a name="layered-dialogs"></a><a name="BKMK_LayeredDialogs"></a> Caixas de diálogo em camadas
As caixas de diálogo em camadas incluem guias, painéis e árvores incorporadas. Eles são usados para maximizar o espaço real quando há vários grupos de controles oferecidos em uma única parte da interface do usuário. Os agrupamentos são dispostos em camadas para que o usuário possa escolher qual Agrupamento verá a qualquer momento.

No caso mais direto, o mecanismo para alternar entre agrupamentos é um controle guia. Há várias alternativas disponíveis. Consulte priorização e disposição em camadas para saber como escolher o estilo mais apropriado.

A caixa de diálogo **&gt; Opções de ferramentas** é um exemplo de uma caixa de diálogo em camadas usando uma árvore incorporada:

![Ferramentas > opções é um exemplo de uma caixa de diálogo em camadas no Visual Studio.](../../extensibility/ux-guidelines/media/0704-02_toolsoptions.png "0704-02_ToolsOptions")<br />Ferramentas > opções é um exemplo de uma caixa de diálogo em camadas no Visual Studio.

#### <a name="wizards"></a><a name="BKMK_Wizards"></a> Assistentes
Os assistentes são úteis para direcionar o usuário por meio de uma sequência lógica de etapas na conclusão de uma tarefa. Uma série de opções são oferecidas em painéis seqüenciais, e o usuário deve continuar em cada etapa antes de prosseguir para a próxima. Quando há padrões suficientes disponíveis, o botão **concluir** é habilitado.

 Os assistentes modais são usados para tarefas que:

- Conter ramificação, em que caminhos diferentes são oferecidos dependendo das opções do usuário

- Conter dependências entre etapas, em que as etapas subsequentes dependem da entrada do usuário das etapas anteriores

- São suficientemente complexos que a interface do usuário deve ser usada para explicar as opções oferecidas e os possíveis resultados em cada etapa

- São transacionais, exigindo que um conjunto de etapas seja concluído em sua totalidade antes que qualquer alteração seja confirmada

### <a name="common-conventions"></a>Convenções comuns
Para obter o design e a funcionalidade ideais com suas caixas de diálogo, siga essas convenções no tamanho da caixa de diálogo, posição, padrões, configuração de controle e alinhamento, texto da interface do usuário, barras de título, botões de controle e chaves de acesso.

Para obter diretrizes específicas de layout, consulte [layout para Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).

#### <a name="size"></a>Tamanho
As caixas de diálogo devem caber em uma resolução de tela mínima de 1024x768 e o tamanho inicial da caixa de diálogo não deve exceder 900x700 pixels. As caixas de diálogo podem ser redimensionáveis, mas não é um requisito.

Há duas recomendações para caixas de diálogo redimensionáveis:

1. Esse tamanho mínimo é definido para a caixa de diálogo que otimizará o conjunto de controle sem recorte e ajustará para acomodar o crescimento de localização razoável.

2. Que o tamanho escalado pelo usuário persiste da sessão para a sessão. Por exemplo, se o usuário dimensionar uma caixa de diálogo para 150%, uma inicialização subsequente da caixa de diálogo será exibida às 150%.

#### <a name="position"></a>Posição
As caixas de diálogo devem aparecer centralizadas no IDE na primeira inicialização. A última posição de caixas de diálogo não redimensionáveis não precisa ser persistente, portanto, elas aparecerão centralizadas em inicializações subsequentes.

Para caixas de diálogo redimensionáveis, o tamanho deve persistir em inicializações subsequentes. Para caixas de diálogo modais redimensionáveis, a posição não precisa ser persistente. Exibi-los centralizados no IDE impede a possibilidade da caixa de diálogo aparecer em uma posição imprevisível ou inutilizável quando a configuração de exibição do usuário é alterada.

Para caixas de diálogo sem janela restrita que podem ser reposicionadas, a posição do usuário deve ser mantida nas inicializações subsequentes, pois a caixa de diálogo pode ser usada com frequência como parte integral de um fluxo de trabalho maior.

Quando as caixas de diálogo devem gerar outras caixas de diálogo, a caixa de diálogo superior deve ser colocada em cascata à direita e abaixo do pai para que seja óbvia para o usuário que navegou para um novo local.

#### <a name="modality"></a>Modalidade
Ser modal significa que os usuários precisam concluir ou cancelar a caixa de diálogo antes de continuar. Como as caixas de diálogo modais impedem que o usuário interaja com outras partes do ambiente, o fluxo de tarefas do recurso deve usá-las da forma mais moderada possível. Quando uma operação modal é necessária, o Visual Studio tem várias caixas de diálogo compartilhadas nas quais você pode integrar seus recursos. Se você precisar criar uma nova caixa de diálogo, siga o padrão de interação de uma caixa de diálogo existente com funcionalidade semelhante.

Quando os usuários precisam executar duas atividades ao mesmo tempo, como **Localizar** e **substituir** durante a gravação de um novo código, a caixa de diálogo deve ser sem janela restrita para que o usuário possa alternar facilmente entre elas. O Visual Studio geralmente usa janelas de ferramentas para esse tipo de tarefa vinculada de suporte ao editor.

#### <a name="control-configuration"></a>Configuração de controle
Seja consistente com as configurações de controle existentes que realizam a mesma coisa no Visual Studio.

#### <a name="title-bars"></a>Barras de título

- O texto na barra de título deve refletir o nome do comando que o iniciou.

- Nenhum ícone deve ser usado nas barras de título da caixa de diálogo. Nos casos em que o sistema requer um, use o logotipo do Visual Studio.

- As caixas de diálogo não devem ter os botões minimizar ou maximizar.

- Os botões de ajuda na barra de título foram preteridos. Não os adicione a novas caixas de diálogo. Quando eles existem, eles devem iniciar um tópico de ajuda conceitualmente relevante para a tarefa.

  ![Especificações de diretrizes para barras de título em caixas de diálogo do Visual Studio](../../extensibility/ux-guidelines/media/0704-03_titlebarspecs.png "0704-03_TitleBarSpecs")<br />Especificações de diretrizes para barras de título em caixas de diálogo do Visual Studio

#### <a name="control-buttons"></a>Botões de controle
Em geral, os botões **OK**, **Cancelar** e **ajuda** devem ser organizados horizontalmente no canto inferior direito da caixa de diálogo. A pilha vertical alternativa será permitida se uma caixa de diálogo tiver vários outros botões na parte inferior da caixa de diálogo que apresentaria uma confusão visual com os botões de controle.

![Configurações aceitáveis para botões de controle em caixas de diálogo do Visual Studio](../../extensibility/ux-guidelines/media/0704-04_controlbuttonconfig.png "0704-04_ControlButtonConfig")<br />Configurações aceitáveis para botões de controle em caixas de diálogo do Visual Studio

A caixa de diálogo deve incluir um botão de controle padrão. Para determinar o melhor comando a ser usado como padrão, escolha uma das seguintes opções (listadas em ordem de precedência):

- Escolha o comando mais seguro e seguro como o padrão. Isso significa escolher o comando com mais probabilidade de evitar a perda de dados e evitar o acesso indesejado ao sistema.

- Se a perda de dados e a segurança não forem fatores, escolha o comando padrão com base na conveniência. Incluir o comando mais provável como padrão melhorará o fluxo de trabalho do usuário quando a caixa de diálogo oferecer suporte a tarefas frequentes ou repetitivas.

Evite escolher uma ação destrutiva permanentemente para o comando padrão. Se esse comando estiver presente, escolha um comando mais seguro como o padrão.

#### <a name="access-keys"></a>Chaves de acesso
Não use chaves de acesso para botões **OK**, **Cancelar** ou **ajuda** . Esses botões são mapeados para teclas de atalho por padrão:

| Nome do botão | Atalho de teclado |
| --- | --- |
| OK | Digite |
| Cancelar | Esc |
| Ajuda | F1 |

#### <a name="imagery"></a>Imagens
Use as imagens com moderação em caixas de diálogo. Não use ícones grandes em caixas de diálogos apenas para usar espaço. Use imagens somente se elas forem uma parte importante da transmissão da mensagem para o usuário, como ícones de aviso ou animações de status.

### <a name="prioritizing-and-layering"></a><a name="BKMK_PrioritizingAndLayering"></a> Priorização e disposição em camadas

#### <a name="prioritizing-your-ui"></a>Priorizando sua interface do usuário
Pode ser necessário trazer certos elementos da interface do usuário para o Forefront e colocar comportamentos e opções mais avançadas (incluindo comandos obscuros) em caixas de diálogo. Traga a funcionalidade comumente usada para o Forefront, deixando espaço para ela e tornando-a visível por padrão na interface do usuário com um rótulo de texto quando a caixa de diálogo for exibida.

#### <a name="layering-your-ui"></a>Camadas da interface do usuário
Se você determinou que uma caixa de diálogo é necessária, mas a funcionalidade relacionada que você deseja apresentar ao usuário vai além do que pode ser exibido em uma caixa de diálogo simples, você precisará colocar a interface do usuário em camadas. Os métodos de camadas mais comuns usados pelo Visual Studio são guias e corredores ou Dashboards. Em alguns casos, as regiões que podem expandir e recolher podem ser apropriadas. A interface do usuário adaptável geralmente não é recomendada no Visual Studio.

Há vantagens e desvantagens em métodos diferentes de interface do usuário de camadas por meio de controles de tabulação. Examine a lista abaixo para garantir que você está escolhendo uma técnica de camadas apropriada para sua situação.

##### <a name="tabbing"></a>Tabulação

| Mecanismo de alternância | Vantagens e uso apropriado | Desvantagens e uso inadequado |
| --- | --- | --- |
| Controle guia | Agrupar logicamente as páginas de caixa de diálogo em conjuntos relacionados<br /><br />Útil para menos de cinco (ou o número de guias que se ajustam em uma linha na caixa de diálogo) páginas de controles relacionados na caixa de diálogo<br /><br />Os rótulos de guia devem ser curtos: uma ou duas palavras que podem identificar facilmente o conteúdo<br /><br />Um estilo de caixa de diálogo comum do sistema<br /><br />Exemplo: **Propriedades do &gt; item do explorador de arquivos** | Tornar os rótulos curtos descritivos pode ser difícil<br /><br />Geralmente não dimensiona as últimas cinco guias em uma caixa de diálogo<br /><br />Inadequado se você tiver muitas guias para uma linha (use uma técnica de camada alternativa)<br /><br />Não extensível |
| Navegação na barra lateral | Dispositivo simples de comutação que pode acomodar mais categorias do que guias<br /><br />Lista simples de categorias (sem hierarquia)<br /><br />Extensível<br /><br />Exemplo: **Personalizar... &gt; Adicionar comando** | Não é um bom uso do espaço horizontal se houver menos de três grupos<br /><br />A tarefa pode ser mais adequada para uma lista suspensa |
| Controle de árvore | Permite categorias ilimitadas<br /><br />Permite o agrupamento e/ou a hierarquia de categorias<br /><br />Extensível<br /><br />Exemplo: **ferramentas &gt; Opções** | Hierarquias fortemente aninhadas podem causar rolagem horizontal excessiva<br /><br />O Visual Studio tem uma abundância de exibições de árvore |
| Assistente | Ajuda com a conclusão de tarefas ao orientar o usuário por meio de etapas sequenciais, baseadas em tarefas: o assistente representa uma tarefa de alto nível e os painéis individuais representam subtarefas necessárias para realizar a tarefa geral<br /><br />Útil quando a tarefa cruza os limites da interface do usuário, como quando, de outra forma, teria de usar vários editores e janelas de ferramentas para concluir a tarefa<br /><br />Útil quando a tarefa requer ramificação<br /><br />Útil quando a tarefa contém dependências entre etapas<br /><br />Útil quando várias tarefas semelhantes com uma bifurcação de decisão podem ser apresentadas em uma caixa de diálogo para reduzir o número de caixas de diálogo diferentes semelhantes | Impróprio para qualquer tarefa que não exija um fluxo de trabalho Sequencial<br /><br />Os usuários podem ficar sobrecarregados e confusos por um assistente com muitas etapas<br /><br />Os assistentes têm espaço de tela inerentemente limitado |

##### <a name="hallways-or-dashboards"></a>Corredores ou dashboards
Corredores e painéis são caixas de diálogo ou painéis que servem como pontos de partida para outras caixas de diálogo e janelas. O "corredor" bem projetado apenas mostra as opções, os comandos e as configurações mais comuns, permitindo que o usuário realize tarefas comuns imediatamente. Como um corredor do mundo real fornece doorways para acessar as salas por trás deles, aqui a interface do usuário menos comum é coletada em "salas" separadas (muitas vezes, outras caixas de diálogo) de funcionalidades relacionadas que podem ser acessadas no corredor principal.

Como alternativa, uma interface do usuário que oferece toda a funcionalidade disponível em uma única coleção em vez de refatorar a funcionalidade menos comum em locais separados é simplesmente um painel.

![Conceito de corredor para expor a interface do usuário adicional no Outlook](../../extensibility/ux-guidelines/media/0704-08_hallway.png "0704-08_Hallway")<br />Conceito de corredor para expor a interface do usuário adicional no Outlook

##### <a name="adaptive-ui"></a>Interface do usuário adaptável
Mostrar ou ocultar a interface do usuário com base no uso ou na experiência autorelata de um usuário é outra maneira de apresentar a interface do usuário necessária e ocultar outras partes. Isso não é recomendado no Visual Studio, pois os algoritmos para decidir quando mostrar ou ocultar a interface do usuário podem ser complicados, e as regras sempre estarão erradas para algum conjunto de casos.

## <a name="projects"></a><a name="BKMK_Projects"></a> Projeto

### <a name="projects-in-the-solution-explorer"></a>Projetos no Gerenciador de Soluções
A maioria dos projetos é classificada como baseada em referência, baseada em diretório ou mista. Todos os três tipos de projetos têm suporte simultaneamente no Gerenciador de Soluções. A raiz da experiência do usuário no trabalho com projetos ocorre dentro desta janela. Embora nós de projeto diferentes sejam de referência, diretório ou projetos de tipo de modo misto, há um padrão de interação comum que deve ser aplicado como um ponto de partida antes de divergente em padrões de usuário específicos do projeto.

Os projetos sempre devem:

- Suporte à capacidade de adicionar pastas de projeto para organizar o conteúdo do projeto

- Manter um modelo consistente para persistência do projeto

Os projetos também devem manter modelos de interação consistentes para:

- Removendo itens de projeto

- Salvando documentos

- Edição de Propriedade do projeto

- Editando o projeto em uma exibição alternativa

- Operações de arrastar e soltar

### <a name="drag-and-drop-interaction-model"></a>Modelo de interação do tipo "arrastar e soltar"
Normalmente, os projetos se classificam como baseados em referência (capazes de persistir apenas as referências a itens de projeto no armazenamento), com base no diretório (capaz de persistir apenas os itens de projeto armazenados fisicamente na hierarquia de um projeto) ou mistos (capazes de manter referências ou itens físicos). O IDE acomoda todos os três tipos de projetos simultaneamente dentro do **Gerenciador de soluções**.

De uma perspectiva de arrastar e soltar, as seguintes características devem ser aplicadas a cada tipo de projeto dentro do **Gerenciador de soluções**:

- **Projeto baseado em referência:** O ponto-chave é que o projeto está arrastando em uma referência a um item no armazenamento. Quando um projeto baseado em referência atua como uma fonte para uma operação de movimentação, ele só deve remover a referência ao item do projeto. O item não deve ser realmente excluído do disco rígido. Quando um projeto baseado em referência atua como um destino para uma operação de movimentação (ou cópia), ele deve adicionar uma referência ao item de origem original sem fazer uma cópia privada do item.

- **Projeto baseado em diretório:** Do ponto de vista do tipo "arrastar e soltar", o projeto é arrastando para o item físico em vez de uma referência. Quando um projeto baseado em diretório atua como uma fonte para uma operação de movimentação, ele deve acabar excluindo o item físico do disco rígido, bem como removendo-o do projeto. Quando um projeto baseado em diretório atua como um destino para uma operação de movimentação (ou cópia), ele deve fazer uma cópia do item de origem em seu local de destino.

- **Projeto de destino misto:** De um ponto de vista de arrastar e soltar, o comportamento desse tipo de projeto é baseado na natureza do item que está sendo arrastado (uma referência a um item no armazenamento ou no próprio item). O comportamento correto para referências e itens físicos é descrito acima.

Se houver apenas um tipo de projeto na **Gerenciador de soluções**, as operações de arrastar e soltar seriam simples. Como cada sistema de projeto tem a capacidade de definir seu próprio comportamento de arrastar e soltar, determinadas diretrizes (com base no comportamento do tipo "arrastar e soltar" do Windows Explorer) devem ser seguidas para garantir uma experiência de usuário previsível:

- Uma operação de arrastar não modificada no **Gerenciador de soluções** (quando nenhuma tecla CTRL nem Shift é mantida) deve resultar em uma operação de movimentação.

- A operação de arrastar e mover também deve resultar em uma operação de movimentação.

- A operação Ctrl-Drag deve resultar em uma operação de cópia.

- Sistemas de projeto mistos e baseados em referência dão suporte à noção de adicionar um link (ou referência) ao item de origem. Quando esses projetos são o destino de uma operação de arrastar e soltar (quando **Ctrl + Shift** é mantido), ele deve resultar em uma referência ao item que está sendo adicionado ao projeto

Nem todas as operações de arrastar e soltar são sensatas entre combinações de projetos baseados em referência, baseados em diretório e mistos. Em particular, é problemático fingir permitir uma operação de movimentação entre um projeto de origem baseado em diretório e um projeto de destino baseado em referência, pois o projeto baseado no diretório de origem terá que excluir o item de origem após a conclusão da movimentação. O projeto baseado em referência de destino, em seguida, acabaria com uma referência a um item excluído.

Também é enganoso fingir permitir uma operação de cópia entre esses tipos de projetos porque o projeto baseado em referência de destino não deve fazer uma cópia independente do item de origem. Da mesma forma, Ctrl + Shift para arrastar para um projeto de destino baseado em diretório não deve ser permitido porque um projeto baseado em diretório não pode persistir referências. Nos casos em que a operação de arrastar e soltar não tem suporte, o IDE deve desautorizar o descarte e mostrar ao usuário o cursor no-drop (mostrado na tabela de ponteiros abaixo).

Para implementar corretamente o comportamento de arrastar e soltar, o projeto de origem do drag precisa comunicar sua natureza com o projeto de destino. (Por exemplo, é baseado em referência ou em diretório?) Essas informações são indicadas pelo formato de área de transferência que é oferecido pela origem. Como a origem de uma operação de arrastar (ou de cópia da área de transferência), um projeto deve oferecer `CF_VSREFPROJECTITEMS` ou `CF_VSSTGPROJECTITEMS` respectivamente, dependendo se o projeto é baseado em referência ou baseado em diretório. Ambos os formatos têm o mesmo conteúdo de dados, que é semelhante ao formato do Windows, `CF_HDROP` exceto que as listas de cadeias de caracteres, em vez de serem nomes de File, são uma `NULL` lista de cadeias de caracteres com finalidades duplas `Projref` (como retornado de `IVsSolution::GetProjrefOfItem` ou `::GetProjrefOfProject` conforme apropriado).

Como o destino de um drop (ou operação de colagem da área de transferência), um projeto deve aceitar ambos `CF_VSREFPROJECTITEMS` e `CF_VSSTGPROJECTITEMS` , embora o tratamento exato da operação de arrastar e soltar varie, dependendo da natureza do projeto de destino e do projeto de origem. O projeto de origem declara sua natureza pelo fato de ele oferecer `CF_VSREFPROJECTITEMS` ou `CF_VSSTGPROJECTITEMS` . O destino da queda compreende sua própria natureza e, portanto, tem informações suficientes para tomar decisões sobre se um movimento, uma cópia ou um link devem ser executados. O usuário também modifica o que a operação de arrastar e soltar deve ser executada pressionando as teclas CTRL, Shift ou CTRL e Shift. É importante que o destino de soltura indique corretamente qual operação será executada com antecedência em seus `DragEnter` métodos e `DragOver` . O **Gerenciador de soluções** automaticamente sabe se o projeto de origem e o projeto de destino são o mesmo projeto.

Não há suporte especificamente para arrastar itens de projeto entre instâncias do Visual Studio (por exemplo, de uma instância do devenv.exe para outro). O **Gerenciador de soluções** também desabilita diretamente isso.

O usuário sempre deve ser capaz de determinar o efeito de uma operação de arrastar e soltar selecionando um item, arrastando-o para o local de destino e observando quais dos seguintes ponteiros do mouse aparecem antes de o item ser descartado:

| Ponteiro do mouse | Comando | Descrição |
| :---: | --- | --- |
| ![Ícone "sem soltar" do mouse](../../extensibility/ux-guidelines/media/0706-01_mousenodrop.png "0706-01_MouseNoDrop") | Sem drop | Não é possível remover o item para o local especificado. |
| ![Ícone de "cópia" do mouse](../../extensibility/ux-guidelines/media/0706-02_mousecopy.png "0706-02_MouseCopy") | Copiar | O item será copiado para o local de destino. |
| ![Ícone "mover" do mouse](../../extensibility/ux-guidelines/media/0706-03_mousemove.png "0706-03_MouseMove") | Mover | O item será movido para o local de destino. |
| ![Ícone "Adicionar referência" do mouse](../../extensibility/ux-guidelines/media/0706-04_mouseaddref.png "0706-04_MouseAddRef") | Adicionar referência | Uma referência ao item selecionado será adicionada ao local de destino. |

#### <a name="reference-based-projects"></a>Projetos baseados em referência
 A tabela a seguir resume as operações de arrastar e soltar (bem como recortar/copiar/colar) que devem ser executadas com base na natureza do item de origem e nas teclas modificadoras pressionadas para projetos de destino baseados em referência:

| Modificador | Categoria | Item de origem: referência/link | Item de origem: Item físico ou sistema de arquivos ( `CF_HDROP` ) |
| --- | --- | --- | --- |
| Nenhum modificador | Ação | Mover | Link |
| Nenhum modificador | Destino | Adiciona referência ao item original | Adiciona referência ao item original |
| Nenhum modificador | Fonte | Exclui a referência ao item original | Retém o item original |
| Nenhum modificador | Resultado | `DROPEFFECT_MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Shift + arrastar | Ação | Mover | Sem drop |
| Shift + arrastar | Destino | Adiciona referência ao item original | Sem drop |
| Shift + arrastar | Fonte | Exclui a referência ao item original | Sem drop |
| Shift + arrastar | Resultado | `DROPEFFECT_MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | Sem drop |
| Ctrl + arrastar | Ação | Copiar | Sem drop |
| Ctrl + arrastar | Destino | Adiciona referência ao item original | Sem drop |
| Ctrl + arrastar | Fonte | Retém a referência ao item original | Sem drop |
| Ctrl + arrastar | Resultado | `DROPEFFECT_COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | Sem drop |
| Ctrl + Shift + arrastar | Ação | Link | Link |
| Ctrl + Shift + arrastar | Destino | Adiciona referência ao item original | Adiciona referência ao item original |
| Ctrl + Shift + arrastar | Fonte | Retém a referência ao item original | Retém o item original |
| Ctrl + Shift + arrastar | Resultado | `DROPEFFECT_LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl + Shift + arrastar | Observação | O mesmo que o comportamento de arrastar e soltar para atalhos no Windows Explorer. ||
| Recortar/colar | Ação | Mover | Link |
| Recortar/colar | Destino | Adiciona referência ao item original | Adiciona referência ao item original |
| Recortar/colar | Fonte | Retém a referência ao item original|Retém o item original |
| Recortar/colar | Resultado | O item permanece no local original no armazenamento | O item permanece no local original no armazenamento |
| Copiar/colar | Ação | Copiar | Link |
| Copiar/colar | Fonte | Adiciona referência ao item original | Adiciona referência ao item original |
| Copiar/colar | Resultado | Retém a referência ao item original | Retém o item original |
| Copiar/colar | Ação | O item permanece no local original no armazenamento | O item permanece no local original no armazenamento |

#### <a name="directory-based-projects"></a>Projetos baseados em diretório
A tabela a seguir resume as operações de arrastar e soltar (bem como recortar/copiar/colar) que devem ser executadas com base na natureza do item de origem e nas teclas modificadoras pressionadas para projetos de destino baseados em diretório:

| Modificador | Categoria | Item de origem: referência/link | Item de origem: Item físico ou sistema de arquivos ( `CF_HDROP` ) |
|-----------------|----------| - | - |
| Nenhum modificador | Ação | Mover | Mover |
| Nenhum modificador | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Nenhum modificador | Fonte | Exclui a referência ao item original | Exclui a referência ao item original |
| Shift + arrastar | Ação | Mover | Mover |
| Shift + arrastar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Shift + arrastar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Shift + arrastar | Resultado | `DROPEFFECT_MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl + arrastar | Ação | Copiar | Copiar |
| Ctrl + arrastar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Ctrl + arrastar | Fonte | Retém a referência ao item original | Retém a referência ao item original |
| Ctrl + arrastar | Resultado | `DROPEFFECT_COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl + Shift + arrastar | | Sem drop | Sem drop |
| Recortar/colar | Ação | Mover | Mover |
| Recortar/colar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Recortar/colar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Recortar/colar | Resultado | O item permanece no local original no armazenamento | O item foi excluído do local original no armazenamento |
| Copiar/colar | Ação | Copiar | Copiar |
| Copiar/colar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Copiar/colar | Fonte | Retém o item original | Retém o item original |
| Copiar/colar | Resultado | O item permanece no local original no armazenamento | O item permanece no local original ins de armazenamento |

#### <a name="mixed-target-projects"></a>Projetos de destino misto
A tabela a seguir resume as operações de arrastar e soltar (bem como recortar/copiar/colar) que devem ser executadas com base na natureza do item de origem e nas teclas modificadoras pressionadas para projetos de destino misto:

| Modificador | Categoria | Item de origem: referência/link | Item de origem: Item físico ou sistema de arquivos ( `CF_HDROP` ) |
| --- | --- | --- | --- |
| Nenhum modificador | Ação | Mover | Mover |
| Nenhum modificador | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Nenhum modificador | Fonte | Exclui a referência ao item original | Exclui a referência ao item original |
| Nenhum modificador | Resultado | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item é excluído do local original no armazenamento |
| Shift + arrastar | Ação | Mover | Mover |
| Shift + arrastar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Shift + arrastar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Shift + arrastar | Resultado | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item é excluído do local original no armazenamento |
| Ctrl + arrastar | Ação | Copiar | Copiar |
| Ctrl + arrastar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Ctrl + arrastar | Fonte | Retém a referência ao item original | Retém o item original |
| Ctrl + arrastar | Resultado | `DROPEFFECT_ COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl + Shift + arrastar | Ação | Link | Link |
| Ctrl + Shift + arrastar | Destino | Adiciona referência ao item original | Adiciona referência ao item de origem original |
| Ctrl + Shift + arrastar | Fonte | Retém a referência ao item original | Retém o item original |
| Ctrl + Shift + arrastar | Resultado | `DROPEFFECT_ LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Recortar/colar | Ação | Mover | Mover |
| Recortar/colar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Recortar/colar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Recortar/colar | Resultado | O item permanece no local original no armazenamento | O item foi excluído do local original no armazenamento |
| Copiar/colar | Ação | Copiar | Copiar |
| Copiar/colar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Copiar/colar | Fonte | Retém o item original | Retém o item original |
| Copiar/colar | Resultado | O item permanece no local original no armazenamento | O item permanece no local original no armazenamento |

Esses detalhes devem ser levados em consideração ao implementar o recurso de arrastar no **Gerenciador de soluções**:

- Design para vários cenários de seleção.

- Os nomes de arquivo (caminho completo) devem ser exclusivos no projeto de destino ou o descarte não deve ser permitido.

- Os nomes de pastas devem ser exclusivos (não diferencia maiúsculas de minúsculas) no nível em que estão sendo descartados.

- Há diferenças de comportamento entre arquivos abertos ou fechados no momento da operação de arrastar (não mencionado em cenários acima).

- Os arquivos de nível superior têm um comportamento ligeiramente diferente dos arquivos nas pastas.

Outro problema a ser considerado é como lidar com operações de movimentação em itens que têm designers ou editores abertos. O comportamento esperado é o seguinte (isso se aplica a todos os tipos de projeto):

1. Se o Editor/Designer aberto não tiver alterações não salvas, a janela Editor/Designer deverá ser silenciosamente fechada.

2. Se o Editor/Designer aberto tiver alterações não salvas, a origem da operação de arrastar deverá aguardar até que o descarte ocorra e, em seguida, pedir ao usuário para salvar as alterações não confirmadas nos documentos abertos antes de fechar a janela com um prompt semelhante ao seguinte:

    ```
    ==========================================================
         One or more open documents have unsaved changes.
    Do you want to save uncommitted changes before proceeding?
                      [Yes]  [No]  [Cancel]
    ==========================================================
    ```

Isso dá ao usuário a oportunidade de salvar o trabalho em andamento antes que o destino faça suas cópias. Um novo método foi `IVsHierarchyDropDataSource2::OnBeforeDropNotify` adicionado para habilitar essa manipulação.

O destino, em seguida, copiará o estado do item como está no armazenamento (não incluindo as alterações não salvas no editor se o usuário escolher **não**). Depois que o destino tiver concluído sua cópia (em `IVsHierarchyDropDataSource::Drop` ), a origem terá a oportunidade de concluir a parte de exclusão da operação de movimentação (em `IVsHierarchyDropDataSource::OnDropNotify` ).

Todos os editores com alterações não salvas devem ser deixados abertos. Para esses documentos com alterações não salvas, isso significa que a parte de cópia da operação de movimentação será executada, mas a parte de exclusão será anulada. Em um cenário de seleção múltipla quando o usuário escolhe **não**, os documentos com alterações não salvas não devem ser fechados ou removidos, mas aqueles sem alterações não salvas devem ser fechados e removidos.
