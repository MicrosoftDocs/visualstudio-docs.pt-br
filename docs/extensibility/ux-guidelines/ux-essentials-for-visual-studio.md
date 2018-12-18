---
title: Fundamentos de UX para Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 37d2942e64a4c964ad696d1eb2c0d4bf3c777b87
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49848586"
---
# <a name="ux-essentials-for-visual-studio"></a>Fundamentos de UX para Visual Studio
## <a name="best-practices"></a>Práticas recomendadas  
  
### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. Seja consistente no ambiente do Visual Studio.  
  
-   Siga existente [padrões de interação](interaction-patterns-for-visual-studio.md) dentro do shell.  
  
-   Recursos para ser consistente com os idiomas do shell do visual design e [requisitos de habilidade](evaluation-tools-for-visual-studio.md).  
  
-   Use controles e comandos compartilhados quando existirem.  
  
-   Compreenda a hierarquia do Visual Studio e como ele estabelece o contexto e unidades de interface do usuário.  
  
### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. Use o serviço de ambiente para fontes e cores.  
  
-   Interface do usuário deve respeitar o atual [fonte de ambiente](fonts-and-formatting-for-visual-studio.md) , a menos que ela é exposta para personalização na página de fontes e cores na caixa de diálogo Opções de configuração.  
  
-   Elementos de interface do usuário devem usar o [VSColor Service](colors-and-styling-for-visual-studio.md), usar compartilhado tokens de ambiente ou tokens de recurso específico.  
  
### <a name="3-make-all-imagery-consistent-with-the-new-vs-style"></a>3. Tornar todas as imagens consistente com o novo estilo de VS.  
  
-   Siga os princípios de design do Visual Studio para ícones, glifos e outros elementos gráficos.  
  
-   Não coloque texto em elementos gráficos.  
  
### <a name="4-design-from-a-user-centric-perspective"></a>4. Design de uma perspectiva centrada no usuário.  
  
-   Crie o fluxo de tarefas antes dos recursos individuais dentro dele.  
  
-   Estar familiarizado com os usuários e tornar esse conhecimento explícito em suas especificações.  
  
-   Ao revisar a interface do usuário, avalie a experiência completa, bem como os detalhes.  
  
-   Projete a interface do usuário para que ele permaneça funcional e atraente, independentemente do idioma ou localidade.  
  
## <a name="screen-resolution"></a>Resolução de tela  
  
### <a name="minimum-resolution"></a>Resolução mínima  
 - É a resolução mínima Dev14 do Visual Studio **1280 x 720**. Isso significa que ele *possíveis* para usar o Visual Studio nessa resolução, embora não seja uma excelente experiência do usuário. Não há nenhuma garantia de que todos os aspectos poderá ser usados em resoluções menores que 1280 x 720.  
  
 - É a resolução de destino para o Visual Studio **1366 x 768**. Esta é a resolução mais baixa no qual podemos prometer um *boa* experiência do usuário.

 - Altura da caixa de diálogo inicial deve ser **menor que 700 pixels**, de modo que ele caiba na resolução mínima de quadro do IDE em 96 dpi.
  
### <a name="high-density-displays"></a>Monitores de alta densidade  
 Interface do usuário no Visual Studio deve funcionar bem em DPI todos os fatores que oferece suporte a Windows fora da caixa de dimensionamento: 150%, 200% e % de 250.  
  
## <a name="anti-patterns"></a>Antipadrões  
 Visual Studio contém muitos exemplos de interface do usuário que sigam nossas diretrizes e práticas recomendadas. Em um esforço para ser consistente, os desenvolvedores geralmente emprestam de padrões de design de interface do usuário de produto semelhantes a que está compilando. Embora essa seja uma boa abordagem que ajuda a nos orientar consistência na interação do usuário e design visual, podemos ocasionalmente enviar recursos com alguns detalhes que não atender às nossas diretrizes devido a restrições de agendamento ou defeito priorização. Nesses casos, queremos que as equipes de cópia em um destes "antipadrões" porque elas se proliferam inválido ou está inconsistente da interface do usuário dentro do ambiente do Visual Studio.  
  
### <a name="required-fieldssettings-shown-in-error-state-by-default"></a>Campos/configurações necessárias mostradas em estado de erro por padrão  
  
#### <a name="feature-team-goals"></a>Metas da equipe de recursos  
  
-   Avise os usuários que incluíram um elemento que deve ser configurado.  
  
-   Chame a atenção do usuário para as áreas que precisam de entrada.  
  
#### <a name="anti-pattern-solution"></a>Antipadrão de solução  
 Assim que o usuário iniciou uma ação e antes da tarefa estiver concluída, coloque imediatamente parada crítica ícones ao lado de áreas que precisam de configuração.  
  
#### <a name="example-manifest-designer-declarations"></a>Exemplo: Declarações de Designer de manifesto  
 Adicionar uma declaração à lista imediatamente coloca-o em um estado de erro, que persiste até que o usuário define as propriedades necessárias.  
  
 Nesse caso, há uma preocupação adicional porque o ícone usado para o alerta contém um "&times;" ícone, portanto, o ícone Remover comum não pode ser usado ao lado dela. Como resultado, a interface do usuário usa um botão Remover, um controle mais trabalhoso.  
  
 ![Colocando a interface do usuário em um estado de erro por padrão é um antipadrão do Visual Studio. ](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti padrão")<br />Colocando a interface do usuário em um estado de erro por padrão é um antipadrão do Visual Studio.
  
#### <a name="alternatives"></a>Alternativas  
 Uma solução muito melhor para esse problema seria:  
  
-   Permitir que o usuário adicione uma declaração sem aviso e, em seguida, mover imediatamente para definir propriedades no item.  
  
-   Adicionar o ícone de aviso (triângulo gold) quando foco é movido do item, como para adicionar outra declaração à lista de ou para tentar alterar guias dentro do designer.  
  
-   Se o usuário tenta alterar guias antes de definir propriedades em todas as declarações, exibida uma caixa de diálogo explicando que o aplicativo não será criado (ou qualquer das implicações) até que os avisos sejam resolvidos. Se o usuário fecha a caixa de diálogo e guias de alterações assim mesmo, em seguida, um ícone (crítico ou aviso, conforme apropriado) é adicionado à guia de declarações.  
  
### <a name="multiple-clicks-to-dismiss-ui"></a>Vários cliques para ignorar a interface do usuário  
  
#### <a name="feature-team-goals"></a>Metas da equipe de recursos  
 Não permitir que o usuário ignorar a interface do usuário sem primeiro ver o texto de explicação.  
  
#### <a name="anti-pattern"></a>Antipadrão  
 A equipe inserindo os links de vídeos em vários locais dentro da interface do usuário VS decidimos contra o padrão comum do "&times;" Fechar explicação de botão e a dica de ferramenta, como especificado pela experiência do usuário e implementados em vez disso, uma lista suspensa e vincular "Não mostrar novamente".  

#### <a name="example-video-links-in-team-explorer"></a>Exemplo: links de vídeo no Team Explorer
Forçar o usuário leia textos explicativos antes de ignorar a interface do usuário é um antipadrão dentro do Visual Studio. Links projetado corretamente, o vídeo deve exibir uma dica de ferramenta com informações adicionais no hover e clicando o "&times;" deve ignorar a mensagem sem a necessidade de interação adicional.


 ![Texto explicativo anti&#45;padrão &#45; incorreto](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")<br />Padrão de link de vídeo incorreto
  
#### <a name="result"></a>Resultado  
 Em vez de um botão de fechar simple (um clique), o usuário é forçado a usar dois cliques para simplesmente ignorar a interface do usuário em cada local que pareça que os links de vídeos.  
  
#### <a name="alternatives"></a>Alternativas  
 O design correto para essa situação seria seguem o padrão comum para o Internet Explorer, o Office e o Visual Studio: ao focalizar, o usuário pode ver a descrição da dica de ferramenta e um clique oculta a interface do usuário.  
  
 ![Texto explicativo anti&#45;padrão &#45; correto](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-padrão-corrigir")<br />Padrão de link de vídeo correto
  
### <a name="using-command-bars-for-settings"></a>Usando barras de comando para configurações  
 **A Figura A** representa esse antipadrão: colocar uma configuração abaixo de um botão de comando que se aplica a mais do que apenas o comando. Nesse esboço, há comandos além de iniciar depuração — como o modo de exibição no navegador, iniciar sem depuração e intervir — que respeita a configuração selecionada.  

  ![Figura a: comando barra antipadrão](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-padrão-FigureA")<br />Figura r: antipadrão comando barra
  
 Um pouco melhor, mas que ainda indesejável, é colocar as configurações desse tipo em barras de ferramentas, conforme mostrado na **Figura B**. Enquanto os botões de divisão ocupar menos espaço e, portanto, uma melhoria em listas suspensas, ambos os designs ainda estiver usando uma barra de ferramentas para promover a algo que não é realmente um comando.  
 
 ![Figura b: melhor, mas ainda um antipadrão de barra comando](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-padrão-FigureB")<br />Figura b: melhor, mas ainda um antipadrão de barra comando
 
  Na abordagem correta mostrada na **Figura C**, a configuração está vinculada a uma série de comandos. Não há nenhuma configuração global que está sendo definida e estamos mudando apenas entre quatro comandos. Isso é a única situação em que os comandos na barra de ferramentas são aceitáveis. 

 ![Figura c: uso correto de padrão de barra de comando do Visual Studio](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-padrão-FigureC")<br />Use a Figura c: correto do padrão de barra de comando do Visual Studio
   
### <a name="control-anti-patterns"></a>Antipadrões de controle  
 Alguns antipadrões são uso simplesmente incorreto ou apresentação de um controle ou um grupo de controles.  
  
#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>Sublinhado usado como um rótulo de grupo, não um hiperlink  
 Texto sublinhado deve ser usado apenas para os hiperlinks.  
  
 **Ruim:**    
 ![Texto sublinhado que não é um hiperlink é um antipadrão do Visual Studio. ](../../extensibility/ux-guidelines/media/0102-g_grouplabelincorrect.png "g_GroupLabelIncorrect 0102")<br />Texto sublinhado que não é um hiperlink é um antipadrão do Visual Studio.
  
 **Boa:**   
 ![Estilizada corretamente, não-hyperlink texto aparece não adornado da fonte de ambiente. ](../../extensibility/ux-guidelines/media/0102-h_grouplabelcorrect.png "h_GroupLabelCorrect 0102")<br />Estilizada corretamente, não-hyperlink texto aparece não adornado da fonte de ambiente.
  
#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>Clicar em uma caixa de seleção de resulta em uma caixa de diálogo pop-up  
 Clicando na caixa de seleção "Habilitar a área de trabalho remota para todas as funções" no Assistente "Publicar aplicativo do Windows Azure" imediatamente abre uma caixa de diálogo pop-up, um antipadrão do Visual Studio. Além disso, o campo da caixa de seleção não preenche com uma caixa de seleção após ser selecionado, antipadrão de outra interação.  
  
 ![Trazendo uma caixa de diálogo depois de clicar em uma caixa de seleção é um antipadrão do Visual Studio. ](../../extensibility/ux-guidelines/media/0102-i_checkboxpopup.png "i_CheckboxPopup 0102")<br />Trazendo uma caixa de diálogo depois de clicar em uma caixa de seleção é um antipadrão do Visual Studio.
  
### <a name="hyperlink-anti-patterns"></a>Antipadrões de hiperlink  
 O exemplo a seguir contém dois antipadrões.  
  
1. Em primeiro plano ativar vermelho em foco significa compartilhado cor correta do serviço da fonte não está sendo usado.  
  
2. Não é o texto apropriado para um link para um tópico conceitual "Saiba mais". Objetivo do usuário não é saber mais, é compreender as ramificações de sua preferência.  
  
   ![Ignorando o serviço de cor e uso de "Saiba mais" para os hiperlinks são antipadrões do Visual Studio. ](../../extensibility/ux-guidelines/media/0102-j_hyperlinkincorrect.png "j_HyperlinkIncorrect 0102")<br />Ignorando o serviço de cor e uso de "Saiba mais" para os hiperlinks são antipadrões do Visual Studio.  
  
   **Uma melhor solução:** faça a pergunta que o usuário deve estar se perguntando, clicando no link.  
  
-   Como funcionam os serviços do Windows Azure?  
  
-   Quando é necessário um projeto de serviços móveis do Windows Azure?  
  
#### <a name="using-click-here-for-links"></a>Usando "Clique aqui" para links  
 Hiperlinks devem ser um nome bastante auto-explicativo. É um antipadrão usar "Clique aqui" ou qualquer variação semelhante.  
  
 **Inválido:** "Clique aqui para obter instruções sobre como criar um novo projeto."
  
 **Boa:** "Como criar um novo projeto?"