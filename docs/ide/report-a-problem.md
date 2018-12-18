---
title: 'Visão geral: relatar um problema no Visual Studio'
description: Fornece uma visão geral da ferramenta Relatar um problema e inclui estados e definições de problemas
ms.date: 11/15/2018
ms.prod: visual-studio-dev15
ms.technology: vs-acquisition
ms.topic: conceptual
author: seaniyer
ms.author: seiyer
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 56047150ce98cb6554248e43b7b8d7ff433cf283
ms.sourcegitcommit: 331dbb12e11fcd7f5d15fab05f3c861e48126e43
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51826668"
---
# <a name="overview-report-a-problem"></a>Visão geral: relatar um problema

A ferramenta Relatar um problema permite que a comunidade de desenvolvedores do Visual Studio envie problemas. Cada um dos seus relatórios do problema se torna um item de trabalho em nosso sistema de engenharia principal, capacitando você para interagir diretamente com nossas equipes de produtos para nos ajudar a identificar e a resolver problemas com impacto. Os comentários enviados com informações avançadas de diagnóstico são fundamentais para melhorar a família de produtos do Visual Studio. Nós realmente agradecemos seu tempo para relatar problemas.

Além disso, é possível votar nos comentários de outros membros da comunidade para trazer mais atenção a um problema e ajudar a corrigi-lo mais rapidamente.

## <a name="problem-status"></a>Status do problema

Depois de relatar um problema, os estados indicam onde seus envios estão no seu ciclo de vida. Enquanto as equipes da Microsoft examinam seus comentários, elas o definem com um estado adequado.  Acompanhe o andamento dos seus relatórios de problema referenciando os estados listados abaixo, juntamente com seu significado e indicadores de cor.

![Novo estado para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/New.jpg)

**Novo** indica que o bug ou problema foi recém-relatado e que nenhuma ação foi executada nele ainda.

- - -

![Estado triado para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/Triaged.jpg)

**Triado** indica que etapas preliminares como moderação, conversão e verificação inicial para que os duplicados sejam concluídos. O tíquete foi encaminhado para a equipe de engenharia adequada para consideração.

- - -

![Estado Em Questão para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/UnderConsideration.jpg)

**Em Questão** indica que a Microsoft está examinando seu problema quanto ao impacto da comunidade e o priorizará adequadamente. Se o impacto da comunidade ainda não estiver claro nem for significativo, continuaremos monitorando o problema nesse estado.

- - -

![Estado Sob Investigação para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/UnderInvestigation.jpg)

**Sob Investigação** indica que os engenheiros estão investigando ativamente seu problema para encontrar uma resolução.

- - -

![Estado Precisamos de Mais Informações para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/NeedMoreInfo.jpg)

**Precisamos de Mais Informações** indica que é necessário obter mais informações de diagnóstico antes de podermos ir adiante com a investigação.  [Saiba como responder a solicitações de Precisamos de Mais Informações.](./how-to-report-a-problem-with-visual-studio-2017.md#when-further-information-is-needed-need-more-info)

- - -

![Estado Corrigido – Lançamento Pendente para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/FixedPendingRelease.jpg)

**Corrigido – Lançamento Pendente** indica que temos uma correção para o problema e que ela estará disponível em uma versão prévia ou lançamento futuro.  Quando a correção for disponibilizada em uma versão prévia, o problema será marcado com "corrigido na" especificando a versão prévia.

- - -

![Estado Fechado – Corrigido para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedFixed.jpg) 

**Fechado – Corrigido** indica que lançamos uma correção para o problema. Agora o problema também é marcado com "corrigido na:" especificando a versão de lançamento.

- - -

![Estado Fechado – Duplicado para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedDuplicate.jpg)

**Fechado – Duplicado** indica que o problema já foi relatado por meio de outros comentários. Forneceremos o link em que você pode acompanhar a comunicação do problema original.

- - -

![Estado Fechado – Baixa Prioridade para comunicação de problema na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedLowerPriority.jpg)

**Fechado – Baixa Prioridade** Para concentrar-se em levar a cada um de vocês em nossa comunidade de desenvolvedores o melhor valor, priorizamos problemas com o mais alto impacto sobre o cliente. Embora não seja possível resolver esse problema específico neste momento, tenha certeza de que todos os seus comentários são valiosos e ajudam a melhorar o Visual Studio.

- - -

![Estado Fechado – Não é um Bug para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedNotaBug.jpg)

**Fechado – Não é um Bug** indica que determinamos que a funcionalidade relatada é atualmente esperada.

- - -

![Estado Fechado – Informações Não Suficientes para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedNotEnoughInfo.jpg)

**Fechado – Informações Insuficientes** indica que não temos informações suficientes para investigar isso para você. Será um prazer reconsiderar os comentários depois que as informações necessárias estiverem disponíveis.

- - -

![Estado Fechado – Outro Produto para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedOtherProduct.jpg)

**Fechado – Outro Produto** indica que determinamos que seu problema se aplica a outro produto. Confira o comentário da Microsoft para quais produtos e links relacionados.

- - -

![Estado Fechado – Não será Corrigido para comunicação de problemas na Comunidade de Desenvolvedores](../ide/media/ProblemStates/ClosedWontFix.jpg)

**Fechado – Não será Corrigido** indica que não estamos resolvendo esse problema devido a fatores como a falta de alinhamento de direção do produto ou do impacto na comunidade. Confira o comentário da Microsoft para maior clareza.  Embora não seja possível resolver esse problema específico, tenha certeza de que todos os seus comentários são valiosos e ajudam a melhorar o Visual Studio.

- - -

## <a name="faq"></a>Perguntas Frequentes

### <a name="how-can-i-increase-the-chance-of-my-problem-getting-resolved-quickly"></a>Como faço para aumentar a chance de o meu problema ser resolvido rapidamente?

É recomendável usar a pesquisa para garantir que o problema que você está prestes a relatar ainda não tenha sido comunicado. Se você encontrar um item existente que corresponda a seu problema, siga e vote nesse tíquete de problema.

 Forneça todas as informações que você tem para ajudar nossas equipes a reproduzir o que você está enfrentando.  Essas informações incluem etapas de reprodução necessárias, fragmentos de código, capturas de tela, gravações de reprodução, arquivos de log e outros artefatos.  Veja [como relatar um problema no Visual Studio](./how-to-report-a-problem-with-visual-studio-2017.md).

### <a name="how-is-my-feedback-prioritized"></a>Como meus comentários são priorizados?

Recebemos um grande número de problemas valiosos dos nossos clientes. Para garantir que estamos levando o melhor valor para cada um de vocês em nossa comunidade de desenvolvedores, priorizamos ações em comentários que têm o mais alto impacto na comunidade.

Se não conseguirmos responder pessoalmente seus comentários, saiba que agradecemos bastante sua colaboração. Tenha certeza de que seus comentários chegarão à equipe certa.

Nós valorizamos verdadeiramente seu tempo investido na melhoria do Visual Studio.

### <a name="what-actions-can-i-take-if-im-not-satisfied-with-the-resolution"></a>Quais medidas poderei tomar se não estiver satisfeito com a resolução?

Nossas equipes fazem seu melhor para diagnosticar e corrigir quaisquer problemas que você enfrentar; no entanto, pode haver situações em que você não esteja totalmente satisfeito com nossa recomendação. Comente novamente no comentário e nos informe exatamente com o que você não está satisfeito e tentaremos dar nosso melhor para garantir que atendamos às suas necessidades.

### <a name="how-will-i-get-notified-of-progress-on-my-feedback"></a>Como serei notificado do andamento do meu comentário?

As equipes de engenharia da Microsoft se comunicarão com você por meio do seu comentário no tíquete e da alteração do estado do seu tíquete à medida que progredirem. Fique atento a notificações por email que sejam enviadas quando o estado do tíquete for alterado ou quando um comentário for postado.  É possível gerenciar a frequência de notificações nas configurações do Perfil e Preferências no site da Comunidade de Desenvolvedores.

### <a name="why-cant-i-add-a-problem-for-visual-studio-ide-on-the-developer-community-website"></a>Por que não posso adicionar um problema ao IDE do Visual Studio no site da Comunidade de Desenvolvedores?

Relatar um problema por meio do Visual Studio permite que as informações de diagnóstico sejam automaticamente incluídas no relatório. São informações essenciais que fornecem aos nossos engenheiros o contexto de que eles precisam para entender completamente seu problema e para trabalhar para resolvê-lo.

Quando você comunica por meio do Visual Studio, pode compartilhar facilmente informações de diagnóstico avançadas conosco, como grandes arquivos de log, informações de falha, capturas de tela, gravações de reprodução e outros artefatos que nos ajudam a oferecer resoluções de maior qualidade com mais rapidez para você.