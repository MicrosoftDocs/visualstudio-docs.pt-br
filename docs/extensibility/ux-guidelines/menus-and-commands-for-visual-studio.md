---
title: Menus e comandos para o Visual Studio | Microsoft Docs
description: Saiba como as barras de comando permitem flexibilidade na interface do usuário quando você cria novos recursos para o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 0a1ed675-2bd1-4603-ba3a-f40dfb5cfb69
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ef66123e1a4d62f89fc1c69b81bcb780d0b294f0
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902092"
---
# <a name="menus-and-commands-for-visual-studio"></a>Menus e comandos para Visual Studio
## <a name="command-usage"></a>Uso do comando

### <a name="overview"></a>Visão geral
 Ao contrário do Microsoft Office, que é um pacote que abrange muitos produtos separados, o Visual Studio contém muitos produtos que cada um contribui com seus conjuntos de comandos para o IDE global do Visual Studio. O IDE gerencia a complexidade de milhares de comandos filtrando a funcionalidade disponível para o usuário com base no contexto.

 Quando o contexto de um usuário é alterado, como alternar de uma janela de design para uma janela de edição de código, a funcionalidade não relacionada ao novo contexto desaparece. Ao mesmo tempo, novas funcionalidades se unem com informações dinâmicas relacionadas, como propriedades e opções de caixa de ferramentas. O usuário não deve observar a troca do conjunto de comandos disponíveis. Se o usuário for distraídos ou confundido por comandos que aparecem ou desaparecerem, o design da interface do usuário precisará de ajuste. O contexto atual do usuário é sempre indicado de uma ou mais maneiras, como na barra de título do IDE, na janela Propriedades ou na caixa de diálogo páginas de propriedades.

 As barras de comando permitem flexibilidade na interface do usuário. As únicas estruturas de comando inerentes ao ambiente do Visual Studio são o menu principal e a barra de comandos principal, que podem ser personalizadas e até mesmo ocultas. Outras barras de comando aparecem e desaparecem com base no estado do aplicativo. Janelas de ferramentas e editores de documentos também podem conter barras de ferramentas incorporadas dentro de suas bordas de janela.

#### <a name="basic-guidelines"></a>Diretrizes básicas

##### <a name="use-existing-shared-commands-command-groups-and-menus-whenever-possible"></a>Use comandos compartilhados existentes, grupos de comandos e menus sempre que possível.
 Como os comandos são geralmente mostrados com base no contexto, o uso de menus compartilhados e grupos de comandos existentes garante que a estrutura do comando permaneça relativamente estável entre as alterações no contexto. Reutilizar comandos compartilhados e colocar novos comandos próximos a comandos compartilhados relacionados também reduz a complexidade do IDE e cria uma experiência mais fácil de usar. Se um novo comando precisar ser definido, tente colocá-lo em um grupo de comandos compartilhados existente. Se um novo grupo precisar ser definido, coloque-o em um menu compartilhado existente próximo a um grupo de comandos relacionados antes de criar um novo menu de nível superior.

##### <a name="do-not-create-icons-for-every-command"></a>Não crie ícones para cada comando.
 Pense atentamente antes de criar um ícone de comando. Os ícones devem ser criados somente para comandos que:

- aparecem em uma barra de ferramentas padrão.

- provavelmente serão adicionados por usuários a uma barra de ferramentas por meio da caixa de diálogo **Personalizar...** .

- ter um ícone associado à mesma ação em outro produto da Microsoft.

##### <a name="limit-the-addition-of-keyboard-shortcuts"></a>Limitar a adição de atalhos de teclado
 A grande maioria dos usuários emprega uma pequena fração de todos os atalhos disponíveis. Em caso de dúvida, não associe seu recurso a um atalho de teclado. Trabalhe com sua equipe de experiência do usuário antes de adicionar novos atalhos.

##### <a name="give-commands-a-default-menu-placement"></a>Dê aos comandos um posicionamento de menu padrão.
 Lembre-se de que os comandos serão personalizados por outras pessoas e os projetará de acordo. Não há tal coisa como um comando oculto. Todos os comandos do Visual Studio aparecem na caixa de diálogo **ferramentas > personalizar** , a janela de comando, preenchimento automático, **Opções de > de ferramentas >** caixa de diálogo de teclado e o ambiente de ferramentas de desenvolvimento (DTE). Certifique-se de dar a seus comandos um nome e uma dica de ferramenta em seu arquivo. CTC para que os usuários possam encontrá-los facilmente.

##### <a name="do-not-duplicate-shared-commands-on-an-embedded-toolbar"></a>Não duplique os comandos compartilhados em uma barra de ferramentas inserida.
 É útil posicionar os comandos em proximidade com a área do foco do usuário. Uma maneira de fazer isso é criar uma barra de ferramentas inserida na parte superior da janela de ferramentas ou do editor de documentos. Os comandos colocados na barra de ferramentas devem ser específicos para a região de conteúdo dentro da janela. Não duplique os comandos compartilhados nessas barras de ferramentas. Por exemplo, nunca coloque um ícone "salvar" dentro de uma barra de ferramentas inserida.

### <a name="content-and-command-visibility"></a>Visibilidade de conteúdo e comando
 Os comandos existem nos seguintes escopos: **ambiente**, **hierarquia** e **documento**. Conheça cada escopo para ter confiança no posicionamento do comando.

 Os comandos no escopo do **ambiente** estabelecem o contexto primário e são compartilhados entre vários contextos. Eles alteram a visibilidade ou a organização de documentos e janelas de ferramentas. Entre os comandos no escopo do ambiente estão **novos projetos**, **Conecte-se ao servidor**, **anexe processo**, **recortar**, **copiar**, **colar**, **Localizar**, **Opções**, **Personalizar**, **nova janela** e **Exibir ajuda**.

 Os comandos no escopo da **hierarquia** gerenciam hierarquias no Visual Studio, incluindo **projeto**, **equipe** e **dados**. Eles estão relacionados ao subcontexto de um projeto, por exemplo, **depuração**, **compilação**, **teste**, **arquitetura** ou **análise**. Entre os comandos no escopo da hierarquia estão **adicionados novo item**, **nova consulta**, **configurações do projeto**, **Adicionar nova fonte de dados**, assistente de inicialização de **desempenho** e **novo diagrama**.

 Os comandos no escopo do **documento** agem sobre o conteúdo de um documento, como código, design ou uma wiq (consulta de item de trabalho). Eles também atuam na exibição de uma janela de ferramentas ou, de outra forma, são específicos para essa janela de ferramentas. Os comandos de escopo do documento também agem nos objetos de arquivo que são específicos da hierarquia, como **remover do projeto**. Entre os comandos no escopo do documento estão **refatorar > renomear**, **criar cópia do item de trabalho**, **expandir tudo**, **recolher tudo** e **criar tarefa do usuário**.

### <a name="command-placement-decisions"></a>Decisões de posicionamento de comando
 Depois de decidir criar um comando, você precisará determinar seu posicionamento apropriado e se deseja criar um atalho de teclado. Siga este caminho de decisão para estabelecer onde posicionar o comando:

 ![Gráfico de decisão de posicionamento do comando](../../extensibility/ux-guidelines/media/0501-a_commandplacement.png "0501-a_CommandPlacement")

 **Caminho de decisão para posicionamento de comando no Visual Studio**

### <a name="command-placement-in-menus"></a>Posicionamento do comando em menus

#### <a name="main-menu-bar"></a>Barra de menus principal
 A barra de menus principal deve ser o local padrão para comandos de qualquer um dos pacotes de menu específicos de contexto que contribuem para a interface do usuário. A barra de menus principal difere de outras estruturas de comando, pois o ambiente a utiliza para controlar quais comandos são visíveis. Todas as outras barras de comandos simplesmente desabilitam comandos que estão fora de contexto, sejam eles colocados em um menu ou em uma barra de ferramentas.

 O ambiente define um conjunto de comandos incorporados à barra de menus principal que são comuns em todo o IDE e em vários domínios de tarefa. Esses comandos são sempre visíveis, independentemente de quais VSPackages são carregados no ambiente. Embora VSPackages possa estender esse conjunto de comandos, o comando definido de cada produto e o posicionamento de seus comandos é responsabilidade de cada equipe.

 A estrutura do menu principal do Visual Studio pode ser dividida nas seguintes categorias de menu:

##### <a name="core-menus"></a>Menus principais

- Arquivo

- Editar

- Visualizar

- Ferramentas

- Janela

- Ajuda

##### <a name="project-specific-menus"></a>Menus específicos do projeto

- Project

- Build

- Depurar

##### <a name="context-specific-menus"></a>Menus específicos do contexto

- Equipe

- Dados

- Teste

- Arquitetura

- Analisar

##### <a name="document-specific-menus"></a>Menus específicos do documento

- Formatar

- Tabela

##### <a name="when-designing-main-menus-adhere-to-these-rules"></a>Ao criar menus principais, siga estas regras:

- Não exceder 25 itens de nível superior em um determinado contexto

- Os menus nunca devem exceder 600 pixels de altura.

- Avalie um menu principal em vários contextos, como no SKU final e no perfil geral.

- Os menus flutuantes são aceitáveis.

- Os menus flutuantes devem conter pelo menos três itens e não mais do que sete.

- Os menus flutuantes devem ir apenas um nível de profundidade – alguns itens de menu do Visual Studio têm submenus em cascata, mas esse padrão não é incentivado.

- Não use mais do que seis separadores. Os agrupamentos devem aderir à ilustração a seguir:

     ![Diretrizes para o agrupamento de menus principal](../../extensibility/ux-guidelines/media/0501-b_mainmenus.png "0501-b_MainMenus")

- Embora não seja necessário ter cada agrupamento na figura, a adição de agrupamentos adicionais é restrita.

- Cada agrupamento deve ter de dois a sete itens de menu.

#### <a name="main-menu-ordering"></a>Ordenação do menu principal
 Antes de adicionar um novo item de nível superior, considere colocar o comando em um menu de nível superior existente. Ao adicionar um novo menu de nível superior, certifique-se de colocá-lo no local correto. Decida se o menu é específico do projeto, contexto ou documento. Mantenha o nome do menu de nível superior conciso e use apenas uma palavra.

 Os menus principais devem delimitador o restante dos comandos. O arquivo, a edição e a exibição devem estar sempre à esquerda, e as ferramentas, a janela e a ajuda devem estar sempre à direita.

#### <a name="context-menus"></a>Menus de contexto
 Colocar muitas funcionalidades nos menus de contexto resulta em uma interface difícil de aprender. Toda a funcionalidade principal deve estar disponível por meio da barra de menus principal. O posicionamento de comandos deve ser reconciliado com comandos existentes para evitar comandos duplicados. Para menus de contexto, o Shell define os grupos de menus padrão que devem ser incluídos, dependendo se o menu de contexto é para a solução, um nó de projeto ou um item de projeto.

 Ao criar menus de contexto, siga as mesmas regras do menu principal e, além disso:

- Não exceda 25 itens de menu de nível superior.

- Os menus flutuantes são aceitáveis, mas não devem exceder um nível de profundidade, nunca use submenus em cascata.

- Não use mais do que seis separadores.

### <a name="command-placement-in-toolbars"></a>Posicionamento de comando em barras de ferramentas

#### <a name="general-toolbars"></a>Barras de ferramentas gerais
 Ao projetar e organizar barras de ferramentas, siga estes padrões:

- Não use mais de um verbo por botão. Um botão = uma ação.

- Use o texto ao lado do ícone somente se ele precisar ser reforçado com o rótulo.

- Use uma caixa de combinação exclusivamente para propriedades que serão alternadas várias vezes em uma sessão. Caso contrário, expor a propriedade em outro lugar.

- A largura de uma caixa de combinação deve ser igual à largura do item mais longo na caixa + 30%. Por exemplo, se o item mais longo for 200 pixels, a caixa de combinação deverá ter 260 pixels de largura.

- Limitar o uso de separadores. O uso de um separador ao lado de uma lista suspensa é um antipadrão, porque a forma da lista suspensa atua como um separador Visual.

- Os grupos de ícones devem conter de três a seis ícones.

- Se os qualificadores resultarem em vários comandos úteis, use um botão de divisão que armazena a última configuração:

     ![Botões de divisão no Visual Studio](../../extensibility/ux-guidelines/media/0501-c_splitbuttons.png "0501-c_SplitButtons")

     **Exemplo de um botão de divisão. Os seis comandos à esquerda podem caber em um único botão.**

#### <a name="product-specific-toolbars"></a>Barras de ferramentas específicas do produto
 Cada produto pode fornecer uma barra de ferramentas padrão que contém comandos frequentemente usados e importantes, e a barra de ferramentas padrão de cada produto deve aparecer na primeira vez que o Visual Studio for iniciado depois que o produto for instalado.

 Os produtos também devem aproveitar os grupos de comandos compartilhados e os menus fornecidos pelo IDE. Cada grupo de comandos compartilhado é colocado em um menu compartilhado destinado a organizar comandos relacionados de uma maneira significativa para o usuário. É importante aproveitar essa estrutura de comando compartilhado para reduzir a complexidade.

#### <a name="global-toolbars"></a>Barras de ferramentas globais
 É necessário que as barras de ferramentas globais caibam em uma linha imediatamente. Ao criar uma nova barra de ferramentas global, siga as diretrizes para esse tipo de barra de ferramentas.

 **Diretrizes gerais da barra de ferramentas:**

- Cada barra de ferramentas tem 24 pixels em controles comuns (garra, overflow).

- Cada botão da barra de ferramentas tem 22 pixels de largura, incluindo preenchimento. Tornar o ícone um botão de divisão adiciona outros 11 pixels de largura.

- A duplicação de comandos entre barras de ferramentas é permitida.

  **Barras de ferramentas específicas do documento** aparecem quando um determinado tipo de arquivo está ativo e desaparece quando um tipo de arquivo diferente se torna ativo.

- Barras de ferramentas específicas do documento não podem ter mais de 12 botões.

- A largura total da barra de ferramentas não pode exceder 300 pixels.

- Cada tipo de arquivo pode ter uma barra de ferramentas inserida ou uma barra de ferramentas global específica do documento, mas não ambos.

  **Barras de ferramentas específicas do contexto** aparecem quando um determinado contexto é definido e tendem a permanecer ativas por períodos estendidos.

- O limite de botão para todas as barras de ferramentas específicas do contexto é 18.

- Se a maioria dos usuários não empregar consistentemente os comandos dessa barra de ferramentas quando o contexto estiver ativo, não associe essa barra de ferramentas a um contexto.

- Verifique se a barra de ferramentas desaparece ao sair do contexto. Nenhuma dessas barras de ferramentas deve aparecer na inicialização.

  **Barras de ferramentas sem nenhum contexto** nunca aparecem automaticamente. Elas são mostradas somente quando o usuário as ativa. Mantenha a largura máxima abaixo de 200 pixels.

### <a name="general-organization-and-shell-defined-groups"></a>Organização geral e grupos definidos por shell
 Use comandos compartilhados, grupos de comandos e menus existentes. Se um novo comando precisar ser definido, tente colocá-lo em um grupo de comandos compartilhados existente. Se um novo grupo precisar ser definido, tente colocá-lo em um menu compartilhado existente próximo a um grupo de comandos relacionados antes de criar um novo menu de nível superior. Isso reduz a complexidade do comando, garantindo o posicionamento consistente do comando no IDE.

 O menu de **formato** compartilhado, geralmente mostrado no contexto de janelas de documento no estilo de designer, é ilustrado na imagem a seguir:

 ![Menu Formatar do Visual Studio com textos explicativos](../../extensibility/ux-guidelines/media/0501-d_formatmenu.png "0501-d_FormatMenu")

 **Grupos de menus no Visual Studio**

### <a name="reducing-and-reusing-commands"></a>Reduzindo e reutilizando comandos
 Os comandos são geralmente mostrados com base no contexto, para reduzir o número de comandos que o usuário vê em um determinado momento. No entanto, você também deve reutilizar os menus compartilhados existentes e os grupos de comandos para garantir que a estrutura do comando permaneça relativamente estável entre as alterações no contexto.

 Reutilizar comandos compartilhados e colocar novos comandos próximos aos comandos compartilhados relacionados reduz a complexidade do IDE e cria uma experiência mais fácil de usar.

## <a name="naming-commands"></a>Comandos de nomenclatura

### <a name="naming-conventions"></a>Convenções de nomenclatura
 A nomenclatura consistente de comandos é essencial para que os usuários possam localizar e executar comandos, seja usando a linha de comando ou a associação a um atalho de teclado. Os nomes de comando também ajudam o usuário a entender qual finalidade um comando serve quando é exibido em uma barra de ferramentas ou em um menu de contexto ou em cascata.

#### <a name="when-naming-commands"></a>Ao nomear comandos:

- Construa texto para que ele seja facilmente localizável. Para obter mais informações sobre a localização de texto, consulte [práticas recomendadas de localização](/dotnet/standard/globalization-localization/best-practices-for-developing-world-ready-apps#localization-best-practices).

- Seja conciso. Os comandos não devem usar mais do que três palavras.

- Usar capitalização do caso de título: a primeira letra de cada palavra deve ser capitalizada. Para obter mais informações sobre a formatação de texto no Visual Studio, consulte [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).

- Leve em consideração onde o comando será colocado. Ele está em um menu de nível superior ou um submenu? Por exemplo, ao agrupar comandos de alinhamento em um submenu, o comando de nível superior deve ser "Alinhar" e os comandos de submenu devem ser "esquerdo", "à direita," "centralizado", "justificar" e assim por diante. Seria redundante nomear os comandos de submenu "Alinhar à esquerda" ou "Alinhar à direita".

     ![Menu Formatar do Visual Studio](../../extensibility/ux-guidelines/media/0502-a_formatmenu.png "0502-a_FormatMenu")

### <a name="using-icons-with-commands"></a>Usando ícones com comandos
 Ser sobressalente no uso do emparelhamento de ícone com comandos. Embora a associação de uma imagem exclusiva a um comando Hastens a capacidade do usuário de identificar esse comando, a desordem Visual e a ineficiência ocorrem com o uso excessivo de imagem. As regras a seguir ajudam a decidir se um ícone de comando deve ser criado.

#### <a name="use-an-icon-with-a-command-only-if"></a>Use um ícone com um comando somente se:

- O mesmo comando tem um ícone associado a ele em outro produto da Microsoft em destaque, como um dos aplicativos Microsoft Office.

- O comando será colocado em uma barra de ferramentas padrão.

- O comando é um comando Specialty que os usuários provavelmente adicionarão a uma barra de ferramentas usando a caixa de diálogo **"Personalizar..."** .

## <a name="access-and-shortcut-keys"></a>Teclas de atalho e acesso

### <a name="overview"></a>Visão geral
 Há dois tipos de atribuições de teclas de teclado:

- **As chaves de acesso** (também conhecidas como aceleradores) permitem o acesso ao teclado por meio dos menus para comando e para cada rótulo na interface do usuário da caixa de diálogo. As chaves de acesso são principalmente para fins de acessibilidade, são atribuídas a todos os menus e à maioria dos controles da caixa de diálogo, não devem ser memorizadas, afetam apenas a janela atual e são localizadas.

- **As teclas de atalho** usam principalmente as sequências de teclas Control (Ctrl) e function (FN). Elas foram projetadas mais para usuários avançados e auxiliam na produtividade. Eles são atribuídos apenas aos comandos usados com mais frequência e permitem acesso rápido ao ignorar o menu principal. As teclas de atalho devem ser memorizadas e, por esse motivo, deve ser atribuída consistente com o esquema de perfil. Os esquemas de teclas de atalho podem variar de perfil para perfil. Um usuário pode personalizar as teclas de atalho por meio de **ferramentas > opções > teclado**.

### <a name="assigning-access-keys"></a>Atribuindo chaves de acesso
 As chaves de acesso consistem em Alt mais chaves alfanuméricas. Atribua uma chave de acesso a cada item de menu sem exceção. Siga as convenções do Windows e comuns para atribuir chaves de acesso. por exemplo, a chave de acesso para o **arquivo > novo** sempre deve ser **ALT, F, N**.

 Não use letras de largura de pixel único, como ' i ' (em letras maiúsculas ou minúsculas) ou uma letra minúscula ' l ', e evite usar caracteres com descendentes (g, j, p, q e y), pois eles são difíceis de distinguir.

 Evite usar chaves duplicadas quando possível. Nos casos em que a duplicação é inevitável, o sistema de menus manipula conflitos ao percorrer todos os comandos que usam a chave. Por exemplo, para um comando hipotético "número" no menu arquivo que duplica a tecla de acesso "N", **ALT, F, n** criaria um novo arquivo, e **ALT, f** , n, n executaria o comando "Number".

### <a name="assigning-shortcut-keys"></a>Atribuindo teclas de atalho
 Evite atribuir novas teclas de atalho, pois elas não são necessárias para todos os comandos e impostos o sistema (e a memória do usuário) se estiverem em uso. Os dados do Programa de Aperfeiçoamento da Experiência do Usuário (CEIP) indicam que os usuários do Visual Studio usam apenas um pequeno subconjunto dos atalhos integrados.

 Ao definir atalhos, siga estas regras:

- **Use as sequências de teclas Control (Ctrl) e function (FN).**

- **Preserve os atalhos usados com frequência.** Mantenha os atalhos mais populares.

- **Torne os atalhos do editor fáceis de digitar.** Associe atalhos fáceis de digitar a comandos que os desenvolvedores precisam mais ao escrever código. Por exemplo, **Edit. InvokeSmartTag** precisa ter uma tecla de atalho rápida como CTRL +/e não Alt + Shift + F10.

- **Busque atalhos com tema consistente.**

- **Siga as diretrizes do Windows para determinar quais chaves de modificador empregar.** Use combinações de teclas CTRL para comandos que têm efeitos em larga escala, como comandos que se aplicam a um documento inteiro. Use combinações de teclas Shift para comandos que estendem ou complementem as ações da tecla de atalho padrão. Não use combinações CTRL + ALT.

- **Remover atalhos incorretos.** Se você tiver um recurso herdado, considere remover atalhos que são usados com extrema frequência (menos de 10 vezes a partir dos dados do CEIP) ou a frequência moderada (menos de 100 vezes a partir dos dados do CEIP) se uma chave de acesso fornecer acesso rápido ao mesmo comando. Por exemplo: Alt, H, C abrirá ajuda/conteúdo.

  Não há uma maneira simples de verificar a disponibilidade do atalho. Se você quiser adicionar um atalho, siga estas etapas:

1. Verifique a lista de [atalhos de Visual Studio 2013](http://visualstudioshortcuts.com/2013/) para determinar se há comandos semelhantes para agrupá-los.

2. Vá para **ferramentas > opções > ambiente > teclado** e teste seu atalho. Verifique cada esquema de mapeamento de teclado listado em "aplicar o esquema de mapeamento de teclado adicional a seguir". Verifique os perfis geral, C#, VB e C++, pois eles compartilham atalhos exclusivos. O atalho estará disponível se não estiver mapeado em nenhum desses lugares.
