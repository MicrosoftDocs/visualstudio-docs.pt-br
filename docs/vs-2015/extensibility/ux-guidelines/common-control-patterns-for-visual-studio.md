---
title: Padrões comuns de controle para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3e893949-6398-42f1-9eab-a8d8c2b7f02d
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 111323a416f8388fe553824e83edd5f48b3201d4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817523"
---
# <a name="common-control-patterns-for-visual-studio"></a>Padrões comuns de controle para o Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

##  <a name="BKMK_CommonControls"></a> Controles comuns  
  
### <a name="overview"></a>Visão geral  
 Controles comuns compõem a maior parte da interface do usuário no Visual Studio. Controles mais comuns usados na interface do Visual Studio devem seguir a [diretrizes de interação de área de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/dn742399.aspx). Este documento é específico para o Visual Studio e aborda situações especiais ou detalhes que aumentam a essas diretrizes do Windows.  
  
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
 A primeira coisa a considerar ao definir o estilo de controles é se os controles serão usados na interface do usuário com tema. Controles na interface do usuário padrão são a interface do usuário não está com tema e devem seguir [estilo normal da área de trabalho do Windows](https://msdn.microsoft.com/library/windows/desktop/dn742399\(v=vs.85\).aspx), que significa que eles não forem templated de re e devem aparecer na sua aparência de controle padrão.  
  
-   **Caixas de diálogo padrão (utilitário do):** não tema. Fazer não re-modelo. Use padrões de estilo de controle básico.  
  
-   **Ferramentas, editores de documento, superfícies de design e de caixas de diálogo com tema:** usar especializada aparência com tema usando o serviço de cor.  
  
###  <a name="BKMK_Scrollbars"></a> Barras de rolagem  
 Barras de rolagem devem seguir [padrões comuns de interação para barras de rolagem do Windows](https://msdn.microsoft.com/library/windows/desktop/bb787527\(v=vs.85\).aspx) , a menos que eles são aumentados com informações de conteúdo, como no editor de códigos.  
  
###  <a name="BKMK_InputFields"></a> Campos de entrada  
 Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para as caixas de texto](https://msdn.microsoft.com/library/windows/desktop/dn742442\(v=vs.85\).aspx).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Campos de entrada não devem ser estilizados nas caixas de diálogo do utilitário. Use o estilo básico intrínseco para o controle.  
  
-   Campos de entrada com tema só devem ser usados em janelas de ferramentas e caixas de diálogo com tema.  
  
#### <a name="specialized-interactions"></a>Interações especializadas  
  
-   Campos somente leitura terá um plano de fundo cinza (desabilitado), mas o padrão (Active Directory) no primeiro plano.  
  
-   Necessário campos devem ter  **\<necessárias >** como marcas d'água dentro deles. Você não deve alterar a cor do plano de fundo, exceto em raras situações.  
  
-   Validação de erro: consulte [notificações e progresso para o Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)  
  
-   Campos de entrada devem ser dimensionados para caber o conteúdo não se ajustar à largura da janela na qual eles são mostrados, nem arbitrariamente corresponde ao tamanho de um campo longo, como um caminho. Comprimento pode ser uma indicação ao usuário de limitações sobre quantos caracteres é permitido no campo.  
  
     ![Largura do controle de campo de entrada incorretos](../../extensibility/ux-guidelines/media/0707-01-incorrectinputfieldcontrol.png "0707 01_IncorrectInputFieldControl")   
     **Tamanho do campo de entrada incorreta: é improvável que o nome será longo.**  
  
     ![Corrija a largura do controle de campo de entrada](../../extensibility/ux-guidelines/media/0707-02-correctinputfieldcontrol.png "0707 02_CorrectInputFieldControl")   
     **Corrija o comprimento do campo de entrada: O campo de entrada é uma largura razoável para o conteúdo esperado.**  
  
###  <a name="BKMK_ComboBoxesAndDropDowns"></a> Caixas de combinação e listas suspensas  
 Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para listas suspensas e caixas de combinação](https://msdn.microsoft.com/library/windows/desktop/dn742404\(v=vs.85\).aspx).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Caixas de diálogo do utilitário, fazer não re-modelo do controle. Use o estilo básico intrínseco para o controle.  
  
-   No tema da interface do usuário, caixas de combinação suspensos e siga o tema padrão para os controles.  
  
#### <a name="layout"></a>Layout  
 Suspensos e caixas de combinação devem ser ajustados para caber o conteúdo não se ajustar à largura da janela na qual eles são mostrados, nem arbitrariamente corresponde ao tamanho de um campo longo, como um caminho.  
  
 ![Soltar incorreto&#45;para baixo de layout](../../extensibility/ux-guidelines/media/0707-03-incorrectdropdownlayout.png "0707 03_IncorrectDropDownLayout")  
  
 **Tamanho do campo incorreto para um controle de lista suspensa**  
  
 ![Soltar correta&#45;para baixo de layout](../../extensibility/ux-guidelines/media/0707-04-correctdropdownlayout.png "0707 04_CorrectDropDownLayout")  
  
 **Comprimento de campo correto para um controle de lista suspensa**  
  
###  <a name="BKMK_CheckBoxes"></a> Caixas de seleção  
 Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para as caixas de seleção](https://msdn.microsoft.com/library/windows/desktop/dn742401\(v=vs.85\).aspx).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Caixas de diálogo do utilitário, fazer não re-modelo do controle. Use o estilo básico intrínseco para o controle.  
  
-   Caixas de seleção com tema da interface do usuário, siga o tema padrão para os controles.  
  
#### <a name="specialized-interactions"></a>Interações especializadas  
  
-   Interação com uma caixa de seleção nunca deve ser exibida uma caixa de diálogo ou navegar para outra área.  
  
-   Alinhe as caixas de seleção com a linha de base da primeira linha de texto.  
  
     ![Alinhamento de caixa de seleção incorreto](../../extensibility/ux-guidelines/media/0707-05-incorrectcheckboxalign.png "0707 05_IncorrectCheckBoxAlign")   
     **Alinhamento de caixa de seleção incorreto: caixa de seleção é centralizada no texto.**  
  
     ![Corrija o alinhamento da caixa de seleção](../../extensibility/ux-guidelines/media/0707-06-correctcheckboxalign.png "0707 06_CorrectCheckBoxAlign")   
     **Corrija o alinhamento da caixa de seleção: caixa de seleção é alinhada com a linha de base da primeira linha de texto.**  
  
###  <a name="BKMK_RadioButtons"></a> Botões de opção  
 Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para botões de opção](https://msdn.microsoft.com/library/windows/desktop/dn742436\(v=vs.85\).aspx).  
  
#### <a name="visual-style"></a>Estilo Visual  
 Caixas de diálogo do utilitário, fazer não botões de opção de estilo. Use o estilo básico intrínseco para o controle.  
  
#### <a name="specialized-interactions"></a>Interações especializadas  
 Não é necessário usar um quadro de grupo para incluir as opções de rádio.  
  
###  <a name="BKMK_GroupFrames"></a> Quadros de grupo  
 Para o comportamento de interação típica, execute as [diretrizes de área de trabalho do Windows para quadros de grupo](https://msdn.microsoft.com/library/windows/desktop/dn742405\(v=vs.85\).aspx).  
  
#### <a name="visual-style"></a>Estilo Visual  
 Caixas de diálogo do utilitário, fazer não quadros de grupo de estilo. Use o estilo básico intrínseco para o controle.  
  
#### <a name="layout"></a>Layout  
  
-   Não é necessário usar um quadro de grupo para incluir as opções de rádio, a menos que você precisa manter a distinção de grupo em um layout estreito.  
  
-   Nunca use um quadro de grupo para um único controle.  
  
-   Às vezes, é aceitável usar uma régua horizontal, em vez de um contêiner de quadro de grupo.  
  
##  <a name="BKMK_TextControls"></a> Controles de texto  
  
### <a name="labels"></a>Rótulos  
  
#### <a name="active-label-state"></a>Estado do rótulo do Active Directory  
  
##### <a name="utility-standard-dialogs"></a>Utilitário de caixas de diálogo (padrão))  
  
-   Em geral, siga as orientações de área de trabalho do Windows para rótulos de controle.  
  
-   Caixas de diálogo do utilitário, rótulos devem aparecer negrito, em que a cor de fonte e texto de ambiente padrão. Ver [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md).  
  
-   Reticências devem sempre seguir rótulos.  
  
##### <a name="signature-themed-dialogs"></a>(Temas) caixas de diálogo de assinatura)  
 Controles de rótulo podem ser em negrito ou cinza claro.  
  
#### <a name="disabled-label-state"></a>Estado de rótulo desativado  
 Rótulos devem refletir a aparência do controle que estão associados. Por exemplo, se o controle associado é desabilitado, o rótulo deve aparecer cinza e desabilitado. Isso geralmente é manipulado pelo sistema operacional e não exige nenhum tratamento especial.  
  
#### <a name="dynamic-labels"></a>Rótulos dinâmicos  
 Alteração de rótulos dinâmico com base na seleção atual. Sempre que possível, use rótulos dinâmicos em layouts de mestre/detalhes para ajudar o usuário a entender que as informações exibidas são relevantes para uma seleção específica e obter informações gerais não.  
  
 ![Rótulo dinâmico usado com conteúdo dinâmico](../../extensibility/ux-guidelines/media/070702-01-dynamiclabel.png "070702 01_DynamicLabel")  
  
 **Exemplo de um rótulo dinâmico usado com conteúdo dinâmico**  
  
#### <a name="instructional-text"></a>Texto de instrução  
 Alguns elementos de interface se beneficiar do texto de instrução para ajudar o usuário a entender a finalidade da interface do usuário ou para indicar qual ação executar.  
  
-   Texto com instrução é mais comum na parte superior das caixas de diálogo, mas pode aparecer em outras áreas para fornecer instruções para um agrupamento de controle complexo.  
  
-   Texto de instrução não é interativo, mas pode conter hiperlinks para tópicos de Ajuda.  
  
-   Use o texto de instrução com parcimônia e somente quando necessário.  
  
##### <a name="formatting"></a>Formatação  
 Texto de instrução deve ser a fonte de ambiente, o texto do controle (com tema) padrão. Ver [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md).  
  
 Para obter detalhes sobre como escrever o texto de instrução, consulte [interface do usuário do texto e a terminologia](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology).  
  
 ![Formatação de texto de instrução](../../extensibility/ux-guidelines/media/070702-02-instructionaltextformatting.png "070702 02_InstructionalTextFormatting")  
  
 **Texto de instrução em uma caixa de diálogo do Visual Studio**  
  
#### <a name="informational-text"></a>Texto informativo  
 Texto informativo é o texto que fornece as informações adicionais do usuário. Ele pode ser estático ou dinâmico ou que foi usado como uma notificação. É sempre somente leitura, mas se ele é útil para o usuário tenha a capacidade de copiar as informações, o texto dinâmico deve ser colocado em um contêiner de controle como um campo de texto somente leitura.  
  
##### <a name="dynamic-context-specific-text"></a>Texto dinâmico de (específico do contexto)  
 Texto de informações dinâmicas é alterado dependendo do contexto, como quando o usuário muda o foco. Muitas vezes, mas não sempre, conteúdo dinâmico é emparelhado com um rótulo dinâmico.  
  
 ![Texto de informações dinâmicas](../../extensibility/ux-guidelines/media/070702-03-informationaldynamictext.png "070702 03_InformationalDynamicText")  
  
 **Texto informativo dinâmico altera dependendo do contexto.**  
  
##### <a name="formatting"></a>Formatação  
 Para exibir campos de texto somente leitura de duas maneiras: diretamente na interface do usuário (veja acima) da superfície ou contido dentro de outro controle, como uma caixa de texto ou quadro de grupo. Qualquer um estiver correto, dependendo da situação. É responsabilidade do designer de recursos para determinar como apresentar informações somente leitura.  
  
 Texto pode ser dentro de uma caixa de texto somente leitura. Isso geralmente indica que o conteúdo pode ser selecionado e copiado, embora ele não pode ser editado.  
  
 ![Texto informativo para leitura de formatação&#45;somente os campos](../../extensibility/ux-guidelines/media/070702-04-informationalformatting.png "070702 04_InformationalFormatting")  
  
 **Texto informativo formatação para campos somente leitura**  
  
#### <a name="watermarks"></a>Marcas d'água  
 Embora o texto pode ser o mesmo, a diferença entre as marcas d'água e texto de instrução é que as marcas d'água são substituídas pelo conteúdo quando a janela/controle não está vazia e texto de instrução permanece visível em todos os momentos.  
  
 As marcas d'água devem ser usadas quando uma janela ou controle está vazio. Eles indicam o que precisa ser feito para preencher a área e podem incluir links de ação para abrir janelas relevantes, como uma origem do arrasto.  
  
##### <a name="visual-style"></a>Estilo Visual  
  
- As marcas d'água devem ser centralizadas horizontalmente dentro da janela.  
  
- As marcas d'água devem ser centralizado, não alinhado à esquerda.  
  
- As marcas d'água podem centralizadas verticalmente ou posicionadas na parte superior da área. Se localizado próximo à parte superior da área, deve haver espaço suficiente acima para que a marca d'água se destaca.  
  
- Use o `Environment.GrayText` fonte do ambiente padrão e token de cor. Hiperlinks devem usar os tokens de hiperlink padrão compartilhado: `Environment.PanelHyperlink`, `Environment.PanelHyperlinkHover`, `Environment.PanelHyperlinkPressed`, e `Environment.PanelHyperlinkDisabled`.  
  
- As marcas d'água não podem ser selecionadas no plano de fundo  
  
- Se possível, inclua links em que a marca d'água para ajudar o usuário a se familiarizar.  
  
  ![Texto em uma janela do designer de marca d'água](../../extensibility/ux-guidelines/media/070702-05-watermark1.png "070702 05_Watermark1")  
  
  ![Texto em uma janela de ferramenta de marca d'água](../../extensibility/ux-guidelines/media/070702-06-watermark2.png "070702 06_Watermark2")  
  
  **Exemplos de texto de marca d'água no Visual Studio**  
  
##  <a name="BKMK_ButtonsAndHyperlinks"></a> Hiperlinks e botões  
  
### <a name="overview"></a>Visão geral  
 Controles de botões e links (hiperlinks) devem seguir [diretrizes básicas de área de trabalho do Windows em hiperlinks](https://msdn.microsoft.com/library/windows/desktop/dn742406\(v=vs.85\).aspx) para utilização de palavras, dimensionando e espaçamento.  
  
### <a name="choosing-between-buttons-and-links"></a>Escolhendo entre os botões e links  
 Tradicionalmente, os botões foram usados para ações e hiperlinks foram reservados para navegação. Botões podem ser usados em todos os casos, mas a função de links foi expandida no Visual Studio para que os botões e links são mais intercambiáveis em algumas condições.  
  
 Quando usar os botões de comando:  
  
- Comandos primários  
  
- Exibição do windows usada para coletar entrada ou fazer escolhas, mesmo se eles são comandos secundários  
  
- Ações destrutivas ou irreversíveis  
  
- Botões de compromisso em assistentes e fluxos de página  
  
  Evite os botões de comando nas janelas de ferramentas, ou se precisar de mais de duas palavras para o rótulo. Os links podem ter mais rótulos.  
  
  Quando usar links:  
  
- Navegação para outra janela, documento ou página da web  
  
- Situações que exigem um rótulo mais tempo ou uma frase curta para descrever a intenção da ação  
  
- Uma forte espaços em que um botão seria sobrecarregar a interface do usuário, desde que a ação não destrutivas ou irreversível  
  
- Ocupando comandos secundários em situações em que há muitos comandos  
  
#### <a name="examples"></a>Exemplos  
 ![Uma mensagem de status a seguir os links de comando da barra de informações](../../extensibility/ux-guidelines/media/070703-01-commandlinkinfobar.png "070703 01_CommandLinkInfobar")  
  
 **Links de comando usada na barra de informações a seguir de uma mensagem de status**  
  
 ![Links usados o pop-up do CodeLens](../../extensibility/ux-guidelines/media/070703-02-linksincodelens.png "070703 02_LinksInCodeLens")  
  
 **Links usados o pop-up do CodeLens**  
  
 ![Links usados como comandos secundários](../../extensibility/ux-guidelines/media/070703-03-linksassecondarycommands.png "070703 03_LinksAsSecondaryCommands")  
  
 **Usado para comandos secundários onde botões atrairia muita atenção de links**  
  
### <a name="common-buttons"></a>Botões comuns  
  
#### <a name="text"></a>Texto  
 Siga as diretrizes de escrita [interface do usuário do texto e a terminologia](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology).  
  
#### <a name="visual-style"></a>Estilo Visual  
  
##### <a name="standard-dialogs"></a>Caixas de diálogo padrão  
 A maioria dos botões no Visual Studio será exibida nas caixas de diálogo padrão e não deve ser estilizados. Eles devem refletir a aparência padrão dos botões, conforme determinado pelo sistema operacional.  
  
##### <a name="themed"></a>Com temas  
 Em alguns casos, botões podem ser usados na interface do usuário com estilo e esses botões devem ser estilizados adequadamente. Ver [caixas de diálogo](../../extensibility/ux-guidelines/application-patterns-for-visual-studio.md#BKMK_Dialogs) para obter informações sobre controles com tema.  
  
### <a name="special-buttons"></a>Botões especiais  
  
#### <a name="browse-buttons"></a>Procure... botões  
 **[Procurar...]**  botões são usados em grades, caixas de diálogo e janelas de ferramentas e outros elementos de interface do usuário sem janela restrita. Eles exibem um seletor que ajuda a preencher um valor em um controle de usuário. Há duas variações deste botão curtos e longos.  
  
 ![Longo &#91;procurar... &#93; botão](../../extensibility/ux-guidelines/media/070703-04-browselong.gif "070703 04_BrowseLong")  
  
 **O botão [procurar...] longo**  
  
 ![Curto reticências&#45;somente &#91;procurar... &#93; botão](../../extensibility/ux-guidelines/media/070703-05-browseshort.gif "070703 05_BrowseShort")  
  
 **O botão curto somente nas reticências [...]**  
  
 Quando usar o botão curto somente reticências:  
  
- Se houver mais de um longo **[procurar...]**  botão na caixa de diálogo, como quando vários campos permitem para navegação. Usar curto **[...]**  botão de cada um para evitar as chaves de acesso confuso criadas por essa situação (**& navegue** e **p & rocurar** na mesma caixa de diálogo).  
  
- Em uma caixa de diálogo estreita, ou quando não há nenhum lugar razoável para colocar o botão longo.  
  
- Se o botão será exibido em um controle de grade.  
  
  Diretrizes para usar o botão:  
  
- Não use uma chave de acesso. Para acessá-lo usando o teclado, o usuário deve guia do controle adjacente. Certifique-se de que a ordem de tabulação é, de modo que qualquer botão de procurar fica imediatamente após o campo que ele será preenchido. Nunca use um caractere de sublinhado abaixo do primeiro período.  
  
- Defina o Active Accessibility MSAA (Microsoft) **nome** propriedade **procurar...**  (incluindo as reticências) para que a tela leitores lerá como "Procurar" e não "dot-ponto-ponto" ou "período período-período." Para controles gerenciados, isso significa que a configuração de **AccessibleName** propriedade.  
  
- Nunca use um sinal de reticências **[...]**  botão para qualquer coisa, exceto uma ação de navegação. Por exemplo, se você precisar um **[novo...]**  botão, mas não tem espaço suficiente para o texto, em seguida, a caixa de diálogo precisa ser reprojetada.  
  
##### <a name="sizing-and-spacing"></a>Dimensionamento e espaçamento  
 ![Dimensionamento &#91;procurar... &#93; botões](../../extensibility/ux-guidelines/media/070703-06-browsesizing.png "070703 06_BrowseSizing")  
  
 **Botões de dimensionamento [procurar...]**  
  
 ![Espaçamento &#91;procurar... &#93; botões](../../extensibility/ux-guidelines/media/070703-07-browsespacing.png "070703 07_BrowseSpacing")  
  
 **Botões de espaçamento [procurar...]**  
  
#### <a name="graphical-buttons"></a>Botões gráficos  
 Alguns botões devem sempre usar uma imagem gráfica e nunca inclua texto para conservar o espaço e evitar problemas de localização. Geralmente, eles são usados no seletor de campo e outras listas classificável.  
  
> [!NOTE]
>  Os usuários precisam pressionar tab até esses botões (não há nenhuma chave de acesso), portanto, colocá-los em uma ordem adequada. Mapear a propriedade de nome do botão para a ação que leva para que os leitores de tela interpretam corretamente a ação do botão.  
  
|||  
|-|-|  
|Adicionar|![Botão de "Adicionar" gráfica](../../extensibility/ux-guidelines/media/070703-08-buttonadd.png "070703 08_ButtonAdd")|  
|Remover|![Botão "Remover" gráfico](../../extensibility/ux-guidelines/media/070703-09-buttonremove.png "070703 09_ButtonRemove")|  
|Adicionar todos|![Botão "Adicionar tudo" gráfica](../../extensibility/ux-guidelines/media/070703-10-buttonaddall.png "070703 10_ButtonAddAll")|  
|Remover tudo|![Botão "Remover tudo" gráfica](../../extensibility/ux-guidelines/media/070703-11-buttonremoveall.png "070703 11_ButtonRemoveAll")|  
|Mover Para Cima|![Botão de "Mover para cima" gráfica](../../extensibility/ux-guidelines/media/070703-12-buttonmoveup.png "070703 12_ButtonMoveUp")|  
|Mover Para Baixo|![Botão de "Mover para baixo" gráfica](../../extensibility/ux-guidelines/media/070703-13-buttonmovedown.png "070703 13_ButtonMoveDown")|  
|Excluir|![Botão "Excluir" de gráfico](../../extensibility/ux-guidelines/media/070703-14-buttondelete.png "070703 14_ButtonDelete")|  
  
##### <a name="sizing-and-spacing"></a>Dimensionamento e espaçamento  
 Dimensionamento para botões gráfica é da mesma maneira que uma versão abreviada do **[procurar...]**  botão (26 x 23 pixels):  
  
 ![Botão com e sem cor transparente mostrando](../../extensibility/ux-guidelines/media/070703-15-graphicalbuttonspacing.png "070703 15_GraphicalButtonSpacing")  
  
 **Aparência de uma imagem gráfica no botão, com e sem cor transparente mostrando**  
  
### <a name="hyperlinks"></a>Hiperlinks  
 Os hiperlinks são adequados para ações com base em navegação, como abrir um tópico da Ajuda, a caixa de diálogo modal ou o assistente. Se um hiperlink é usado para um comando, ele sempre deve exibir uma alteração perceptível e visível na interface do usuário. Em geral, as ações que confirme para uma ação (como salvar, cancelar e excluir) são comunicadas melhor usando um botão.  
  
#### <a name="writing-style"></a>Estilo de escrita  
 Siga as [diretrizes de área de trabalho do Windows para o texto da interface do usuário](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx). Não use "Saiba mais sobre," "Diga-me mais sobre" ou a frase "Get help com isso". Frase em vez disso, o texto do link de Ajuda em termos da pergunta principal respondida pelo conteúdo da Ajuda. Por exemplo, "**como adicionar um servidor para o Gerenciador de servidores?**"  
  
#### <a name="visual-style"></a>Estilo Visual  
  
-   Sempre devem usar hiperlinks [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService). Se um hiperlink não é estilizado corretamente, ele pisca em vermelho quando ativo ou mostra uma cor diferente após a que está sendo visitado.  
  
-   Não inclua sublinhados pairando estado, a menos que o link é um fragmento da sentença em uma frase completa, como em uma marca d'água para o controle.  
  
-   Sublinhados não devem aparecer em foco. Em vez disso, os comentários para o usuário que o link está ativo são uma alteração de cor pequena e o cursor de link apropriado.  
  
##  <a name="BKMK_TreeViews"></a> Modos de exibição de árvore  
  
### <a name="overview"></a>Visão geral  
 Modos de exibição de árvore fornecem uma maneira de organizar complexos lista em grupos pai-filho. Um usuário pode expandir ou recolher grupos pai para revelar ou ocultar itens de filho subjacente. Cada item em uma exibição de árvore pode ser selecionado para fornecer mais ação.  
  
 Este tópico aborda o uso aceitável, o design adequado e a funcionalidade dos modos de exibição de árvore.  
  
#### <a name="in-this-topic"></a>Neste tópico  
  
-   [Estilo Visual](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewVisualStyle)  
  
-   [Interações](../../extensibility/ux-guidelines/common-control-patterns-for-visual-studio.md#BKMK_TreeViewInteractions)  
  
###  <a name="BKMK_TreeViewVisualStyle"></a> Estilo Visual  
  
#### <a name="expanders"></a>Expansores  
 Controles de exibição de árvore devem estar de acordo com o design de expansor usado pelo Windows e o Visual Studio. Cada nó usa um controle expander para revelar ou ocultar itens subjacentes. Usar um controle expander fornece consistência para os usuários que podem ser encontrados modos de exibição de árvore diferente dentro do Windows e o Visual Studio.  
  
 ![Corrija o controle de exibição de árvore](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705 1_TreeViewCorrect")  
  
 **Correto: estilo adequado do nó de exibição de árvore usando um controle expander**  
  
 ![Nós de modo de exibição de árvore incorreto](../../extensibility/ux-guidelines/media/070705-2-treeviewincorrect1.png "070705 2_TreeViewIncorrect1")  
  
 **Incorreto: estilo de inadequada modo de exibição do nó de árvore**  
  
#### <a name="selection"></a>Seleção  
 Quando um nó é selecionado na exibição de árvore, o realce deve expandir para a largura total do controle de exibição de árvore. Isso ajuda os usuários a identificar claramente qual item que foi selecionado. Cores de seleção devem refletir o tema atual do Visual Studio.  
  
 ![Corrija o controle de exibição de árvore](../../extensibility/ux-guidelines/media/070705-1-treeviewcorrect.png "070705 1_TreeViewCorrect")  
  
 **Correto: realce do nó selecionado se encaixa em toda a largura do controle de exibição de árvore.**  
  
 ![Realce do modo de exibição de árvore incorreto](../../extensibility/ux-guidelines/media/070705-3-treeviewincorrect2.png "070705 3_TreeViewIncorrect2")  
  
 **Incorreto: realce do nó selecionado não é adequado para toda a largura do controle de exibição de árvore.**  
  
#### <a name="icons"></a>Ícones  
 Ícones só devem ser usados em controles de exibição de árvore, se eles ajudar a identificar visualmente as diferenças entre os itens. Em geral, os ícones devem ser usados apenas em listas heterogêneas nos quais os ícones transportam informações para diferenciar os tipos de elementos. Em uma lista homogênea usando ícones com frequência pode ser visto como o ruído e deve ser evitado. Nesse caso, o ícone do grupo (pai) pode transmitir o tipo de itens dentro dela. A exceção a essa regra seria se o ícone é dinâmico e é usado para indicar o estado.  
  
#### <a name="scroll-bars"></a>Barras de rolagem  
 Barras de rolagem sempre deverão estar ocultos se o conteúdo caiba no controle de exibição de árvore. É aceitável para barras de rolagem ser ocultos ou semitransparente em uma janela rolável e aparecem quando a janela que contém a exibição de árvore tem o foco ou após a passagem da árvore de exibir em si.  
  
 ![Árvore de exibição com barras de rolagem](../../extensibility/ux-guidelines/media/070705-4-scrollbars.png "070705 4_Scrollbars")  
  
 **Ambas as barras de rolagem vertical e horizontal são exibidas porque o conteúdo excederam os limites do controle de exibição de árvore.**  
  
###  <a name="BKMK_TreeViewInteractions"></a> Interações  
  
#### <a name="context-menus"></a>Menus de contexto  
 Um nó do modo de exibição de árvore pode revelar as opções do submenu em um menu de contexto. Normalmente, isso ocorre quando um usuário tem pequeno um item ou pressionou a tecla de Menu em um teclado do Windows com o item selecionado. É importante que o nó obtém foco e está selecionado. Isso ajuda o usuário a identificar qual item de submenu pertence.  
  
 ![Menu de contexto e o nó selecionado na árvore](../../extensibility/ux-guidelines/media/070705-5-contextmenu.png "070705 5_ContextMenu")  
  
 **O item que tem geram o foco de ganhos de menu de contexto para notificar o usuário que o item foi selecionado.**  
  
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
  
- **Seta para a direita:** expandir um nó. Depois que o nó é expandido, ele deve continuar navegando até a coluna mais próxima à direita. Deve interromper a navegação no final da linha.  
  
- **Guia:** navega para a célula mais próxima à direita.  No final da linha, a navegação continua para a próxima linha.  
  
- **Shift + Tab:** navega para a célula mais próxima à esquerda.  No início da linha, a navegação continua para a célula mais à direita na linha anterior.  
  
  ![Controle Trid no Visual Studio](../../extensibility/ux-guidelines/media/070705-6-trid.png "070705 6_Trid")  
  
  **Um controle trid no Visual Studio**

