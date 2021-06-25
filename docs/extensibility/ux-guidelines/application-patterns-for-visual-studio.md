---
title: Padrões de aplicativo para o Visual Studio | Microsoft Docs
description: Saiba mais sobre a diferença entre janelas de documentos, janelas de ferramentas e caixas de diálogo sem janela restrita, incluindo padrões de uso de janelas para novos recursos para o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: 8ed68602-4e28-46fe-b39f-f41979b308a2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2726c7096bbf4606fbab2c32b01ffd197549e13c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899180"
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
As janelas de ferramentas são de instância única ou de várias instâncias. Algumas janelas de ferramentas de instância única podem estar associadas à janela ativa do documento, enquanto as janelas de ferramentas de várias instâncias podem não estar. As janelas de ferramentas de várias instâncias respondem ao **comando Janela &gt; Nova Janela** criando uma nova instância da janela. A imagem a seguir ilustra uma janela de ferramentas que habilita o comando Nova Janela quando uma instância da janela está ativa:

![Janela de ferramentas habilitando o comando 'Nova Janela' quando uma instância da janela está ativa](../../extensibility/ux-guidelines/media/0702-02_toolwindowenablingcommand.png "0702-02_ToolWindowEnablingCommand")<br />Janela de ferramentas habilitando o comando 'Nova Janela' quando uma instância da janela está ativa

As janelas de ferramentas de instância única podem ser ocultas ou mostradas, enquanto as janelas de ferramentas de várias instâncias podem ser fechadas, bem como ocultas. Todas as janelas de ferramentas podem ser encaixadas, vinculadas a guias, flutuantes ou definidas como uma janela filho MDI (interface Multiple-Document) (semelhante a uma janela de documento). Todas as janelas de ferramentas devem responder aos comandos de gerenciamento de janela apropriados no menu Janela:

![Comandos de gerenciamento de janela no menu Visual Studio Janela](../../extensibility/ux-guidelines/media/0702-03_windowmanagementcontrols.png "0702-03_WindowManagementControls")<br />Comandos de gerenciamento de janela no menu Visual Studio Janela

#### <a name="document-specific-tool-windows"></a>Janelas de ferramentas específicas do documento
Algumas janelas de ferramentas são projetadas para mudar com base em um determinado tipo de documento. Essas janelas são atualizadas continuamente para refletir a funcionalidade aplicável à janela de documento ativa no IDE.

Exemplos de janelas de ferramentas cujo conteúdo muda para refletir o editor selecionado são a Caixa de Ferramentas e o Contorno do Documento. Essas janelas mostram uma marca-d'água quando um editor tem foco que não oferece contexto para a janela.

#### <a name="navigable-list-tool-windows"></a>Janelas da ferramenta de lista navegável
Algumas janelas de ferramentas exibem uma lista de itens navegáveis com os que o usuário pode interagir. Nesse tipo de janela, sempre deve haver comentários para o item atual na lista, mesmo se a janela estiver inativa. A lista deve responder aos comandos **GoToNextLocation** e **GoToPrevLocation** alterando também o item selecionado no momento na janela

Exemplos de janelas de ferramentas de lista navegável são a Gerenciador de Soluções e a janela Encontrar Resultados.

### <a name="tool-window-types"></a>Tipos de janela de ferramentas

#### <a name="common-tool-windows-and-their-functions"></a>Janelas de ferramentas comuns e suas funções

**Janelas de ferramentas hierárquicas**

| Janela de ferramentas | Função |
| --- | --- |
| Gerenciador de Soluções | Uma árvore hierárquica que exibe uma lista de documentos contidos em projetos, arquivos diversos e itens de solução. A exibição dos itens em projetos é definida pelo pacote que possui o tipo de projeto (por exemplo, tipos baseados em referência, baseados em diretório ou de modo misto). |
| Exibição de Classe | Uma árvore hierárquica das classes e vários elementos no conjunto de trabalho de documentos, independentemente dos próprios arquivos. |
| Gerenciador de Servidores | Uma árvore hierárquica que exibe todos os servidores e conexões de dados na solução. |
| Estrutura de Tópicos do Documento | A estrutura hierárquica do documento ativo. |

**Janelas de ferramentas de grade**

| Janela de ferramentas | Função |
| --- | --- |
| Propriedades | Uma grade que exibe uma lista de propriedades para o objeto selecionado, juntamente com seletores de valor para editar essas propriedades. |
| Lista de Tarefas | Uma grade que permite que o usuário crie/edite/exclua tarefas e comentários. |

**Janelas da ferramenta de conteúdo**

| Janela de ferramentas | Função |
| --- | --- |
| Ajuda | Uma janela que permite que os usuários acessem vários métodos de obter ajuda, de "Como fazer?" vídeos para fóruns do MSDN. |
| Ajuda dinâmica | Uma janela de ferramentas que exibe links para tópicos de ajuda aplicáveis à seleção atual. |
| Pesquisador de Objetos | Um quadro de duas colunas com uma lista de componentes de objeto hierárquico no painel esquerdo e as propriedades e métodos do objeto na coluna direita. |

**Janelas da ferramenta de caixa de diálogo**

| Janela de ferramentas | Função |
| --- | --- |
| Localizar | Uma caixa de diálogo que permite que o usuário encontre ou encontre e substitua em vários arquivos dentro da solução. |
| Localização Avançada | Uma caixa de diálogo que permite que o usuário encontre ou encontre e substitua em vários arquivos dentro da solução. |

**Outras janelas de ferramentas**

::: moniker range="vs-2017"

| Janela de ferramentas | Função |
| --- | --- |
| Caixa de Ferramentas | A janela de ferramentas usada para armazenar elementos que serão descartados em superfícies de design, fornecendo uma fonte de arrastar consistente para todos os designers. |
| Start Page | O portal do usuário para Visual Studio, com acesso a feeds de notícias do desenvolvedor, Visual Studio ajuda e projetos recentes. Os usuários também podem criar páginas de início personalizadas copiando o arquivo StartPage.xaml do diretório de arquivos de programas "Common7\IDE\StartPages Visual Studio para a pasta StartPages no diretório de documentos do Visual Studio e editando o XAML manualmente ou abrindo-o no Visual Studio ou em outro editor de \" código. |

::: moniker-end

::: moniker range=">=vs-2019"

| Janela de ferramentas | Função |
| --- | --- |
| Caixa de Ferramentas | A janela de ferramentas usada para armazenar elementos que serão descartados em superfícies de design, fornecendo uma fonte de arrastar consistente para todos os designers. |

::: moniker-end

**Janelas de ferramentas do depurador**

| Janela de ferramentas | Função |
| --- | --- |
| Autos ||
| Imediata ||
| Saída | A janela de saída pode ser usada sempre que você tiver eventos textuais ou status a serem declarados. |
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

## <a name="document-editor-conventions"></a><a name="BKMK_DocumentEditorConventions"></a> Convenções do editor de documentos

### <a name="document-interactions"></a>Interações de documento
O "documento bem" é o maior espaço dentro do IDE e é onde o usuário geralmente concentra sua atenção para concluir suas tarefas, auxiliadas por janelas de ferramentas complementares. Os editores de documentos representam as unidades fundamentais de trabalho que o usuário abre e salva em Visual Studio. Eles mantêm uma forte noção de seleção vinculada a Gerenciador de Soluções ou outras janelas de hierarquia ativas. O usuário deve ser capaz de apontar para uma dessas janelas de hierarquia e saber onde o documento está contido e sua relação com a solução, o projeto ou outro objeto raiz fornecido por um pacote Visual Studio.

A edição de documentos requer uma experiência de usuário consistente. Para permitir que o usuário se concentre na tarefa em mãos, em vez de no gerenciamento de janelas e na descoberta de comandos, selecione uma estratégia de exibição de documento que melhor se ajuste às tarefas do usuário para editar esse tipo de documento.

#### <a name="common-interactions-for-the-document-well"></a>Interações comuns para o documento também

- Mantenha um modelo de interação consistente nas experiências comuns **de Novo Arquivo** e Abrir **Arquivo.**

- Atualize a funcionalidade relacionada em janelas e menus relacionados quando a janela do documento for aberta.

- Os comandos de menu são adequadamente integrados a menus comuns, como **Editar**, **Formatar** e **Exibir** menus. Se uma quantidade significativa de comandos especializados estiver disponível, um novo menu poderá ser criado. Esse novo menu deve ficar visível somente quando o documento tiver foco.

- Uma barra de ferramentas inserida pode ser colocada na parte superior do editor. Isso é preferível a ter uma barra de ferramentas separada que aparece fora do editor.

- Sempre mantenha uma seleção na janela Gerenciador de Soluções hierarquia ativa semelhante.

- Clicar duas vezes em um documento no Gerenciador de Soluções deve executar a mesma ação que **Abrir**.

- Se mais de um editor puder ser usado em um tipo de documento, o usuário deverá  ser capaz de substituir ou redefinir a ação padrão em um determinado tipo de documento usando a caixa de diálogo Abrir com clicando com o botão direito do mouse no arquivo e selecionando **Abrir com** no menu de atalho.

- Não crie um assistente em um documento também.

### <a name="user-expectations-for-specific-document-types"></a>Expectativas do usuário para tipos de documentos específicos
Há vários tipos básicos diferentes de editores de documentos e cada um tem um conjunto de interações consistentes com outros do mesmo tipo.

- **Editor baseado em texto: editor** de código, arquivos de log

- **Superfície de design:** Designer de formulários do WPF, formulários do Windows

- **Editor de estilo de diálogo:** Designer de Manifesto, propriedades do projeto

- **Designer de modelo:** designer de fluxo de trabalho, codemap, diagrama de arquitetura, progressão

Também há vários tipos que não são editores que usam o documento também. Embora eles não editem documentos em si, eles precisam seguir as interações padrão para janelas de documentos.

- **Relatórios:** Relatório do IntelliTrace, relatório do Hyper-V, relatório do profiler

- **Painel:** Hub de Diagnóstico

#### <a name="text-based-editors"></a>Editores baseados em texto

- O documento participa do modelo de guia de visualização, permitindo a visualização do documento sem abri-lo.

- A estrutura do documento pode ser representada dentro de uma janela de ferramentas, como um contorno de documento.

- O IntelliSense (se apropriado) se comportará consistentemente com outros editores de código.

- Pop-ups ou interface do usuário adaptativa seguem estilos e padrões semelhantes para a interface do usuário semelhante existente, como o CodeLens.

- As mensagens sobre o status do documento serão apresentadas em um controle de barra de informações na parte superior do documento ou na barra de status.

- O usuário deve ser capaz de personalizar a aparência de fontes e cores usando uma página Ferramentas **> Opções,** a página Fontes e Cores compartilhadas ou uma específica para o editor.

#### <a name="design-surfaces"></a>Superfícies de design

- Um designer vazio deve ter uma marca-d'água na superfície indicando como começar.

- Os mecanismos de alternação de exibição seguirão padrões existentes, como clicar duas vezes para abrir um editor de código ou guias dentro da janela do documento, permitindo a interação com ambos os painéis.

- A adição de elementos à superfície de design deve ser feita por meio da Caixa de Ferramentas, a menos que uma janela de ferramentas altamente específica seja necessária.

- Os itens na superfície seguirão um modelo de seleção consistente.

- As barras de ferramentas inseridas contêm apenas comandos específicos de documento, não comandos comuns, como **Salvar**.

#### <a name="dialog-style-editors"></a>Editores de estilo de diálogo

- O layout de controle deve seguir as convenções normais de layout da caixa de diálogo.

- As guias dentro do editor não devem corresponder à aparência das guias do documento, elas devem corresponder a um dos dois estilos de guia interior permitidos.

- Os usuários devem ser capazes de interagir com os controles usando apenas o teclado; ativando o editor e tabulando controles ou usando mnemônicos padrão.

- O designer deve usar o modelo Salvar comum. Nenhum botão Geral salvar ou fazer commit deve ser colocado na superfície, embora outros botões possam ser apropriados.

#### <a name="model-designers"></a>Designers de modelo

- Um designer vazio deve ter uma marca-d'água na superfície indicando como começar.

- A adição de elementos à superfície de design deve ser feita por meio da Caixa de Ferramentas.

- Os itens na superfície seguirão um modelo de seleção consistente.

- As barras de ferramentas inseridas contêm apenas comandos específicos de documento, não comandos comuns, como **Salvar**.

- Uma legenda pode aparecer na superfície, indicando ou uma marca-d'água.

- O usuário deve ser capaz de personalizar a aparência das fontes/cores usando uma página Ferramentas **> Opções,** a página Fontes e Cores compartilhada ou uma específica para o editor.

#### <a name="reports"></a>Relatórios

- Os relatórios normalmente são somente informações e não participam do modelo Salvar. No entanto, eles podem incluir interação, como links para outras informações relevantes ou seções que se expandem e se ressuem.

- A maioria dos comandos na superfície deve ser hiperlinks, não botões.

- O layout deve incluir um header e seguir as diretrizes de layout de relatório padrão.

#### <a name="dashboards"></a>Painéis

- Os painéis não têm um modelo de interação em si, mas servem como um meio de oferecer uma variedade de outras ferramentas.

- Eles não participam do modelo Salvar.

- Os usuários devem ser capazes de interagir com os controles usando apenas o teclado, ativando o editor e tabulando controles ou usando mnemônicos padrão.

## <a name="dialogs"></a><a name="BKMK_Dialogs"></a> Diálogos

### <a name="introduction"></a>Introdução
Os diálogos Visual Studio normalmente devem dar suporte a uma unidade discreta do trabalho do usuário e, em seguida, ser ignorados.

Se você tiver determinado que precisa de uma caixa de diálogo, terá três opções, em ordem de preferência:

1. Integre seus recursos a uma das caixas de diálogo compartilhadas Visual Studio.

2. Crie sua própria caixa de diálogo usando um padrão encontrado em uma caixa de diálogo semelhante existente.

3. Crie um novo diálogo seguindo as diretrizes de interação e layout.

Esta seção descreve como escolher o padrão de diálogo correto em fluxos Visual Studio fluxos de trabalho e as convenções comuns para design de diálogo.

### <a name="themes"></a>Temas
Os diálogos Visual Studio seguir um dos dois estilos básicos:

#### <a name="standard-unthemed"></a>Standard (sem-themed)
A maioria dos diálogos são caixas de diálogo de utilitário padrão e devem ser sem-marca. Não reorganizar controles comuns ou tentar criar botões ou controles "modernos" estilizados. Controles e aparência cromada seguem [as diretrizes](/windows/desktop/uxguide/win-dialog-box)padrão de interação da Área de Trabalho do Windows para caixas de diálogo .

#### <a name="themed"></a>Temáticos
Caixas de diálogo de "assinatura" de especialização podem ser temas. Os diálogos tem uma aparência distinta, que também tem alguns padrões de interação especiais associados ao estilo. A caixa de diálogo será tema somente se ela atender a estes requisitos:

- A caixa de diálogo é uma experiência comum que será vista e usada com frequência ou por muitos usuários (por exemplo, a caixa **de diálogo Novo** Projeto.

- A caixa de diálogo contém elementos de marca de produto proeminentes (por exemplo, a **caixa de diálogo Configurações da** Conta).

- A caixa de diálogo aparece como parte integrante de um fluxo maior que inclui outros diálogos com temas (por exemplo, a caixa de diálogo **Adicionar Serviço** Conectado).

- A caixa de diálogo é uma parte importante de uma experiência que desempenha um papel estratégico na promoção ou diferenciação de uma versão do produto.

Ao criar um diálogo temático, use as cores de ambiente apropriadas e siga os padrões corretos de layout e interação. (Consulte [Layout para Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).)

### <a name="dialog-design"></a>Design da caixa de diálogo
Os diálogos bem projetados levam em consideração os seguintes elementos:

- A tarefa do usuário que tem suporte

- O estilo, o idioma e a terminologia do texto da caixa de diálogo

- Escolha de controle e convenções de interface do usuário

- Especificação de layout visual e alinhamento de controle

- Acesso pelo teclado

#### <a name="content-organization"></a>Organização de conteúdo
Considere as diferenças entre esses tipos básicos de diálogos:

- [Caixas de diálogo simples](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_SimpleDialogs) apresentam controles em uma única janela modal. A apresentação pode incluir variações de padrões de controle complexos, incluindo um selador de campo ou uma barra de ícones.

- [Caixas de diálogo em camadas](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_LayeredDialogs) são usadas para fazer o máximo de imóveis de tela quando uma única parte da interface do usuário é composta por vários grupos de controles. Os agrupamentos da caixa de diálogo são "em camadas" por meio de controles de tabulação, controles de lista de navegação ou botões para que o usuário possa escolher qual grupo ver a qualquer momento.

- [Os assistentes](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Wizards) são úteis para direcionar o usuário por meio de uma sequência lógica de etapas até a conclusão de uma tarefa. Uma série de opções são oferecidas em painéis sequenciais, às vezes introduzindo diferentes fluxos de trabalho ("branches") dependendo de uma escolha feita no painel anterior.

#### <a name="simple-dialogs"></a><a name="BKMK_SimpleDialogs"></a> Caixas de diálogo simples
Uma caixa de diálogo simples é uma apresentação de controles em uma única janela modal. Essa apresentação pode incluir variações de padrões de controle complexos, como um selador de campo. Para caixas de diálogo simples, siga o layout geral padrão, bem como qualquer layout específico necessário para grupos de controle complexos.

![>Criar Chave de Nome Forte é um exemplo de uma caixa de diálogo simples Visual Studio.](../../extensibility/ux-guidelines/media/0704-01_createstrongnamekey.png "0704-01_CreateStrongNameKey")<br />Criar Chave de Nome Forte é um exemplo de uma caixa de diálogo simples no Visual Studio.

#### <a name="layered-dialogs"></a><a name="BKMK_LayeredDialogs"></a> Caixas de diálogo em camadas
As caixas de diálogo em camadas incluem guias, painéis e árvores inseridas. Eles são usados para maximizar a propriedade quando há vários grupos de controles oferecidos em uma única parte da interface do usuário. Os agrupamentos são em camadas para que o usuário possa escolher qual grupo ver a qualquer momento.

No caso mais simples, o mecanismo para alternar entre os grupos é um controle de tabulação. Há várias alternativas disponíveis. Consulte Priorizando e em camadas para saber como escolher o estilo mais apropriado.

A **caixa de diálogo &gt; Opções** de Ferramentas é um exemplo de uma caixa de diálogo em camadas usando uma árvore inserida:

![Ferramentas > Opções é um exemplo de uma caixa de diálogo em camadas Visual Studio.](../../extensibility/ux-guidelines/media/0704-02_toolsoptions.png "0704-02_ToolsOptions")<br />Ferramentas > Opções é um exemplo de uma caixa de diálogo em camadas Visual Studio.

#### <a name="wizards"></a><a name="BKMK_Wizards"></a> Assistentes
Os assistentes são úteis para direcionar o usuário por meio de uma sequência lógica de etapas na conclusão de uma tarefa. Uma série de opções são oferecidas em painéis sequenciais e o usuário deve continuar em cada etapa antes de prosseguir para a próxima. Quando padrões suficientes estão disponíveis, o **botão** Concluir é habilitado.

 Assistentes modais são usados para tarefas que:

- Conter ramificação, em que caminhos diferentes são oferecidos dependendo das opções do usuário

- Conter dependências entre etapas, em que as etapas subsequentes dependem da entrada do usuário das etapas anteriores

- São suficientemente complexos que a interface do usuário deve ser usada para explicar as opções oferecidas e os possíveis resultados em cada etapa

- São transacionais, exigindo que um conjunto de etapas seja concluído em sua totalidade antes que as alterações sejam confirmados

### <a name="common-conventions"></a>Convenções comuns
Para obter o design e a funcionalidade ideais com seus diálogos, siga estas convenções sobre tamanho da caixa de diálogo, posição, padrões, configuração e alinhamento de controle, texto da interface do usuário, barras de título, botões de controle e chaves de acesso.

Para diretrizes específicas de [layout,](../../extensibility/ux-guidelines/layout-for-visual-studio.md)consulte Layout para Visual Studio .

#### <a name="size"></a>Tamanho
As caixas de diálogo devem caber em uma resolução de tela mínima de 1024x768 e o tamanho inicial da caixa de diálogo não deve exceder 900 x 700 pixels. Os diálogos podem ser reizáveis, mas não é um requisito.

Há duas recomendações para diálogos reizáveis:

1. Que um tamanho mínimo é definido para a caixa de diálogo que otimizará o conjunto de controles sem recorte e se ajustará para acomodar o crescimento razoável da localização.

2. Que o tamanho dimensionado pelo usuário persiste de sessão em sessão. Por exemplo, se o usuário dimensionar uma caixa de diálogo para 150%, um lançamento subsequente da caixa de diálogo será exibido em 150%.

#### <a name="position"></a>Posição
As caixas de diálogo devem aparecer centralizadas no IDE na primeira iniciação. A última posição de diálogos não reizáveis não precisa ser persistida, portanto, elas aparecerão centralizadas em lançamentos subsequentes.

Para caixas de diálogo reizáveis, o tamanho deve ser persistido em lançamentos subsequentes. Para diálogos modais reizáveis, a posição não precisa ser persistida. Exibi-los centralizados no IDE impede que a caixa de diálogo apareça em uma posição imprevisível ou inutilizável quando a configuração de exibição do usuário foi alterada.

Para caixas de diálogo sem modo que podem ser reposicionadas, a posição do usuário deve ser mantida em lançamentos subsequentes, pois o diálogo pode ser usado com frequência como parte integrante de um fluxo de trabalho maior.

Quando os diálogos devem gerar outros diálogos, o diálogo mais alto deve estar em cascata para a direita e para baixo do pai para que seja óbvio para o usuário que ele navegue até um novo local.

#### <a name="modality"></a>Modalidade
Ser modal significa que os usuários precisam concluir ou cancelar a caixa de diálogo antes de continuar. Como as caixas de diálogo modais bloqueiam a interação do usuário com outras partes do ambiente, o fluxo de tarefas do recurso deve usá-los da maneira mais esparsa possível. Quando uma operação modal é necessária, Visual Studio tem várias caixas de diálogo compartilhadas nas que você pode integrar seus recursos. Se você precisa criar um novo diálogo, siga o padrão de interação de uma caixa de diálogo existente com funcionalidade semelhante.

Quando os usuários precisam executar duas  atividades  ao mesmo tempo, como Encontrar e Substituir ao escrever um novo código, a caixa de diálogo deve ser sem modos para que o usuário possa alternar facilmente entre elas. Visual Studio geralmente usa janelas de ferramentas para esse tipo de tarefa vinculada com suporte do editor.

#### <a name="control-configuration"></a>Configuração de controle
Seja consistente com as configurações de controle existentes que realizem a mesma coisa em Visual Studio.

#### <a name="title-bars"></a>Barras de título

- O texto na barra de título deve refletir o nome do comando que o iniciou.

- Nenhum ícone deve ser usado nas barras de título da caixa de diálogo. Nos casos em que o sistema requer um, use o logotipo Visual Studio segurança.

- As caixas de diálogo não devem ter botões de minimização ou maximização.

- Os botões de ajuda na barra de título foram preterido. Não os adicione a novos diálogos. Quando existirem, eles deverão iniciar um tópico de Ajuda que seja conceitualmente relevante para a tarefa.

  ![Especificações de diretrizes para barras de título Visual Studio diálogos](../../extensibility/ux-guidelines/media/0704-03_titlebarspecs.png "0704-03_TitleBarSpecs")<br />Especificações de diretrizes para barras de título Visual Studio diálogos

#### <a name="control-buttons"></a>Botões de controle
Em geral, os **botões** **OK**, Cancelar **e** Ajuda devem ser organizados horizontalmente no canto inferior direito da caixa de diálogo. A pilha vertical alternativa será permitida se uma caixa de diálogo tiver vários outros botões na parte inferior da caixa de diálogo que apresentariam confusão visual com os botões de controle.

![Configurações aceitáveis para botões de controle Visual Studio diálogos](../../extensibility/ux-guidelines/media/0704-04_controlbuttonconfig.png "0704-04_ControlButtonConfig")<br />Configurações aceitáveis para botões de controle Visual Studio diálogos

A caixa de diálogo deve incluir um botão de controle padrão. Para determinar o melhor comando a ser usado como o padrão, escolha entre as seguintes opções (listadas em ordem de precedência):

- Escolha o comando mais seguro e seguro como o padrão. Isso significa escolher o comando com maior probabilidade de evitar a perda de dados e evitar o acesso não intencional ao sistema.

- Se a perda de dados e a segurança não são fatores, escolha o comando padrão com base na conveniência. Incluir o comando mais provável como padrão melhorará o fluxo de trabalho do usuário quando a caixa de diálogo dá suporte a tarefas frequentes ou repetitivas.

Evite escolher uma ação permanentemente destrutiva para o comando padrão. Se esse comando estiver presente, escolha um comando mais seguro como o padrão.

#### <a name="access-keys"></a>Chaves de acesso
Não use chaves de acesso para **os botões OK,** **Cancelar** ou **Ajuda.** Esses botões são mapeados para teclas de atalho por padrão:

| Nome do botão | Atalho de teclado |
| --- | --- |
| OK | Digite |
| Cancelar | Esc |
| Ajuda | F1 |

#### <a name="imagery"></a>Imagens
Use imagens com moderação em diálogos. Não use ícones grandes em caixas de diálogo simplesmente para usar espaço. Use imagens somente se elas são uma parte importante da transmissão da mensagem para o usuário, como ícones de aviso ou animações de status.

### <a name="prioritizing-and-layering"></a><a name="BKMK_PrioritizingAndLayering"></a> Priorizando e em camadas

#### <a name="prioritizing-your-ui"></a>Priorizando sua interface do usuário
Pode ser necessário colocar determinados elementos da interface do usuário à frente e colocar opções e comportamentos mais avançados (incluindo comandos obscurecidos) em diálogos. Traga a funcionalidade comumente usada para a frente, dando espaço para ela e tornando-a visível por padrão na interface do usuário com um rótulo de texto quando a caixa de diálogo é mostrada.

#### <a name="layering-your-ui"></a>Em camadas da interface do usuário
Se você tiver determinado que uma caixa de diálogo é necessária, mas a funcionalidade relacionada que você deseja apresentar ao usuário vai além do que pode ser exibido em uma caixa de diálogo simples, você precisará fazer a camada da interface do usuário. Os métodos de camada mais comuns Visual Studio são guias e painéis. Em alguns casos, regiões que podem ser expandidas e colapsadas podem ser apropriadas. A interface do usuário adaptável geralmente não é recomendada Visual Studio.

Há vantagens e desvantagens para diferentes métodos de camadas da interface do usuário por meio de controles de tabulação. Revise a lista abaixo para garantir que você está escolhendo uma técnica de camadas apropriada para sua situação.

##### <a name="tabbing"></a>Tabulação

| Mecanismo de alternação | Vantagens e uso apropriado | Desvantagens e uso inadequado |
| --- | --- | --- |
| Controle guia | Agrupar logicamente páginas de diálogo em conjuntos relacionados<br /><br />Útil para menos de cinco páginas (ou o número de guias que cabem em uma linha na caixa de diálogo) de controles relacionados na caixa de diálogo<br /><br />Os rótulos de tabulação devem ser curtos: uma ou duas palavras que podem identificar facilmente o conteúdo<br /><br />Um estilo de diálogo do sistema comum<br /><br />Exemplo: propriedades **Explorador de Arquivos &gt; item** | Tornar rótulos curtos descritivos pode ser difícil<br /><br />Geralmente, não escala mais de cinco guias em uma caixa de diálogo<br /><br />Inadequado se você tiver muitas guias para uma linha (use uma técnica de camada alternativa)<br /><br />Não extensível |
| Navegação na barra lateral | Dispositivo de alternação simples que pode acomodar mais categorias do que guias<br /><br />Lista simples de categorias (sem hierarquia)<br /><br />Extensível<br /><br />Exemplo: **Personalizar... &gt; Adicionar comando** | Não é um bom uso de espaço horizontal se houver menos de três grupos<br /><br />A tarefa pode ser mais adequada para uma lista listada |
| Controle de árvore | Permite categorias ilimitadas<br /><br />Permite agrupar e/ou hierarquia de categorias<br /><br />Extensível<br /><br />Exemplo: **Opções de &gt; ferramentas** | Hierarquias muito aninhadas podem causar rolagem horizontal excessiva<br /><br />Visual Studio tem uma superabundância de exibições de árvore |
| Assistente | Ajuda com a conclusão da tarefa orientando o usuário por meio de etapas sequenciais baseadas em tarefas: o assistente representa uma tarefa de alto nível e os painéis individuais representam as subtarefas necessárias para realizar a tarefa geral<br /><br />Útil quando a tarefa cruza os limites da interface do usuário, como quando o usuário teria que usar vários editores e janelas de ferramentas para concluir a tarefa<br /><br />Útil quando a tarefa requer ramificação<br /><br />Útil quando a tarefa contém dependências entre etapas<br /><br />Útil quando várias tarefas semelhantes com uma bifurcação de decisão podem ser apresentadas em uma caixa de diálogo para reduzir o número de diferentes diálogos semelhantes | Inadequado para qualquer tarefa que não exige um fluxo de trabalho sequencial<br /><br />Os usuários podem ficar sobrecarregados e confusos por um assistente com muitas etapas<br /><br />Os assistentes têm propriedades de tela inerentemente limitadas |

##### <a name="hallways-or-dashboards"></a>Painéis ou painéis
Painéis e painéis são caixas de diálogo ou painéis que servem como pontos de lançamento para outros diálogos e janelas. A "responsabilidade" bem projetada imediatamente revela apenas as opções, comandos e configurações mais comuns, permitindo que o usuário realize tarefas comuns prontamente. Assim como uma equipe do mundo real fornece entradas para acessar as salas atrás delas, aqui, a interface do usuário menos comum é coletada em "salas" separadas (geralmente outras caixas de diálogo) de funcionalidades relacionadas que podem ser acessadas do grupo principal.

Como alternativa, uma interface do usuário que oferece todas as funcionalidades disponíveis em uma única coleção em vez de refactorar a funcionalidade menos comum em locais separados é simplesmente um painel.

![Conceito básico para expor a interface do usuário adicional no Outlook](../../extensibility/ux-guidelines/media/0704-08_hallway.png "0704-08_Hallway")<br />Conceito básico para expor a interface do usuário adicional no Outlook

##### <a name="adaptive-ui"></a>Interface do usuário adaptável
Mostrar ou ocultar a interface do usuário com base no uso ou na experiência autorre reportada de um usuário é outra maneira de apresentar a interface do usuário necessária enquanto oculta outras partes. Isso não é recomendado no Visual Studio, pois os algoritmos para decidir quando mostrar ou ocultar a interface do usuário podem ser complicados e as regras sempre estarão erradas para alguns conjunto de casos.

## <a name="projects"></a><a name="BKMK_Projects"></a> Projetos

### <a name="projects-in-the-solution-explorer"></a>Projetos no Gerenciador de Soluções
A maioria dos projetos é classificada como baseada em referência, baseada em diretório ou misturada. Todos os três tipos de projetos têm suporte simultaneamente no Gerenciador de Soluções. A raiz da experiência do usuário ao trabalhar com projetos ocorre dentro dessa janela. Embora nós de projeto diferentes sejam projetos de tipo de referência, diretório ou modo misto, há um padrão de interação comum que deve ser aplicado como um ponto de partida antes de divergentes em padrões de usuário específicos do projeto.

Os projetos devem sempre:

- Dar suporte à capacidade de adicionar pastas de projeto para organizar o conteúdo do projeto

- Manter um modelo consistente para persistência de projeto

Os projetos também devem manter modelos de interação consistentes para:

- Removendo itens de projeto

- Salvando documentos

- Edição de propriedade do projeto

- Editando o projeto em uma exibição alternativa

- Operações do tipo "arrastar e soltar"

### <a name="drag-and-drop-interaction-model"></a>Modelo de interação do tipo "arrastar e soltar"
Os projetos normalmente se classificam como baseados em referência (capazes de persistir apenas referências a itens de projeto no armazenamento), baseados em diretório (capazes de persistir apenas itens de projeto fisicamente armazenados na hierarquia de um projeto) ou mistos (capazes de persistir referências ou itens físicos). O IDE acomoda todos os três tipos de projetos simultaneamente dentro do **Gerenciador de Soluções**.

De uma perspectiva do tipo "arrastar e soltar", as seguintes características devem se aplicar a cada tipo de projeto dentro do **Gerenciador de Soluções**:

- **Projeto baseado em referência:** O ponto principal é que o projeto está arrastando uma referência para um item no armazenamento. Quando um projeto baseado em referência atua como uma origem para uma operação de movimentação, ele só deve remover a referência ao item do projeto. Na verdade, o item não deve ser excluído do disco rígido. Quando um projeto baseado em referência atua como um destino para uma operação de movimentação (ou cópia), ele deve adicionar uma referência ao item de origem original sem fazer uma cópia privada do item.

- **Projeto baseado em diretório:** De um ponto de vista do tipo "arrastar e soltar", o projeto está arrastando o item físico em vez de uma referência. Quando um projeto baseado em diretório atua como uma origem para uma operação de movimentação, ele deve acabar excluindo o item físico do disco rígido, bem como removendo-o do projeto. Quando um projeto baseado em diretório atua como um destino para uma operação de movimentação (ou cópia), ele deve fazer uma cópia do item de origem em seu local de destino.

- **Projeto de destino misto:** De um ponto de vista do tipo "arrastar e soltar", o comportamento desse tipo de projeto é baseado na natureza do item que está sendo arrastado (uma referência a um item no armazenamento ou ao próprio item). O comportamento correto para referências e itens físicos é descrito acima.

Se houvesse apenas um tipo de projeto no **Gerenciador de Soluções**, as operações do tipo "arrastar e soltar" seriam simples. Como cada sistema de projeto tem a capacidade de definir seu próprio comportamento do tipo "arrastar e soltar", determinadas diretrizes (com base no comportamento de arrastar e soltar do Windows Explorer) devem ser seguidas para garantir uma experiência previsível do usuário:

- Uma operação de arrastar não modificada no **Gerenciador de Soluções** (quando as teclas Ctrl ou Shift não são mantidas para baixo) devem resultar em uma operação de movimentação.

- A operação shift-drag também deve resultar em uma operação de movimentação.

- A operação ctrl-drag deve resultar em uma operação de cópia.

- Sistemas de projeto mistos e baseados em referência suportam a noção de adição de um link (ou referência) ao item de origem. Quando esses projetos são o destino de uma operação do tipo "arrastar e soltar" (quando **Ctrl + Shift** é mantido para baixo), isso deve resultar em uma referência ao item que está sendo adicionado ao projeto

Nem todas as operações do tipo "arrastar e soltar" são sensíveis entre combinações de projetos baseados em referência, baseados em diretório e mistos. Em particular, é problemático tentar permitir uma operação de movimentação entre um projeto de origem baseado em diretório e um projeto de destino baseado em referência porque o projeto baseado em diretório de origem terá que excluir o item de origem após a conclusão da movimentação. O projeto baseado em referência de destino terminaria com uma referência a um item excluído.

Também é enganoso tentar permitir uma operação de cópia entre esses tipos de projetos porque o projeto baseado em referência de destino não deve fazer uma cópia independente do item de origem. Da mesma forma, Ctrl + Shift arrastando para um projeto de destino baseado em diretório não deve ser permitido porque um projeto baseado em diretório não pode persistir referências. Nos casos em que não há suporte para a operação do tipo "arrastar e soltar", o IDE deve não permitir a soltar e mostrar ao usuário o cursor no-drop (mostrado na tabela de ponteiro abaixo).

Para implementar corretamente o comportamento do tipo "arrastar e soltar", o projeto de origem do arrastar precisa comunicar sua natureza ao projeto de destino. (Por exemplo, é baseado em referência ou em diretório?) Essas informações são indicadas pelo formato de área de transferência oferecido pela origem. Como a origem de uma operação de arrastar (ou de cópia da área de transferência) um projeto deve oferecer ou, respectivamente, dependendo se o projeto é baseado em referência ou em `CF_VSREFPROJECTITEMS` `CF_VSSTGPROJECTITEMS` diretório. Ambos os formatos têm o mesmo conteúdo de dados, que é semelhante ao formato do Windows, exceto que as listas de cadeias de caracteres, em vez de serem nomes de arquivo, são uma lista de cadeias de caracteres terminadas duas vezes (conforme retornado de ou conforme `CF_HDROP` `NULL` `Projref` `IVsSolution::GetProjrefOfItem` `::GetProjrefOfProject` apropriado).

Como o destino de uma operação de redução (ou de colar área de transferência), um projeto deve aceitar e , embora a manipulação exata da operação do tipo "arrastar e soltar" varie dependendo da natureza do projeto de destino e do projeto de `CF_VSREFPROJECTITEMS` `CF_VSSTGPROJECTITEMS` origem. O projeto de origem declara sua natureza se ele oferece `CF_VSREFPROJECTITEMS` ou `CF_VSSTGPROJECTITEMS` . O destino da queda compreende sua própria natureza e, portanto, tem informações suficientes para tomar decisões sobre se uma movimentação, cópia ou link deve ser executado. O usuário também modifica qual operação do tipo "arrastar e soltar" deve ser executada pressionando as teclas Ctrl, Shift ou Ctrl e Shift. É importante que o destino de soltar indique corretamente qual operação será executada com antecedência em seus `DragEnter` `DragOver` métodos e . O **Gerenciador de Soluções** automaticamente sabe se o projeto de origem e o projeto de destino são o mesmo projeto.

Não há suporte especificamente para arrastar itens de projeto entre instâncias do Visual Studio (por exemplo, de uma instância do devenv.exe para outra). O **Gerenciador de Soluções** também desabilita isso diretamente.

O usuário sempre deve ser capaz de determinar o efeito de uma operação do tipo "arrastar e soltar" selecionando um item, arrastando-o para o local de destino e observando quais dos seguintes ponteiros do mouse aparecem antes que o item seja descartado:

| Ponteiro do mouse | Comando | Descrição |
| :---: | --- | --- |
| ![Ícone "sem soltar" do mouse](../../extensibility/ux-guidelines/media/0706-01_mousenodrop.png "0706-01_MouseNoDrop") | Nenhuma queda | O item não pode ser descartado para o local especificado. |
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
A tabela a seguir resume as operações do tipo "arrastar e soltar" (bem como recortar/copiar/colar) que devem ser executadas com base na natureza do item de origem e das teclas modificadora pressionadas para projetos de destino baseados em diretório:

| Modificador | Categoria | Item de origem: Referência/Link | Item de origem: item físico ou sistema de arquivos ( `CF_HDROP` ) |
|-----------------|----------| - | - |
| Nenhum modificador | Ação | Mover | Mover |
| Nenhum modificador | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Nenhum modificador | Fonte | Exclui a referência ao item original | Exclui a referência ao item original |
| Shift+Arrastar | Ação | Mover | Mover |
| Shift+Arrastar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Shift+Arrastar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Shift+Arrastar | Resultado | `DROPEFFECT_MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl+Arrastar | Ação | Copiar | Copiar |
| Ctrl+Arrastar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Ctrl+Arrastar | Fonte | Retém a referência ao item original | Retém a referência ao item original |
| Ctrl+Arrastar | Resultado | `DROPEFFECT_COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl+Shift+Arrastar | | Nenhuma queda | Nenhuma queda |
| Recortar/colar | Ação | Mover | Mover |
| Recortar/colar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Recortar/colar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Recortar/colar | Resultado | O item permanece no local original no armazenamento | O item é excluído do local original no armazenamento |
| Copiar/colar | Ação | Copiar | Copiar |
| Copiar/colar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Copiar/colar | Fonte | Retém o item original | Retém o item original |
| Copiar/colar | Resultado | O item permanece no local original no armazenamento | O item permanece no local original no armazenamento ins |

#### <a name="mixed-target-projects"></a>Projetos de destino misto
A tabela a seguir resume as operações do tipo "arrastar e soltar" (bem como recortar/copiar/colar) que devem ser executadas com base na natureza do item de origem e das teclas modificadora pressionadas para projetos de destino misto:

| Modificador | Categoria | Item de origem: Referência/Link | Item de origem: item físico ou sistema de arquivos ( `CF_HDROP` ) |
| --- | --- | --- | --- |
| Nenhum modificador | Ação | Mover | Mover |
| Nenhum modificador | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Nenhum modificador | Fonte | Exclui a referência ao item original | Exclui a referência ao item original |
| Nenhum modificador | Resultado | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item é excluído do local original no armazenamento |
| Shift+Arrastar | Ação | Mover | Mover |
| Shift+Arrastar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Shift+Arrastar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Shift+Arrastar | Resultado | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ MOVE` é retornado como ação de `::Drop` e o item é excluído do local original no armazenamento |
| Ctrl+Arrastar | Ação | Copiar | Copiar |
| Ctrl+Arrastar | Destino | Adiciona referência ao item original | Copia o item para o local de destino |
| Ctrl+Arrastar | Fonte | Retém a referência ao item original | Retém o item original |
| Ctrl+Arrastar | Resultado | `DROPEFFECT_ COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ COPY` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Ctrl+Shift+Arrastar | Ação | Link | Link |
| Ctrl+Shift+Arrastar | Destino | Adiciona referência ao item original | Adiciona referência ao item de origem original |
| Ctrl+Shift+Arrastar | Fonte | Retém a referência ao item original | Retém o item original |
| Ctrl+Shift+Arrastar | Resultado | `DROPEFFECT_ LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento | `DROPEFFECT_ LINK` é retornado como ação de `::Drop` e o item permanece no local original no armazenamento |
| Recortar/colar | Ação | Mover | Mover |
| Recortar/colar | Destino | Copia o item para o local de destino | Copia o item para o local de destino |
| Recortar/colar | Fonte | Exclui a referência ao item original | Exclui o item do local original |
| Recortar/colar | Resultado | O item permanece no local original no armazenamento | O item é excluído do local original no armazenamento |
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
