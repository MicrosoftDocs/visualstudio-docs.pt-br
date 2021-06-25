---
title: UX Essentials para Visual Studio | Microsoft Docs
description: Revise essas práticas recomendadas de experiência do usuário para novos recursos que você desenvolve para Visual Studio, incluindo o conhecimento sobre a resolução de tela.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 74b27e87e6f16130573ef6671286501f77e44352
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899414"
---
# <a name="ux-essentials-for-visual-studio"></a>Fundamentos de UX para Visual Studio

## <a name="best-practices"></a>Melhores práticas

### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. Seja consistente dentro do Visual Studio ambiente.

- Siga os padrões [de interação existentes](interaction-patterns-for-visual-studio.md) dentro do shell.

- Projete recursos para serem consistentes com a linguagem visual do shell e [os requisitos de design.](evaluation-tools-for-visual-studio.md)

- Use comandos e controles compartilhados quando eles existirem.

- Entenda a Visual Studio hierarquia e como ela estabelece o contexto e orienta a interface do usuário.

### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. Use o serviço de ambiente para fontes e cores.

- A interface do usuário deve respeitar a [configuração](fonts-and-formatting-for-visual-studio.md) de fonte do ambiente atual, a menos que ela seja exposta para personalização na página Fontes e Cores na caixa de diálogo Opções.

- Os elementos da interface do usuário devem usar o [Serviço VSColor,](colors-and-styling-for-visual-studio.md)usando tokens de ambiente compartilhados ou tokens específicos do recurso.

### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. Tornar todas as imagens consistentes com o novo estilo vs.

- Siga Visual Studio de design para ícones, glifos e outros elementos gráficos.

- Não coloque texto em elementos gráficos.

### <a name="4-design-from-a-user-centric-perspective"></a>4. Projetar de uma perspectiva centrada no usuário.

- Crie o fluxo de tarefas antes dos recursos individuais dentro dele.

- Familiarizar-se com os usuários e tornar esse conhecimento explícito em sua especificação.

- Ao revisar a interface do usuário, avalie a experiência completa, bem como os detalhes.

- Projete sua interface do usuário para que ela permaneça funcional e atraente, independentemente da localidade ou idioma.

## <a name="screen-resolution"></a>Resolução da tela

### <a name="minimum-resolution"></a>Resolução mínima

- A resolução mínima para Visual Studio 2015 é **1280 x 720**. Isso significa que é *possível usar* o Visual Studio nessa resolução, embora possa não ser uma experiência de usuário ideal. Não há nenhuma garantia de que todos os aspectos serão usáveis em resoluções inferiores a 1280 x 720.

- A resolução de destino para Visual Studio é **1366 x 768**. Essa é a resolução mais baixa na qual garantimos uma *boa experiência* do usuário.

- A altura inicial do diálogo deve ser menor que **700 pixels,** portanto, ela se ajusta à resolução mínima do quadro IDE em 96 dpi.

### <a name="high-density-displays"></a>Exibições de alta densidade
 A interface do usuário Visual Studio funcionar bem em todos os fatores de dimensionamento de DPI que o Windows dá suporte: 150%, 200% e 250%.

## <a name="anti-patterns"></a>Anti-padrões
 Visual Studio contém muitos exemplos de interface do usuário que seguem nossas diretrizes e práticas recomendadas. Em um esforço para ser consistente, os desenvolvedores geralmente fazem empréstimos de padrões de design de interface do usuário do produto semelhantes ao que estão criando. Embora essa seja uma boa abordagem que nos ajude a impulsionar a consistência na interação do usuário e no design visual, às vezes, apresentamos recursos com alguns detalhes que não atendem às nossas diretrizes devido a restrições de agendamento ou priorização de defeitos. Nesses casos, não queremos que as equipes copiem um desses "anti-padrões", pois eles proliferam uma interface do usuário ruim ou inconsistente dentro do Visual Studio ambiente.

### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>Campos/configurações necessários mostrados no estado de erro por padrão

#### <a name="feature-team-goals"></a>Metas da equipe de recursos

- Avisar os usuários de que eles adicionaram um elemento que deve ser configurado.

- Chamar a atenção do usuário para as áreas que precisam de entrada.

#### <a name="anti-pattern-solution"></a>Solução anti-padrão
 Assim que o usuário tiver iniciado uma ação e antes de concluir a tarefa, coloque imediatamente os ícones de parada crítica ao lado das áreas que precisam de configuração.

#### <a name="example-manifest-designer-declarations"></a>Exemplo: declarações do Designer de Manifesto
 Adicionar uma declaração à lista imediatamente a coloca em um estado de erro, que persiste até que o usuário desmarcar as propriedades necessárias.

 Nesse caso, há uma preocupação adicional porque o ícone usado para o alerta contém um ícone " " e, portanto, o ícone de remoção comum não pode &times; ser usado ao lado dele. Como resultado, a interface do usuário usa um botão Remover, um controle mais clunky.

 ![Colocar a interface do usuário em um estado de erro por padrão é um Visual Studio anti-padrão.](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti-padrão")<br />Colocar a interface do usuário em um estado de erro por padrão é um Visual Studio anti-padrão.

#### <a name="alternatives"></a>Alternativas

Uma solução melhor para esse problema é:

- Permita que o usuário adicione uma declaração sem aviso e, em seguida, mova-se imediatamente para definir propriedades no item.

- Adicione o ícone de aviso (triângulo ouro) quando o foco se mover do item, como para adicionar outra declaração à lista ou para tentar alterar as guias dentro do designer.

- Se o usuário tentar alterar as guias antes de definir propriedades em qualquer declaração, pop uma caixa de diálogo explicando que o aplicativo não será construído (ou quaisquer que sejam as implicações) até que os avisos sejam resolvidos. Se o usuário descartar a caixa de diálogo e mudar as guias de qualquer forma, um ícone (crítico ou aviso, conforme apropriado) será adicionado à guia Declarações.

### <a name="multiple-clicks-to-dismiss-ui"></a>Vários cliques para descartar a interface do usuário

#### <a name="feature-team-goals"></a>Metas da equipe de recursos
 Não permita que o usuário descarte a interface do usuário sem primeiro ver o texto da explicação.

#### <a name="anti-pattern"></a>Anti-padrão
 A equipe que inseriu os links de vídeo em vários locais na interface do usuário do VS decidiu em relação ao padrão comum do " " fechar botão e explicação da dica de ferramenta, conforme especificado pela UX, e, em vez disso, implementou uma lista de opções e um link "Não mostrar &times; novamente".

#### <a name="example-video-links-in-team-explorer"></a>Exemplo: links de vídeo no Team Explorer
Forçar o usuário a ler texto explicativo antes de descartar a interface do usuário é um anti-padrão no Visual Studio. Projetados corretamente, os links de vídeo devem exibir uma dica de ferramenta com informações adicionais sobre o foco e clicar em " " deve descartar a mensagem sem a necessidade de &times; interação adicional.

 ![Texto explicativo anti&#45;padrão &#45; incorreto](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />Padrão de link de vídeo incorreto

Em vez de um botão fechar simples (um clique), o usuário é forçado a usar dois cliques para simplesmente descartar a interface do usuário em todos os lugares em que os links de vídeo aparecem.

O design correto para essa situação é seguir o padrão comum para Internet Explorer, Office e Visual Studio: ao passar o mouse, o usuário pode ver a descrição da dica de ferramenta e um clique oculta a interface do usuário.

 ![Texto explicativo anti&#45;padrão &#45; correto](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-padrão-correto")<br />Padrão de link de vídeo correto

### <a name="using-command-bars-for-settings"></a>Usando barras de comando para configurações

**A Figura A** representa esse anti-padrão: colocar uma configuração sob um botão de comando que se aplica a mais do que apenas ao comando . Neste esboço, há comandos além de Iniciar Depuração – como Exibir no Navegador, Iniciar Sem Depuração e Entrar – que respeitarão a configuração selecionada.

![Figura A: Anti-padrão da barra de comandos](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-padrão-Figuraa")<br />Figura A: Anti-padrão da barra de comandos

Um pouco melhor, mas ainda indesejável, é colocar configurações desse tipo nas barras de ferramentas, conforme mostrado na **Figura B.** Embora os botões divididos usem menos espaço e, portanto, sejam uma melhoria nas listadas, ambos os designs ainda estão usando uma barra de ferramentas para promover algo que não é realmente um comando.

![Figura B: Melhor, mas ainda um anti-padrão de barra de comandos](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-padrão-FigureB")<br />Figura B: Melhor, mas ainda um anti-padrão de barra de comandos

Na abordagem correta mostrada na **Figura C**, a configuração está vinculada a uma série de comandos. Não há nenhuma configuração global sendo definida e estamos apenas alternando entre quatro comandos. Essa é a única situação em que os comandos na barra de ferramentas são aceitáveis.

![Figura C: Uso correto do padrão Visual Studio barra de comandos](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-padrão-FigureC")<br />Figura C: Uso correto do padrão Visual Studio barra de comandos

### <a name="control-anti-patterns"></a>Controlar anti-padrões
 Alguns antipadrões são simplesmente uso incorreto ou apresentação de um controle ou grupo de controles.

#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>Sublinhado usado como um rótulo de grupo, não um hiperlink
 O texto sublinhado deve ser usado somente para hiperlinks.

 **Ruim:**\
 ![Texto sublinhado que não é um hiperlink é um Visual Studio anti-padrão.](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "0102-g_GroupLabelIncorrect")<br />Texto sublinhado que não é um hiperlink é um Visual Studio anti-padrão.

 **Bom:**\
 ![Estilizado corretamente, o texto que não é de hiperlink é exibido sem alterações na fonte do ambiente.](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "0102-h_GroupLabelCorrect")<br />Estilizado corretamente, o texto que não é de hiperlink é exibido sem alterações na fonte do ambiente.

#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>Clicar em uma caixa de seleção resulta em uma caixa de diálogo pop-up
 Clicar na caixa de seleção "Habilitar Área de Trabalho Remota para todas as funções" no assistente "Publicar Windows Aplicativo Azure" imediatamente abrirá uma caixa de diálogo pop-up, um Visual Studio anti-padrão. Além disso, o campo de caixa de seleção não preenche com uma caixa de seleção depois de ser selecionado, outro anti-padrão de interação.

 ![Abrir uma caixa de diálogo depois de clicar em uma caixa de seleção é Visual Studio anti-padrão.](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "0102-i_CheckboxPopup")<br />Abrir uma caixa de diálogo depois de clicar em uma caixa de seleção é Visual Studio anti-padrão.

### <a name="hyperlink-anti-patterns"></a>Anti-padrões de hiperlink
 O exemplo a seguir contém dois anti-padrões:

1. O primeiro plano que fica vermelho ao passar o mouse significa que a cor compartilhada correta do serviço de fonte não está sendo usada.

2. "Saiba mais" não é o texto apropriado para um link para um tópico conceitual. A meta do usuário não é saber mais, é entender as ramificações de sua escolha.

   ![Ignorar o serviço de cores e usar "Saiba mais" para hiperlinks são antipadrões do Visual Studio.](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "0102-j_HyperlinkIncorrect")<br />Ignorar o serviço de cores e usar "Saiba mais" para hiperlinks são antipadrões do Visual Studio.

**Melhor solução:** Ponha a pergunta que o usuário deveria fazer clicando no link. Por exemplo:

- Como funcionam os serviços do Windows Azure?

- Quando preciso de um projeto de serviços móveis do Windows Azure?

#### <a name="using-click-here-for-links"></a>Usando "clique aqui" para obter links
 Os hiperlinks devem ser autodescritivos. É um antipadrão usar "clique aqui" ou qualquer variação semelhante.

 **Inadequado:** "Clique aqui para obter instruções sobre como criar um novo projeto".

 **Bom:** "Como fazer criar um novo projeto?"
