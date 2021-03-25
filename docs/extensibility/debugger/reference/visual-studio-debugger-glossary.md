---
title: Glossário do depurador do Visual Studio | Microsoft Docs
description: Este artigo explica vários termos usados no SDK de depuração do Visual Studio, como ponto de interrupção associado, causalidade e contexto de código.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- glossary [Debugging SDK]
- debugging [Debugging SDK], glossary
ms.assetid: 4a2cfaab-1fbd-4a23-bd00-9ac4cc50d7fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1871a395e87177c89f8af2bfce640a63c2cba324
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070681"
---
# <a name="visual-studio-debugger-glossary"></a>Glossário do depurador do Visual Studio
Veja a seguir os termos usados no [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] SDK de depuração.

## <a name="terms"></a>Termos
 ponto de interrupção associado uma abstração para um ponto de interrupção definido no código. Há uma relação um-para-um entre um ponto de interrupção associado e uma instrução de ponto de interrupção no fluxo de código. Quando o código é descarregado, os pontos de interrupção associados podem desassociar.

 o causalidade fornece a capacidade de controlar um thread lógico de execução em vários threads, processos e máquinas físicos e reconstruir a pilha de chamadas desse thread lógico em qualquer ponto no tempo de vida desse thread.

 o contexto de código fornece uma abstração de uma posição no código conhecida pelo mecanismo de depuração. Para a maioria das arquiteturas de tempo de execução, um contexto de código é um endereço no fluxo de instruções de um programa. Para linguagens não tradicionais, em que o código não pode ser representado por instruções, um contexto de código pode ser representado por outros meios.

 o caminho do código representa um ponto de execução no código em que um Branch é tirado ou uma chamada de função é feita. Um rastreamento de pilha é essencialmente uma lista de caminhos de código de chamada de função.

 mecanismo DE depuração (DE) um componente que permite a depuração de uma arquitetura de tempo de execução. Um mecanismo de depuração funciona em conjunto com o interpretador ou o sistema operacional e fornece serviços de depuração, como controle de execução, pontos de interrupção e avaliação de expressão.

 o contexto do documento fornece uma abstração de uma posição em um documento de arquivo de origem conhecido pelo mecanismo de depuração. Para a maioria dos idiomas, um contexto de documento é uma posição em um arquivo de origem. Para idiomas não tradicionais, para os quais o arquivo de origem pode não ser texto, um contexto de documento pode ser representado por outros meios. Consulte também *posição do documento*.

 a posição do documento fornece uma abstração de uma posição em um arquivo de origem conhecido pelo IDE. Para a maioria dos idiomas, uma posição de documento é uma posição em um arquivo de origem. Para idiomas não tradicionais, uma posição de documento pode ser representada de outras maneiras. Consulte também *contexto de documento*.

 erro de ponto de interrupção uma abstração para descrever um erro em um ponto de interrupção pendente. Um ponto de interrupção de erro pode descrever um erro no local do ponto de interrupção pendente, a expressão associada ao ponto de interrupção pendente ou outras informações que impedem que o ponto de interrupção pendente seja vinculado a um local de código.

 o contexto de avaliação fornece uma abstração de um contexto de programação para a avaliação da expressão. Normalmente, um contexto de avaliação é um escopo. Ao fazer a avaliação de expressão em um contexto de expressão, o contexto de expressão fornece regras de escopo que correspondem a seu ponto de criação. Por exemplo, um contexto de expressão criado em um quadro de pilha fornecerá o contexto para avaliar variáveis locais, parâmetros de método, membros de classe (se aplicável) e variáveis globais.

 exceção interceptada uma exceção que é interceptada por um mecanismo de depuração, mesmo que nenhum mecanismo de manipulação de exceção esteja em vigor no registro de ativação atual.

 JustMyCode o conceito de depuração apenas do código que pertence a um usuário e ignorando todo o código intermediário, como código do sistema, mesmo se o código-fonte estiver disponível para esse código do sistema.

 o ponto de interrupção pendente fornece uma abstração para pontos de interrupção antes, durante e após o código ser carregado e uma maneira de virtualizar pontos de interrupção. Um ponto de interrupção pendente:

- Contém todas as informações necessárias para associar um ponto de interrupção ao código em um ou mais programas.

- Pode associar a vários locais de código em um ou mais programas.

- Nunca se associa a código.

  Cada vez que o código é carregado, todos os pontos de interrupção pendentes em um programa são verificados para ver se eles podem se associar. Um ponto de interrupção pendente é dito para conter todos os pontos de interrupção associados que ele associa.

  processar um processo do Win32 físico. Um processo pode conter vários programas. Consulte também *programa*.

  programar um único namespace em execução dentro de uma arquitetura de tempo de execução específica. Consulte também *processar*.

  o SDM (Gerenciador de depuração de sessão) gerencia qualquer número de mecanismos de depuração Depurando qualquer número de programas em vários processos em qualquer número de computadores. No nível básico, o SDM é um multiplexador de mecanismos de depuração. Além disso, o SDM fornece uma exibição unificada da sessão de depuração para o IDE.

  o registro de ativação representa o estado de computação em um determinado quadro e um nível específico de chamadas de função aninhadas.

  Threade a noção generalizada da execução de instrução baseada em pilha em execução em pelo menos um programa.

  ponto de interrupção de aviso uma abstração para descrever um aviso em um ponto de interrupção pendente. Um ponto de interrupção de aviso descreve um motivo pelo qual o ponto de interrupção pendente ainda não está associado a um local de código. Isso pode ser que o código ainda não foi carregado para o local descrito pelo ponto de interrupção pendente ou por algum outro motivo.

## <a name="see-also"></a>Confira também
- [Extensibilidade do depurador do Visual Studio](../../../extensibility/debugger/visual-studio-debugger-extensibility.md)
