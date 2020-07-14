---
title: Padrões de controle comuns
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dd2b2723a5ecfe66e9471cfea1e8eb55ed7ced59
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547440"
---
# <a name="common-control-patterns-for-visual-studio"></a>Padrões de controle comuns para Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="common-controls"></a><a name="BKMK_CommonControls"></a>Controles comuns

### <a name="overview"></a>Visão geral
 Os controles comuns compõem a maior parte da interface do usuário no Visual Studio. Os controles mais comuns usados na interface do Visual Studio devem seguir as [diretrizes de interação do Windows Desktop](https://msdn.microsoft.com/library/windows/desktop/dn742399.aspx). Este documento é específico do Visual Studio e cobre situações especiais ou detalhes que aumentam essas diretrizes do Windows.

#### <a name="common-controls-in-this-topic"></a>Controles comuns neste tópico

- [Rolagem](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)

- [Campos de entrada](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)

- [Caixas de combinação e listas suspensas](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)

- [Caixas de seleção](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)

- [Botões de opção](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)

- [Agrupar quadros](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)

- [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)

- [Botões e hiperlinks](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)

- [Modos de exibição de árvore](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)

#### <a name="visual-style"></a>Estilo visual
 A primeira coisa a considerar ao estilizar controles é se os controles serão usados na interface do usuário com tema. Os controles na interface do usuário padrão são uma interface do usuário sem temas e devem seguir o [estilo normal do Windows Desktop](https://msdn.microsoft.com/library/windows/desktop/dn742399\(v=vs.85\).aspx), o que significa que eles não são redefinidos e devem aparecer na aparência de controle padrão.

- **Caixas de diálogo padrão (utilitário):** não são. Não recriar modelo. Usar padrões de estilo de controle básico.

- **Janelas de ferramentas, editores de documentos, superfícies de design e caixas de diálogo com tema:** Use a aparência com tema especializada usando o serviço de cores.

### <a name="scrollbars"></a><a name="BKMK_Scrollbars"></a>Rolagem
 As barras de rolagem devem seguir [padrões comuns de interação para barras de rolagem do Windows](https://msdn.microsoft.com/library/windows/desktop/bb787527\(v=vs.85\).aspx) , a menos que sejam aumentadas com informações de conteúdo, como no editor de códigos.

### <a name="input-fields"></a><a name="BKMK_InputFields"></a>Campos de entrada
 Para um comportamento de interação típico, siga as [diretrizes de área de trabalho do Windows para caixas de texto](https://msdn.microsoft.com/library/windows/desktop/dn742442\(v=vs.85\).aspx).

#### <a name="visual-style"></a>Estilo visual

- Os campos de entrada não devem ser estilizados em caixas de diálogo do utilitário. Use o estilo básico intrínseco ao controle.

- Os campos de entrada com tema só devem ser usados em caixas de diálogo e janelas de ferramentas com tema.

#### <a name="specialized-interactions"></a>Interações especializadas

- Os campos somente leitura terão um plano de fundo cinza (desabilitado), mas padrão (ativo).

- Os campos obrigatórios devem ter **\<Required>** marcas d' água dentro deles. Você não deve alterar a cor do plano de fundo, exceto em situações raras.

- Validação de erro: consulte [notificações e progresso para o Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)

- Os campos de entrada devem ser dimensionados para ajustar o conteúdo, não ajustar a largura da janela na qual eles são mostrados, nem corresponder arbitrariamente ao comprimento de um campo longo, como um caminho. Comprimento pode ser uma indicação para o usuário de limitações quanto a quantos caracteres são permitidos no campo.

     Tamanho do campo de entrada incorreto da ![largura de controle do campo de entrada](../../extensibility/ux-guidelines/media/0707-01-incorrectinputfieldcontrol.png "0707-01_IncorrectInputFieldControl") incorreto **: é improvável que o nome seja o longo.**

     ![Correta largura de controle do campo de entrada](../../extensibility/ux-guidelines/media/0707-02-correctinputfieldcontrol.png "0707-02_CorrectInputFieldControl") **tamanho correto do campo de entrada: o campo de entrada é uma largura razoável para o conteúdo esperado.**

### <a name="combo-boxes-and-drop-down-lists"></a><a name="BKMK_ComboBoxesAndDropDowns"></a>Caixas de combinação e listas suspensas
 Para comportamento de interação típico, siga as [diretrizes de área de trabalho do Windows para listas suspensas e caixas de combinação](https://msdn.microsoft.com/library/windows/desktop/dn742404\(v=vs.85\).aspx).

#### <a name="visual-style"></a>Estilo visual

- Em caixas de diálogo do utilitário, não refaça o remodelo do controle. Use o estilo básico intrínseco ao controle.

- Na interface do usuário com tema, caixas de combinação e menus suspensos seguem os padrões para os controles.

#### <a name="layout"></a>Layout
 As caixas de combinação e os menus suspensos devem ser dimensionados para ajustar o conteúdo, não ajustar a largura da janela na qual eles são mostrados, nem corresponder arbitrariamente ao comprimento de um campo longo, como um caminho.

 ![Layout de soltar&#45;para baixo incorreto](../../extensibility/ux-guidelines/media/0707-03-incorrectdropdownlayout.png "0707-03_IncorrectDropDownLayout")

 **Comprimento de campo incorreto para um controle suspenso**

 ![Corrigir layout de soltar&#45;para baixo](../../extensibility/ux-guidelines/media/0707-04-correctdropdownlayout.png "0707-04_CorrectDropDownLayout")

 **Corrigir o tamanho do campo para um controle suspenso**

### <a name="check-boxes"></a><a name="BKMK_CheckBoxes"></a>Caixas de seleção
 Para comportamento de interação típico, siga as [diretrizes de área de trabalho do Windows para caixas de seleção](https://msdn.microsoft.com/library/windows/desktop/dn742401\(v=vs.85\).aspx).

#### <a name="visual-style"></a>Estilo visual

- Em caixas de diálogo do utilitário, não refaça o remodelo do controle. Use o estilo básico intrínseco ao controle.

- Na interface do usuário com tema, as caixas de seleção seguem as instruções padrão para os controles.

#### <a name="specialized-interactions"></a>Interações especializadas

- A interação com uma caixa de seleção nunca deve aparecer ou navegar para outra área.

- Alinhar caixas de seleção com a linha de base da primeira linha de texto.

     Alinhamento da caixa de seleção ![incorreto](../../extensibility/ux-guidelines/media/0707-05-incorrectcheckboxalign.png "0707-05_IncorrectCheckBoxAlign") alinhamento **da caixa de seleção: a caixa de seleção está centralizada no texto.**

     Correção da caixa de seleção ![corrigir alinhamento](../../extensibility/ux-guidelines/media/0707-06-correctcheckboxalign.png "0707-06_CorrectCheckBoxAlign") da caixa de seleção **: a caixa de seleção está alinhada com a linha de base da primeira linha de texto.**

### <a name="radio-buttons"></a><a name="BKMK_RadioButtons"></a>Botões de opção
 Para um comportamento de interação típico, siga as [diretrizes de área de trabalho do Windows para botões de opção](https://msdn.microsoft.com/library/windows/desktop/dn742436\(v=vs.85\).aspx).

#### <a name="visual-style"></a>Estilo visual
 Em caixas de diálogo do utilitário, não faça o estilo dos botões de opção. Use o estilo básico intrínseco ao controle.

#### <a name="specialized-interactions"></a>Interações especializadas
 Não é necessário usar um quadro de grupo para incluir opções de rádio.

### <a name="group-frames"></a><a name="BKMK_GroupFrames"></a>Agrupar quadros
 Para comportamento de interação típico, siga as [diretrizes de área de trabalho do Windows para quadros de grupo](https://msdn.microsoft.com/library/windows/desktop/dn742405\(v=vs.85\).aspx).

#### <a name="visual-style"></a>Estilo visual
 Em caixas de diálogo de utilitário, não estilizar quadros de grupo. Use o estilo básico intrínseco ao controle.

#### <a name="layout"></a>Layout

- Não é necessário usar um quadro de grupo para incluir opções de rádio, a menos que você precise manter a distinção de grupos em um layout rígido.

- Nunca use um quadro de grupo para um único controle.

- Às vezes, é aceitável usar uma regra horizontal em vez de um contêiner de quadro de grupo.

## <a name="text-controls"></a><a name="BKMK_TextControls"></a>Controles de texto

### <a name="labels"></a>Rótulos

#### <a name="active-label-state"></a>Estado do rótulo ativo

##### <a name="utility-standard-dialogs"></a>Caixas de diálogo do utilitário (padrão))

- Em geral, siga as diretrizes de área de trabalho do Windows para rótulos de controle.

- Nas caixas de diálogo do utilitário, os rótulos devem aparecer em negrito, na fonte do ambiente padrão e na cor do texto. Consulte [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md).

- As reticências sempre devem seguir rótulos.

##### <a name="signature-themed-dialogs"></a>Caixas de diálogo de assinatura (com tema))
 Os controles de rótulo podem estar em negrito ou cinza claro.

#### <a name="disabled-label-state"></a>Estado de rótulo desabilitado
 Os rótulos devem refletir a aparência do controle ao qual estão associados. Por exemplo, se o controle associado estiver desabilitado, o rótulo deverá aparecer em cinza e desabilitado. Isso geralmente é tratado pelo sistema operacional e não requer tratamento especial.

#### <a name="dynamic-labels"></a>Rótulos dinâmicos
 Rótulos dinâmicos são alterados com base na seleção atual. Sempre que possível, use rótulos dinâmicos em layouts mestre/de detalhes para ajudar o usuário a entender que as informações exibidas são relevantes para uma seleção específica e não informações gerais.

 ![Rótulo dinâmico usado com conteúdo dinâmico](../../extensibility/ux-guidelines/media/070702-01-dynamiclabel.png "070702-01_DynamicLabel")

 **Exemplo de um rótulo dinâmico usado com conteúdo dinâmico**

#### <a name="instructional-text"></a>Texto de instrução
 Alguns elementos de interface beneficiam-se de texto instrutivo para ajudar o usuário a entender a finalidade da interface ou indicar qual ação deve ser tomada.

- O texto instrutivo é mais comum na parte superior das caixas de diálogo, mas pode aparecer em outras áreas para dar instruções a um agrupamento de controle complexo.

- O texto de instrução não é interativo, mas pode conter hiperlinks para tópicos de ajuda.

- Use o texto de instrução com moderação e apenas quando necessário.

##### <a name="formatting"></a>Formatação
 O texto instrutivo deve ser uma fonte de ambiente, texto de controle padrão (não-com). Consulte [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md).

 Para obter detalhes sobre como escrever texto de instruções, consulte a [terminologia e o texto da interface do usuário](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology).

 ![Formatação de texto de instrução](../../extensibility/ux-guidelines/media/070702-02-instructionaltextformatting.png "070702-02_InstructionalTextFormatting")

 **Texto instrutivo em uma caixa de diálogo do Visual Studio**

#### <a name="informational-text"></a>Texto informativo
 Texto informativo é um texto que fornece informações adicionais ao usuário. Pode ser estático ou dinâmico, ou ser usado como uma notificação. Ele é sempre somente leitura, mas se for útil para o usuário ter a capacidade de copiar as informações, o texto dinâmico deverá ser colocado em um contêiner de controle, como um campo de texto somente leitura.

##### <a name="dynamic-context-specific-text"></a>Texto dinâmico (específico do contexto)
 Alterações de texto de informações dinâmicas dependendo do contexto, como quando o usuário alterna o foco. Geralmente, mas nem sempre, o conteúdo dinâmico é emparelhado com um rótulo dinâmico.

 ![Texto de informações dinâmicas](../../extensibility/ux-guidelines/media/070702-03-informationaldynamictext.png "070702-03_InformationalDynamicText")

 **Alterações de texto informativo dinâmico dependendo do contexto.**

##### <a name="formatting"></a>Formatação
 Há duas maneiras de exibir campos de texto somente leitura: diretamente na superfície da interface do usuário (veja acima) ou contidos em outro controle, como um quadro de grupo ou uma caixa de texto. O está correto, dependendo da situação. Cabe ao designer de recursos determinar como apresentar as informações somente leitura.

 O texto pode estar dentro de uma caixa de texto somente leitura. Isso geralmente indica que o conteúdo pode ser selecionado e copiado, embora não possa ser editado.

 ![Formatação de texto informativo para campos somente leitura&#45;](../../extensibility/ux-guidelines/media/070702-04-informationalformatting.png "070702-04_InformationalFormatting")

 **Formatação de texto informativo para campos somente leitura**

#### <a name="watermarks"></a>Marcas d' água
 Embora as palavras possam ser as mesmas, a diferença entre marcas-d ' água e texto de instrução é que as marcas d' água são substituídas por conteúdo quando o controle/janela não está vazio, e o texto de instrução permanece visível em todos os momentos.

 As marcas d' água devem ser usadas quando uma janela ou um controle estiver vazio. Eles indicam o que precisa ser feito para preencher a área e podem incluir links de ação para abrir janelas relevantes, como uma origem de arrastar.

##### <a name="visual-style"></a>Estilo visual

- As marcas d' água devem ser centralizadas horizontalmente dentro da janela.

- As marcas d' água devem ser alinhadas no centro, não alinhadas à esquerda.

- As marcas d' água podem estar verticalmente centralizadas ou posicionadas próximo à parte superior da área. Se estiver localizado próximo à parte superior da área, deverá haver espaço suficiente acima para que a marca d' água se destaque.

- Use o `Environment.GrayText` token de cor e a fonte de ambiente padrão. Os hiperlinks devem usar os tokens compartilhados de hiperlink padrão: `Environment.PanelHyperlink` , `Environment.PanelHyperlinkHover` , `Environment.PanelHyperlinkPressed` e `Environment.PanelHyperlinkDisabled` .

- As marcas d' água não podem ser selecionadas em segundo plano

- Se possível, inclua links na marca d' água para ajudar o usuário a começar.

  ![Texto de marca d' água em uma janela do designer](../../extensibility/ux-guidelines/media/070702-05-watermark1.png "070702-05_Watermark1")

  ![Texto de marca d' água em uma janela de ferramentas](../../extensibility/ux-guidelines/media/070702-06-watermark2.png "070702-06_Watermark2")

  **Exemplos de texto de marca d' água no Visual Studio**

## <a name="buttons-and-hyperlinks"></a><a name="BKMK_ButtonsAndHyperlinks"></a>Botões e hiperlinks

### <a name="overview"></a>Visão geral
 Os botões e controles de link (hiperlinks) devem seguir as [diretrizes básicas da área de trabalho do Windows em hiperlinks](https://msdn.microsoft.com/library/windows/desktop/dn742406\(v=vs.85\).aspx) para uso, palavras, dimensionamento e espaçamento.

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
 ![Links de comando da barra de opções seguindo uma mensagem de status](../../extensibility/ux-guidelines/media/070703-01-commandlinkinfobar.png "070703-01_CommandLinkInfobar")

 **Links de comando usados na barra de opções seguindo uma mensagem de status**

 ![Links usados no pop-up CodeLens](../../extensibility/ux-guidelines/media/070703-02-linksincodelens.png "070703-02_LinksInCodeLens")

 **Links usados no pop-up CodeLens**

 ![Links usados como comandos secundários](../../extensibility/ux-guidelines/media/070703-03-linksassecondarycommands.png "070703-03_LinksAsSecondaryCommands")

 **Links usados para comandos secundários em que os botões atraiam muita atenção**

### <a name="common-buttons"></a>Botões comuns

#### <a name="text"></a>Texto
 Siga as diretrizes de escrita em [texto e terminologia da interface do usuário](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology).

#### <a name="visual-style"></a>Estilo visual

##### <a name="standard-dialogs"></a>Caixas de diálogo padrão
 A maioria dos botões no Visual Studio aparecerá em caixas de diálogo padrão e não deverá ser estilizada. Eles devem refletir a aparência padrão dos botões, conforme determinado pelo sistema operacional.

##### <a name="themed"></a>Com tema
 Em alguns casos, os botões podem ser usados na interface do usuário com estilo e esses botões devem ser estilizados adequadamente. Consulte [caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) para obter informações sobre controles com tema.

### <a name="special-buttons"></a>Botões especiais

#### <a name="browse-buttons"></a>Procurar... botões
 **[Procurar...]** os botões são usados em grades, caixas de diálogo e janelas de ferramentas e outros elementos de interface do usuário sem janela restrita. Eles exibem um seletor que auxilia o usuário a preencher um valor em um controle. Há duas variações desse botão, longas e curtas.

 ![Botão longo &#91;procurar... &#93;](../../extensibility/ux-guidelines/media/070703-04-browselong.gif "070703-04_BrowseLong")

 **O botão longo [procurar...]**

 ![Reticências curtas&#45;apenas &#91;botão procurar... &#93;](../../extensibility/ux-guidelines/media/070703-05-browseshort.gif "070703-05_BrowseShort")

 **O botão [...] curto somente-reticências**

 Quando usar o botão curto somente de reticências:

- Se houver mais de um botão **[procurar...]** em uma caixa de diálogo, como quando vários campos permitirem navegação. Use o botão **[...]** curto para cada um para evitar as chaves de acesso confusas criadas por essa situação (**&procurar** e **B&linhas** na mesma caixa de diálogo).

- Em uma caixa de diálogo rígida ou quando não há nenhum local razoável para colocar o botão longo.

- Se o botão aparecerá em um controle de grade.

  Diretrizes para usar o botão:

- Não use uma chave de acesso. Para acessá-lo usando o teclado, o usuário deve fazer a Tabulação a partir do controle adjacente. Verifique se a ordem de tabulação é de modo que qualquer botão de navegação cai imediatamente após o campo que ele preencherá. Nunca use um sublinhado abaixo do primeiro período.

- Defina a propriedade **nome** do Microsoft acessibilidade ativa (MSAA) como **procurar...** (incluindo as reticências) para que os leitores de tela o leiam como "procurar" e não "ponto-ponto-ponto" ou "período período". Para controles gerenciados, isso significa definir a propriedade **AccessibleName** .

- Nunca use um botão de reticências **[...]** para qualquer coisa, exceto uma ação de procura. Por exemplo, se você precisar de um botão **[novo...]** , mas não tiver espaço suficiente para o texto, a caixa de diálogo precisará ser reformulada.

##### <a name="sizing-and-spacing"></a>Dimensionamento e espaçamento
 ![Dimensionando &#91;procurar... &#93; botões](../../extensibility/ux-guidelines/media/070703-06-browsesizing.png "070703-06_BrowseSizing")

 **Dimensionando os botões [procurar...]**

 ![Botões de espaçamento &#91;procurar... &#93;](../../extensibility/ux-guidelines/media/070703-07-browsespacing.png "070703-07_BrowseSpacing")

 **Botões de espaçamento [procurar...]**

#### <a name="graphical-buttons"></a>Botões gráficos
 Alguns botões sempre devem usar uma imagem gráfica e nunca incluir texto para conservar espaço e evitar problemas de localização. Eles são frequentemente usados em seletores de campo e outras listas classificável.

> [!NOTE]
> Os usuários precisam Tab para esses botões (não há chaves de acesso), portanto, coloque-os em uma ordem sensata. Mapeie a propriedade Name do botão para a ação que ele leva para que os leitores de tela interpretem corretamente a ação do botão.

|Nome|Imagem|
|-|-|
|Adicionar|![Botão "Adicionar" gráfico](../../extensibility/ux-guidelines/media/070703-08-buttonadd.png "070703-08_ButtonAdd")|
|Remover|![Botão "remover" gráfico](../../extensibility/ux-guidelines/media/070703-09-buttonremove.png "070703-09_ButtonRemove")|
|Adicionar todos|![Botão "Adicionar tudo" gráfico](../../extensibility/ux-guidelines/media/070703-10-buttonaddall.png "070703-10_ButtonAddAll")|
|Remover Tudo|![Botão "remover tudo" do gráfico](../../extensibility/ux-guidelines/media/070703-11-buttonremoveall.png "070703-11_ButtonRemoveAll")|
|Mover para Cima|![Botão "mover para cima" gráfico](../../extensibility/ux-guidelines/media/070703-12-buttonmoveup.png "070703-12_ButtonMoveUp")|
|Mover para Baixo|![Botão gráfico "mover para baixo"](../../extensibility/ux-guidelines/media/070703-13-buttonmovedown.png "070703-13_ButtonMoveDown")|
|Excluir|![Botão "excluir" gráfico](../../extensibility/ux-guidelines/media/070703-14-buttondelete.png "070703-14_ButtonDelete")|

##### <a name="sizing-and-spacing"></a>Dimensionamento e espaçamento
 O dimensionamento de botões gráficos é o mesmo da versão curta do botão **[procurar...]** (26x23 pixels):

 ![Botão com e sem cor transparente mostrando](../../extensibility/ux-guidelines/media/070703-15-graphicalbuttonspacing.png "070703-15_GraphicalButtonSpacing")

 **Aparência de uma imagem gráfica no botão, com e sem cor transparente mostrando**

### <a name="hyperlinks"></a>Hiperlinks
 Os hiperlinks são adequados para ações baseadas na navegação, como abrir um tópico de ajuda, uma caixa de diálogo modal ou um assistente. Se um hiperlink for usado para um comando, ele sempre deverá exibir uma alteração visível e perceptível na interface do usuário. Em geral, as ações que são confirmadas para uma ação (como salvar, cancelar e excluir) são melhor comunicadas usando um botão.

#### <a name="writing-style"></a>Estilo de escrita
 Siga as [diretrizes da área de trabalho do Windows para texto da interface do usuário](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx). Não use a frase "Saiba mais sobre", "mais informações sobre" ou "obter ajuda com este". Em vez disso, a ajuda de frase vincula o texto em termos da pergunta principal respondida pelo conteúdo da ajuda. Por exemplo, "**como fazer adicionar um servidor ao Gerenciador de servidores?**"

#### <a name="visual-style"></a>Estilo visual

- Os hiperlinks sempre devem usar [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService). Se um hiperlink não tiver o estilo correto, ele piscará vermelho quando ativo ou mostrar uma cor diferente depois de ser visitado.

- Não inclua sublinhados no estado de repouso do controle, a menos que o link seja um fragmento de frase dentro de uma frase completa, como em uma marca-d ' água.

- Sublinhados não devem aparecer em foco. Em vez disso, os comentários para o usuário em que o link está ativo é uma pequena alteração de cor e o cursor de link apropriado.

## <a name="tree-views"></a><a name="BKMK_TreeViews"></a>Exibições de árvore

### <a name="overview"></a>Visão geral
 As exibições de árvore fornecem uma maneira de organizar listas complexas em grupos pai-filho. Um usuário pode expandir ou recolher grupos pai para revelar ou ocultar itens filho subjacentes. Cada item dentro de um modo de exibição de árvore pode ser selecionado para fornecer mais ações.

 Este tópico aborda o uso aceitável, o design adequado e a funcionalidade de exibições de árvore.

#### <a name="in-this-topic"></a>Neste tópico

- [Estilo visual](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewVisualStyle)

- [Interações](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewInteractions)

### <a name="visual-style"></a><a name="BKMK_TreeViewVisualStyle"></a>Estilo visual

#### <a name="expanders"></a>Expansores
 Os controles de exibição de árvore devem estar em conformidade com o design do expansor usado pelo Windows e pelo Visual Studio. Cada nó usa um controle Expander para revelar ou ocultar itens subjacentes. O uso de um controle Expander fornece consistência para os usuários que podem encontrar exibições de árvore diferentes no Windows e no Visual Studio.

 ![Controle de exibição de árvore correto](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705-1_TreeViewCorrect")

 **Correto: estilo adequado do nó de exibição de árvore usando um controle Expander**

 ![Nós de exibição de árvore incorretos](../../extensibility/ux-guidelines/media/070705-2-treeviewincorrect1.png "070705-2_TreeViewIncorrect1")

 **Incorreto: estilo inadequado do nó de exibição de árvore**

#### <a name="selection"></a>Seleção
 Quando um nó é selecionado dentro do modo de exibição de árvore, o realce deve expandir até a largura total do controle de exibição de árvore. Isso ajuda os usuários a identificar claramente qual item foi selecionado. As cores de seleção devem refletir o tema atual do Visual Studio.

 ![Controle de exibição de árvore correto](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705-1_TreeViewCorrect")

 **Correto: o realce do nó selecionado se ajusta a toda a largura do controle de exibição de árvore.**

 ![Realce de exibição de árvore incorreta](../../extensibility/ux-guidelines/media/070705-3-treeviewincorrect2.png "070705-3_TreeViewIncorrect2")

 **Incorreto: o realce do nó selecionado não se ajusta à largura inteira do controle de exibição de árvore.**

#### <a name="icons"></a>Ícones
 Os ícones só devem ser usados em controles de exibição de árvore se ajudarem a identificar visualmente as diferenças entre os itens. Em geral, os ícones devem ser usados somente em listas heterogêneas nas quais os ícones contêm informações para diferenciar os tipos de elementos. Em uma lista homogênea usando ícones, muitas vezes podem ser vistos como ruído e devem ser evitados. Nesse caso, o ícone de grupo (pai) pode transmitir o tipo de itens dentro dele. A exceção a essa regra seria se o ícone fosse dinâmico e é usado para indicar o estado.

#### <a name="scroll-bars"></a>Barras de rolagem
 As barras de rolagem sempre devem estar ocultas se o conteúdo couber no controle de exibição de árvore. É aceitável que as barras de rolagem sejam ocultas ou semitransparentes em uma janela rolável e apareçam quando a janela que contém a exibição de árvore tem foco, ou ao focalizar a exibição de árvore em si.

 ![Modo de exibição de árvore com barras de rolagem](../../extensibility/ux-guidelines/media/070705-4-scrollbars.png "070705-4_Scrollbars")

 **As barras de rolagem vertical e horizontal são exibidas porque o conteúdo excedeu os limites do controle de exibição de árvore.**

### <a name="interactions"></a><a name="BKMK_TreeViewInteractions"></a>Ações

#### <a name="context-menus"></a>Menus de contexto
 Um nó de exibição de árvore pode revelar as opções de submenu em um menu de contexto. Normalmente, isso ocorre quando um usuário clica com o botão direito do mouse em um item ou pressionou a tecla de menu em um teclado do Windows com o item selecionado. É importante que o nó tenha foco e esteja selecionado. Isso ajuda o usuário a identificar a qual item o submenu pertence.

 ![Nó de árvore e menu de contexto selecionados](../../extensibility/ux-guidelines/media/070705-5-contextmenu.png "070705-5_ContextMenu")

 **O item que gerou o menu de contexto ganha foco para notificar o usuário qual item foi selecionado.**

#### <a name="keyboard"></a>Teclado
 O modo de exibição de árvore deve fornecer a capacidade de selecionar itens e expandir/recolher nós usando o teclado. Isso garante que a navegação atenda aos nossos requisitos de acessibilidade.

##### <a name="tree-view-control"></a>Controle de exibição de árvore
 Os controles de árvore do Visual Studio devem seguir a navegação de teclado comum:

- **Seta para cima:** Selecionar itens movendo a árvore para cima

- **Seta para baixo:** Selecionar itens movendo a árvore para baixo

- **Seta para a direita:** Expandir um nó na árvore

- **Seta para a esquerda:** Recolher um nó na árvore

- **Inserir chave:** Iniciar, carregar, executar o item selecionado

##### <a name="trid-tree-view-and-grid-view"></a>TrID (exibição de árvore e exibição de grade)
 Um controle TrID é um controle complexo que contém um modo de exibição de árvore dentro de uma grade. Expandir, recolher e navegar na árvore deve respeitar os mesmos comandos de teclado que um modo de exibição de árvore, com as seguintes adições:

- **Seta para a direita:** Expanda um nó. Depois que o nó é expandido, ele deve continuar navegando até a coluna mais próxima à direita. A navegação deve parar no final da linha.

- **Guia:** Navega até a célula mais próxima à direita.  No final da linha, a navegação continua para a próxima linha.

- **Shift + Tab:** Navega para a célula mais próxima à esquerda.  No início da linha, a navegação continua para a célula mais à direita na linha anterior.

  ![Controle TrID no Visual Studio](../../extensibility/ux-guidelines/media/070705-6-trid.png "070705-6_Trid")

  **Um controle TrID no Visual Studio**
