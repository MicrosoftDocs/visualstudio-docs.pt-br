---
title: Padrões comuns de controle para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e10fdcea9819c34735f285c78a0e2ebb0650f64a
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39512311"
---
# <a name="common-control-patterns-for-visual-studio"></a>Padrões comuns de controle para o Visual Studio
##  <a name="BKMK_CommonControls"></a> Controles comuns  
  
### <a name="overview"></a>Visão geral  
Controles comuns compõem a maior parte da interface do usuário no Visual Studio. Controles mais comuns usados na interface do Visual Studio devem seguir a [diretrizes de interação de área de trabalho do Windows](/windows/desktop/uxguide/controls). Este tópico é específico para o Visual Studio e aborda situações especiais ou detalhes que aumentam a essas diretrizes do Windows.  
  
#### <a name="common-controls-in-this-topic"></a>Controles comuns neste tópico  
  
-   [Barras de rolagem](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_Scrollbars)  
  
-   [Campos de entrada](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_InputFields)  
  
-   [Caixas de combinação e listas suspensas](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ComboBoxesAndDropDowns)  
  
-   [Caixas de seleção](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_CheckBoxes)  
  
-   [Botões de opção](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_RadioButtons)  
  
-   [Quadros de grupo](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_GroupFrames)  
  
-   [Controles de texto](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TextControls)  
  
-   [Hiperlinks e botões](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_ButtonsAndHyperlinks)  
  
-   [Modos de exibição de árvore](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViews)  
  
#### <a name="visual-style"></a>Estilo Visual  
A primeira coisa a considerar ao definir o estilo de controles é se os controles serão usados na interface do usuário com tema. Controles na interface do usuário padrão são a interface do usuário não está com tema e devem seguir [estilo normal da área de trabalho do Windows](/windows/desktop/uxguide/controls), que significa que eles não forem templated de re e devem aparecer na sua aparência de controle padrão.  
  
-   **Caixas de diálogo padrão (utilitário do):** não tema. Não re-modelo. Use padrões de estilo de controle básico.  
  
-   **Ferramentas, editores de documento, superfícies de design e de caixas de diálogo com tema:** usar especializada aparência com tema usando o serviço de cor.  
  
###  <a name="BKMK_Scrollbars"></a> Barras de rolagem  
 Barras de rolagem devem seguir [barras de rolagem de padrões comuns de interação para Windows](/windows/desktop/Controls/about-scroll-bars) , a menos que eles são aumentados com informações de conteúdo, como no editor de códigos.  
  
###  <a name="BKMK_InputFields"></a> Campos de entrada  
 Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para as caixas de texto](/windows/desktop/uxguide/ctrl-text-boxes).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Campos de entrada não devem ser estilizados nas caixas de diálogo do utilitário. Use o estilo básico intrínseco para o controle.  
  
-   Campos de entrada com tema só devem ser usados em janelas de ferramentas e caixas de diálogo com tema.  
  
#### <a name="specialized-interactions"></a>Interações especializadas  
  
-   Campos somente leitura terá um plano de fundo cinza (desabilitado), mas o padrão (Active Directory) no primeiro plano.  
  
-   Necessário campos devem ter  **\<necessárias >** como marcas d'água dentro deles. Você não deve alterar a cor do plano de fundo, exceto em raras situações.  
  
-   Validação de erro: consulte [notificações e progresso para o Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)  
  
-   Campos de entrada devem ser dimensionados para caber o conteúdo não se ajustar à largura da janela na qual eles são mostrados, nem arbitrariamente corresponde ao tamanho de um campo longo, como um caminho. Comprimento pode ser uma indicação ao usuário de limitações sobre quantos caracteres é permitido no campo.  
  
     ![Tamanho do campo de entrada incorreta: é improvável que o nome será longo. ](../../extensibility/ux-guidelines/media/0707-01_incorrectinputfieldcontrol.png "0707 01_IncorrectInputFieldControl")<br />Tamanho do campo de entrada incorreta: é improvável que o nome será longo.
  
     ![Corrija o comprimento do campo de entrada: o campo de entrada é uma largura razoável para o conteúdo esperado. ](../../extensibility/ux-guidelines/media/0707-02_correctinputfieldcontrol.png "0707 02_CorrectInputFieldControl")<br />Corrija o comprimento do campo de entrada: o campo de entrada é uma largura razoável para o conteúdo esperado.
  
###  <a name="BKMK_ComboBoxesAndDropDowns"></a> Caixas de combinação e listas suspensas  
Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para listas suspensas e caixas de combinação](/windows/desktop/uxguide/ctrl-drop).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Caixas de diálogo do utilitário, não re-modelo do controle. Use o estilo básico intrínseco para o controle.  
  
-   No tema da interface do usuário, caixas de combinação suspensos e siga o tema padrão para os controles.  
  
#### <a name="layout"></a>Layout  
Suspensos e caixas de combinação devem ser ajustados para caber o conteúdo não se ajustar à largura da janela na qual eles são mostrados, nem arbitrariamente corresponde ao tamanho de um campo longo, como um caminho.  
  
![Incorreto: a largura da lista suspensa é muito longa para o conteúdo que será exibido. ](../../extensibility/ux-guidelines/media/0707-03_incorrectdropdownlayout.png "0707 03_IncorrectDropDownLayout")<br />Incorreto: a largura da lista suspensa é muito longa para o conteúdo que será exibido.
  
![Correto: na lista suspensa é dimensionada para permitir o crescimento de tradução, mas não desnecessariamente longas. ](../../extensibility/ux-guidelines/media/0707-04_correctdropdownlayout.png "0707 04_CorrectDropDownLayout")<br />Correto: na lista suspensa é dimensionada para permitir o crescimento de tradução, mas não desnecessariamente longas. 
  
###  <a name="BKMK_CheckBoxes"></a> Caixas de seleção  
Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para as caixas de seleção](/windows/desktop/uxguide/ctrl-check-boxes).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Caixas de diálogo do utilitário, não re-modelo do controle. Use o estilo básico intrínseco para o controle.  
  
-   Caixas de seleção com tema da interface do usuário, siga o tema padrão para os controles.  
  
#### <a name="specialized-interactions"></a>Interações especializadas  
  
-   Interação com uma caixa de seleção nunca deve ser exibida uma caixa de diálogo ou navegar para outra área.  
  
-   Alinhe as caixas de seleção com a linha de base da primeira linha de texto.  
  
     ![Incorreto: a caixa de seleção é centralizada no texto. ](../../extensibility/ux-guidelines/media/0707-05_incorrectcheckboxalign.png "0707 05_IncorrectCheckBoxAlign")<br />Incorreto: a caixa de seleção é centralizada no texto.
  
     ![Correto: a caixa de seleção é alinhada com a primeira linha do texto. ](../../extensibility/ux-guidelines/media/0707-06_correctcheckboxalign.png "0707 06_CorrectCheckBoxAlign")<br />Correto: a caixa de seleção é alinhada com a primeira linha do texto.
  
###  <a name="BKMK_RadioButtons"></a> Botões de opção  
Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para botões de opção](/windows/desktop/uxguide/ctrl-radio-buttons).  
  
#### <a name="visual-style"></a>Estilo Visual  
Caixas de diálogo do utilitário, fazer não botões de opção de estilo. Use o estilo básico intrínseco para o controle.  
  
#### <a name="specialized-interactions"></a>Interações especializadas  
Não é necessário usar um quadro de grupo para incluir as opções de rádio, a menos que você precisa manter a distinção de grupo em um layout estreito.  
  
###  <a name="BKMK_GroupFrames"></a> Quadros de grupo  
Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para quadros de grupo](/windows/desktop/uxguide/ctrl-group-boxes).  
  
#### <a name="visual-style"></a>Estilo Visual  
Caixas de diálogo do utilitário, não o Estilize quadros de grupo. Use o estilo básico intrínseco para o controle.  
  
#### <a name="layout"></a>Layout  
  
-   Não é necessário usar um quadro de grupo para incluir as opções de rádio, a menos que você precisa manter a distinção de grupo em um layout estreito.  
  
-   Nunca use um quadro de grupo para um único controle.  
  
-   Às vezes, é aceitável usar uma régua horizontal, em vez de um contêiner de quadro de grupo.  
  
##  <a name="BKMK_TextControls"></a> Controles de texto

### <a name="static-text-fields"></a>Campos de texto estático

Um campo de texto estático apresenta informações somente leitura e não pode ser selecionado pelo usuário. Evite usá-lo para qualquer texto que o usuário talvez queira copiar na área de transferência. No entanto, somente leitura texto estático pode ser alterado para refletir uma alteração de estado. No exemplo a seguir, o texto estático do nome de saída em que as alterações de grupo de informações para refletir as alterações feitas na caixa de texto do Namespace raiz acima dele.

Há duas maneiras de exibir informações de texto estático.

Texto estático pode ser em sua própria em uma caixa de diálogo sem nenhuma contenção quando não há nenhum conflito de agrupamento. Decida se as linhas extras de uma caixa são realmente necessárias. Um exemplo é a exibição de um caminho de diretório em uma seção criado por uma linha de grupo, conforme mostrado abaixo:  

![Informações de texto estático em controles de texto](../../extensibility/ux-guidelines/media/DisplayingStaticText.png "DisplayingStaticText.png")<br />Informações de texto estático em controles de texto

Na caixa de diálogo em que existem outras áreas agrupadas e confinamento das informações de ajuda a facilitar a leitura, e quando uma seção pode ser ocultada ou exibida (como na **janela de propriedades** painel de descrição) ou ser consistente com a interface do usuário semelhante, Coloque o texto dentro de uma caixa. Essa caixa de grupo deve ser uma única regra e coloridos com a `ButtonShadow`:

![Na janela Propriedades de um texto estático](../../extensibility/ux-guidelines/media/PropertiesWindow.png "PropertiesWindow.png")<br />Texto estático na janela Propriedades

### <a name="read-only-text-box"></a>Caixa de texto somente leitura

Isso permite que o usuário selecione o texto dentro do campo, mas não editá-lo. Essas caixas de texto são com borda pelo Cinzel 3D normal com um `ButtonShadow` preenchimento.

Uma caixa de texto pode se tornar ativa (editável) quando um usuário altera um controle associado, como verificar/desmarcar uma caixa de seleção ou Selecionar/desmarcar um botão de opção. Por exemplo, nos **ferramentas &gt; opções** página mostrada abaixo, o **Home Page** caixa de texto se torna ativo quando o **usar padrão** caixa de seleção está desmarcada.

![Caixa de texto somente leitura, mostrando os estados ativos e inativos](../../extensibility/ux-guidelines/media/ReadOnlyTextBox.png "ReadOnlyTextBox.png")<br />Caixa de texto somente leitura, mostrando os estados ativos e inativos

### <a name="using-text-in-dialogs"></a>Usando texto em caixas de diálogo

Diretrizes importantes para o texto nas caixas de diálogo:

-   Rótulos para caixas de texto, caixas de listagem e quadros nas caixas de diálogo unthemed começam com um verbo, tem uma maiuscula inicial em apenas a primeira palavra e terminam com dois-pontos.

    > Controles de texto nas caixas de diálogo com tema seguem [diretrizes de experiência do usuário da área de trabalho do Windows](/windows/desktop/uxguide/top-violations) e não levam a pontuação final, com exceção dos pontos de interrogação em links de Ajuda.

-   Rótulos para caixas de seleção e botões de opção começam com um verbo, uma maiuscula inicial na primeira palavra somente e tem sem pontuação final.

-   Rótulos de botões, menus, itens de menu e as guias têm iniciais maiusculas em cada palavra (maiusculas/minúsculas).

-   Terminologia de rótulo deve ser consistente com rótulos semelhantes em outras caixas de diálogo.

-   Se possível, ter um editor de gravador/gravação ou aprovar o texto para que ele vai para o desenvolvedor para implementação.

-   Todos os controles devem ter rótulos, exceto em circunstâncias especiais em que uso da tecla TAB é suficiente.
Use o texto de auxiliar quando apropriado.

### <a name="helper-text"></a>Texto de auxiliar

Incluído nas caixas de diálogo para ajudar o usuário a entender a finalidade da caixa de diálogo ou para indicar qual ação executar. Texto de auxiliar deve ser usado apenas quando necessário, para evitar problemas de caixas de diálogo simples. Duas variações do texto de auxiliar são a caixa de diálogo e a marca d'água.

Siga os locais comuns para texto auxiliar e seja seletivo ao introduzir novas áreas. Cenários comuns para texto auxiliar são:

-   Texto de auxiliar nas caixas de diálogo, para dar uma direção adicional sobre como interagir com uma caixa de diálogo complexa.

-   Texto de marca d'água em janelas de ferramentas vazia ou caixas de diálogo, para explicar por que nenhum conteúdo é visível.

-   Um painel de descrição, na parte inferior, como o **janela de propriedades**.

-   Marca d'água em texto em um editor vazio, para explicar a ação que o usuário deve tomar para começar a usar.
  
### <a name="dialog-helper-text"></a>Texto do auxiliar de diálogo

Um designer de experiência do usuário pode ajudar a determinar quando o texto do auxiliar é apropriado. O designer pode definir onde o texto do auxiliar é exibido, bem como seu conteúdo geral. Assistência ao usuário pode gravar/editar o texto real.

### <a name="watermarks"></a>Marcas d'água

Caixas de diálogo se beneficiar de diretrizes de marca d'água ligeiramente diferente. Porque uma caixa de diálogo pode aparecer ocupada com muitos elementos de interface do usuário (rótulos, texto de dica, botões e outros controles de contêiner com texto), especialmente quando esses aparecem em preto, marcas d'água se destacam melhor em cinza escuro (VSColor: `ButtonShadow`). Normalmente uma marca d'água é exibido dentro de um controle, como uma caixa de listagem com um plano de fundo branco (VSColor: `Window`).

-   O texto é exibido em cinza escuro (VSColor: `ButtonShadow`). No entanto, se a marca d'água é exibida em um cinza médio ou de outras cores (VSColor: `ButtonFace`) em segundo plano e não há referem-se sobre sua legibilidade, vá com texto preto (VSColor: `WindowText`).

-   As marcas d'água podem ser centralizadas ou recuo à esquerda. Aplica regras de padrão de design ao tomar decisões de alinhamento. A marca d'água não pode ser selecionada no plano de fundo.

![Exemplo de texto de marca d'água](../../extensibility/ux-guidelines/media/WatermarkTextExample.gif)<br />Exemplo de texto de marca d'água

### <a name="context-specific-dynamic-text"></a>Texto de contexto específico (dinâmico)

Texto dinâmico pode ser usado de duas maneiras em uma caixa de diálogo ou a interface do usuário sem janela restrita: como um rótulo dinâmico ou como o conteúdo dinâmico.

-   Rótulo dinâmico: um uso comum do texto dinâmico está em painéis descritivos que oferecem mais informações para o item selecionado, como em uma caixa de diálogo que contém uma lista de elementos e propriedades para esses elementos exibidos em uma grade à direita. O rótulo para a grade de propriedade pode ser dinâmico, para que quando um item é selecionado à esquerda, a grade à direita mostra as informações para aquele item específico.

-   Texto dinâmico: pode ser útil em casos em que você precisa exibir informações específicas e informações gerais não dessa maneira, mas tome cuidado para não usar demasiadamente.

Se você quiser que os usuários tenham a capacidade de copiar as informações, texto dinâmico deve estar em um campo de texto somente leitura.
  
##  <a name="BKMK_ButtonsAndHyperlinks"></a> Hiperlinks e botões  
  
### <a name="overview"></a>Visão geral  
Controles de botões e links (hiperlinks) devem seguir [diretrizes básicas de área de trabalho do Windows em hiperlinks](/windows/desktop/uxguide/ctrl-links) para utilização de palavras, dimensionando e espaçamento.  
  
### <a name="choosing-between-buttons-and-links"></a>Escolhendo entre os botões e links  
Tradicionalmente, os botões foram usados para ações e hiperlinks foram reservados para navegação. Botões podem ser usados em todos os casos, mas a função de links foi expandida no Visual Studio para que os botões e links são mais intercambiáveis em algumas condições.  
  
Quando usar os botões de comando:  
  
-   Comandos primários  
  
-   Exibição do windows usada para coletar entrada ou fazer escolhas, mesmo se eles são comandos secundários  
  
-   Ações destrutivas ou irreversíveis  
  
-   Botões de compromisso em assistentes e fluxos de página  
  
Evite os botões de comando nas janelas de ferramentas, ou se precisar de mais de duas palavras para o rótulo. Os links podem ter mais rótulos.  
  
 Quando usar links:  
  
-   Navegação para outra janela, documento ou página da web  
  
-   Situações que exigem um rótulo mais tempo ou uma frase curta para descrever a intenção da ação  
  
-   Uma forte espaços em que um botão seria sobrecarregar a interface do usuário, desde que a ação não destrutivas ou irreversível  
  
-   Ocupando comandos secundários em situações em que há muitos comandos  
  
#### <a name="examples"></a>Exemplos  
![Comando vínculos usados na barra de informações a seguir de uma mensagem de status](../../extensibility/ux-guidelines/media/070703-01_commandlinkinfobar.png "070703 01_CommandLinkInfobar")<br />Links de comando usada na barra de informações a seguir de uma mensagem de status
  
![Links usados o pop-up do CodeLens](../../extensibility/ux-guidelines/media/070703-02_linksincodelens.png "070703 02_LinksInCodeLens")<br />Links usados o pop-up do CodeLens
  
![Links usado para comandos secundários onde botões atrairia muita atenção](../../extensibility/ux-guidelines/media/070703-03_linksassecondarycommands.png "070703 03_LinksAsSecondaryCommands")<br />Usado para comandos secundários onde botões atrairia muita atenção de links
  
### <a name="common-buttons"></a>Botões comuns  
  
#### <a name="text"></a>Texto  
Siga as diretrizes de escrita [interface do usuário do texto e a terminologia](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
##### <a name="standard-unthemed"></a>Standard (unthemed)  
A maioria dos botões no Visual Studio será exibida nas caixas de diálogo do utilitário e não deve ser estilizados. Eles devem refletir a aparência padrão dos botões, conforme determinado pelo sistema operacional.  
  
##### <a name="themed"></a>Com temas  
Em alguns casos, botões podem ser usados na interface do usuário com estilo e esses botões devem ser estilizados adequadamente. Ver [caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) para obter informações sobre controles com tema.  
  
### <a name="special-buttons"></a>Botões especiais  
  
#### <a name="browse-buttons"></a>Botões de navegação...  
**[Procurar...]**  botões são usados em grades, caixas de diálogo e janelas de ferramentas e outros elementos de interface do usuário sem janela restrita. Eles exibem um seletor que ajuda a preencher um valor em um controle de usuário. Há duas variações deste botão curtos e longos.  
  
![O botão [procurar...] longo](../../extensibility/ux-guidelines/media/070703-04_browselong.gif "070703 04_BrowseLong")<br />O botão [procurar...] longo
  
![O botão curto somente nas reticências [...]](../../extensibility/ux-guidelines/media/070703-05_browseshort.gif "070703 05_BrowseShort")<br />O botão curto somente nas reticências [...]
  
Quando usar o botão curto somente reticências:  
  
-   Se houver mais de um longo **[procurar...]**  botão na caixa de diálogo, como quando vários campos permitem para navegação. Usar curto **[...]**  botão de cada um para evitar as chaves de acesso confuso criadas por essa situação (**& navegue** e **p & rocurar** na mesma caixa de diálogo).  
  
-   Em uma caixa de diálogo estreita, ou quando não há nenhum lugar razoável para colocar o botão longo.  
  
-   Se o botão será exibido em um controle de grade.  
  
Diretrizes para usar o botão:  
  
-   Não use uma chave de acesso. Para acessá-lo usando o teclado, o usuário deve guia do controle adjacente. Certifique-se de que a ordem de tabulação é, de modo que qualquer botão de procurar fica imediatamente após o campo que ele será preenchido. Nunca use um caractere de sublinhado abaixo do primeiro período.  
  
-   Defina o Active Accessibility MSAA (Microsoft) **nome** propriedade **procurar...**  (incluindo as reticências) para que a tela leitores lerá como "Procurar" e não "dot-ponto-ponto" ou "período período-período." Para controles gerenciados, isso significa que a configuração de **AccessibleName** propriedade.  
  
-   Nunca use um sinal de reticências **[...]**  botão para qualquer coisa, exceto uma ação de navegação. Por exemplo, se você precisar um **[novo...]**  botão, mas não tem espaço suficiente para o texto, em seguida, a caixa de diálogo precisa ser reprojetada.  
  
##### <a name="sizing-and-spacing"></a>Dimensionamento e espaçamento  
![Botões de dimensionamento [procurar...]: versão padrão é 75 x 23 pixels, a versão curta é 26 x 23 pixels](../../extensibility/ux-guidelines/media/070703-06_browsesizing.png "070703 06_BrowseSizing")<br />Botões de dimensionamento [procurar...]
  
![Botões de espaçamento [procurar...]: espaçamento entre o controle relacionado e pixels de 7 do botão de navegação padrão, o espaçamento entre o controle relacionado e procurar curto botão 5 pixels](../../extensibility/ux-guidelines/media/070703-07_browsespacing.png "070703 07_BrowseSpacing")<br />Botões de espaçamento [procurar...]
  
#### <a name="graphical-buttons"></a>Botões gráficos  
Alguns botões devem sempre usar uma imagem gráfica e nunca inclua texto para conservar o espaço e evitar problemas de localização. Geralmente, eles são usados no seletor de campo e outras listas classificável.  
  
> **Observação:** os usuários precisarão de guia para esses botões (não há nenhuma chave de acesso), portanto, colocá-los em uma ordem adequada. Mapa de `name` propriedade do botão para a ação que leva para que os leitores de tela interpretam corretamente a ação do botão.  
  
| Função | Botão |  
| --- | --- |  
| Adicionar | ![Botão de "Adicionar" gráfica](../../extensibility/ux-guidelines/media/070703-08_buttonadd.png "070703 08_ButtonAdd") |
| Remover | ![Botão "Remover" gráfico](../../extensibility/ux-guidelines/media/070703-09_buttonremove.png "070703 09_ButtonRemove") |
| Adicionar todos | ![Botão "Adicionar tudo" gráfica](../../extensibility/ux-guidelines/media/070703-10_buttonaddall.png "070703 10_ButtonAddAll") |
| Remover tudo | ![Botão "Remover tudo" gráfica](../../extensibility/ux-guidelines/media/070703-11_buttonremoveall.png "070703 11_ButtonRemoveAll") |
| Mover Para Cima | ![Botão de "Mover para cima" gráfica](../../extensibility/ux-guidelines/media/070703-12_buttonmoveup.png "070703 12_ButtonMoveUp") |
| Mover Para Baixo | ![Botão de "Mover para baixo" gráfica](../../extensibility/ux-guidelines/media/070703-13_buttonmovedown.png "070703 13_ButtonMoveDown") |
| Excluir | ![Botão "Excluir" de gráfico](../../extensibility/ux-guidelines/media/070703-14_buttondelete.png "070703 14_ButtonDelete") |
  
##### <a name="sizing-and-spacing"></a>Dimensionamento e espaçamento  
Dimensionamento para botões gráfica é da mesma maneira que uma versão abreviada do **[procurar...]**  botão (26 x 23 pixels):  
  
![Aparência de uma imagem gráfica no botão, com e sem cor transparente mostrando](../../extensibility/ux-guidelines/media/070703-15_graphicalbuttonspacing.png "070703 15_GraphicalButtonSpacing")<br />Aparência de uma imagem gráfica no botão, com e sem cor transparente mostrando
  
### <a name="hyperlinks"></a>Hiperlinks  
Os hiperlinks são adequados para ações com base em navegação, como abrir um tópico da Ajuda, a caixa de diálogo modal ou o assistente. Se um hiperlink é usado para um comando, ele sempre deve exibir uma alteração perceptível e visível na interface do usuário. Em geral, as ações que confirme para uma ação (como salvar, cancelar e excluir) são comunicadas melhor usando um botão.  
  
#### <a name="writing-style"></a>Estilo de escrita  
Siga as [diretrizes de área de trabalho do Windows para o texto da interface do usuário](/windows/desktop/uxguide/text-ui). Não use "Saiba mais sobre," "Diga-me mais sobre" ou a frase "Get help com isso". Frase em vez disso, o texto do link de Ajuda em termos da pergunta principal respondida pelo conteúdo da Ajuda. Por exemplo, "**como adicionar um servidor para o Gerenciador de servidores?**"  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Sempre devem usar hiperlinks [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService). Se um hiperlink não é estilizado corretamente, ele pisca em vermelho quando ativo ou mostra uma cor diferente após a que está sendo visitado.  
  
-   Não inclua sublinhados pairando estado, a menos que o link é um fragmento da sentença em uma frase completa, como em uma marca d'água para o controle.  
  
-   Sublinhados não devem aparecer em foco. Em vez disso, os comentários para o usuário que o link está ativo são uma alteração de cor pequena e o cursor de link apropriado.  
  
##  <a name="BKMK_TreeViews"></a> Modos de exibição de árvore  
  
Modos de exibição de árvore fornecem uma maneira de organizar complexos lista em grupos pai-filho. Um usuário pode expandir ou recolher grupos pai para revelar ou ocultar itens de filho subjacente. Cada item em uma exibição de árvore pode ser selecionado para fornecer mais ação.  
  
###  <a name="BKMK_TreeViewVisualStyle"></a> Estilo visual de modo de exibição de árvore  
  
#### <a name="expanders"></a>Expansores  
Controles de exibição de árvore devem estar de acordo com o design de expansor usado pelo Windows e o Visual Studio. Cada nó usa um controle expander para revelar ou ocultar itens subjacentes. Usar um controle expander fornece consistência para os usuários que podem ser encontrados modos de exibição de árvore diferente dentro do Windows e o Visual Studio.  
  
![Correto: estilo adequado do nó de exibição de árvore usando um controle expander](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705 1_TreeViewCorrect")<br />Correto: estilo adequado do nó de exibição de árvore usando um controle expander
  
![Incorreto: estilo de inadequada modo de exibição do nó de árvore](../../extensibility/ux-guidelines/media/070705-2_treeviewincorrect1.png "070705 2_TreeViewIncorrect1")<br />Incorreto: estilo de inadequada modo de exibição do nó de árvore
  
#### <a name="selection"></a>Seleção  
Quando um nó é selecionado na exibição de árvore, o realce deve expandir para a largura total do controle de exibição de árvore. Isso ajuda os usuários a identificar claramente qual item que foi selecionado. Cores de seleção devem refletir o tema atual do Visual Studio.  
  
![Correto: realce do nó selecionado se encaixa em toda a largura do controle de exibição de árvore. ](../../extensibility/ux-guidelines/media/070705-1_treeviewcorrect.png "070705 1_TreeViewCorrect")<br />Correto: realce do nó selecionado se encaixa em toda a largura do controle de exibição de árvore.
  
![Incorreta: o realce do nó selecionado não couber toda a largura do controle de exibição de árvore. ](../../extensibility/ux-guidelines/media/070705-3_treeviewincorrect2.png "070705 3_TreeViewIncorrect2")<br />Incorreta: o realce do nó selecionado não couber toda a largura do controle de exibição de árvore.
  
#### <a name="icons"></a>Ícones  
Ícones só devem ser usados em controles de exibição de árvore, se eles ajudar a identificar visualmente as diferenças entre os itens. Em geral, os ícones devem ser usados apenas em listas heterogêneas nos quais os ícones transportam informações para diferenciar os tipos de elementos. Em uma lista homogênea usando ícones com frequência pode ser visto como o ruído e deve ser evitado. Nesse caso, o ícone do grupo (pai) pode transmitir o tipo de itens dentro dela. A exceção a essa regra seria se o ícone é dinâmico e é usado para indicar o estado.  
  
#### <a name="scroll-bars"></a>Barras de rolagem  
Barras de rolagem sempre deverão estar ocultos se o conteúdo caiba no controle de exibição de árvore. É aceitável para barras de rolagem ser ocultos ou semitransparente em uma janela rolável e aparecem quando a janela que contém a exibição de árvore tem o foco ou após a passagem da árvore de exibir em si.  
  
![Ambas as barras de rolagem vertical e horizontal são exibidas porque o conteúdo excederam os limites do controle de exibição de árvore. ](../../extensibility/ux-guidelines/media/070705-4_scrollbars.png "070705 4_Scrollbars")<br />Ambas as barras de rolagem vertical e horizontal são exibidas porque o conteúdo excederam os limites do controle de exibição de árvore.
  
###  <a name="BKMK_TreeViewInteractions"></a> Interações de modo de exibição de árvore  
  
#### <a name="context-menus"></a>Menus de contexto  
Um nó do modo de exibição de árvore pode revelar as opções do submenu em um menu de contexto. Normalmente, isso ocorre quando um usuário tem pequeno um item ou pressionou a tecla de Menu em um teclado do Windows com o item selecionado. É importante que o nó obtém foco e está selecionado. Isso ajuda o usuário a identificar qual item de submenu pertence.  
  
![O item que tem geram o foco de ganhos de menu de contexto para notificar o usuário que o item foi selecionado. ](../../extensibility/ux-guidelines/media/070705-5_contextmenu.png "070705 5_ContextMenu")<br />O item que tem geram o foco de ganhos de menu de contexto para notificar o usuário que o item foi selecionado.
  
#### <a name="keyboard"></a>Teclado  
O modo de exibição de árvore deve fornecer a capacidade de selecionar itens e expandir/recolher nós usando o teclado. Isso garante que a navegação atende aos nossos requisitos de acessibilidade.  
  
##### <a name="tree-view-control"></a>Controle de exibição de árvore  
Controles de árvore do Visual Studio devem seguir a navegação de teclado comuns:  
  
-   **Seta para cima:** selecionar itens movendo a árvore  
  
-   **Seta para baixo:** selecionar itens movendo-se abaixo da árvore  
  
-   **Seta para a direita:** expandir um nó na árvore  
  
-   **Seta para a esquerda:** recolher um nó na árvore  
  
-   **Insira a chave:** Iniciar, carregar, executar o item selecionado  
  
##### <a name="trid-tree-view-and-grid-view"></a>Trid (exibição de árvore e exibição de grade)  
Um controle trid é um controle complexo que contém uma exibição de árvore em uma grade. Expandindo, recolhimento e navegar pela árvore devem respeitar os mesmos comandos de teclado que uma exibição de árvore, com as seguintes adições:  
  
-   **Seta para a direita:** expandir um nó. Depois que o nó é expandido, ele deve continuar navegando até a coluna mais próxima à direita. Deve interromper a navegação no final da linha.  
  
-   **Guia:** navega para a célula mais próxima à direita.  No final da linha, a navegação continua para a próxima linha.  
  
-   **Shift + Tab:** navega para a célula mais próxima à esquerda.  No início da linha, a navegação continua para a célula mais à direita na linha anterior.  
  
![Um controle trid no Visual Studio](../../extensibility/ux-guidelines/media/070705-6_trid.png "070705 6_Trid")<br />Um controle trid no Visual Studio