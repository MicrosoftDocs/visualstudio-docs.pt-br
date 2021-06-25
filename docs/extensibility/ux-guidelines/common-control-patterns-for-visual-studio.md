---
title: Padrões de controle comuns para Visual Studio | Microsoft Docs
description: Saiba mais sobre como Visual Studio controles comuns seguem as diretrizes de interação da Área de Trabalho do Windows e sobre situações especiais que ampliam essas diretrizes.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 12d514bdc0aa37598ad57e0466bf57ba75ed2601
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899297"
---
# <a name="common-control-patterns-for-visual-studio"></a>Padrões de controle comuns para Visual Studio
## <a name="common-controls"></a><a name="BKMK_CommonControls"></a> Controles comuns

### <a name="overview"></a>Visão geral
Controles comuns comem a maioria da interface do usuário no Visual Studio. Os controles mais comuns usados na interface Visual Studio devem seguir as diretrizes de interação [da Área de Trabalho do Windows](/windows/desktop/uxguide/controls). Este tópico é específico para Visual Studio e aborda situações especiais ou detalhes que ampliam essas diretrizes do Windows.

#### <a name="common-controls-in-this-topic"></a>Controles comuns neste tópico

- [Barras de rolagem](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [Campos de entrada](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [Caixas de combinação e listas listadas](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [Caixas de seleção](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [Botões de opção](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [Quadros de grupo](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [Botões e hiperlinks](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [Modos de exibição de árvore](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>Estilo visual
A primeira coisa a ser considerada ao definir o estilo dos controles é se os controles serão usados na interface do usuário com temas. Os controles na interface do usuário padrão não têm temas e devem seguir o estilo normal da Área de Trabalho do [Windows,](/windows/desktop/uxguide/controls)o que significa que eles não são re-modelo e devem aparecer em sua aparência de controle padrão.

- **Caixas de diálogo padrão (utilitário) :** não tem temas. Não re-modelo. Use padrões de estilo de controle básico.

- **Janelas de ferramentas, editores de documentos, superfícies de design e caixas de diálogo com temas:** Use a aparência com temas especializados usando o serviço de cores.

### <a name="scroll-bars"></a><a name="BKMK_Scrollbars"></a> Barras de rolagem
 As barras de rolagem devem seguir padrões comuns de interação para barras de rolagem do [Windows,](/windows/desktop/Controls/about-scroll-bars) a menos que elas são aumentadas com informações de conteúdo, como no editor de código.

### <a name="input-fields"></a><a name="BKMK_InputFields"></a> Campos de entrada
 Para o comportamento de interação típico, siga as diretrizes [da Área de Trabalho do Windows para caixas de texto](/windows/desktop/uxguide/ctrl-text-boxes).

#### <a name="visual-style"></a>Estilo visual

- Os campos de entrada não devem ser estilados em caixas de diálogo do utilitário. Use o estilo básico intrínseco ao controle.

- Os campos de entrada com temas só devem ser usados em caixas de diálogo e janelas de ferramentas temas.

#### <a name="specialized-interactions"></a>Interações especializadas

- Os campos somente leitura terão um plano de fundo cinza (desabilitado), mas o primeiro plano padrão (ativo).

- Os campos necessários devem **\<Required>** ter como marcas-d'água dentro deles. Você não deve alterar a cor da tela de fundo, exceto em situações raras.

- Validação de erro: consulte [Notificações e progresso para Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- Os campos de entrada devem ser dimensionado para se ajustarem ao conteúdo, não para ajustar a largura da janela na qual eles são mostrados, nem corresponder arbitrariamente ao comprimento de um campo longo, como um caminho. Comprimento pode ser uma indicação para o usuário de limitações quanto a quantos caracteres são permitidos no campo.

     ![Comprimento incorreto do campo de entrada: é improvável que o nome seja tão longo.](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl")<br />Comprimento incorreto do campo de entrada: é improvável que o nome seja tão longo.

     ![Comprimento correto do campo de entrada: o campo de entrada é uma largura razoável para o conteúdo esperado.](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl")<br />Comprimento correto do campo de entrada: o campo de entrada é uma largura razoável para o conteúdo esperado.

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a> Caixas de combinação e listas listadas
Para o comportamento de interação típico, siga as diretrizes da Área de Trabalho do Windows para listas [e caixas de combinação.](/windows/desktop/uxguide/ctrl-drop)

#### <a name="visual-style"></a>Estilo visual

- Em caixas de diálogo do utilitário, não re-modelo do controle. Use o estilo básico intrínseco ao controle.

- Na interface do usuário com temas, as caixas de combinação e as listas de lista listadas seguem o temas padrão para os controles.

#### <a name="layout"></a>Layout
As caixas de combinação e as listadas devem ser dimensionada para se ajustar ao conteúdo, não para ajustar a largura da janela na qual elas são mostradas, nem para corresponder arbitrariamente ao comprimento de um campo longo, como um caminho.

![Incorreto: a largura do drop-down é muito longa para o conteúdo que será exibido.](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")<br />Incorreto: a largura do drop-down é muito longa para o conteúdo que será exibido.

![Correto: o drop-down é dimensionado para permitir o crescimento da tradução, mas não desnecessariamente longo.](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707-04_CorrectDropDownLayout")<br />Correto: o drop-down é dimensionado para permitir o crescimento da tradução, mas não desnecessariamente longo.

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a> Caixas de seleção
Para o comportamento de interação típico, siga as diretrizes da Área de [Trabalho do Windows para caixas de seleção](/windows/desktop/uxguide/ctrl-check-boxes).

#### <a name="visual-style"></a>Estilo visual

- Em caixas de diálogo do utilitário, não re-modelo do controle. Use o estilo básico intrínseco ao controle.

- Na interface do usuário com temas, as caixas de seleção seguem o temas padrão para os controles.

#### <a name="specialized-interactions"></a>Interações especializadas

- A interação com uma caixa de seleção nunca deve abrir uma caixa de diálogo ou navegar para outra área.

- Alinhe as caixas de seleção com a linha de base da primeira linha de texto.

     ![Incorreto: a caixa de seleção é centralizada no texto.](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign")<br />Incorreto: a caixa de seleção é centralizada no texto.

     ![Correto: a caixa de seleção é alinhada com a primeira linha do texto.](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign")<br />Correto: a caixa de seleção é alinhada com a primeira linha do texto.

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a> Botões
Para o comportamento de interação típico, siga as diretrizes da Área de [Trabalho do Windows para botões de rádio](/windows/desktop/uxguide/ctrl-radio-buttons).

#### <a name="visual-style"></a>Estilo visual
Em caixas de diálogo do utilitário, não estilmente os botões de rádio. Use o estilo básico intrínseco ao controle.

#### <a name="specialized-interactions"></a>Interações especializadas
Não é necessário usar um quadro de grupo para incluir opções de rádio, a menos que você precise manter a distinção de grupo em um layout rígido.

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a> Quadros de grupo
Para o comportamento de interação típico, siga as diretrizes da Área de [Trabalho do Windows para quadros de grupo.](/windows/desktop/uxguide/ctrl-group-boxes)

#### <a name="visual-style"></a>Estilo visual
Em caixas de diálogo do utilitário, não estilise quadros de grupo. Use o estilo básico intrínseco ao controle.

#### <a name="layout"></a>Layout

- Não é necessário usar um quadro de grupo para incluir opções de rádio, a menos que você precise manter a distinção de grupo em um layout rígido.

- Nunca use um quadro de grupo para um único controle.

- Às vezes, é aceitável usar uma regra horizontal em vez de um contêiner de quadro de grupo.

## <a name="text-controls"></a><a name="BKMK_TextControls"></a> Controles de texto

### <a name="static-text-fields"></a>Campos de texto estáticos

Um campo de texto estático apresenta informações somente leitura e não pode ser selecionado pelo usuário. Evite usá-lo para qualquer texto que o usuário queira copiar para a área de transferência. No entanto, o texto estático somente leitura pode mudar para refletir uma alteração no estado. No exemplo a seguir, o texto estático Nome de Saída no grupo Informações muda para refletir as alterações feitas na caixa de texto Namespace Raiz acima dele.

Há duas maneiras de exibir informações de texto estático.

O texto estático pode estar por conta própria em uma caixa de diálogo sem nenhuma contenção quando não há nenhum conflito de agrupamento. Decida se as linhas extras de uma caixa são realmente necessárias. Um exemplo é a exibição de um caminho de diretório em uma seção criada por uma linha de grupo, conforme mostrado abaixo:

![Informações de texto estático em controles de texto](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "DisplayingStaticText.png")<br />Informações de texto estático em controles de texto

Em uma caixa de diálogo em que existem outras áreas agrupadas e a contenção das informações ajudaria na leitura e quando uma seção puder ser oculta ou mostrada (como no painel de descrição do **janela Propriedades)** ou se você quiser ser consistente com uma interface do usuário semelhante, coloque o texto estático dentro de uma caixa. Essa caixa de grupo deve ser uma única regra e colorida com o `ButtonShadow` :

![Texto estático no janela Propriedades](../../extensibility/ux-guidelines/media/PropertiesWindow.png "PropertiesWindow.png")<br />Texto estático na janela Propriedades

### <a name="read-only-text-box"></a>Caixa de texto somente leitura

Isso permite que o usuário selecione o texto dentro do campo, mas não o edite. Essas caixas de texto são preenchidas pelo cinzel tradicional de 3D com um `ButtonShadow` preenchimento.

Uma caixa de texto pode se tornar ativa (editável) quando um usuário altera um controle associado, como marcar/desmarcar uma caixa de seleção ou selecionar/desmarcar um botão de opção. Por exemplo, na página **&gt; Opções de ferramentas** mostrada abaixo, a caixa de texto **página inicial** fica ativa quando a caixa de seleção **usar padrão** está desmarcada.

![Caixa de texto somente leitura, mostrando Estados inativos e ativos](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "ReadOnlyTextBox.png")<br />Caixa de texto somente leitura, mostrando Estados inativos e ativos

### <a name="using-text-in-dialogs"></a>Usando texto em caixas de diálogo

Principais diretrizes para texto em caixas de diálogo:

- Os rótulos para caixas de texto, caixas de listagem e quadros em caixas de diálogo com falha começam com um verbo, têm uma capital inicial na primeira palavra apenas e terminam com dois-pontos.

    > Os controles de texto nas caixas de diálogo com tema seguem as [diretrizes de UX do Windows Desktop](/windows/desktop/uxguide/top-violations) e não assumem a pontuação final, com exceção dos pontos de interrogação nos links da ajuda.

- Os rótulos para caixas de seleção e botões de opção começam com um verbo, uma capital inicial na primeira palavra apenas e não têm pontuação final.

- Rótulos de botões, menus, itens de menu e guias têm maiúsculas iniciais em cada palavra (caso de título).

- A terminologia do rótulo deve ser consistente com rótulos semelhantes em outras caixas de diálogo.

- Se possível, faça com que um gravador/editor grave ou aprove o texto antes de ir para o desenvolvedor para implementação.

- Todos os controles devem ter rótulos, exceto em circunstâncias especiais nas quais a Tabulação é suficiente.
Use o texto auxiliar quando apropriado.

### <a name="helper-text"></a>Texto do auxiliar

Incluído em caixas de diálogo para ajudar o usuário a entender a finalidade da caixa de diálogo ou para indicar a ação a ser tomada. O texto do auxiliar deve ser usado somente quando necessário para evitar a aglomeração de caixas de diálogo simples. As duas variações de texto auxiliar são caixa de diálogo e marca-d ' água.

Siga locais comuns para texto auxiliar e seja seletivo na introdução de novas áreas. Os cenários comuns de texto auxiliar são:

- Texto auxiliar em caixas de diálogo, para dar mais orientação sobre como interagir com uma caixa de diálogo complexa.

- Texto de marca d' água em janelas de ferramentas vazias ou caixas de diálogo, para explicar por que nenhum conteúdo está visível.

- Um painel de descrição, como na parte inferior da **janela Propriedades**.

- Texto de marca d' água em um editor vazio, para explicar a ação que o usuário deve executar para começar.

### <a name="dialog-helper-text"></a>Texto auxiliar de diálogo

Um designer de experiência do usuário pode ajudar a determinar quando o texto auxiliar é apropriado. O designer pode definir onde o texto auxiliar aparece, bem como seu conteúdo geral. A assistência ao usuário pode gravar/editar o texto real.

### <a name="watermarks"></a>Marcas d' água

As caixas de diálogo se beneficiam de diretrizes de marca d' água ligeiramente diferentes. Como uma caixa de diálogo pode aparecer ocupada com muitos elementos da interface do usuário (rótulos, texto de dica, botões e outros controles de contêiner com texto), especialmente quando eles aparecem em preto, as marcas d' água se destacam melhor em cinza escuro (VSColor: `ButtonShadow` ). Normalmente, uma marca d' água aparece dentro de um controle como uma caixa de listagem com um plano de fundo branco (VSColor: `Window` ).

- O texto aparece em cinza escuro (VSColor: `ButtonShadow` ). No entanto, se a marca d' água aparecer em um segundo plano cinza médio ou outro colorido (VSColor: `ButtonFace` ) e houver preocupação com a legibilidade, vá com texto em preto (VSColor: `WindowText` ).

- As marcas d' água podem ser centralizadas ou alinhadas à esquerda. Aplique regras de design padrão ao tomar decisões de alinhamento. A marca d' água não pode ser selecionada em segundo plano.

![Exemplo de texto de marca d' água](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />Exemplo de texto de marca d' água

### <a name="context-specific-dynamic-text"></a>Texto específico do contexto (dinâmico)

O texto dinâmico pode ser usado de duas maneiras em uma interface do usuário sem janela restrita: como um rótulo dinâmico ou um conteúdo dinâmico.

- Rótulo dinâmico: um uso comum de texto dinâmico está em painéis descritivos que oferecem mais informações para o item selecionado, como em uma caixa de diálogo que contém uma lista de elementos e propriedades para esses elementos exibidos em uma grade à direita. O rótulo da grade de propriedades pode ser dinâmico para que, quando um item for selecionado à esquerda, a grade à direita mostre informações para esse item específico.

- Texto dinâmico: pode ser útil em instâncias em que você precisa exibir informações específicas e não informações gerais dessa maneira, mas deve-se tomar cuidado para não estar em excesso.

Se você quiser que os usuários tenham a capacidade de copiar as informações, o texto dinâmico deverá estar em um campo de texto somente leitura.

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a> Botões e hiperlinks

### <a name="overview"></a>Visão geral
Os botões e controles de link (hiperlinks) devem seguir as [diretrizes básicas da área de trabalho do Windows em hiperlinks](/windows/desktop/uxguide/ctrl-links) para uso, palavras, dimensionamento e espaçamento.

### <a name="choosing-between-buttons-and-links"></a>Escolhendo entre botões e links
Tradicionalmente, os botões foram usados para ações e os hiperlinks foram reservados para navegação. Os botões podem ser usados em todos os casos, mas a função de links foi expandida no Visual Studio para que os botões e links sejam mais intercambiáveis em algumas condições.

Quando usar botões de comando:

- Comandos principais

- Exibindo as janelas usadas para reunir entrada ou fazer escolhas, mesmo que sejam comandos secundários

- Ações destrutivas ou irreversíveis

- Botões de compromisso dentro de assistentes e fluxos de página

Evite botões de comando em janelas de ferramentas ou se precisar de mais de duas palavras para o rótulo. Os links podem ter rótulos mais longos.

 Quando usar links:

- Navegação para outra janela, documento ou página da Web

- Situações que exigem um rótulo mais longo ou uma frase curta para descrever a intenção da ação

- Espaços apertados em que um botão sobrecarrega a interface do usuário, contanto que a ação não seja destrutiva ou irreversível

- Desenfatizando comandos secundários em situações em que há muitos comandos

#### <a name="examples"></a>Exemplos
![Links de comando usados na barra de opções seguindo uma mensagem de status](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703-01_CommandLinkInfobar")<br />Links de comando usados na barra de opções seguindo uma mensagem de status

![Links usados no pop-up CodeLens](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703-02_LinksInCodeLens")<br />Links usados no pop-up CodeLens

![Links usados para comandos secundários em que os botões atraiam muita atenção](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")<br />Links usados para comandos secundários em que os botões atraiam muita atenção

### <a name="common-buttons"></a>Botões comuns

#### <a name="text"></a>Texto
Siga as diretrizes de escrita em [texto e terminologia da interface do usuário](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology).

#### <a name="visual-style"></a>Estilo visual

##### <a name="standard-unthemed"></a>Padrão (não-tem)
A maioria dos botões no Visual Studio aparecerá nas caixas de diálogo do utilitário e não deverá ser estilizada. Eles devem refletir a aparência padrão dos botões, conforme determinado pelo sistema operacional.

##### <a name="themed"></a>Com tema
Em alguns casos, os botões podem ser usados na interface do usuário com estilo e esses botões devem ser estilizados adequadamente. Consulte [caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) para obter informações sobre controles com tema.

### <a name="special-buttons"></a>Botões especiais

#### <a name="browse-buttons"></a>Procurar... botões
**[Procurar...]** os botões são usados em grades, caixas de diálogo e janelas de ferramentas e outros elementos de interface do usuário sem janela restrita. Eles exibem um seletor que auxilia o usuário a preencher um valor em um controle. Há duas variações desse botão, longas e curtas.

![O botão longo [procurar...]](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703-04_BrowseLong")<br />O botão longo [procurar...]

![O botão [...] curto somente-reticências](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703-05_BrowseShort")<br />O botão [...] curto somente-reticências

Quando usar o botão curto somente de reticências:

- Se houver mais de um botão **[procurar...]** em uma caixa de diálogo, como quando vários campos permitirem navegação. Use o botão **[...]** curto para cada um para evitar as chaves de acesso confusas criadas por essa situação (**&procurar** e **B&linhas** na mesma caixa de diálogo).

- Em uma caixa de diálogo rígida ou quando não há nenhum local razoável para colocar o botão longo.

- Se o botão aparecerá em um controle de grade.

Diretrizes para usar o botão:

- Não use uma chave de acesso. Para acessá-lo usando o teclado, o usuário deve tabular do controle adjacente. Verifique se a ordem de tabulação é tal que qualquer botão procurar cai imediatamente após o campo que ele preencherá. Nunca use um sublinhado abaixo do primeiro período.

- De definir a propriedade Microsoft Active Accessibility (MSAA) **Name** **como Procurar...** (incluindo as reellipses) para que os leitores de tela a leiam como "Procurar" e não como "ponto-ponto" ou "período de período". Para controles gerenciados, isso significa definir **a propriedade AccessibleName.**

- Nunca use um botão de reellipse **[...]** para qualquer coisa, exceto uma ação de navegação. Por exemplo, se você precisar de um **botão [Novo...]** mas não tiver espaço suficiente para o texto, a caixa de diálogo precisará ser reprojetada.

##### <a name="sizing-and-spacing"></a>Espaçamento e espaçamento
![Botões de [Procurar...]: a versão padrão tem 75 x 23 pixels, a versão curta é de 26x23 pixels](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703-06_BrowseSizing")<br />Botões de [Procurar...]

![Espaçamento [Procurar...] botões: espaçamento entre o controle relacionado e o botão Procurar padrão de 7 pixels, espaçamento entre o controle relacionado e o botão Procurar curto de 5 pixels](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703-07_BrowseSpacing")<br />Botões de espaçamento [Procurar...]

#### <a name="graphical-buttons"></a>Botões gráficos
Alguns botões sempre devem usar uma imagem gráfica e nunca incluir texto para economizar espaço e evitar problemas de localização. Elas geralmente são usadas em seladores de campo e em outras listas sortíveis.

> [!NOTE]
> Os usuários têm que tabular para esses botões (não há chaves de acesso), portanto, coloque-os em uma ordem razoável. Mapeie a propriedade do botão para a ação que ele toma para que os leitores de tela `name` interpretem corretamente a ação do botão.

| Função | Botão |
| --- | --- |
| Adicionar | ![Botão gráfico "Adicionar"](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703-08_ButtonAdd") |
| Remover | ![Botão gráfico "Remover"](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703-09_ButtonRemove") |
| Adicionar todos | ![Botão gráfico "Adicionar Tudo"](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703-10_ButtonAddAll") |
| Remover Tudo | ![Botão gráfico "Remover Tudo"](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703-11_ButtonRemoveAll") |
| Mover para Cima | ![Botão gráfico "Mover para Cima"](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703-12_ButtonMoveUp") |
| Mover para Baixo | ![Botão gráfico "Mover para Baixo"](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703-13_ButtonMoveDown") |
| Excluir | ![Botão "Excluir" gráfico](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703-14_ButtonDelete") |

##### <a name="sizing-and-spacing"></a>Espaçamento e espaçamento
O tamanho dos botões gráficos é o mesmo da versão curta **do botão [Procurar...]** (26x23 pixels):

![Aparência de uma imagem gráfica no botão, com e sem cor transparente mostrando](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")<br />Aparência de uma imagem gráfica no botão, com e sem cor transparente mostrando

### <a name="hyperlinks"></a>Hiperlinks
Hiperlinks são adequados para ações baseadas em navegação, como abrir um tópico de Ajuda, uma caixa de diálogo modal ou um assistente. Se um hiperlink for usado para um comando, ele sempre deverá exibir uma alteração visível e perceptível na interface do usuário. Em geral, as ações que se comprometem com uma ação (como Salvar, Cancelar e Excluir) são mais bem comunicadas usando um botão.

#### <a name="writing-style"></a>Estilo de escrita
Siga as [diretrizes da Área de Trabalho do Windows para o texto da interface do usuário](/windows/desktop/uxguide/text-ui). Não use a frase "Saiba mais sobre", "Conte-me mais sobre" ou "Obter ajuda com isso". Em vez disso, a frase Ajuda vincula texto em termos da pergunta primária respondida pelo conteúdo da Ajuda. Por exemplo, "**Como fazer adicionar um servidor ao Gerenciador de Servidores?**"

#### <a name="visual-style"></a>Estilo visual

- Os hiperlinks sempre devem usar [o Serviço VSColor.](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService) Se um hiperlink não tiver o estilo correto, ele piscará em vermelho quando estiver ativo ou mostrará uma cor diferente depois de ser visitado.

- Não inclua sublinhados no estado de controle de controle, a menos que o link seja um fragmento de frase dentro de uma frase completa, como em uma marca-d'água.

- Sublinhados não devem aparecer ao passar o mouse. Em vez disso, os comentários para o usuário de que o link está ativo são uma pequena alteração de cor e o cursor de link apropriado.

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a> Exibições de árvore

As exibições de árvore fornecem uma maneira de organizar listas complexas em grupos pai-filho. Um usuário pode expandir ou ressumentar grupos pai para revelar ou ocultar itens filho subjacentes. Cada item dentro de uma exibição de árvore pode ser selecionado para fornecer mais ações.

### <a name="tree-view-visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a> Estilo visual de exibição de árvore

#### <a name="expanders"></a>Expansores
Os controles de exibição de árvore devem estar em conformidade com o design do expansador usado pelo Windows e Visual Studio. Cada nó usa um controle de expansão para revelar ou ocultar itens subjacentes. O uso de um controle de expansão fornece consistência para usuários que podem encontrar diferentes exibições de árvore no Windows e Visual Studio.

![Correto: estilo adequado do nó de exibição de árvore usando um controle de expansão](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />Correto: estilo adequado do nó de exibição de árvore usando um controle de expansão

![Incorreto: estilo inadequado do nó de exibição de árvore](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705-2_TreeViewIncorrect1")<br />Incorreto: estilo inadequado do nó de exibição de árvore

#### <a name="selection"></a>Seleção
Quando um nó é selecionado no exibição de árvore, o realçando deve expandir para a largura total do controle de exibição de árvore. Isso ajuda os usuários a identificar claramente qual item eles selecionaram. As cores da seleção devem refletir o tema Visual Studio atual.

![Correto: realça o nó selecionado se ajusta a toda a largura do controle de exibição de árvore.](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705-1_TreeViewCorrect")<br />Correto: realça o nó selecionado se ajusta a toda a largura do controle de exibição de árvore.

![Incorreto: o destaque do nó selecionado não se ajusta a toda a largura do controle de exibição de árvore.](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705-3_TreeViewIncorrect2")<br />Incorreto: o destaque do nó selecionado não se ajusta a toda a largura do controle de exibição de árvore.

#### <a name="icons"></a>Ícones
Os ícones só deverão ser usados em controles de exibição de árvore se ajudarem a identificar visualmente as diferenças entre os itens. Em geral, os ícones devem ser usados somente em listas heterogêneas nas quais os Ícones transportam informações para diferenciar os tipos de elementos. Em uma lista homogênea usando ícones, frequentemente pode ser visto como ruído e deve ser evitado. Nesse caso, o ícone de grupo (pai) pode transmitir o tipo de itens dentro dele. A exceção a essa regra seria se o ícone fosse dinâmico e fosse usado para indicar o estado.

#### <a name="scroll-bars"></a>Barras de rolagem
As barras de rolagem sempre deverão ser ocultas se o conteúdo se encaixar no controle de exibição de árvore. É aceitável que as barras de rolagem sejam ocultas ou semi transparentes em uma janela rolável e apareçam quando a janela que contém a exibição de árvore tiver foco ou ao passar o mouse do próprio ponto de exibição de árvore.

![As barras de rolagem vertical e horizontal são exibidas porque o conteúdo excedeu os limites do controle de exibição de árvore.](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705-4_Scrollbars")<br />As barras de rolagem vertical e horizontal são exibidas porque o conteúdo excedeu os limites do controle de exibição de árvore.

### <a name="tree-view-interactions"></a><a name="BKMK_TreeViewInteractions"></a> Interações de exibição de árvore

#### <a name="context-menus"></a>Menus de contexto
Um nó de exibição de árvore pode revelar opções de submenu em um menu de contexto. Normalmente, isso ocorre quando um usuário clica com o botão direito do mouse em um item ou pressiona a tecla Menu em um teclado do Windows com o item selecionado. É importante que o nó se concentre e seja selecionado. Isso ajuda o usuário a identificar a qual item o submenu pertence.

![O item que gerou o menu de contexto obtém o foco para notificar o usuário sobre qual item foi selecionado.](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705-5_ContextMenu")<br />O item que gerou o menu de contexto obtém o foco para notificar o usuário sobre qual item foi selecionado.

#### <a name="keyboard"></a>Teclado
A exibição de árvore deve fornecer a capacidade de selecionar itens e expandir/fechar nós usando o teclado. Isso garante que a navegação atenda aos nossos requisitos de acessibilidade.

##### <a name="tree-view-control"></a>Controle de exibição de árvore
Visual Studio de árvore devem seguir a navegação comum do teclado:

- **Seta para cima:** Selecionar itens movendo a árvore para cima

- **Seta para baixo:** Selecionar itens movendo para baixo a árvore

- **Seta para a direita:** Expandir um nó na árvore

- **Seta para a esquerda:** Recolher um nó na árvore

- **Inserir chave:** Iniciar, carregar, executar o item selecionado

##### <a name="trid-tree-view-and-grid-view"></a>TrID (exibição de árvore e exibição de grade)
Um controle TrID é um controle complexo que contém um modo de exibição de árvore dentro de uma grade. Expandir, recolher e navegar na árvore deve respeitar os mesmos comandos de teclado que um modo de exibição de árvore, com as seguintes adições:

- **Seta para a direita:** Expanda um nó. Depois que o nó é expandido, ele deve continuar navegando até a coluna mais próxima à direita. A navegação deve parar no final da linha.

- **Guia:** Navega até a célula mais próxima à direita.  No final da linha, a navegação continua para a próxima linha.

- **Shift + Tab:** Navega para a célula mais próxima à esquerda.  No início da linha, a navegação continua para a célula mais à direita na linha anterior.

![Um controle TrID no Visual Studio](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705-6_Trid")<br />Um controle TrID no Visual Studio
