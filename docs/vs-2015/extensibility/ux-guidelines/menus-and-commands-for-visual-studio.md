---
title: Menus e comandos para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0a1ed675-2bd1-4603-ba3a-f40dfb5cfb69
caps.latest.revision: 5
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e75a800ab86cc1ec902382bee06efd65c276b046
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51804463"
---
# <a name="menus-and-commands-for-visual-studio"></a>Menus e comandos para o Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="command-usage"></a>Uso do comando  
  
### <a name="overview"></a>Visão geral  
 Ao contrário do Microsoft Office, que é um conjunto que consiste em vários produtos separados, o Visual Studio contém muitos produtos que cada contribuir com seus conjuntos de comandos ao IDE do Visual Studio global. O IDE gerencia a complexidade de milhares de comandos, a funcionalidade disponível para o usuário com base no contexto de filtragem.  
  
 Quando um contexto do usuário é alterada – como alternar de uma janela de design para um janela de edição de código – funcionalidade não relacionada ao novo contexto desaparece. Ao mesmo tempo, novas superfícies de funcionalidade junto com informações dinâmicas relacionadas, como opções de propriedades e a caixa de ferramentas. O usuário não deverá observar a troca do conjunto de comandos disponíveis. Se o usuário é distraído ou confuso com comandos que aparecem ou desaparecem, em seguida, o design de interface do usuário precisa de ajuste. O contexto do usuário atual sempre é indicado em uma ou mais formas, como na barra de título do IDE, a janela Propriedades ou a caixa de diálogo páginas de propriedades.  
  
 Barras de comandos permitem flexibilidade na interface do usuário. O único comando estruturas do Visual Studio ambiente estão o menu principal e a barra de comandos principal, que pode ambos ser personalizada e até mesmo oculta inerente. Outras barras de comando aparecem e desaparecem com base no estado do aplicativo. Editores de documento e janelas de ferramenta também podem conter barras de ferramentas inseridas dentro de suas bordas de janela.  
  
#### <a name="basic-guidelines"></a>Diretrizes básicas  
  
##### <a name="use-existing-shared-commands-command-groups-and-menus-whenever-possible"></a>Use os comandos existentes compartilhados, grupos de comando e menus sempre que possível.  
 Uma vez que os comandos são normalmente mostrados com base no contexto, o uso de menus compartilhadas existentes e grupos de comando garante que a estrutura de comando permanece relativamente estável entre as alterações no contexto. Reutilizando comandos compartilhados e colocando novos comandos próximos comandos compartilhados relacionados também reduz a complexidade do IDE e cria uma experiência mais amigável. Se um novo comando precisa ser definida, tente colocá-lo em um grupo de comando compartilhado existente. Se um novo grupo deve ser definido, colocá-lo em um menu compartilhado existente perto de um grupo de comandos relacionados antes de criar um novo menu de nível superior.  
  
##### <a name="do-not-create-icons-for-every-command"></a>Não crie ícones para cada comando.  
 Pense cuidadosamente antes de criar um ícone do comando. Ícones devem ser criados somente para os comandos que:  
  
-   são exibidos em uma barra de ferramentas padrão.  
  
-   têm probabilidade de ser adicionados por usuários para uma barra de ferramentas por meio de **personalizar...** caixa de diálogo.  
  
-   tem um ícone associado com a mesma ação em outro produto da Microsoft.  
  
##### <a name="limit-the-addition-of-keyboard-shortcuts"></a>Limitar a adição de atalhos de teclado  
 A grande maioria dos usuários empregar uma pequena fração de todos os atalhos disponíveis. Em caso de dúvida, a não vincule seu recurso para um atalho de teclado. Trabalhar com seu usuário experiência equipe antes de adicionar novos atalhos.  
  
##### <a name="give-commands-a-default-menu-placement"></a>Dar uma colocação de menu padrão de comandos.  
 Lembre-se de que seus comandos serão personalizados por outras pessoas e criá-las adequadamente. Não há nenhum algo como um comando oculto. Todos os comandos do Visual Studio aparecem na **Ferramentas > Personalizar** caixa de diálogo, a janela de comando, preenchimento automático, o **Ferramentas > Opções > teclado** caixa de diálogo e o desenvolvimento de ferramentas de DTE (ambiente). Certifique-se de dar a seus comandos de um nome e uma dica de ferramenta em seu arquivo. ctc para que os usuários podem encontrá-los facilmente.  
  
##### <a name="do-not-duplicate-shared-commands-on-an-embedded-toolbar"></a>Não duplica compartilhados comandos em uma barra de ferramentas inserida.  
 É útil colocar os comandos em estreita proximidade com a área de foco do usuário. Uma maneira de fazer isso é criar uma barra de ferramentas inserida na parte superior da sua janela de ferramentas ou documento editor. Os comandos colocados na barra de ferramentas devem ser específicos para a região de conteúdo dentro da janela. Não duplica comandos compartilhados nessas barras de ferramentas. Por exemplo, nunca coloque um ícone de "Salvar" dentro de uma barra de ferramentas inserida.  
  
### <a name="content-and-command-visibility"></a>Visibilidade de comando e conteúda  
 Comandos existem os seguintes escopos: **ambiente**, **hierarquia**, e **documento**. Sabe a cada escopo para ter confiança no posicionamento de comando.  
  
 Os comandos na **ambiente** escopo estabelecer contexto primário e são compartilhados entre vários contextos. Alteram a visibilidade ou a disposição dos documentos e janelas de ferramentas. Entre os comandos no ambiente do escopo estão **novo projeto**, **conectar ao servidor**, **anexar processo**, **Recortar**,  **Cópia**, **colar**, **localizar**, **opções**, **personalizar**, **nova janela de**, e **exibir a Ajuda**.  
  
 Os comandos na **hierarquia** escopo gerenciar hierarquias no Visual Studio, incluindo **Project**, **equipe**, e **dados**. Eles se relacionam com subcontexto do projeto – por exemplo, **Debug**, **compilação**, **teste**, **arquitetura**, ou **analisar** . Entre os comandos na hierarquia de escopo estão **Adicionar Novo Item**, **nova consulta**, **configurações de projeto**, **Add New Data Source**, **Iniciar o Assistente de desempenho**, e **novo diagrama**.  
  
 Os comandos na **documento** ato de escopo no conteúdo de um documento, como código, design ou uma consulta de item de trabalho (WIQ). Eles também atuam no modo de exibição de uma janela de ferramenta ou caso contrário, são específicos para essa janela de ferramenta. Comandos de escopo de documento também agir sobre os objetos de arquivo que também são específicas à hierarquia, como **remover do projeto**. Entre os comandos no documento de escopo estão **Refatorar > Renomear**, **criar cópia do Item de trabalho**, **Expandir tudo**, **Recolher tudo**, e **Criar tarefa do usuário**.  
  
### <a name="command-placement-decisions"></a>Decisões de posicionamento do comando  
 Depois de decidir criar um comando, você precisará determinar o posicionamento adequado e se é necessário criar um atalho de teclado. Siga este caminho de decisão para estabelecer onde colocar o comando:  
  
 ![Gráfico de decisão de posicionamento do comando](../../extensibility/ux-guidelines/media/0501-a-commandplacement.png "a_CommandPlacement 0501")  
  
 **Caminho de decisão para posicionamento de comando no Visual Studio**  
  
### <a name="command-placement-in-menus"></a>Posicionamento do comando nos menus  
  
#### <a name="main-menu-bar"></a>Barra de menus principal  
 Barra de menus principal deve ser o local padrão para comandos de todos os pacotes menu de contexto específico que contribuem para a interface do usuário. Barra de menus principal é diferente de outras estruturas de comando, o ambiente o usa para controlar quais comandos estão visíveis. Todas as barras de comando simplesmente desabilitar comandos que estão fora do contexto, eles são colocados em um menu ou em uma barra de ferramentas.  
  
 O ambiente define um conjunto de comandos incorporado a barra de menus principais que são comuns em todo o IDE e vários domínios de tarefa. Esses comandos estão sempre visíveis independentemente dos quais os VSPackages são carregados no ambiente. Embora os VSPackages pode estender este conjunto de comandos, o conjunto de cada produto e o posicionamento dos comandos de comandos é responsabilidade de cada equipe.  
  
 A estrutura do menu principal do Visual Studio pode ser dividida nas seguintes categorias de menu:  
  
##### <a name="core-menus"></a>Menus de núcleo  
  
-   Arquivo  
  
-   Editar  
  
-   View  
  
-   Ferramentas  
  
-   Janela  
  
-   Ajuda  
  
##### <a name="project-specific-menus"></a>Menus específicos de projeto  
  
-   Projeto  
  
-   Build  
  
-   Depuração  
  
##### <a name="context-specific-menus"></a>Menus de contexto específico  
  
-   Equipe  
  
-   Dados  
  
-   Testar  
  
-   Arquitetura  
  
-   Analisar  
  
##### <a name="document-specific-menus"></a>Menus específicos de documento  
  
-   Formatar  
  
-   Tabela  
  
##### <a name="when-designing-main-menus-adhere-to-these-rules"></a>Durante a criação de menus principais, seguem estas regras:  
  
-   Não exceda 25 itens de nível superior em um determinado contexto  
  
-   Menus nunca devem exceder 600 pixels de altura.  
  
-   Avalie um menu principal em vários contextos, como no SKU Ultimate e o perfil geral.  
  
-   Menus suspensos são aceitáveis.  
  
-   Menus suspensos devem conter pelo menos três itens e não mais de sete.  
  
-   Menus suspensos devem ir somente um nível profundo – alguns itens de menu do Visual Studio tem submenus em cascata, mas não é incentivado, esse padrão.  
  
-   Use separadores não mais do que seis. Agrupamentos devem aderir à ilustração a seguir:  
  
     ![Diretrizes para o agrupamento do menu principal](../../extensibility/ux-guidelines/media/0501-b-mainmenus.png "b_MainMenus 0501")  
  
-   Embora isso não é necessário ter cada agrupamento na figura, adicionar agrupamentos adicionais é restrito.  
  
-   Cada agrupamento deve ter de dois a sete itens de menu.  
  
#### <a name="main-menu-ordering"></a>Ordenação de menu principal  
 Antes de adicionar um novo item de nível superior, considere colocar o comando em um menu de nível superior existente. Ao adicionar um novo menu de nível superior, certifique-se de colocá-lo no local correto. Decida se o menu é específico ao projeto, o contexto ou o documento. Manter o nome do menu de nível superior concisa e usar apenas uma palavra.  
  
 Os menus core devem ser o restante dos comandos do delimitador. Arquivo, editar e exibir sempre deverá ser à esquerda e ferramentas de janela, e ajuda sempre deve ser à direita.  
  
#### <a name="context-menus"></a>Menus de contexto  
 Colocar muita funcionalidade em menus de contexto resulta em uma interface difícil de aprender. Todas as principais funcionalidades devem estar disponíveis por meio da barra de menu principal. Posicionamento dos comandos deve ser reconciliado com os comandos existentes para evitar comandos duplicados. Menus de contexto, o shell define grupos de menus padrão que devem ser incluídos, dependendo se o menu de contexto é a solução, um nó do projeto ou um item de projeto.  
  
 Durante a criação de menus de contexto, seguem as mesmas regras que para o menu principal e, além disso:  
  
-   Não exceda 25 itens de menu de nível superior.  
  
-   Menus suspensos são aceitáveis, mas deve não exceder um nível de profundidade – nunca usar submenus em cascata.  
  
-   Use separadores não mais do que seis.  
  
### <a name="command-placement-in-toolbars"></a>Posicionamento do comando em barras de ferramentas  
  
#### <a name="general-toolbars"></a>Barras de ferramentas gerais  
 Ao projetar e organizando as barras de ferramentas, siga estes padrões:  
  
-   Não use mais de um verbo por botão. Um botão = uma ação.  
  
-   Use texto junto com o ícone somente se ele precisar ser reforçado com o rótulo.  
  
-   Use uma caixa de combinação exclusivamente para as propriedades que serão alternadas várias vezes em uma sessão. Caso contrário, expõem a propriedade em outro lugar.  
  
-   A largura de uma caixa de combinação deve ser igual a largura do item dentro do caixa + 30% mais longa. Por exemplo, se o item mais longo é 200 pixels, a caixa de combinação deve ser 260 pixels de largura.  
  
-   Limite o uso de separadores. O uso de um separador ao lado de uma lista suspensa é um antipadrão, porque a forma da lista suspensa em si atua como um separador visual.  
  
-   Grupos de ícone devem conter de três a seis ícones.  
  
-   Se os qualificadores resultarem em vários comandos úteis, use um botão de divisão que armazena a última configuração:  
  
     ![Dividir botões no Visual Studio](../../extensibility/ux-guidelines/media/0501-c-splitbuttons.png "c_SplitButtons 0501")  
  
     **Exemplo de um botão de divisão. Os seis comandos à esquerda em vez disso, podem se ajustar em um único botão.**  
  
#### <a name="product-specific-toolbars"></a>Barras de ferramentas específicas do produto  
 Cada produto pode fornecer uma barra de ferramentas padrão que contém usados com frequência e comandos importantes e barra de ferramentas de padrão de cada produto devem aparecer na primeira vez em que o Visual Studio é iniciado depois que o produto foi instalado.  
  
 Produtos também devem aproveitar os grupos de comando compartilhado e menus fornecidos pelo IDE. Cada grupo de comando compartilhado é colocado em um menu compartilhado deve organizar os comandos relacionados de forma significativa para o usuário. É importante aproveitar essa estrutura de comando compartilhado para reduzir a complexidade.  
  
#### <a name="global-toolbars"></a>Barras de ferramentas globais  
 Barras de ferramentas globais são necessárias para se ajustar à direita de uma linha fora da caixa. Ao criar uma nova barra de ferramentas global, siga as diretrizes para esse tipo de barra de ferramentas.  
  
 **Diretrizes gerais de barra de ferramentas:**  
  
- Cada barra de ferramentas tem 24 pixels em controles comuns (garra, estouro).  
  
- Cada botão de barra de ferramentas é de 22 pixels de largura incluindo preenchimento. Tornar o ícone de um botão de divisão adiciona outro pixels 11 da largura.  
  
- É permitida a duplicação de comandos em barras de ferramentas.  
  
  **Barras de ferramentas específicas de documentos** aparecem quando um determinado tipo de arquivo está ativo e desaparecem quando outro tipo de arquivo se torna ativo.  
  
- Barras de ferramentas específicas de documentos não podem ter mais de 12 botões.  
  
- A largura total da barra de ferramentas não pode exceder 300 pixels.  
  
- Cada tipo de arquivo pode ter uma barra de ferramentas inserida ou um documento específico barra de ferramentas global, mas não ambos.  
  
  **Barras de ferramentas específicas de contexto** aparecem quando um determinado contexto é definido e tendem a permanecer ativas por longos períodos.  
  
- O limite de botão para todas as barras de ferramentas específicas de contexto é 18.  
  
- Se a maioria dos usuários não consistentemente empregar os comandos dessa barra de ferramentas quando o contexto está ativo, em seguida, não associe essa barra de ferramentas com um contexto.  
  
- Certifique-se de que a barra de ferramentas desaparece quando você sair do contexto. Nenhuma dessas barras de ferramentas deve aparecer na inicialização.  
  
  **Barras de ferramentas sem contexto** nunca aparecem automaticamente. Eles mostram somente quando o usuário os ativa. Manter a largura máxima abaixo de 200 pixels.  
  
### <a name="general-organization-and-shell-defined-groups"></a>Organização geral e grupos definidos pelo shell  
 Use os comandos existentes compartilhados, grupos de comando e menus. Se um novo comando precisa ser definida, tente colocá-lo em um grupo de comando compartilhado existente. Se um novo grupo deve ser definido, tente colocá-lo em um menu compartilhado existente perto de um grupo de comandos relacionados antes de criar um novo menu de nível superior. Isso reduz a complexidade de comando, garantindo o posicionamento do comando consistente no IDE.  
  
 Compartilhado **formato** menu, normalmente é mostrado no contexto de janelas de documentos de estilo do designer, é ilustrada na imagem a seguir:  
  
 ![Menu do Visual Studio formato com textos explicativos](../../extensibility/ux-guidelines/media/0501-d-formatmenu.png "d_FormatMenu 0501")  
  
 **Grupos de menus no Visual Studio**  
  
### <a name="reducing-and-reusing-commands"></a>Reduzindo e reutilização de comandos  
 Comandos são normalmente mostrados com base no contexto, para reduzir o número de comandos que o usuário vê a qualquer momento. No entanto, você também deve reutilizar os menus compartilhadas existentes e grupos de comando para garantir que a estrutura de comando permanece relativamente estável entre as alterações no contexto.  
  
 Reutilizando comandos compartilhados e colocando novos comandos próximos comandos compartilhados relacionados reduz a complexidade do IDE e cria uma experiência mais amigável.  
  
## <a name="naming-commands"></a>Comandos de nomenclatura  
  
### <a name="naming-conventions"></a>Convenções de nomenclatura  
 Comando consistente de nomeação é essencial para que os usuários podem localizar e executar comandos, usando a linha de comando ou associação a um atalho de teclado. Nomes de comando também ajudam o usuário a entender quais finalidade atende a um comando quando ele for exibido em uma barra de ferramentas ou em um menu de contexto ou em cascata.  
  
#### <a name="when-naming-commands"></a>Quando nomear comandos:  
  
-   Construa o texto para que ele seja facilmente localizável. Para obter mais informações sobre como localizar texto, consulte [preparação para o mundo para o Visual Studio](http://msdn.microsoft.com/en-us/1cc35051-8126-441f-bea9-059245a47b1d).  
  
-   Seja conciso. Comandos devem usar não mais do que três palavras.  
  
-   Usar a capitalização de capitalização de título: a primeira letra de cada palavra deve estar em letras maiusculas. Para obter mais informações sobre formatação de texto no Visual Studio, consulte [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).  
  
-   Leve em consideração onde o comando será colocado. Está em um menu de nível superior ou um submenu? Por exemplo, quando os comandos de alinhamento de agrupamento em um submenu, o comando de nível superior devem ser "Alinhar" e os comandos do submenu deve ser "À esquerda," "Direita", "Centro", "justificar" e assim por diante. Seria redundante para nomear os comandos de menu suspenso "Alinhar à esquerda" ou "Alinhar à direita."  
  
     ![Menu do Visual Studio formato](../../extensibility/ux-guidelines/media/0502-a-formatmenu.png "a_FormatMenu 0502")  
  
### <a name="using-icons-with-commands"></a>Usando ícones com comandos  
 Ser econômico no uso do emparelhamento com comandos de ícone. Embora a associação de uma imagem exclusiva com um comando acelera muito a capacidade do usuário para identificar esse comando, ineficiência e desordem visual ocorrem com uso excessivo de imagem. As regras a seguir ajudam ao decidir se deseja criar um ícone de comando.  
  
#### <a name="use-an-icon-with-a-command-only-if"></a>Use um ícone com um comando apenas se:  
  
-   O mesmo comando tem um ícone associado a ele em outro produto da Microsoft proeminente, por exemplo, um dos aplicativos do Microsoft Office.  
  
-   O comando será colocado em uma barra de ferramentas padrão.  
  
-   O comando é um comando de especialidade que os usuários podem adicionar a uma barra de ferramentas usando o **"Personalizar..."** caixa de diálogo.  
  
## <a name="access-and-shortcut-keys"></a>Teclas de atalho e acesso  
  
### <a name="overview"></a>Visão geral  
 Há dois tipos de atribuições de teclas do teclado:  
  
-   **Chaves de acesso** (também conhecido como aceleradores) permitem o acesso do teclado por meio de menus para comandos e a cada rótulo na caixa de diálogo da interface do usuário. Chaves de acesso são principalmente para fins de acessibilidade, são atribuídas a todos os menus e a maioria dos controles de caixa de diálogo, não devem ser memorizadas, afeta somente a janela atual e são localizadas.  
  
-   **Teclas de atalho** usar principalmente o controle (Ctrl) e sequências de teclas de função (Fn). Eles são projetados mais para usuários avançados e auxiliam na produtividade. Eles são atribuídos somente aos comandos usados com mais frequência e permitem o acesso rápido ao ignorar o menu principal. Teclas de atalho devem ser memorizadas e para que os motivo deve ser atribuído consistente com o esquema de perfil. Esquemas de chave de atalho podem variar de perfis. Um usuário pode personalizar as teclas de atalho por meio **Ferramentas > Opções > teclado**.  
  
### <a name="assigning-access-keys"></a>Atribuindo teclas de acesso  
 Chaves de acesso consistem em chaves Alt plus alfanuméricos. Atribua uma chave de acesso para cada item de menu sem exceção. Siga as convenções comuns para a atribuição de chaves de acesso e Windows. Por exemplo, a chave de acesso **arquivo > novo** deve ser sempre **Alt, F, N**.  
  
 Não use letras de largura de pixel único como 'i' (em maiusculas ou minúsculas) ou uma 'l' minúscula e evite usar caracteres com descendentes (g, j, p, q e y), já que elas são difíceis de distinguir.  
  
 Evite usar chaves duplicadas, sempre que possível. Em casos em que a eliminação de duplicação é inevitável, o sistema de menu manipula conflitos passando por todos os comandos que usam a chave. Por exemplo, para um controle de comando "Number" no menu Arquivo, o que duplica a chave de acesso de "N" **Alt, F, N** criaria um novo arquivo, e **Alt, F, N, N** deve executar o comando "Number".  
  
### <a name="assigning-shortcut-keys"></a>Atribuindo teclas de atalho  
 Evite atribuir novas teclas de atalho, porque eles não são necessários para todos os comandos e se o uso excessivo de imposto do sistema (e memória do usuário). Dados do programa de aperfeiçoamento de experiência para cliente (CEIP) indicam que os usuários do Visual Studio usem apenas um pequeno subconjunto dos atalhos integrados.  
  
 Ao definir atalhos, siga estas regras:  
  
- **Usar o controle (Ctrl) e sequências de teclas de função (Fn).**  
  
- **Preserve os atalhos usados com frequência.** Manter os atalhos mais populares.  
  
- **Atalhos do editor tornam fácil de tipo.** Associe atalhos de tipo fácil aos comandos que os desenvolvedores precisam maioria durante a gravação de código. Por exemplo, **Edit.InvokeSmartTag** precisa ter uma tecla de atalho rápido, como Ctrl + / e não Alt + Shift + F10.  
  
- **Se esforçar para atalhos consistentemente com tema.**  
  
- **Siga as diretrizes do Windows para determinar quais modificador teclas empregar.** Use combinações de teclas Ctrl para comandos que têm efeitos em larga escala, como comandos que se aplicam a um documento inteiro. Use combinações de tecla Shift para comandos que estenderem ou complementam as ações de tecla de atalho padrão. Não use combinações de teclas Ctrl + Alt.  
  
- **Remova atalhos estranhos.** Se você tiver um recurso herdado, considere remover atalhos que são usados com pouca frequência extrema, a (menos de 10 vezes dos dados do CEIP) ou pouca frequência moderada (menos de 100 vezes do que os dados do CEIP), se uma chave de acesso fornece acesso rápido para o mesmo comando. Por exemplo: C Alt, H, abrirá/conteúdo da Ajuda.  
  
  Não há uma maneira simples de verificar a disponibilidade de atalho. Se você quiser adicionar um atalho, siga estas etapas:  
  
1.  Verifique a lista de [atalhos do Visual Studio 2013](http://visualstudioshortcuts.com/2013/) para determinar se há comandos semelhantes para agrupar seus com.  
  
2.  Vá para **Ferramentas > Opções > ambiente > teclado** e testar o atalho. Verifique cada esquema de mapeamento de teclado listados em "Aplicar o seguinte esquema de mapeamento de teclado adicionais". Verifique perfis geral, c#, VB e C++, como aqueles compartilham atalhos exclusivos. O atalho está disponível se ela não estiver mapeada em qualquer um desses locais.

