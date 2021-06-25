---
title: Ferramentas de avaliação para Visual Studio | Microsoft Docs
description: Use esta lista de verificação para avaliar a qualidade da experiência do usuário para Visual e detalhes de interação para novos recursos que você projeta para o Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 94e0e9a3-440c-4943-ad7b-772ed742e034
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: baee9f3e2eaefcd659f8428bd566711949d0fe90
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900753"
---
# <a name="evaluation-tools-for-visual-studio"></a>Ferramentas de avaliação para Visual Studio
## <a name="craftsmanship-checklist-for-visual-studio"></a>Lista de verificação do habilidade para Visual Studio
 Use esta lista de verificação para avaliar a qualidade da experiência do usuário para detalhes visuais e de interação.

### <a name="overview"></a>Visão geral

- Verifique se todos os comandos resultam em comentários que dizem aos usuários que seus comandos foram executados.

- Verifique se todos os elementos e controles da interface do usuário estão visíveis em todos os temas e no modo de Alto Contraste.

- Verifique se a seleção inativa e ativa sempre são diferenciadas, tanto no modo padrão quanto no Alto Contraste.

- Verifique se o foco está sempre visível e aparente.

### <a name="performance"></a>Desempenho

- Verifique se algum tipo de indicador "ocupado" é mostrado se um comando levar mais de um segundo para ser concluído.

- Verifique se um comando leva mais de 10 segundos para ser concluído, uma barra de progresso explícita, de desterminação (preferencial) ou indeterminada, é exibida.

### <a name="ui-text"></a>Texto da interface do usuário

- Verifique se todos os rótulos são de sentença ou de título e se nenhum texto está totalmente em minúsculas.

    ||Correto|Incorreto|
    |-|-------------|---------------|
    |**Texto do comando (All)**|Caso de sentença:<br /><br /> **Nome do diretório:**|Nome do diretório:|
    |**Texto do botão (cliente)**|Caso de título:<br /><br /> **[Definir como padrão]**|DEFINIR COMO PADRÃO|
    |**Texto do botão (online)**|Caso de sentença:<br /><br /> **[Definir como padrão]**||

- Verifique se todos os rótulos, exceto os cabeçalhos de grupo e os botões, terminam com dois-pontos e precedem o controle com o qual eles são emparelhados.

- Verifique se os botões, comandos e links de comando que iniciam a interface do usuário para capturar a entrada de usuários terminam em uma elipse **[...]**.

  Exemplos:

  - Um botão **[avançado...]** em uma caixa de diálogo.

  - As opções de comando no menu ferramentas (**ferramentas > opções**) não devem ter reticências, pois iniciar a própria caixa de diálogo é a intenção do comando.

- Verifique se a interface do usuário não contém abreviações, exceto os termos padrão do setor. Por exemplo, nem HTML nem TCP/IP precisam ser escritos, embora OOM (sem memória) e PII (informações de identificação pessoal) devam.

### <a name="keyboard-access"></a>Acesso pelo teclado

- Verifique se há uma maneira de realizar cada tarefa com o teclado. Em geral, isso é feito por meio do acesso de teclado para cada controle, mas para algumas áreas altamente visuais, uma solução alternativa, como ir para o modo de exibição de código, é aceitável.

- Verifique se você pode tabular os controles em uma ordem lógica (da esquerda para a direita e de cima para baixo). Embora essa seja uma prática recomendada para a maioria dos controles, nem todos os controles exigem essa abordagem. Por exemplo, verifique se os controles de botão de opção estão em um grupo com uma única parada de tabulação.

- Verifique se todos os controles têm rótulos e se cada rótulo tem um mnemônico (exceções incluem alguns controles não rotulados que podem seguir um controle rotulado na guia).

- Verifique se não há conflitos mnemônicos.

### <a name="fonts"></a>Fontes

- Verifique se todas as fontes (face, tamanho, cor) são usadas de forma consistente e mantenha a hierarquia.

- Verifique se todos os elementos da interface do usuário usam o serviço de fonte do ambiente. (Consulte [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md))

     Para verificar se o serviço está sendo usado, acesse **ferramentas > opções > fontes e cores**. No menu suspenso configurações, escolha fonte de ambiente e altere a face da fonte para algo de forma estilístico diferente (como Harrington ou Comic Sans) e defina o tamanho como 12 pt. Em seguida, clique em OK. Talvez seja necessário reiniciar o IDE, mas a maioria da interface do usuário será alterada imediatamente. As áreas que não pegam a alteração de fonte até mesmo na reinicialização não estão usando a fonte do ambiente.

- Verifique se as fontes que são derivadas do serviço (por exemplo, texto em negrito ou ampliado) mantêm seu tamanho e formatação em relação ao texto "normal" quando o tamanho da fonte do ambiente é alterado.

- Verifique se não há bugs de recorte devido a fontes ampliadas. As fontes que são recortadas são provavelmente o resultado de controles de altura fixa ou contêineres de altura fixa.

### <a name="dialogs"></a>Diálogos

- Verifique se o título da caixa de diálogo é igual ao comando que o iniciou.

- Verifique se todos os controles padrão são consistentes com o sistema operacional: a cor do plano de fundo é padrão e nenhum controle deve ter um estilo de remodelo especial que os torne uma aparência diferente dos controles padrão.

- Verifique se as margens dentro do formulário devem ser 12 pixels e se devem aparecer uniformes e consistentes.

- Verifique se as caixas de diálogo aparecem centralizadas no Shell do IDE ou na janela que as gerou.

- Quando útil, as caixas de diálogo devem ser redimensionáveis. Para caixas de diálogo que são redimensionáveis, verifique se, após o redimensionamento, os controles apropriados devem ser redimensionados enquanto outras partes da caixa de diálogo permanecem constantes.

- Verifique se as caixas de diálogo redimensionáveis mantêm qualquer tamanho ajustado pelo usuário (tamanho, local, expansão de controles de caixa de diálogo e assim por diante).

- Verifique se não há nenhum ícone na barra de título.

- Verifique se não há botões minimizar e maximizar na barra de título.

#### <a name="dialog-operation-buttons-vs-client-only"></a>Botões de operação da caixa de diálogo (somente no VS Client)

- Verifique se os botões de operação estão nesta ordem: **OK**, **Cancelar**, **aplicar**.

- Verifique se os botões **OK** e **Cancelar** são o tamanho padrão: 75x23 pixels.

- Verifique se os botões **OK** e **Cancelar** são de tamanho igual, independentemente do tamanho da cadeia de caracteres.

- Se o rótulo em um botão de operação exigir que o botão seja maior do que o padrão, verifique se o botão de **cancelamento** correspondente é de tamanho igual.

- Verifique se há um preenchimento de 6 pixels entre os botões e os controles associados.

- Verifique se os botões **OK** e **Cancelar** não têm mnemônicos (chaves de acesso definidas por uma letra sublinhada).

- Verifique se um botão (normalmente **OK**) tem foco por padrão.

- Verifique se **ESC** cancela a caixa de diálogo

- Verifique se **Enter** executa o botão padrão se o foco não estiver em um controle que processa.

- Verifique se os botões **OK** e **Cancelar** estão posicionados no canto inferior direito da caixa de diálogo. Em raras exceções, é aceitável que elas sejam empilhadas verticalmente no canto superior direito.

- Verifique se a configuração vertical é usada somente se outros botões estiverem em um alinhamento horizontal dentro da caixa de diálogo.

### <a name="control-standards"></a>Padrões de controle

#### <a name="general"></a>Geral

- Verifique se, quando possível, há bons valores padrão para acelerar a interação do usuário e direcionar os usuários para um resultado seguro ou comum.

- Verifique se os controles padrão se comportam da mesma forma para que os usuários saibam o que acontecerá com base na experiência anterior.

#### <a name="label-controls"></a>Controles de rótulo

- Verifique se cada controle tem um rótulo e se cada rótulo está visualmente emparelhado com seu controle (geralmente dentro de um intervalo de 4-6 pixels) e está mais próximo de seu controle correspondente do que a outros controles.

- Verifique se os rótulos estão posicionados à esquerda com a borda esquerda do controle, se posicionado acima e centralizado horizontalmente, para que a linha de base do rótulo seja alinhada com a linha de base do texto de entrada, se estiver posicionada à esquerda.

- Verifique se vários controles de rótulo e entrada empilhados estão posicionados à esquerda de um controle, se os rótulos são liberados para a esquerda e uma distância igual da borda da caixa de diálogo, nunca para a direita e uma distância igual dos controles. Os pares devem ser distribuídos uniformemente, a menos que precisem de espaçamento adicional para indicar o agrupamento.

#### <a name="input-controls-text-boxes-and-combo-boxes"></a>Controles de entrada (caixas de texto e caixas de combinação)

- Verifique se, ao usar a fonte de ambiente padrão, a altura de exibição para caixas de texto, caixas de combinação e botões são todos 23 pixels.

- Se o texto de dica for usado, verifique se a cor está definida como `Environment.ControlEditHintText` usando o serviço de cores.

- Se o campo for um campo obrigatório que deve ser identificado como tal, verifique:

  - Se o plano de fundo está definido como `Environment.ControlEditRequiredBackground` e o primeiro plano está definido como `Environment.ControlEditRequiredHintText`

  - que há texto de dica dentro do controle que aparece como **" \<Required> "**

#### <a name="button-controls"></a>Controles de botão

- Verifique se os botões são um tamanho mínimo de pixels de 75x23, a menos que haja mais texto.

- Verifique se os botões têm margens esquerda e direita de 3-5 pixels, bem como o preenchimento do conteúdo.

- É aceitável usar um pequeno botão quadrado com apenas uma elipse **[...]** nele, em vez de um botão **[procurar...]** (ou funcionalidade semelhante). Se usado, verifique se o botão tem 23x23 de tamanho.

- Se houver mais de um botão **[procurar...]** em uma caixa de diálogo, verifique se a versão reduzida (somente reticências **[...]**) é usada para todos.

- Verifique se os botões de reticências **[...]** não têm um mnemônico. Quando o foco está no controle de entrada ao lado, uma guia deve mover o foco para o botão de reticências.

- Verifique se os botões, comandos e links de comando que iniciam a interface do usuário secundária que captura mais entradas de usuários devem terminar com uma reticências **[...]**.

#### <a name="hyperlinks"></a>Hiperlinks

- Verifique se um controle HyperLink nunca pisca em vermelho quando ativo. Este é um indicador de que o serviço de cores não está sendo usado

- Verifique se as cores do VS usadas são:

  - `Environment.ControlLinkText`

  - `Environment.ControlLinkTextHover`

  - `Environment.ControlLinkTextPressed`

- Verifique se os hiperlinks aparecem azuis sem sublinhado, a menos que inserido em um parágrafo.

#### <a name="check-boxes"></a>Caixas de seleção

- Se uma caixa de seleção tiver texto de várias linhas, verifique se a caixa está alinhada com a primeira linha de texto, não centralizada verticalmente em todas as linhas.

- Verifique se as caixas de seleção sempre indicam uma opção binária e não navegam pelo usuário ou abrem novas janelas ou páginas.

- Se uma caixa de seleção apresentar uma opção relacionada a um controle de entrada, verifique se ela está posicionada em posição esquerda e muito próximo sob esse controle para indicar sua relação.

- Verifique se uma caixa de seleção **nunca** é usada como um meio de habilitar todo o conteúdo de um diálogo ou página.

#### <a name="group-boxes"></a>Caixas de grupo

- Verifique se um diálogo não contém uma única caixa de grupo dentro dele que contém todo o conteúdo do diálogo.

- Verifique se há pelo menos dois controles dentro de cada caixa de grupo.

- Raramente deve haver mais de duas caixas de grupo em uma caixa de diálogo.

- Verifique se não há caixas de grupo aninhadas.

### <a name="icons"></a>Ícones

- Verifique se os ícones aparecem corretamente invertidos quando estiver no tema escuro.

- Verifique se todos os ícones são baseados em conceitos principais.

- Verifique se cada ícone é distinto, fácil de reconhecer e não contém mais de dois conceitos (sem o modificador de status/idioma).

- Verifique se o ícone base aparece centralizado dentro do espaço.

- Verifique se todos os ícones aparecem legíveis no modo de Alto Contraste.

- Verifique se qualquer cor usada se alinha com os padrões de uso de cores.

- Verifique se não há halos (bordas) em torno de ícones. (Se presente, o Halo deve corresponder à cor do plano de fundo da interface do usuário adjacente).

### <a name="touch-enabled-ui"></a>Interface do usuário habilitada para toque

- Verifique se os controles interativos são grandes o suficiente para serem facilmente tocáveis-tamanho mínimo de **pixels de 23x23**

- Verifique se os controles usados com mais frequência têm pelo menos **40x40 pixels** de tamanho.

- Verificar se os controles interativos têm pelo menos **5 pixels de espaçamento** entre eles
