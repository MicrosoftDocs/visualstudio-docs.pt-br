---
title: Fundamentos de UX para Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a793cf7a-f230-43ce-88d0-fa5d6f1aa9c7
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: e7c9c2fe1c076a8851b1b95a9957cd721c61ae21
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799490"
---
# <a name="ux-essentials-for-visual-studio"></a>Fundamentos de UX para Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="best-practices"></a>Práticas recomendadas  
  
### <a name="1-be-consistent-within-the-visual-studio-environment"></a>1. Seja consistente no ambiente do Visual Studio.  
  
-   Siga padrões de interação existente dentro do shell.  
  
-   Recursos para ser consistente com os requisitos de idioma e a habilidade do visual do shell de design.  
  
-   Use controles e comandos compartilhados quando existirem.  
  
-   Compreenda a hierarquia do Visual Studio e como ele estabelece o contexto e unidades de interface do usuário.  
  
### <a name="2-use-the-environment-service-for-fonts-and-colors"></a>2. Use o serviço de ambiente para fontes e cores.  
  
-   Interface do usuário deve respeitar a configuração de fonte do ambiente atual, a menos que ela é exposta para personalização na página de fontes e cores na caixa de diálogo Opções.  
  
-   Elementos de interface do usuário devem usar o VSColor Service, usando tokens de ambiente compartilhado ou tokens de recurso específico.  
  
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
 A resolução mínima Dev14 do Visual Studio é 1280 x 1024. Isso significa que ele *possíveis* para usar o Visual Studio nessa resolução, embora não seja uma excelente experiência do usuário. Não há nenhuma garantia de que todos os aspectos poderá ser usados em resoluções menores que 1280 x 1024.  
  
 Tamanho inicial da caixa de diálogo não deve exceder 1000 pixels de altura para se ajustar dentro do quadro do IDE dentro dessa resolução mínima a 96 dpi.  
  
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
  
 Nesse caso, há uma preocupação adicional porque o ícone usado para o alerta contém um "x", para que o comum remover ícone não pode ser usado ao lado dela. Como resultado, a interface do usuário usa um botão Remover, um controle mais trabalhoso.  
  
 ![Declaração de erro do Designer anti de manifesto&#45;padrão de](../../extensibility/ux-guidelines/media/manifestdesignererrordeclarationsanti-pattern.png "ManifestDesignererrordeclarationsanti padrão")  
  
 **Colocando a interface do usuário em um estado de erro por padrão é um antipadrão do Visual Studio.**  
  
#### <a name="alternatives"></a>Alternativas  
 Uma solução muito melhor para esse problema seria:  
  
-   Permitir que o usuário adicione uma declaração sem aviso e, em seguida, mover imediatamente para definir propriedades no item.  
  
-   Adicionar o ícone de aviso (triângulo gold) quando foco é movido do item, como para adicionar outra declaração à lista de ou para tentar alterar guias dentro do designer.  
  
-   Se o usuário tenta alterar guias antes de definir propriedades em todas as declarações, exibida uma caixa de diálogo explicando que o aplicativo não será criado (ou qualquer das implicações) até que os avisos sejam resolvidos. Se o usuário fecha a caixa de diálogo e guias de alterações assim mesmo, em seguida, um ícone (crítico ou aviso, conforme apropriado) é adicionado à guia de declarações.  
  
### <a name="forcing-the-user-to-read-text-before-dismissing-ui"></a>Forçar o usuário ler o texto antes de ignorar a interface do usuário  
  
#### <a name="feature-team-goals"></a>Metas da equipe de recursos  
 Não permitir que o usuário ignorar a interface do usuário sem primeiro ver o texto de explicação.  
  
#### <a name="anti-pattern"></a>Antipadrão  
 A equipe inserindo os links de vídeos em vários locais dentro da interface do usuário do VS, decidimos contra o padrão comum de um X feche explicação de botão e a dica de ferramenta conforme especificado pelo UX e implementados em vez disso, uma lista suspensa e o link "Não mostrar novamente".  
  
 ![Texto explicativo anti&#45;padrão &#45; incorreto](../../extensibility/ux-guidelines/media/incorrectuseofmultipleclicks.png "Incorrectuseofmultipleclicks")  
  
 **Incorreto: forçar o usuário leia textos explicativos antes de ignorar a interface do usuário é um antipadrão dentro do Visual Studio.**  
  
#### <a name="result"></a>Resultado  
 Em vez de um botão de fechar simple (um clique), o usuário é forçado a usar dois cliques para simplesmente ignorar a interface do usuário em cada local que pareça que os links de vídeos.  
  
#### <a name="alternatives"></a>Alternativas  
 O design correto para essa situação seria seguem o padrão comum para o Internet Explorer, o Office e o Visual Studio: ao focalizar, o usuário pode ver a descrição da dica de ferramenta e um clique oculta a interface do usuário.  
  
 ![Texto explicativo anti&#45;padrão &#45; correto](../../extensibility/ux-guidelines/media/explanatorytextanti-pattern-correct.png "Explanatorytextanti-padrão-corrigir")  
  
 **Correto: conforme projetado, links de vídeo deve exibir uma dica de ferramenta com informações adicionais ao passar o e clicando no "X" deve ignorar a mensagem sem a necessidade de interação adicional.**  
  
### <a name="using-command-bars-for-settings"></a>Usando barras de comando para configurações  
 ![Barra de comandos anti&#45;padrão &#45; A Figura](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurea.png "Commandbaranti-padrão-FigureA")  
  
 **Figura r: antipadrão comando barra**  
  
 **A Figura A** representa esse antipadrão: colocar uma configuração abaixo de um botão de comando que se aplica a mais do que apenas o comando. Nesse esboço, há comandos além de iniciar depuração — como o modo de exibição no navegador, iniciar sem depuração e intervir — que respeita a configuração selecionada.  
  
 ![Barra de comandos anti&#45;padrão &#45; Figura B](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figureb.png "Commandbaranti-padrão-FigureB")  
  
 **Figura b: melhor, mas ainda um antipadrão de barra comando**  
  
 Um pouco melhor, mas que ainda indesejável, é colocar as configurações desse tipo em barras de ferramentas, conforme mostrado na **Figura B**. Enquanto os botões de divisão ocupar menos espaço e, portanto, uma melhoria em listas suspensas, ambos os designs ainda estiver usando uma barra de ferramentas para promover a algo que não é realmente um comando.  
  
 ![Barra de comandos anti&#45;padrão &#45; Figura C](../../extensibility/ux-guidelines/media/commandbaranti-pattern-figurec.png "Commandbaranti-padrão-FigureC")  
  
 **Use a Figura c: correto do padrão de barra de comando do Visual Studio**  
  
 Na **Figura C**, a configuração está vinculada a uma série de comandos. Não há nenhuma configuração global que está sendo definida e estamos mudando apenas entre quatro comandos. Isso é a única situação em que os comandos na barra de ferramentas são aceitáveis.  
  
### <a name="control-anti-patterns"></a>Antipadrões de controle  
 Alguns antipadrões são uso simplesmente incorreto ou apresentação de um controle ou um grupo de controles.  
  
#### <a name="underlining-used-as-a-group-label-not-a-hyperlink"></a>Sublinhado usado como um rótulo de grupo, não um hiperlink  
 Texto sublinhado deve ser usado apenas para os hiperlinks.  
  
 **Ruim:**  
  
 ![Sublinhado&#45;padrão de rótulos de grupo](../../extensibility/ux-guidelines/media/0102-g-grouplabelincorrect.png "g_GroupLabelIncorrect 0102")  
  
 **Texto sublinhado que não é um hiperlink é um antipadrão do Visual Studio.**  
  
 **Boa:**  
  
 ![Sublinhado&#45;padrão de rótulos de grupo &#40;correto&#41;](../../extensibility/ux-guidelines/media/0102-h-grouplabelcorrect.png "h_GroupLabelCorrect 0102")  
  
 **Estilizada corretamente, não-hyperlink texto aparece não adornado da fonte de ambiente.**  
  
#### <a name="clicking-on-a-check-box-results-in-a-pop-up-dialog"></a>Clicar em uma caixa de seleção de resulta em uma caixa de diálogo pop-up  
 Clicando na caixa de seleção "Habilitar a área de trabalho remota para todas as funções" no Assistente "Publicar aplicativo do Windows Azure" imediatamente abre uma caixa de diálogo pop-up, um antipadrão do Visual Studio. Além disso, o campo da caixa de seleção não preenche com uma caixa de seleção após ser selecionado, antipadrão de outra interação.  
  
 ![Pop de caixa de seleção&#45;antise&#45;padrão](../../extensibility/ux-guidelines/media/0102-i-checkboxpopup.png "i_CheckboxPopup 0102")  
  
 **Trazendo uma caixa de diálogo depois de clicar em uma caixa de seleção é um antipadrão do Visual Studio.**  
  
### <a name="hyperlink-anti-patterns"></a>Antipadrões de hiperlink  
 O exemplo a seguir contém dois antipadrões.  
  
1. Em primeiro plano ativar vermelho em foco significa compartilhado cor correta do serviço da fonte não está sendo usado.  
  
2. Não é o texto apropriado para um link para um tópico conceitual "Saiba mais". Objetivo do usuário não é saber mais, é compreender as ramificações de sua preferência.  
  
   ![Hiperlink anti&#45;padrões](../../extensibility/ux-guidelines/media/0102-j-hyperlinkincorrect.png "j_HyperlinkIncorrect 0102")  
  
   **Ignorando o serviço de cor e uso de "Saiba mais" para os hiperlinks são antipadrões do Visual Studio.**  
  
   **Uma melhor solução:** faça a pergunta que o usuário deve estar se perguntando, clicando no link.  
  
-   Como funcionam os serviços do Windows Azure?  
  
-   Quando é necessário um projeto de serviços móveis do Windows Azure?  
  
#### <a name="using-click-here-for-links"></a>Usando "Clique aqui" para links  
 Hiperlinks devem ser um nome bastante auto-explicativo. É um antipadrão usar "Clique aqui" ou qualquer variação semelhante.  
  
 **Inválido:** "Clique aqui para obter instruções sobre como criar um novo projeto."  
  
 **Boa:** "Como criar um novo projeto?"

