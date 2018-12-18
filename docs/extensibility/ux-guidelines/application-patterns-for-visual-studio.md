---
title: Padrões de aplicativo para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 8ed68602-4e28-46fe-b39f-f41979b308a2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b62f7f75293c895ca1dcfd39c2a03162a43a3904
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877407"
---
# <a name="application-patterns-for-visual-studio"></a>Padrões de aplicativo para o Visual Studio
##  <a name="BKMK_WindowInteractions"></a> Interações de janela  

### <a name="overview"></a>Visão geral  
Os dois tipos de janela principal usados no Visual Studio são editores de documento e janelas de ferramentas. Rara, mas possível, é grandes caixas de diálogo sem janela restrita. Embora essas sejam tudo sem janela restrita no shell, seus padrões são fundamentalmente diferentes. Esta seção aborda a diferença entre janelas de documentos, janelas e caixas de diálogo sem janela restrita. Padrões da caixa de diálogo modal são abordados [caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs).  

### <a name="comparing-window-usage-patterns"></a>Comparando os padrões de uso de janela  
**Janelas do documento** quase sempre são exibidos dentro do documento também. Isso fornece o editor de documentos "estágio de center" para organizar as janelas de ferramenta complementar ao redor.  

Um **janela de ferramentas** geralmente é exibido como uma janela separada, menor recolhida em relação a borda do IDE. Isso pode ser visível, oculto ou ocultada automaticamente. No entanto, às vezes, as janelas de ferramentas são apresentadas no documento bem, desmarcando as **janela/encaixe** propriedade na janela. Isso resulta em mais de espaço real, mas também um comum decisão de design: ao tentar se integrar ao Visual Studio, você deve decidir se o recurso deve exibir uma janela de ferramentas ou uma janela do documento.  

**Caixas de diálogo sem janela restrita** desaconselhável no Visual Studio. Caixas de diálogo sem janela restrita mais são, por definição, as janelas de ferramentas flutuantes e devem ser implementadas dessa forma. Caixas de diálogo sem janela restrita são permitidas em casos em que o tamanho de uma janela de ferramenta normal encaixado ao lado do shell seria seja muito limitado. Eles também são permitidos em casos em que o usuário seria provavelmente mover a caixa de diálogo para um monitor secundário.  

Pense cuidadosamente sobre qual tipo de contêiner que você precisa. Considerações de padrão de uso comuns do design de interface do usuário estão na tabela a seguir.  

||Janela do documento|Janela de ferramentas|Caixa de diálogo sem janela restrita|  
|-|---------------------|-----------------|---------------------|  
| **posição** | Sempre posicionados dentro do documento bem e não encaixar ao redor das bordas do IDE. Ele pode ser "bem-sucedido" para que ela flutue separadamente do shell principal. | Geralmente, guia-encaixada ao redor das bordas do IDE, mas pode ser personalizado para ser sobrepostos, ocultos automaticamente (desafixada) ou encaixada bem dentro do documento.|Grande janela flutuante separada do IDE. |  
| **Confirmar modelo** | *Confirmação atrasada*<br /><br /> Para salvar os dados em um documento, o usuário deve emitir a **arquivo &gt; salve**, **Salvar como**, ou **Salvar tudo** comando. Uma janela de documento tem o conceito dos dados dentro dele que está sendo "sujas", em seguida, o compromisso de um dos Salvar comandos. Ao fechar uma janela de documento, todo o conteúdo é salvos em disco ou perdido. | *Confirmação imediata*<br /><br /> Não há nenhum Salvar modelo. Inspetor das janelas de ferramentas que auxiliam na edição de um arquivo, o arquivo deve ser aberto no editor ativo ou no designer e o editor ou designer possui o salvamento. | *Confirmação atrasada ou imediata*<br /><br /> Geralmente, uma caixa de diálogo sem janela restrita grande requer uma ação para confirmar as alterações e permite uma operação "Cancelar", que reverte todas as alterações feitas dentro da sessão de diálogo.  Isso os diferencia uma caixa de diálogo sem janela restrita a partir de uma janela de ferramenta em que as janelas de ferramentas sempre têm um modelo de confirmação imediata. |  
| **Visibilidade** | *Abrir/criar (arquivo) e fechar*<br /><br /> Abrir um janelas de documento é feito por meio de abertura de um documento existente ou usando um modelo para criar um novo documento. Não há nenhum "abrir \<específica do editor >" comando. | *Ocultar e mostrar*<br /><br /> Janelas de ferramentas de instância única podem ser ocultadas ou exibidas. Conteúdo e os estados dentro da janela de ferramenta persistirem se no modo de exibição ou oculto. Janelas de ferramentas de várias instâncias podem ser fechadas bem como ocultadas. Quando uma janela de ferramentas de várias instâncias é fechada, o conteúdo e o estado dentro da janela de ferramenta é descartado. | *Iniciado a partir de um comando*<br /><br /> Caixas de diálogo são iniciadas a partir de um comando baseado em tarefa. |  
| **Instâncias** | *Várias instâncias*<br /><br /> Vários editores podem ser abertos no mesmo momento e edição de arquivos diferentes, embora alguns editores também permitem que o mesmo arquivo seja aberto em mais de um editor (usando o **janela &gt; nova janela** comando).<br /><br /> Um único editor pode estar editando um ou vários arquivos ao mesmo tempo (Designer de projeto). | *Única ou várias instâncias*<br /><br /> Conteúdo alterado para refletir o contexto (como o navegador de propriedade) ou enviar por push o foco/contexto para outras janelas (lista de tarefas, o Gerenciador de soluções).<br /><br /> Janelas de ferramentas de instância única ou várias instâncias devem ser associadas à janela do documento ativo, a menos que haja um motivo convincente não para. | *Instância única* |  
| **Exemplos** | **Editores de texto**, como o editor de código<br /><br /> **As superfícies de design**, como o designer de formulários ou uma superfície de modelagem<br /><br /> **Controlar layouts semelhantes a caixas de diálogo**, como o Designer de manifesto | O **Gerenciador de soluções** oferece uma solução e projetos contidos dentro da solução<br /><br /> O **Gerenciador de servidores** fornece uma exibição hierárquica dos servidores e conexões de dados que o usuário optar por abrir na janela. Abertura de um objeto da hierarquia de banco de dados, como uma consulta, abre uma janela de documento e permite que o usuário editar a consulta.<br /><br /> O **navegador de propriedade** exibe as propriedades do objeto selecionado em uma janela de documento ou em outra janela de ferramenta. As propriedades são apresentadas em uma exibição hierárquica de grade ou em controles de caixa de diálogo semelhante complexos e permitir que o usuário definir os valores dessas propriedades. | |  

##  <a name="BKMK_ToolWindows"></a> Janelas de ferramentas  

### <a name="overview"></a>Visão geral  
Janelas de ferramentas dão suporte para o trabalho do usuário que acontece em janelas de documento. Eles podem ser usados para exibir uma hierarquia que representa um objeto raiz fundamental que o Visual Studio fornece e pode manipular.  

Ao considerar uma nova janela de ferramentas no IDE, os autores devem:  

-   Usar janelas de ferramentas existente apropriado de tarefa e não criar novos com funcionalidade semelhante. Nova janela de ferramentas só deve ser criada se eles oferecem uma funcionalidade que não pode ser integrada em uma janela semelhante ou transformando-se em uma janela existente em um hub dinamização ou "tool" significativamente diferente.  

-   Use uma barra de comando padrão, se necessário, na parte superior da janela de ferramentas.  

-   Seja consistente com padrões já está presentes nas outras janelas de ferramentas para controlar a navegação de teclado e de apresentação.  

-   Seja consistente com a apresentação de controle nas outras janelas de ferramentas.  

-   Verifique as janelas de ferramentas específicas de documentos automaticamente visíveis quando possível, para que eles aparecem somente quando o documento pai é ativado.  

-   Certifique-se de que seu conteúdo da janela é passível de navegação pelo teclado (suporte a teclas de direção).  

#### <a name="tool-window-states"></a>Estados de janela de ferramenta  
Janelas de ferramentas do Visual Studio têm diferentes estados, alguns dos quais são ativados por usuário (como o recurso de ocultar automaticamente). Outros estados, como automaticamente visíveis, permitir janelas de ferramenta apareça no contexto correto e ocultar quando não é necessário. Há cinco estados de janela de ferramenta no total.  

-   **Encaixado/fixado** janelas de ferramentas podem ser anexadas a qualquer um dos quatro lados da área do documento. O ícone de anotações aparece na barra de título da janela de ferramenta. A janela de ferramentas pode ser encaixada horizontal ou verticalmente ao longo da borda de shell e outras janelas de ferramentas e também pode ser vinculada por guia.  

-   **Auto-oculto** janelas de ferramentas não serão fixadas. A janela pode deslizar fora de Vista, deixando uma tabulação (com o nome da janela de ferramenta e seu ícone) na borda da área do documento. A janela da ferramenta desliza quando o usuário passa o mouse sobre a guia.  

-   **Autovisível** janelas de ferramentas será exibida automaticamente quando outra parte da interface do usuário, como um editor, é iniciado ou ganha o foco.  

-   **Flutuante** janelas de ferramenta passe o mouse fora do IDE. Isso é útil para configurações de vários monitores.  

-   **Documentos com guias** janelas de ferramenta podem ser encaixadas dentro do documento também. Isso é útil para janelas de ferramentas grandes, como o Pesquisador de objetos que precisam de mais espaço livre que permite às bordas do quadro de encaixe.  

![Ferramenta de estados de janela no Visual Studio](../../extensibility/ux-guidelines/media/0702-01_toolwindowstates.png "0702 01_ToolWindowStates")<br />Estados de janela de ferramenta no Visual Studio

#### <a name="single-instance-and-multi-instance"></a>Instância única ou várias instâncias  
Janelas de ferramentas são de instância única ou várias instâncias. Algumas janelas de ferramentas de instância única podem ser associadas à janela do documento ativo, enquanto as janelas de ferramentas de várias instâncias não podem. Janelas de ferramentas de várias instâncias respondem para o **janela &gt; nova janela** comando criando uma nova instância da janela. A imagem a seguir ilustra uma janela de ferramentas, permitindo que o comando nova janela quando uma instância da janela está ativa:  

![Janela de ferramentas, permitindo que o comando 'Nova janela' quando uma instância da janela está ativa](../../extensibility/ux-guidelines/media/0702-02_toolwindowenablingcommand.png "0702 02_ToolWindowEnablingCommand")<br />Janela de ferramentas, permitindo que o comando 'Nova janela' quando uma instância da janela está ativa  

Janelas de ferramentas de instância única podem ser ocultadas ou exibidas, enquanto as janelas de ferramentas de várias instâncias podem ser fechadas, bem como ocultadas. Todas as janelas de ferramenta podem ser encaixadas vinculada por guia, flutuante ou definido como uma janela filho da Interface de documentos múltiplos (MDI) (semelhante a uma janela de documento). Todas as janelas de ferramenta devem responder para os comandos de gerenciamento de janela apropriada no menu da janela:  

![Comandos de gerenciamento de janela no menu janela do Visual Studio](../../extensibility/ux-guidelines/media/0702-03_windowmanagementcontrols.png "0702 03_WindowManagementControls")<br />Comandos de gerenciamento de janela no menu janela do Visual Studio

#### <a name="document-specific-tool-windows"></a>Janelas de ferramenta específica do documento  
Algumas janelas de ferramentas são projetadas para mudar com base em um determinado tipo de documento. Essas janelas continuamente atualizada para refletir a funcionalidade aplicável à janela do documento ativo no IDE.  

A caixa de ferramentas e a estrutura de tópicos do documento, são exemplos de janelas de ferramenta cujo conteúdo é alterado para refletir o editor selecionado. Essas janelas mostram uma marca d'água quando um editor tem o foco que oferece contexto para a janela.  

#### <a name="navigable-list-tool-windows"></a>Janelas de ferramentas lista navegável  
Algumas janelas de ferramentas exibem uma lista de itens navegáveis que o usuário pode interagir com o. Esse tipo de janela, deve sempre haver comentários para o item atual na lista, mesmo se a janela está inativa. A lista deve responder para o **GoToNextLocation** e **GoToPrevLocation** comandos, também, alterando o item atualmente selecionado na janela  

Exemplos de janelas de ferramentas lista navegáveis são Gerenciador de soluções e a janela localizar resultados.  

### <a name="tool-window-types"></a>Tipos de janelas de ferramenta  

#### <a name="common-tool-windows-and-their-functions"></a>Janelas de ferramentas comuns e suas funções

**Janelas de ferramenta hierárquica**

| Janela de ferramentas | Função | 
| --- | --- | 
| Gerenciador de Soluções | Uma árvore hierárquica que exibe uma lista de documentos contidos em projetos e arquivos diversos itens de solução. A exibição dos itens dentro de projetos é definida pelo pacote que possui o tipo de projeto (por exemplo, tipos de base de referência, baseada no Active ou modo misto). | 
| Exibição de Classe | Uma árvore hierárquica das classes e vários elementos no conjunto de trabalho de documentos, independentes dos próprios arquivos. | 
| conexões de servidor | Uma árvore hierárquica que exibe todas as conexões de servidores e dados na solução. | 
| Estrutura de Tópicos do Documento | A estrutura hierárquica do documento ativo. | 

**Janelas de ferramentas de grade**

| Janela de ferramentas | Função | 
| --- | --- | 
| Propriedades | Uma grade que exibe uma lista das propriedades do objeto selecionado, junto com os seletores de valor para editar essas propriedades. | 
| Lista de Tarefas | Uma grade que permite ao usuário criar/editar/excluir tarefas e comentários. | 

**Janelas de ferramentas de conteúdo**

| Janela de ferramentas | Função | 
| --- | --- | 
| Ajuda | Uma janela que permite aos usuários acesso a vários métodos de obtenção de Ajuda, de "Como faço para?" vídeos para os fóruns do MSDN. | 
| Ajuda dinâmica | Uma janela de ferramenta que exibe links para tópicos aplicáveis à seleção atual da Ajuda. | 
| Pesquisador de Objetos | Um conjunto de quadros de duas colunas com uma lista de componentes de objeto hierárquica no painel esquerdo e o objeto propriedades e métodos na coluna à direita. | 

**Janelas de ferramentas da caixa de diálogo**

| Janela de ferramentas | Função | 
| --- | --- | 
| Localizar | Uma caixa de diálogo que permite ao usuário localizar ou localizar e substituir em arquivos diversos dentro da solução. |
| Localização avançada | Uma caixa de diálogo que permite ao usuário localizar ou localizar e substituir em arquivos diversos dentro da solução. | 

**Outras janelas de ferramentas**

| Janela de ferramentas | Função | 
| --- | --- | 
| Caixa de Ferramentas | A janela da ferramenta usada para armazenar os elementos que serão removidos em superfícies de design, fornecendo uma origem de arrasto consistente para todos os designers. |
| Start Page | Portal do usuário para o Visual Studio, com acesso a feeds de notícias do desenvolvedor, Ajuda do Visual Studio e projetos recentes. Os usuários também podem criar páginas iniciais personalizadas copiando o arquivo ' StartPage do "Common7\IDE\StartPages\" diretório de arquivos de programa do Visual Studio para a pasta StartPages no Visual Studio documenta o diretório e, em seguida, qualquer edição do XAML pela mão ou abri-lo no Visual Studio ou outro editor de código. | 

**Janelas de ferramenta do depurador**

| Janela de ferramentas | Função | 
| --- | --- |
| Autos ||  
| Imediato ||  
| Saída | A janela de saída pode ser usada sempre que você tiver o status para declarar ou eventos textuais. |  
| Memória ||  
| Pontos de interrupção ||  
| Em execução ||  
| Documentos ||  
| Pilha de chamadas ||  
| Locais ||  
| Inspeções ||  
| Desmontagem ||  
| Registra ||  
| Threads ||  

##  <a name="BKMK_DocumentEditorConventions"></a> Convenções do editor de documento  

### <a name="document-interactions"></a>Interações de documento  
"Documentar bem" é o maior espaço dentro do IDE e onde o usuário geralmente tem se concentrado sua atenção para concluir suas tarefas, a assistência de janelas de ferramentas complementares. Editores de documento representam as unidades fundamentais de trabalho que o usuário abre e salva no Visual Studio. Eles mantêm um forte senso de seleção vinculado ao Gerenciador de soluções ou de outra hierarquia do Active Directory. O usuário deve ser capaz de apontar para uma dessas janelas de hierarquia e saber onde o documento está contido e sua relação para a solução, o projeto ou outro objeto raiz fornecido por um pacote do Visual Studio.  

Edição de documentos requer uma experiência de usuário consistente. Para permitir que o usuário para se concentrar na tarefa em mãos, em vez de no gerenciamento de janelas e localizar comandos, selecione uma estratégia de modo de exibição de documento que melhor se adapta as tarefas do usuário para editar esse tipo de documento.  

#### <a name="common-interactions-for-the-document-well"></a>Interações comuns para o documento bem  

-   Manter um modelo consistente de interação comum **novo arquivo** e **abrir arquivo** experiências.  

-   Atualize funcionalidades relacionadas em menus e janelas relacionadas quando a janela do documento é aberto.  

-   Comandos de menu adequadamente estão integrados aos menus comuns, como **edite**, **formato**, e **exibição** menus. Se houver uma quantidade significativa de comandos especializadas disponível, em seguida, um novo menu pode ser criado. Esse novo menu deve ser visível apenas quando o documento tem o foco.  

-   Uma barra de ferramentas inserida pode ser colocada na parte superior do editor. Isso é preferível ter uma barra de ferramentas separada que aparece fora do editor.  

-   Sempre manter uma seleção no Gerenciador de soluções ou ativos semelhantes a janela de hierarquia.  

-   Clicar duas vezes em um documento no Gerenciador de soluções deve executar a mesma ação que **aberto**.  

-   Se mais de um editor pode ser usado em um tipo de documento, o usuário deve ser capaz de substituir ou redefinir a ação padrão em um tipo de documento fornecido usando o **abrir com** caixa de diálogo clicando duas vezes no arquivo e selecionando **aberto Com** no menu de atalho.  

-   Não crie também um assistente em um documento.  

### <a name="user-expectations-for-specific-document-types"></a>Expectativas dos usuários para os tipos de documento específico  
Há vários tipos diferentes de básicos de editores de documento e cada um tem um conjunto de interações que são consistentes com outros usuários do mesmo tipo.  

-   **Editor de texto:** editor de código, arquivos de log  

-   **Superfície de design:** formulários do WPF forms designer, Windows  

-   **Editor de caixa de diálogo style:** Designer de manifesto, propriedades do projeto  

-   **Designer de modelo:** designer de fluxo de trabalho, codemap, diagrama de arquitetura, progressão  

Também há vários tipos de não de editor que usam o documento também. Embora eles não editam os próprios documentos, que eles precisam seguir as interações padrão para as janelas do documento.  

-   **Relatórios:** relatório do IntelliTrace, Hyper-V de relatórios, relatórios do criador de perfil  

-   **Painel:** Hub de diagnóstico  

#### <a name="text-based-editors"></a>Editores de texto  

-   O documento participa no modelo de guia de visualização, permitindo a visualização do documento sem abri-lo.  

-   A estrutura do documento pode ser representada em uma janela de ferramentas complementares, como uma estrutura de tópicos do documento.  

-   IntelliSense (se apropriado) se comportará consistentemente com outros editores de código.  

-   Pop-ups ou interface do usuário assistencial siga estilos e padrões semelhantes para existente semelhante da interface do usuário, como o CodeLens.  

-   Mensagens sobre o status do documento serão apresentadas em um controle de barra de informações na parte superior do documento ou na barra de status.  

-   O usuário deve ser capaz de personalizar a aparência de fontes e cores usando uma **Ferramentas > Opções** página, a página de fontes e cores compartilhada ou um específico para o editor.  

#### <a name="design-surfaces"></a>Superfícies de design  

-   Um designer vazio deve ter uma marca d'água na superfície do que indica como começar.  

-   Mecanismos de troca de exibição seguirão padrões existentes, como clique duas vezes para abrir um editor de código ou guias na janela do documento, permitindo que a interação com os dois painéis.  

-   Adicionar elementos à superfície de design deve ser feito por meio da caixa de ferramentas, a menos que uma janela de ferramenta altamente específica é necessária.  

-   Itens na superfície de seguirá um modelo consistente de seleção.  

-   Barras de ferramentas inseridas contêm comandos somente, não comum de comandos específicos do documento, como **salvar**.  

#### <a name="dialog-style-editors"></a>Editores de estilo de caixa de diálogo  

-   Layout do controle deve seguir as convenções de layout de caixa de diálogo normal.  

-   Guias dentro do editor não devem corresponder a aparência das guias do documento, eles devem corresponder a um dos dois estilos de guia interiores permitidos.  

-   Os usuários devem ser capazes de interagir com os controles usando o teclado qualquer um, ativando o editor e tabulação pelos controles ou usando mnemônicos padrão.  

-   O designer deve usar o comum Salvar modelo. Sem salvar geral ou botões de confirmação devem ser colocados na superfície, embora outros botões podem ser apropriados.  

#### <a name="model-designers"></a>Designers de modelo  

-   Um designer vazio deve ter uma marca d'água na superfície do que indica como começar.  

-   Adicionar elementos à superfície de design deve ser feito por meio da caixa de ferramentas.  

-   Itens na superfície de seguirá um modelo consistente de seleção.  

-   Barras de ferramentas inseridas contêm comandos somente, não comum de comandos específicos do documento, como **salvar**.  

-   Uma legenda pode aparecer na superfície, uma indicação ou uma marca d'água.  

-   O usuário deve ser capaz de personalizar a aparência das fontes/cores usando uma **Ferramentas > Opções** página, a página de fontes e cores compartilhada ou um específico para o editor.  

#### <a name="reports"></a>Relatórios  

-   Relatórios são normalmente somente informações e não participam Salvar modelo. No entanto, eles podem incluir a interação como links para outras informações relevantes ou seções expandir e recolher.  

-   A maioria dos comandos na superfície de devem ser hiperlinks, não os botões.  

-   O layout deve incluir um cabeçalho e siga as diretrizes de layout de relatório padrão.  

#### <a name="dashboards"></a>Painéis  

-   Painéis de controle não tem um modelo de interação em si, mas servem como um meio para oferecer uma variedade de outras ferramentas.  

-   Eles não participam Salvar modelo.  

-   Os usuários devem ser capazes de interagir com os controles usando o teclado, ativando o editor e percorrer os controles ou usando mnemônicos padrão.  

##  <a name="BKMK_Dialogs"></a> Caixas de diálogo  

### <a name="introduction"></a>Introdução  
Caixas de diálogo no Visual Studio normalmente devem dar suporte a uma unidade separada do trabalho do usuário e, em seguida, ser descartadas.  

Se tiver determinado que você precisa de uma caixa de diálogo, você tem três opções, na ordem de preferência:  

1.  Integre seus recursos em uma das caixas de diálogo compartilhadas no Visual Studio.  

2.  Crie sua própria caixa de diálogo usando um padrão encontrado em uma caixa de diálogo semelhante existente.  

3.  Crie uma nova caixa de diálogo, interação com o seguinte e diretrizes de layout.  

Esta seção descreve como escolher o padrão de caixa de diálogo corretas nos fluxos de trabalho do Visual Studio e as convenções comuns para design de caixa de diálogo.  

### <a name="themes"></a>Temas  
Caixas de diálogo no Visual Studio execute um dos dois estilos básicos:  

#### <a name="standard-unthemed"></a>Standard (unthemed)  
A maioria das caixas de diálogo são caixas de diálogo do utilitário padrão e deve ser unthemed. Não controles comuns não re-modelo ou tentar criar botões "moderno" estilizado ou controles. Controles e a aparência de cromo siga [diretrizes de interação de área de trabalho do Windows padrão para caixas de diálogo](/windows/desktop/uxguide/win-dialog-box).  

#### <a name="themed"></a>Com temas  
Caixas de diálogo de "assinatura" de especialidade podem ser com tema. Caixas de diálogo com tema têm uma aparência distinta, que também tem alguns padrões de interação especial associadas ao estilo. Tema a caixa de diálogo somente se ele atende a esses requisitos:  

-   A caixa de diálogo é uma experiência comum que será Vista e usada com frequência ou por muitos usuários (por exemplo, o **novo projeto** caixa de diálogo.  

-   A caixa de diálogo contém elementos de marca do produto proeminente (por exemplo, o **configurações de conta** caixa de diálogo).  

-   A caixa de diálogo é exibida como parte integrante de um fluxo maior que inclui outras caixas de diálogo com tema (por exemplo, o **Adicionar serviço conectado** caixa de diálogo).  

-   A caixa de diálogo é uma parte importante de uma experiência que desempenha um papel estratégico em promover ou diferenciando uma versão do produto.  

Ao criar uma caixa de diálogo com tema, use as cores de ambiente adequadas e siga o layout correto e os padrões de interação. (Consulte [Layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).)  

### <a name="dialog-design"></a>Design de caixa de diálogo  
Caixas de diálogo bem projetadas levar os elementos a seguir em consideração:  

-   A tarefa de usuário com suporte  

-   O estilo de texto da caixa de diálogo, idioma e terminologia  

-   Opção de controle e convenções de interface do usuário  

-   Alinhamento de especificação e controle de layout Visual  

-   Acesso pelo teclado  

#### <a name="content-organization"></a>Organização do conteúdo  
Considere as diferenças entre esses tipos básicos de caixas de diálogo:  

-   [Caixas de diálogo simples](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_SimpleDialogs) apresentar controles em uma única janela modal. A apresentação pode incluem as variações dos padrões de controle complexo, incluindo um seletor de campo ou uma barra de ícones.  

-   [Em camadas a diálogos](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_LayeredDialogs) são usados para obter o máximo de espaço na tela quando uma única parte da interface do usuário consiste em vários grupos de controles. Agrupamentos da caixa de diálogo estão "em camadas" por meio de botões, controles de lista de navegação ou controles de guia para que o usuário pode escolher qual o agrupamento para ver a qualquer momento.  

-   [Assistentes](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Wizards) são úteis para direcionar o usuário por meio de uma sequência lógica de etapas em direção a conclusão de uma tarefa. Uma série de opções são oferecidos em painéis sequenciais, às vezes, introduzindo diferentes fluxos de trabalho ("branches") dependentes de uma escolha feita no painel anterior.  

####  <a name="BKMK_SimpleDialogs"></a> Caixas de diálogo simples  
Uma caixa de diálogo simple é uma apresentação dos controles em uma única janela modal. Esta apresentação pode incluem as variações dos padrões de controle complexo, como um seletor de campo. Para caixas de diálogo simples, siga o layout geral padrão, bem como qualquer layout específico necessário para agrupamentos de controle complexo.

![> criar chave de nome forte é um exemplo de uma caixa de diálogo simple no Visual Studio. ](../../extensibility/ux-guidelines/media/0704-01_createstrongnamekey.png "01_CreateStrongNameKey 0704")<br />Criar chave de nome forte é um exemplo de uma caixa de diálogo simple no Visual Studio.

####  <a name="BKMK_LayeredDialogs"></a> Caixas de diálogo em camadas  
Caixas de diálogo em camadas incluem guias, painéis e árvores incorporados. Eles são usados para maximizar imóveis quando houver vários grupos de controles oferecidos em um único segmento de interface do usuário. Os agrupamentos são colocadas em camadas para que o usuário pode escolher qual o agrupamento para ver a qualquer momento.  

No caso mais simples, o mecanismo para alternar entre agrupamentos é um controle guia. Há várias alternativas disponíveis. Consulte atribuir prioridades e disposição em camadas para saber como escolher o estilo mais apropriado.  

O **ferramentas &gt; opções** caixa de diálogo é um exemplo de uma caixa de diálogo em camadas, usando uma árvore incorporada:  

![Ferramentas > Opções é um exemplo de uma caixa de diálogo em camadas no Visual Studio. ](../../extensibility/ux-guidelines/media/0704-02_toolsoptions.png "02_ToolsOptions 0704")<br />Ferramentas > Opções é um exemplo de uma caixa de diálogo em camadas no Visual Studio.

####  <a name="BKMK_Wizards"></a> Assistentes  
Assistentes são úteis para direcionar o usuário por meio de uma sequência lógica de etapas na conclusão de uma tarefa. Uma série de opções são oferecidos em painéis sequenciais e o usuário deve continuar por meio de cada etapa antes de prosseguir para a próxima. Depois que os padrões suficientes estão disponíveis, o **concluir** botão está habilitado.  

 Modais assistentes são usados para tarefas que:  

-   Contém a ramificação, onde caminhos diferentes são oferecidos, dependendo das escolhas do usuário  

-   Contém as dependências entre as etapas, em que as etapas subsequentes dependem de entrada do usuário de que as etapas anteriores  

-   São suficientemente complexa que a interface do usuário deve ser usada para explicar as opções oferecidas e os possíveis resultados em cada etapa  

-   São transacionais, que exigem um conjunto de etapas a serem concluídas em sua totalidade antes que as alterações sejam confirmadas  

### <a name="common-conventions"></a>Convenções comuns  
Para obter o design ideal e a funcionalidade com suas caixas de diálogo, siga essas convenções em tamanho de caixa de diálogo, posição, padrões, configuração de controle e alinhamento, interface do usuário texto, barras de título, botões de controle e as chaves de acesso.  

Para obter diretrizes específicas de layout, consulte [Layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).  

#### <a name="size"></a>Tamanho  
Caixas de diálogo devem se ajustar dentro de uma resolução de tela de 1024 x 768 mínimo e o tamanho do diálogo inicial não deve exceder 900 x 700 pixels. Caixas de diálogo podem ser redimensionáveis, mas não é um requisito.  

Há dois recomendações para as caixas de diálogo redimensionáveis:  

1.  Se um tamanho mínimo é definida para a caixa de diálogo otimizar para o controle definido sem recorte e são ajustadas para acomodar o crescimento de localização razoável.  

2.  Se o tamanho da escala de usuário persiste a cada sessão. Por exemplo, se o usuário pode ser dimensionado para 150% de uma caixa de diálogo, uma inicialização subsequente da caixa de diálogo exibirá 150%.  

#### <a name="position"></a>Posição  
Caixas de diálogo devem aparecer centralizadas dentro do IDE na primeira inicialização. A última posição de caixas de diálogo não redimensionável não precisa ser persistentes, portanto, eles aparecerão em inicializações subsequentes. 

Para caixas de diálogo redimensionáveis, o tamanho deve ser persistido nas inicializações subsequentes. Para caixas de diálogo modais redimensionáveis, a posição não precisa ser persistente. Exibi-los centralizado dentro do IDE impede a possibilidade da caixa de diálogo que aparece em uma posição imprevisível ou inutilizável quando a configuração de exibição do usuário foi alterado. 

Para caixas de diálogo sem janela restrita que podem ser reposicionadas, a posição do usuário deve ser mantida nas inicializações subsequentes, como a caixa de diálogo pode ser usada com frequência, como parte integral de um fluxo de trabalho maior.  

Quando as caixas de diálogo devem gerar outras caixas de diálogo, a caixa de diálogo de nível mais alta deve ser colocado em cascata para a direita e para baixo do pai de forma que ele óbvio para o usuário que eles depois de navegar para um novo local.  

#### <a name="modality"></a>Modalidade  
Sendo modal significa que os usuários são necessários para concluir ou cancelar a caixa de diálogo antes de continuar. Uma vez que as caixas de diálogo modais bloqueiam o interação com outras partes do ambiente do usuário, o fluxo de tarefa do seu recurso deve usá-los moderadamente possível. Quando uma operação restrita for necessária, o Visual Studio tem um número de caixas de diálogo compartilhados, em que você pode integrar seus recursos. Se for necessário criar uma nova caixa de diálogo, seguem o padrão de interação de uma caixa de diálogo existente com uma funcionalidade semelhante.  

Quando os usuários precisam para realizar as duas atividades ao mesmo tempo, como **encontrar** e **substituir** ao escrever novo código, a caixa de diálogo deve ser sem janela restrita para que o usuário pode alternar facilmente entre eles. Em geral, o Visual Studio usa janelas de ferramenta para esse tipo de tarefa vinculada que dão suporte a editor.  

#### <a name="control-configuration"></a>Configuração de controle  
Seja consistente com as configurações existentes do controle que realizam a mesma coisa no Visual Studio.  

#### <a name="title-bars"></a>Barras de título  

- O texto na barra de título deve refletir o nome do comando que o iniciou.  

- Nenhum ícone deve ser usada nas barras de título da caixa de diálogo. Em casos em que o sistema requer um, use o logotipo do Visual Studio.  

- Caixas de diálogo não deve minimizar ou maximizar botões.  

- Botões de ajuda na barra de título foram preteridos. Não adicione-os para novas caixas de diálogo. Quando eles existirem, eles devem iniciar um tópico da Ajuda que é conceitualmente relevante para a tarefa.  

  ![Especificações de diretriz para barras de título nas caixas de diálogo do Visual Studio](../../extensibility/ux-guidelines/media/0704-03_titlebarspecs.png "03_TitleBarSpecs 0704")<br />Especificações de diretriz para barras de título nas caixas de diálogo do Visual Studio

#### <a name="control-buttons"></a>Botões de controle  
Em geral, **Okey**, **Cancelar**, e **ajuda** botões devem ser organizados horizontalmente no canto inferior direito da caixa de diálogo. A pilha vertical alternativa é permitida se uma caixa de diálogo tem vários outros botões na parte inferior da caixa de diálogo que poderia apresentar visual confusão com os botões de controle.  

![Configurações aceitáveis para os botões de controle nas caixas de diálogo do Visual Studio](../../extensibility/ux-guidelines/media/0704-04_controlbuttonconfig.png "04_ControlButtonConfig 0704")<br />Configurações aceitáveis para os botões de controle nas caixas de diálogo do Visual Studio

A caixa de diálogo deve incluir um botão de controle padrão. Para determinar o comando recomendado para usar como padrão, escolher as opções seguintes (listadas em ordem de precedência):  

-   Escolha o comando mais seguro e mais seguro como padrão. Isso significa que escolher o comando mais provável evitar a perda de dados e evitar o acesso ao sistema não intencionais.  

-   Se a segurança e perda de dados não forem fatores, em seguida, escolha o comando de padrão com base em sua conveniência. Incluindo o comando provavelmente como padrão melhorará o fluxo de trabalho do usuário quando a caixa de diálogo dá suporte a tarefas frequentes ou repetitivas.  

Evite escolher uma ação destrutiva permanentemente para o comando padrão. Se o comando estiver presente, escolha um comando mais seguro como padrão.  

#### <a name="access-keys"></a>Chaves de acesso  
Não use chaves de acesso para **Okey**, **Cancelar**, ou **ajuda** botões. Por padrão, esses botões são mapeados a teclas de atalho:  

| Nome do botão | Atalho de teclado |  
| --- | --- |  
| OK | Enter |  
| Cancelar | ESC |  
| Ajuda | F1 |  

#### <a name="imagery"></a>Imagens  
Use imagens com moderação nas caixas de diálogo. Não use os ícones grandes nas caixas de diálogo simplesmente para usar o espaço. Use imagens apenas se eles são uma parte importante de transmitir a mensagem para o usuário, como ícones de aviso ou animações de status.  

###  <a name="BKMK_PrioritizingAndLayering"></a> Priorização e a disposição em camadas  

#### <a name="prioritizing-your-ui"></a>Priorizando a interface do usuário  
Ele pode ser necessário trazer determinados elementos de interface do usuário para o forefront e coloque o comportamento mais avançado e opções (incluindo comandos obscuros) em caixas de diálogo. Traga funcionalidade comumente usada para o forefront, tornando o espaço para ele e por torná-lo visível por padrão na interface do usuário com um rótulo de texto quando a caixa de diálogo é exibida.  

#### <a name="layering-your-ui"></a>Disposição em camadas de sua interface do usuário  
Se você tiver determinado que uma caixa de diálogo é necessária, mas a funcionalidade relacionada que você deseja apresentar ao usuário ultrapasse o que pode ser exibido em uma caixa de diálogo simple, você precisa para sua interface do usuário da camada. Os métodos mais comuns de disposição em camadas que usa o Visual Studio são guias e corredores ou painéis. Em alguns casos, as regiões que você podem expandir e recolher podem ser apropriados. Em geral, a interface do usuário adaptável não é recomendado no Visual Studio.  

Há vantagens e desvantagens para diferentes métodos de disposição em camadas da interface do usuário por meio de controles de guia. Examine a lista abaixo para garantir que você está escolhendo uma técnica de disposição em camadas que é apropriada para sua situação.  

##### <a name="tabbing"></a>Tabulação  

| Mecanismo de troca | Vantagens e o uso apropriado | Uso inadequado e desvantagens |  
| --- | --- | --- |  
| Controle guia | Agrupar logicamente as páginas de diálogo em conjuntos relacionados<br /><br />Útil para menos de cinco (ou o número de guias que cabem em uma linha na caixa de diálogo) as páginas de controles relacionados na caixa de diálogo<br /><br />Rótulos de guia devem ser curtos: uma ou duas palavras que podem identificar facilmente o conteúdo<br /><br />Um estilo de caixa de diálogo comuns do sistema<br /><br />Exemplo: **Explorador de arquivos &gt; propriedades de itens** | Pode ser difícil fazer rótulos curtos descritivos<br /><br />Geralmente, não pode ser escalonada após cinco guias em uma caixa de diálogo<br /><br />Inadequado, se você tiver muitos guias para uma linha (use uma técnica alternativa de disposição em camadas)<br /><br />Não extensível |  
| Navegação de barra lateral | Dispositivo de alternância Simple que pode acomodar mais categorias de guias<br /><br />Lista plana das categorias (sem hierarquia)<br /><br />Extensível<br /><br />Exemplo: **personalizar... &gt; Adicionar comando** | Não um bom uso de espaço horizontal se houver menos de três grupos<br /><br />Tarefa pode ser melhor adequada para uma lista suspensa |  
| Controle de árvore | Permite a categorias ilimitadas<br /><br />Permite agrupamento e/ou a hierarquia de categorias<br /><br />Extensível<br /><br />Exemplo: **ferramentas &gt; opções** | Hierarquias aninhadas intensamente podem causar excessiva de rolagem horizontal<br /><br />O Visual Studio tem um overabundance dos modos de exibição de árvore |  
| Wizard | Ajuda com a conclusão da tarefa, guiar o usuário pelas etapas sequenciais, com base em tarefa: o assistente representa uma tarefa de alto nível e painéis individuais representam as subtarefas necessárias para realizar a tarefa geral<br /><br />Útil quando a tarefa ultrapassa os limites da interface do usuário, como quando o usuário teria que usar vários editores e janelas para concluir a tarefa<br /><br />Útil quando a tarefa requer a ramificação<br /><br />Útil quando a tarefa contém dependências entre as etapas<br /><br />Útil quando várias tarefas semelhantes com bifurcação de uma decisão que podem ser apresentadas em uma caixa de diálogo para reduzir o número de caixas de diálogo semelhantes diferentes | Inadequado para qualquer tarefa que não requer um fluxo de trabalho sequencial<br /><br />Os usuários podem se tornar confuso com um assistente com muitas etapas e sobrecarregado<br /><br />Assistentes inerentemente têm limitado o espaço na tela |  

##### <a name="hallways-or-dashboards"></a>Corredores ou painéis  
Corredores e painéis são caixas de diálogo ou painéis que servem como pontos para outras caixas de diálogo e janelas de inicialização. "Corredor" bem projetado imediatamente expõe apenas as mais comuns as opções, comandos e configurações, permitindo que o usuário prontamente realizar tarefas comuns. Como um corredor reais fornece entradas de acesso para acessar as salas por trás deles, aqui a interface do usuário menos comuns é coletado em separado "salas" (geralmente outras caixas de diálogo) de funcionalidades relacionadas que podem ser acessados de corredor principal.  

Como alternativa, uma interface do usuário que oferece toda a funcionalidade disponível em uma única coleção em vez de refatorar a funcionalidade de menos comuns em locais separados é simplesmente um painel.  

![Conceito do corredor para expor a interface do usuário adicional no Outlook](../../extensibility/ux-guidelines/media/0704-08_hallway.png "08_Hallway 0704")<br />Conceito do corredor para expor a interface do usuário adicional no Outlook

##### <a name="adaptive-ui"></a>Interface do usuário adaptável  
Mostrando ou ocultando a interface do usuário com base no uso ou a experiência do usuário automaticamente relatados é outra maneira de apresentar necessário da interface do usuário enquanto oculta a outras partes. Isso não é recomendado no Visual Studio, como os algoritmos para decidir quando mostrar ou ocultar a interface do usuário podem ser complicados, e as regras sempre estará incorreta para um conjunto de casos.  

##  <a name="BKMK_Projects"></a> Projetos  

### <a name="projects-in-the-solution-explorer"></a>Projetos no Gerenciador de soluções  
A maioria dos projetos são classificadas como base de referência, baseada no Active ou misto. Todos os três tipos de projetos têm suporte simultaneamente no Gerenciador de soluções. A raiz da experiência do usuário ao trabalhar com projetos ocorre dentro desta janela. Embora nós diferentes de projeto são projetos do tipo de modo misto, diretório ou referência, há um padrão de interação comum que deve ser aplicado como um ponto de partida antes divergentes padrões de usuário específicos do projeto.  

Projetos devem sempre:  

-   Suporte a capacidade de adicionar pastas de projeto para organizar o conteúdo do projeto  

-   Manter um modelo consistente para persistência de projeto  

Projetos também devem manter modelos de interação consistente para:  

-   Removendo itens de projeto  

-   Salvando documentos  

-   Edição de propriedade do projeto  

-   Editar o projeto em uma exibição alternativa  

-   Operações de arrastar e soltar  

### <a name="drag-and-drop-interaction-model"></a>Modelo de interação de arrastar e soltar  
Projetos normalmente classificam em si como base de referência (capaz de manter apenas referências a itens de projeto no armazenamento), (capaz de manter somente itens de projeto fisicamente armazenado na hierarquia do projeto), com base no diretório ou misto (capaz de manter referências ou itens físicos). O IDE acomode todos os três tipos de projetos simultaneamente dentro de **Gerenciador de soluções**.  

De uma perspectiva de arrastar e soltar, as seguintes características devem ser aplicados a cada tipo de projeto dentro de **Gerenciador de soluções**:  

-   **Projeto de referência:** o ponto principal é que o projeto está sendo arrastado em torno de uma referência a um item no armazenamento. Quando um projeto baseado em referência atua como uma fonte para uma operação de movimentação, ele só deve remover a referência para o item do projeto. O item, na verdade, não deve ser excluído do disco rígido. Quando um projeto baseado em referência atua como um destino para uma operação de movimentação (ou cópia), ele deve adicionar uma referência para o item de origem original sem fazer uma cópia privada do item.  

-   **Com base no diretório de projeto:** de um ponto de vista de arrastar e soltar, o projeto está sendo arrastado em torno do item físico em vez de uma referência. Quando um projeto baseado em diretório atua como uma fonte para uma operação de movimentação, ele deve acabar excluindo o item físico da unidade de disco, bem como removê-lo do projeto. Quando um projeto baseado em diretório atua como um destino para uma operação de movimentação (ou cópia), ele deve fazer uma cópia do item de origem em seu local de destino.  

-   **Projeto de destino misto:** de um ponto de vista de arrastar e soltar, o comportamento desse tipo de projeto se baseia a natureza do item que está sendo arrastado (uma referência a um item no armazenamento) ou o próprio item. O comportamento correto para referências e itens físicos são descritos acima.  

Se houver apenas um tipo de projeto na **Gerenciador de soluções**, em seguida, operações de arrastar e soltar seria simples. Como cada sistema de projeto tem a capacidade de definir seu próprio comportamento de arrastar e soltar, determinadas diretrizes (com base no comportamento de arrastar e soltar do Explorer do Windows) devem ser seguidas para garantir uma experiência de usuário mais previsível:  

-   Arraste um não modificado operação na **Gerenciador de soluções** (quando nem Ctrl nem teclas Shift está pressionada) deve resultar em uma operação de movimentação.  

-   A operação de arrastar SHIFT também deve resultar em uma operação de movimentação.  

-   Operação de CTRL-arrastar deve resultar em uma operação de cópia.  

-   Sistemas de projeto com base em referência e misto suportam a noção de adicionando um link (ou referenciar) para o item de origem. Quando esses projetos são o destino de uma operação de arrastar e soltar (quando **Ctrl + Shift** for mantido pressionado), ele deve resultar em uma referência para o item que está sendo adicionado ao projeto  

Nem todas as operações de arrastar e soltar são sensatas entre combinações de projetos baseados em referências, baseada no Active e mistos. Em particular, é problemático fingir que permitem que uma operação de movimentação entre um projeto com base no diretório de origem e o projeto de referência com base no destino, porque o projeto com base no diretório de origem será necessário excluir o item de origem após a conclusão da mudança. O projeto de referência com base no destino, em seguida, acabaria com uma referência a um item excluído.  

Também é um equívoco fingir permitir que uma operação de cópia entre esses tipos de projetos, pois o projeto de referência com base no destino não deve fazer uma cópia independente do item de origem. Da mesma forma, Ctrl + Shift arrastando para um projeto de destino baseada no Active deve não ser permitido como um projeto baseado no diretório é capaz de persistir as referências. Em casos onde não há suporte para a operação de arrastar e soltar, o IDE deve não permitir a operação de soltar e mostrar ao usuário o cursor não soltar (mostrado na tabela ponteiro abaixo).  

Para implementar corretamente o comportamento de arrastar e soltar, o projeto de origem de arrastar precisa se comunicar sua natureza para o projeto de destino. (Por exemplo, é baseada no Active ou referência?) Essa informação é indicada pelo formato de área de transferência é oferecido pela origem. Como a origem de arrastar (ou operação de cópia da área de transferência), um projeto deve oferecer uma `CF_VSREFPROJECTITEMS` ou `CF_VSSTGPROJECTITEMS` respectivamente, dependendo se o projeto é baseada no diretório ou referência. Esses formatos têm o mesmo conteúdo de dados, que é semelhante do Windows `CF_HDROP` Formatar, exceto que as listas de cadeias de caracteres, em vez de ser nomes de arquivo, são um double -`NULL` encerrada a lista de `Projref` cadeias de caracteres (conforme retornado pelo `IVsSolution::GetProjrefOfItem`ou `::GetProjrefOfProject` conforme apropriado).  

Como o destino de soltar (ou operação de colagem da área de transferência), um projeto deve aceitar os dois `CF_VSREFPROJECTITEMS` e `CF_VSSTGPROJECTITEMS`, embora a manipulação exata da operação de arrastar e soltar varia dependendo da natureza do projeto de destino e o projeto de origem. O projeto de origem declara sua natureza, se ele oferece `CF_VSREFPROJECTITEMS` ou `CF_VSSTGPROJECTITEMS`. O destino de soltar compreende sua própria natureza e, portanto, tem informações suficientes para tomar decisões como e se uma mudança, copie ou link deve ser executado. O usuário também modifica qual operação de arrastar e soltar deve ser executada ao pressionar o Ctrl, Shift, ou as teclas Ctrl e Shift. É importante para o destino de soltar corretamente indicam qual operação será executada com antecedência em seu `DragEnter` e `DragOver` métodos. O **Gerenciador de soluções** sabe automaticamente se o projeto de origem e o projeto de destino são o mesmo projeto.  

Especificamente, não há suporte para a arrastar itens de projeto entre instâncias do Visual Studio (por exemplo, de uma instância do devenv.exe para outro). O **Gerenciador de soluções** diretamente também desabilita a isso.  

O usuário deve sempre ser capaz de determinar o efeito de uma operação de arrastar e soltar selecionando um item, arrastando-o para o local de destino, e observa que um dos ponteiros do mouse a seguir aparece antes do item for solto:  

| Ponteiro do mouse | Comando | Descrição |  
| :---: | --- | --- |  
| ![Ícone de "sem soltar" do mouse](../../extensibility/ux-guidelines/media/0706-01_mousenodrop.png "0706 01_MouseNoDrop") | Nenhum menu | Item não pode ser solto no local especificado. |  
| ![Ícone de "cópia" de mouse](../../extensibility/ux-guidelines/media/0706-02_mousecopy.png "0706 02_MouseCopy") | Copiar | Item será copiado para o local de destino. |  
| ![Ícone de mouse "Mover"](../../extensibility/ux-guidelines/media/0706-03_mousemove.png "0706 03_MouseMove") | Mover | Item será movido para o local de destino. |  
| ![Ícone de "add reference" mouse](../../extensibility/ux-guidelines/media/0706-04_mouseaddref.png "0706 04_MouseAddRef") | Adicionar referência | Uma referência para o item selecionado será adicionada ao local de destino. |

#### <a name="reference-based-projects"></a>Projetos de referência  
 A tabela a seguir resume as operações de arrastar e soltar (bem como Recortar/copiar/colar) que devem ser executadas com base na natureza das chaves de item e o modificador de origem pressionado para projetos de destino com base em referenciado:  

| Modificador | Categoria | Item de origem: / Link de referência | Item de origem: sistema de item ou arquivo físico (`CF_HDROP`) |  
| --- | --- | --- | --- |  
| Nenhum modificador | Ação | Mover | Link |  
| Nenhum modificador | Destino | Adiciona a referência ao item original | Adiciona a referência ao item original |  
| Nenhum modificador | Origem | Referência de exclusões ao item original | Retém o item original |  
| Nenhum modificador | Resultado | `DROPEFFECT_MOVE` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_LINK` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento |  
| SHIFT + arrastar | Ação | Mover | Nenhum menu |  
| SHIFT + arrastar | Destino | Adiciona a referência ao item original | Nenhum menu |  
| SHIFT + arrastar | Origem | Referência de exclusões ao item original | Nenhum menu |  
| SHIFT + arrastar | Resultado | `DROPEFFECT_MOVE` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | Nenhum menu |  
| CTRL + arrastar | Ação | Copiar | Nenhum menu |  
| CTRL + arrastar | Destino | Adiciona a referência ao item original | Nenhum menu |  
| CTRL + arrastar | Origem | Mantém a referência ao item original | Nenhum menu |  
| CTRL + arrastar | Resultado | `DROPEFFECT_COPY` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | Nenhum menu |  
| Ctrl + Shift + arrastar | Ação | Link | Link |  
| Ctrl + Shift + arrastar | Destino | Adiciona a referência ao item original | Adiciona a referência ao item original |  
| Ctrl + Shift + arrastar | Origem | Mantém a referência ao item original | Retém o item original |  
| Ctrl + Shift + arrastar | Resultado | `DROPEFFECT_LINK` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_LINK` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento |  
| Ctrl + Shift + arrastar | Observação | Mesmo que o comportamento de arrastar e soltar para atalhos no Windows Explorer. ||  
| Recortar/colar | Ação | Mover | Link |  
| Recortar/colar | Destino | Adiciona a referência ao item original | Adiciona a referência ao item original |  
| Recortar/colar | Origem | Mantém a referência ao item original|Retém o item original |  
| Recortar/colar | Resultado | Item permanece no local original no armazenamento | Item permanece no local original no armazenamento |  
| Copiar/colar | Ação | Copiar | Link |  
| Copiar/colar | Origem | Adiciona a referência ao item original | Adiciona a referência ao item original |  
| Copiar/colar | Resultado | Mantém a referência ao item original | Retém o item original |  
| Copiar/colar | Ação | Item permanece no local original no armazenamento | Item permanece no local original no armazenamento |  

#### <a name="directory-based-projects"></a>Projetos baseados em diretório  
A tabela a seguir resume as operações de arrastar e soltar (bem como Recortar/copiar/colar) que devem ser executadas com base na natureza nas chaves de item e o modificador de origem pressionado para projetos de destino com base no diretório:  


| Modificador | Categoria | Item de origem: / Link de referência | Item de origem: sistema de item ou arquivo físico (`CF_HDROP`) |
|-----------------|----------| - | - |
| Nenhum modificador | Ação | Mover | Mover |
| Nenhum modificador | Destino | Item de cópias para local de destino | Item de cópias para local de destino |
| Nenhum modificador | Origem | Referência de exclusões ao item original | Referência de exclusões ao item original |
| SHIFT + arrastar | Ação | Mover | Mover |
| SHIFT + arrastar | Destino | Item de cópias para local de destino | Item de cópias para local de destino |
| SHIFT + arrastar | Origem | Referência de exclusões ao item original | Exclui o item do local original |
| SHIFT + arrastar | Resultado | `DROPEFFECT_MOVE` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_MOVE` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento |
| CTRL + arrastar | Ação | Copiar | Copiar |
| CTRL + arrastar | Destino | Item de cópias para local de destino | Item de cópias para local de destino |
| CTRL + arrastar | Origem | Mantém a referência ao item original | Mantém a referência ao item original |
| CTRL + arrastar | Resultado | `DROPEFFECT_COPY` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_COPY` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento |
| Ctrl + Shift + arrastar | | Nenhum menu | Nenhum menu |
| Recortar/colar | Ação | Mover | Mover |
| Recortar/colar | Destino | Item de cópias para local de destino | Item de cópias para local de destino |
| Recortar/colar | Origem | Referência de exclusões ao item original | Exclui o item do local original |
| Recortar/colar | Resultado | Item permanece no local original no armazenamento | Item é excluído do local original no armazenamento |
| Copiar/colar | Ação | Copiar | Copiar |
| Copiar/colar | Destino | Adiciona a referência ao item original | Item de cópias para local de destino |
| Copiar/colar | Origem | Retém o item original | Retém o item original |
| Copiar/colar | Resultado | Item permanece no local original no armazenamento | Item permanece no armazenamento de ins local original |

#### <a name="mixed-target-projects"></a>Projetos de destino misto  
A tabela a seguir resume as operações de arrastar e soltar (bem como Recortar/copiar/colar) que devem ser executadas com base na natureza das chaves de item e o modificador de origem pressionado para projetos de destino misto:  

| Modificador | Categoria | Item de origem: / Link de referência | Item de origem: sistema de item ou arquivo físico (`CF_HDROP`) |  
| --- | --- | --- | --- |
| Nenhum modificador | Ação | Mover | Mover |
| Nenhum modificador | Destino | Adiciona a referência ao item original | Item de cópias para local de destino |
| Nenhum modificador | Origem | Referência de exclusões ao item original | Referência de exclusões ao item original |
| Nenhum modificador | Resultado | `DROPEFFECT_ MOVE` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_ MOVE` é retornado como a ação de `::Drop` e item será excluído do local original no armazenamento |
| SHIFT + arrastar | Ação | Mover | Mover |
| SHIFT + arrastar | Destino | Adiciona a referência ao item original | Item de cópias para local de destino |
| SHIFT + arrastar | Origem | Referência de exclusões ao item original | Exclui o item do local original | 
| SHIFT + arrastar | Resultado | `DROPEFFECT_ MOVE` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_ MOVE` é retornado como a ação de `::Drop` e item será excluído do local original no armazenamento |
| CTRL + arrastar | Ação | Copiar | Copiar |
| CTRL + arrastar | Destino | Adiciona a referência ao item original | Item de cópias para local de destino |
| CTRL + arrastar | Origem | Mantém a referência ao item original | Retém o item original |
| CTRL + arrastar | Resultado | `DROPEFFECT_ COPY` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_ COPY` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento |
| Ctrl + Shift + arrastar | Ação | Link | Link |
| Ctrl + Shift + arrastar | Destino | Adiciona a referência ao item original | Adiciona a referência ao item original do código-fonte |
| Ctrl + Shift + arrastar | Origem | Mantém a referência ao item original | Retém o item original |
| Ctrl + Shift + arrastar | Resultado | `DROPEFFECT_ LINK` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento | `DROPEFFECT_ LINK` é retornado como a ação de `::Drop` e item permanece no local original no armazenamento |
| Recortar/colar | Ação | Mover | Mover |
| Recortar/colar | Destino | Item de cópias para local de destino | Item de cópias para local de destino |
| Recortar/colar | Origem | Referência de exclusões ao item original | Exclui o item do local original |
| Recortar/colar | Resultado | Item permanece no local original no armazenamento | Item é excluído do local original no armazenamento |
| Copiar/colar | Ação | Copiar | Copiar |
| Copiar/colar | Destino | Adiciona a referência ao item original | Item de cópias para local de destino |
| Copiar/colar | Origem | Retém o item original | Retém o item original |
| Copiar/colar | Resultado | Item permanece no local original no armazenamento | Item permanece no local original no armazenamento |

Esses detalhes devem ser levados em consideração ao implementar o arrastar para o **Gerenciador de soluções**:  

-   Design para vários cenários de seleção.  

-   Nomes de arquivo (caminho completo) devem ser exclusivos em todo o projeto de destino ou o descarte não deve ser permitido.  

-   Nomes de pastas devem ser exclusivos (diferencia maiusculas de minúsculas) no nível do qual eles são descartados.  

-   Há diferenças de comportamento entre os arquivos que estão abertos ou fechados no momento de arrastar (não mencionada nos cenários acima).  

-   Arquivos de nível superior se comportam de forma ligeiramente diferente do que os arquivos em pastas.  

Outro problema que deve estar atento é como lidar com operações de movimentação em itens que têm editores ou designers abertos. O comportamento esperado é da seguinte maneira (isso se aplica a todos os tipos de projeto):  

1.  Se o editor Abrir/designer não tem alterações não salvas, em seguida, a janela de editor/designer deve ser silenciosamente fechada.  

2.  Se o editor Abrir/designer tiver alterações não salvas, em seguida, a origem de arrastar deve esperar para o descarte ocorrer e, em seguida, peça ao usuário para salvar as alterações não confirmadas em documentos abertos antes de fechar a janela com um prompt semelhante ao seguinte :  

    ```  
    ==========================================================   
         One or more open documents have unsaved changes.  
    Do you want to save uncommitted changes before proceeding?   
                      [Yes]  [No]  [Cancel]   
    ==========================================================  
    ```  

Isso fornece ao usuário a oportunidade de salvar o trabalho em andamento antes do destino torna suas cópias. Um novo método `IVsHierarchyDropDataSource2::OnBeforeDropNotify` foi adicionado para habilitar esse tratamento.  

O destino, em seguida, copiar o estado do item como ele está no armazenamento (não incluindo as alterações não salvas no editor, se o usuário escolheu **não**). Depois que o destino foi concluída a sua cópia (em `IVsHierarchyDropDataSource::Drop`), a fonte tem a oportunidade para concluir a parte de exclusão da operação de movimentação (em `IVsHierarchyDropDataSource::OnDropNotify`).  

Qualquer editores com alterações não salvas devem ser deixados abertos. Para esses documentos com alterações não salvas, isso significa que a parte da cópia da operação de movimentação será executada, mas a parte de exclusão será anulada. Em um cenário de seleção de vários quando o usuário escolhe **não**, esses documentos com alterações não salvas não devem ser fechados ou removidos, mas devem ser fechados e removidos aqueles sem alterações não salvas.