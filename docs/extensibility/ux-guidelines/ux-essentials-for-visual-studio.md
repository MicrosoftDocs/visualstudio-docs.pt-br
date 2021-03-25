---
title: UX Essentials para Visual Studio | Microsoft Docs
description: Examine essas práticas recomendadas de experiência do usuário para novos recursos que você desenvolve para o Visual Studio, incluindo conhecer a resolução da tela.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ce44b9234465af6bf52ce8baa0e60e641e845d3c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052665"
---
# <a name="ux-essentials-for-visual-studio"></a>Fundamentos de UX para Visual Studio

## <a name="best-practices"></a>Práticas recomendadas

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. seja consistente no ambiente do Visual Studio.

- Siga os [padrões de interação](interaction-patterns-for-visual-studio.md) existentes no Shell.

- Crie recursos para serem consistentes com os [requisitos de habilidade](evaluation-tools-for-visual-studio.md)e linguagem visual do Shell.

- Use comandos e controles compartilhados quando eles existirem.

- Entenda a hierarquia do Visual Studio e como ela estabelece o contexto e orienta a interface do usuário.

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. Use o serviço de ambiente para fontes e cores.

- A interface do usuário deve respeitar a configuração de [fonte do ambiente](fonts-and-formatting-for-visual-studio.md) atual, a menos que seja exposta para personalização na página fontes e cores da caixa de diálogo opções.

- Os elementos da interface do usuário devem usar o [serviço VSColor](colors-and-styling-for-visual-studio.md), usando tokens de ambiente compartilhado ou tokens específicos do recurso.

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. tornar todas as imagens consistentes com o novo estilo VS.

- Siga os princípios de design do Visual Studio para ícones, glifos e outros elementos gráficos.

- Não coloque texto em elementos gráficos.

### <a name="4-design-from-a-user-centric-perspective"></a>4. Projete a partir de uma perspectiva centrada no usuário.

- Crie o fluxo de tarefas antes dos recursos individuais dentro dele.

- Familiarize-se com seus usuários e torne esse conhecimento explícito em sua especificação.

- Ao revisar a interface do usuário, avalie a experiência completa, bem como os detalhes.

- Projete sua interface do usuário para que ela permaneça funcional e atraente, independentemente da localidade ou da linguagem.

## <a name="screen-resolution"></a>Resolução da tela

### <a name="minimum-resolution"></a>Resolução mínima

- A resolução mínima do Visual Studio 2015 é **1280x720**. Isso significa que é *possível* usar o Visual Studio nessa resolução, embora talvez não seja uma experiência de usuário ideal. Não há nenhuma garantia de que todos os aspectos serão utilizáveis em resoluções inferiores a 1280x720.

- A resolução de destino para o Visual Studio é **1366x768**. Essa é a resolução mais baixa na qual prometemos uma *boa* experiência do usuário.

- A altura da caixa de diálogo inicial deve ser **menor que 700 pixels**, então ela se ajusta à resolução mínima do quadro IDE em 96 dpi.

### <a name="high-density-displays"></a>Monitores de alta densidade
 A interface do usuário no Visual Studio deve funcionar bem em todos os fatores de dimensionamento de DPI que o Windows dá suporte à caixa: 150%, 200% e 250%.

## <a name="anti-patterns"></a>Antipadrões
 O Visual Studio contém muitos exemplos de interface do usuário que seguem nossas diretrizes e práticas recomendadas. Em um esforço para ser consistente, os desenvolvedores costumam emprestar os padrões de design da interface do usuário do produto, semelhante ao que estão criando. Embora essa seja uma boa abordagem que nos ajude a impulsionar a consistência na interação do usuário e no design do Visual, fazemos coisas para enviar recursos com alguns detalhes que não atendem às nossas diretrizes devido a restrições de agendamento ou à priorização de defeito. Nesses casos, não queremos que as equipes copiem um desses "antipadrões" porque elas proliferam interface de usuário inconsistente ou insuficiente no ambiente do Visual Studio.

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>Campos/configurações obrigatórios mostrados no estado de erro por padrão

#### <a name="feature-team-goals"></a>Metas da equipe de recursos

- Avise aos usuários que eles adicionaram um elemento que deve ser configurado.

- Chame a atenção do usuário para as áreas que precisam de entrada.

#### <a name="anti-pattern-solution"></a>Solução antipadrão
 Assim que o usuário tiver iniciado uma ação e antes de concluir a tarefa, coloque imediatamente ícones de parada crítica ao lado das áreas que precisam de configuração.

#### <a name="example-manifest-designer-declarations"></a>Exemplo: declarações de designer de manifesto
 A adição de uma declaração à lista a coloca imediatamente em um estado de erro, que persiste até que o usuário defina as propriedades necessárias.

 Nesse caso, há uma preocupação adicional porque o ícone usado para o alerta contém um &times; ícone "", portanto, o ícone de remoção comum não pode ser usado ao lado dele. Como resultado, a interface do usuário usa um botão remover, um controle mais desajeitado.

 ![Colocar a interface do usuário em um estado de erro por padrão é um antipadrão do Visual Studio.](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti-padrão")<br />Colocar a interface do usuário em um estado de erro por padrão é um antipadrão do Visual Studio.

#### <a name="alternatives"></a>Alternativas

Uma solução melhor para esse problema é:

- Permita que o usuário adicione uma declaração sem aviso e, em seguida, mova-se imediatamente para definir propriedades no item.

- Adicione o ícone de aviso (triângulo dourado) quando o foco se mover do item, como para adicionar outra declaração à lista ou tentar alterar as guias no designer.

- Se o usuário tentar alterar as guias antes de definir as propriedades em qualquer declaração, desative uma caixa de diálogo explicando que o aplicativo não compilará (ou quaisquer as implicações) até que os avisos sejam resolvidos. Se o usuário ignorar a caixa de diálogo e alterar as guias de qualquer forma, um ícone (crítico ou aviso, conforme apropriado) será adicionado à guia declarações.

### <a name="multiple-clicks-to-dismiss-ui"></a>Vários cliques para ignorar a interface do usuário

#### <a name="feature-team-goals"></a>Metas da equipe de recursos
 Não permitir que o usuário ignore a interface do usuário sem primeiro ver o texto da explicação.

#### <a name="anti-pattern"></a>Antipadrão
 A equipe que insere os links de vídeo em vários locais na interface do usuário do VS decidiu o padrão comum do &times; botão "" fechar e a explicação da dica de ferramenta conforme especificado pela UX e, em vez disso, implementou um link suspenso e "não mostrar novamente".

#### <a name="example-video-links-in-team-explorer"></a>Exemplo: links de vídeo no Team Explorer
Forçar o usuário a ler o texto explicativo antes de descartar a IU é um antipadrão no Visual Studio. Corretamente projetado, os links de vídeo devem exibir uma dica de ferramenta com informações adicionais sobre o foco e clicar em " &times; " deve ignorar a mensagem sem necessidade de mais interação.

 ![Padrão de&#45;de texto de explicação &#45; incorreto](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />Padrão de link de vídeo incorreto

Em vez de um botão de fechamento simples (um clique), o usuário é forçado a usar dois cliques para simplesmente ignorar a interface do usuário em cada lugar em que os links de vídeo são exibidos.

O design correto para essa situação é seguir o padrão comum para o Internet Explorer, Office e Visual Studio: ao focalizar, o usuário pode ver a descrição da dica de ferramenta e um clique oculta a interface do usuário.

 ![Padrão de&#45;de texto de explicação &#45; correto](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-padrão-correto")<br />Padrão de link de vídeo correto

### <a name="using-command-bars-for-settings"></a>Usando barras de comando para configurações

**A figura A** representa esse antipadrão: colocar uma configuração abaixo de um botão de comando que se aplica a mais do que apenas o comando. Neste esboço, há comandos além de iniciar depuração – como exibir no navegador, iniciar sem depuração e entrar, que respeitarão a configuração selecionada.

![Figura A: anti-padrão de barra de comandos](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-padrão-Figuraa")<br />Figura A: anti-padrão de barra de comandos

Um pouco melhor, mas ainda indesejável, é colocar as configurações desse tipo nas barras de ferramentas, como mostra a **Figura B**. Embora os botões de divisão demorem menos espaço e sejam, portanto, uma melhoria sobre os menus suspensos, os dois designs ainda estão usando uma barra de ferramentas para promover algo que não é realmente um comando.

![Figura B: melhor, mas ainda um antipadrão de barra de comandos](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-padrão-FigureB")<br />Figura B: melhor, mas ainda um antipadrão de barra de comandos

Na abordagem correta mostrada na **Figura C**, a configuração está vinculada a uma série de comandos. Não há nenhuma configuração global sendo definida e estamos apenas alternando entre quatro comandos. Essa é a única situação na qual os comandos na barra de ferramentas são aceitáveis.

![Figura C: uso correto do padrão de barra de comandos do Visual Studio](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-padrão-FigureC")<br />Figura C: uso correto do padrão de barra de comandos do Visual Studio

### <a name="control-anti-patterns"></a>Controlar antipadrões
 Alguns antipadrões são simplesmente uso incorreto ou apresentação de um controle ou grupo de controles.

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>Sublinhado usado como um rótulo de grupo, não um hiperlink
 O texto sublinhado só deve ser usado para hiperlinks.

 **Satisfatório**\
 ![O texto sublinhado que não é um hiperlink é um antipadrão do Visual Studio.](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />O texto sublinhado que não é um hiperlink é um antipadrão do Visual Studio.

 **Recomendá**\
 ![Com estilo correto, o texto sem hiperlink aparece como não adornado na fonte do ambiente.](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />Com estilo correto, o texto sem hiperlink aparece como não adornado na fonte do ambiente.

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>Clicar em uma caixa de seleção resulta em um diálogo pop-up
 Clicar na caixa de seleção "Habilitar Área de Trabalho Remota para todas as funções" no assistente "publicar o Windows Aplicativo Azure" abre imediatamente uma caixa de diálogo pop-up, um antipadrão do Visual Studio. Além disso, o campo caixa de seleção não é preenchido com uma caixa de seleção depois de ser selecionado, outro antipadrão de interação.

 ![A ativação de uma caixa de diálogo após o clique de um antipadrão do Visual Studio.](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />A ativação de uma caixa de diálogo após o clique de um antipadrão do Visual Studio.

### <a name="hyperlink-anti-patterns"></a>Anti-padrões de hiperlink
 O exemplo a seguir contém dois antipadrões:

1. O primeiro plano que ativa o vermelho em foco significa que a cor compartilhada correta do serviço de fonte não está sendo usada.

2. "Saiba mais" não é o texto apropriado para um link para um tópico conceitual. A meta do usuário não é saber mais, é entender as ramificações de sua escolha.

   ![Ignorar o serviço de cores e usar "Saiba mais" para hiperlinks são antipadrões do Visual Studio.](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />Ignorar o serviço de cores e usar "Saiba mais" para hiperlinks são antipadrões do Visual Studio.

**Melhor solução:** Ponha a pergunta que o usuário deveria fazer clicando no link. Por exemplo:

- Como funcionam os serviços do Windows Azure?

- Quando preciso de um projeto de serviços móveis do Windows Azure?

#### <a name="using-click-here-for-links"></a>Usando "clique aqui" para obter links
 Os hiperlinks devem ser autodescritivos. É um antipadrão usar "clique aqui" ou qualquer variação semelhante.

 **Inadequado:** "Clique aqui para obter instruções sobre como criar um novo projeto".

 **Bom:** "Como fazer criar um novo projeto?"
