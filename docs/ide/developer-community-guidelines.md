---
title: Diretrizes do Developer Community
description: Descreve as diretrizes para trabalhar com a comunidade de desenvolvedores do Visual Studio.
ms.date: 6/30/2020
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fb7f821a7b815b29c9f85b6ab0686edb0292866d
ms.sourcegitcommit: 4d5cd0b9de7a87efb69f17b02c2331b749e6ec8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86137561"
---
# <a name="developer-community-guidelines"></a>Diretrizes do Developer Community

A comunidade de desenvolvedores rastreia problemas e sugestões de recursos para o Visual Studio.

## <a name="submitting-problems-and-suggestions"></a>Enviando problemas e sugestões

A [comunidade de desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) rastreia problemas e sugestões de recursos para o Visual Studio.

### <a name="before-submitting-an-issue"></a>Antes de enviar um problema

Procure seu problema na Comunidade de desenvolvedores do Visual Studio para garantir que ela ainda não exista. Se você achar que o problema já existe, faça comentários relevantes e converta seu voto.

Se seu problema for uma pergunta, peça à Comunidade [Stack Overflow](https://stackoverflow.com/questions/tagged/visual-studio?tab=Newest) usando a marca _Visual-Studio_. Temos a equipe de suporte ao cliente que está monitorando essa marca e ajudará a responder as perguntas.

Se você não encontrar um problema existente que descreva seu bug ou recurso, envie um problema usando as diretrizes abaixo.

### <a name="writing-a-good-bug-report-or-feature-suggestion"></a>Escrevendo um bom relatório de bugs ou sugestão de recursos

- Arquivo apenas um problema ou solicitação de recurso por problema.

  - A combinação de vários problemas ou de solicitações de recursos em um único problema dificulta nosso diagnóstico e dificulta a votação do seu problema.
  - Não adicione seu problema como um comentário a um problema existente, a menos que ele seja para a entrada idêntica. Muitos problemas parecem semelhantes, mas têm causas diferentes, o que torna mais difícil diagnosticar seu problema.

- Quanto mais informações você puder fornecer, mais fácil será para nós reproduzir e corrigir o problema.
- Inclua as etapas a seguir com cada problema.

  - Etapas reproduzíveis (1... 2... 3...) e o que você esperava versus o que você experimentou.
  - Imagens, animações ou um link para um vídeo. Imagens e animações ilustram as etapas de reprodução, mas _não_ as substituem.
  - Conforme apropriado, um trecho de código que demonstra o problema ou um link para um repositório de código que podemos facilmente obter em nossa máquina para recriar o problema.

- Lembre-se de realizar as seguintes etapas:

  - Pesquise para ver se existe uma duplicata. Nesse caso, vote no problema existente, fornecendo comentários adicionais ou esclarecimentos, conforme necessário.
  - Recrie o problema depois de desabilitar todas as extensões. Se você achar que o problema é causado por uma extensão que você instalou, execute um problema na extensão, respectivamente.
  - Simplifique seu código em relação ao problema para que possamos isolar melhor o problema.

Mesmo com problemas que incluem detalhes avançados, talvez não seja possível reproduzir o problema e pode pedir mais informações!

## <a name="managing-problem-reports"></a>Gerenciando relatórios de problemas

A separação de um problema é um processo de várias etapas que é feito de forma colaborativa na equipe de recursos. A triagem geralmente leva uma semana, mas pode levar mais tempo. O objetivo da separação é fornecer uma compreensão clara do que acontecerá com o seu problema. Por exemplo, após a triagem, você saberá se planejamos corrigir seu problema ou aguardar mais comentários da Comunidade.

Depois de relatar um problema, os estados indicam onde seus envios estão no seu ciclo de vida. À medida que as equipes de produtos do Visual Studio revisam seus comentários, elas as definem com um estado apropriado. Acompanhe o progresso dos relatórios de problemas referenciando os [Estados e as perguntas frequentes do problema](https://docs.microsoft.com/visualstudio/ide/report-a-problem).

Quando faltam informações importantes no problema, atribuímos o estado de _mais informações_ . Comentamos o problema com as informações específicas de que precisamos e você receberá uma notificação por email. Se não recebermos as informações dentro de sete dias, enviaremos um lembrete. Depois disso, fechamos o tíquete após 14 dias de inatividade.

### <a name="wont-fix-bugs"></a>Não corrigirá bugs

Nós fechamos alguns bugs quando há um saldo negativo de custo-benefício. Por exemplo, se a correção for tão complexa regressão de riscos de ti para muitos usuários, a correção poderá não ser razoável. Quando fecharmos um bug como este, explicaremos por que fazemos isso.

### <a name="other-product"></a>Outro produto

Às vezes, ao relatar um problema, ele se torna causado por outro produto e não pelo Visual Studio. Pode ser outro aplicativo relacionado ou uma extensão. 

Quando isso acontecer, fecharemos o problema e solicitaremos que você o abra com o outro produto. Aqui estão alguns locais comuns para arquivar esses problemas:

* [SQL Server](https://feedback.azure.com/forums/908035-sql-server)
* [Suporte à assinatura do Visual Studio](https://feedback.azure.com/forums/908035-sql-server)
* [Office](https://support.office.com/article/how-do-i-give-feedback-on-microsoft-office-2b102d44-b43f-4dd2-9ff4-23cf144cfb11)
* [Windows](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)

#### <a name="additional-information"></a>Informações adicionais

- [Como aumentar as chances de um problema de desempenho ser corrigido](https://docs.microsoft.com/visualstudio/ide/how-to-increase-chances-of-performance-issue-being-fixed)
- [Solucionar problemas e criar logs para problemas do MSBuild](https://docs.microsoft.com/visualstudio/ide/msbuild-logs)

## <a name="managing-feature-suggestions"></a>Gerenciando sugestões de recursos

As sugestões de recursos são um meio de comunicação entre nós e os membros da comunidade de desenvolvedores. Tecnicamente, poderíamos manter todas as solicitações de recursos abertas para sempre. Mas manter os problemas abertos reduziria a visibilidade da Comunidade no status real de um recurso. Portanto, fechamos as solicitações de recurso que não abordaremos e atribuíremos recursos que nós podemos abordar ao rótulo de _revisão_ .

Se você sugeriu um recurso, talvez esteja desapontado que não planejamos atender à sua solicitação. Compreendemos isso. Todos nós já estamos lá neste projeto ou outros que contribuímos. Portanto, tenha certeza de que você adorará todas as suas entradas. Não pegue ataque pessoais quando fecharmos ou atribuímos o rótulo _sob revisão_ à sua sugestão. Se você sentir que sua sugestão de recursos merece estar aberta, esclareça o caso de uso e fale conosco ou reúna mais votos.

Em nosso processo de tomada de decisão, examinamos as seguintes características sobre a sugestão de recurso:

- Podemos criar e mantê-lo?
- Ele se alinha com nossa estratégia geral de [roteiro](https://docs.microsoft.com/visualstudio/productinfo/vs-roadmap) ?
- Ele tem suporte da Comunidade, conforme indicado por votos e comentários?
- Nós adoramos isso, mesmo com baixo suporte da Comunidade?

Quando não for possível responder "Sim" a qualquer uma dessas perguntas, vamos fechá-la. Mas, muitas vezes, a sugestão permanecerá aberta como _sob análise_ para reunir mais comentários da Comunidade.

Acompanhe o progresso de sua sugestão de recurso referenciando os [Estados de sugestão e as perguntas frequentes](https://docs.microsoft.com/visualstudio/ide/report-a-problem).

## <a name="discussion-etiquette"></a>Etiqueta de discussão

Para manter a conversa clara e transparente, limite a discussão para o inglês e mantenha as coisas relevantes para o problema. Seja considerem para outras pessoas e sempre tente ser educado e Professional.

Para obter mais informações, consulte o [código de conduta da Comunidade da Microsoft](https://answers.microsoft.com/en-us/page/codeofconduct).

Quaisquer violações no etiqueta de discussão podem levar à remoção do comentário e, eventualmente, à proibição do usuário.

## <a name="data-privacy"></a>Privacidade dos dados

Comentários e respostas são visíveis publicamente, mas todos os arquivos anexados são compartilhados de forma privada somente com a Microsoft. Essa visibilidade é benéfica porque permite que toda a Comunidade Veja os problemas e soluções encontrados por outros usuários. Se você estiver preocupado com a privacidade de seus dados ou identidade, terá opções. Leia mais sobre a [privacidade de dados da comunidade de desenvolvedores](https://docs.microsoft.com/visualstudio/ide/developer-community-privacy).

## <a name="next-steps"></a>Próximas etapas

Acesse a comunidade de [desenvolvedores do Visual Studio](https://developercommunity.visualstudio.com/) para relatar problemas, sugerir recursos ou navegar pelos tíquetes existentes. Aproveite!
