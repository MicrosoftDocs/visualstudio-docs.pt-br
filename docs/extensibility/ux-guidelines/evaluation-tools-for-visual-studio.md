---
title: Ferramentas de avaliação para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 94e0e9a3-440c-4943-ad7b-772ed742e034
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6a149d9163e61dd49105f123b373ecd9c7c1c278
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31147327"
---
# <a name="evaluation-tools-for-visual-studio"></a>Ferramentas de avaliação do Visual Studio
## <a name="craftsmanship-checklist-for-visual-studio"></a>Lista de verificação de habilidade para Visual Studio  
 Use esta lista de verificação para avaliar a qualidade de experiência do usuário para obter detalhes do visual e interação.  
  
### <a name="overview"></a>Visão geral  
  
-   Verifique se todos os comandos resultam em comentários que informa aos usuários que os comandos foram realizados.  
  
-   Verifique se todos os elementos de interface do usuário e os controles são visíveis em todos os temas em modo de alto contraste.  
  
-   Verifique se que seleção inativa e ativa sempre são diferenciados, tanto em modo de alto contraste e padrão.  
  
-   Verifique se que o foco está sempre visível e aparente.  
  
### <a name="performance"></a>Desempenho  
  
-   Verifique se algum tipo de "ocupado" indicador é mostrado se um comando tem mais de um segundo para concluir.  
  
-   Verifique se um comando levar mais de 10 segundos para ser concluída, uma barra de progresso explícita, ou determinada (preferencial) ou indeterminado, é exibida.  
  
### <a name="ui-text"></a>Texto de interface do usuário  
  
-   Verifique se todos os rótulos são capitalização de frase ou de título e que nenhum texto é totalmente em minúsculas.  
  
    ||Corrigir|Incorreto|  
    |-|-------------|---------------|  
    |**Texto do comando (todos)**|Caso a frase:<br /><br /> **Nome do diretório:**|Nome do diretório:|  
    |**Texto do botão (cliente)**|Capitalização de título:<br /><br /> **[Definir como padrão]**|DEFINIR COMO PADRÃO|  
    |**Texto do botão (online)**|Caso a frase:<br /><br /> **[Definir como padrão]**||  
  
-   Verifique se todos os rótulos, exceto os cabeçalhos de grupo e os botões, terminam com dois-pontos e precedem o controle com a qual eles são combinados.  
  
-   Verifique se os links de comando que iniciar a interface do usuário para capturar a entrada do usuário, comandos e botões terminar em um botão de reticências **[...]** .  
  
     Exemplos:  
  
    -   Um **[Avançado...]**  botão em uma caixa de diálogo.  
  
    -   As opções de comando do menu Ferramentas (**Ferramentas > Opções**) não deve receber uma elipse, como iniciar a caixa de diálogo em si é a intenção do comando.  
  
-   Verifique se a interface do usuário não contém nenhum abreviações, exceto para os termos de padrão industrial. Por exemplo, HTML, nem TCP/IP precisa ser digitado, embora OOM (memória insuficiente) e PII (informações de identificação pessoal) devem.  
  
### <a name="keyboard-access"></a>Acesso pelo teclado  
  
-   Verifique se há uma maneira de executar cada tarefa com o teclado. Geralmente isso é feito por meio do acesso de teclado para cada controle, mas algumas áreas altamente visuais, uma alternativa como ir para modo de exibição de código é aceitável.  
  
-   Verifique se que você pode percorrer os controles em uma ordem lógica (esquerda para a direita e cima para baixo). Embora essa seja uma prática recomendada para a maioria dos controles, nem todos os controles exigem essa abordagem. Por exemplo, verifique se esse botão de opção são controles em um grupo com uma única parada de tabulação.  
  
-   Verifique se todos os controles com rótulos e cada rótulo tem um mnemônico (exceções incluem alguns controles de rótulo não podem seguir um controle identificado na guia).  
  
-   Verifique se que não haja nenhum conflito mnemônico.  
  
### <a name="fonts"></a>Fontes  
  
-   Verifique se todas as fontes (face, tamanho, cor) são usadas de forma consistente e mantêm a hierarquia.  
  
-   Verifique se todos os elementos de interface de usuário usam o serviço de fonte de ambiente. (Consulte [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md))  
  
     Para verificar se o serviço está sendo usado, vá para **Ferramentas > Opções > fontes e cores**. Na lista suspensa de configurações, escolha a fonte de ambiente e alterar o tipo de fonte para algo diferente stylistically (como Souza ou Cartum Sans) e defina o tamanho para 12 pt. Em seguida, clique em Okey. Talvez seja necessário reiniciar o IDE, mas a maioria de interface do usuário será alterado imediatamente. Áreas não acompanhar a alteração da fonte mesmo na reinicialização não estiver usando a fonte de ambiente.  
  
-   Verifique se que as fontes que são derivados do serviço (por exemplo, texto em negrito ou ampliado) mantenham o tamanho e a formatação em relação ao texto "normal" quando o tamanho da fonte de ambiente é alterado.  
  
-   Verifique se não há nenhum erro de recorte devido a fontes ampliados. As fontes que sejam recortadas provavelmente são o resultado de controles de altura fixa ou contêineres de altura fixa.  
  
### <a name="dialogs"></a>Caixas de diálogo  
  
-   Verifique se o título da caixa de diálogo é o mesmo que o comando que o iniciou.  
  
-   Verifique se todos os controles padrão são consistentes com o sistema operacional: cor de plano de fundo é o padrão e controles não deve ter um estilo de re-modelo especial que faz com que um aspecto diferente dos controles padrão.  
  
-   Verifique se as margens dentro do formulário devem ser 12 pixels e devem aparecer consistente e uniforme.  
  
-   Verifique se as caixas de diálogo aparecem centralizadas no shell do IDE ou a janela que gerou-los.  
  
-   Quando útil, caixas de diálogo devem ser redimensionadas. Para caixas de diálogo que são redimensionáveis, verifique se que, após o redimensionamento, os controles apropriados devem redimensionar enquanto outras partes da caixa de diálogo permanecem constantes.  
  
-   Verifique se as caixas de diálogo redimensionáveis manter qualquer tamanho ajustada pelo usuário (tamanho, localização, expansão de controles de caixa de diálogo e assim por diante).  
  
-   Verifique se não há nenhum ícone na barra de título.  
  
-   Verifique se há sem minimizar e maximizar botões na barra de título.  
  
#### <a name="dialog-operation-buttons-vs-client-only"></a>Botões de operação da caixa de diálogo (VS cliente somente)  
  
-   Verifique se estão operação botões nesta ordem: **Okey**, **Cancelar**, **aplicar**.  
  
-   Verifique **Okey** e **Cancelar** botões são o tamanho padrão: 23 x 75 pixels.  
  
-   Verifique **Okey** e **Cancelar** botões são de tamanho igual, independentemente do comprimento de cadeia de caracteres.  
  
-   Se o rótulo em um botão de operação exige que o botão seja maior do que o padrão, verifique se que o correspondente **Cancelar** botão é de tamanho igual.  
  
-   Verifique se há um preenchimento de pixel 6 entre botões e controles associados.  
  
-   Verifique o **Okey** e **Cancelar** botões não possuem mnemônico (chaves de acesso definidas por uma letra sublinhada).  
  
-   Verifique se um botão (normalmente **Okey**) tem foco por padrão.  
  
-   Verifique **Esc** cancela a caixa de diálogo  
  
-   Verifique **Enter** executa o botão padrão se o foco não está em um controle que processa Enter.  
  
-   Verifique o **Okey** e **Cancelar** botões são posicionados no canto inferior direito da caixa de diálogo. Em raras exceções, é aceitável para que eles possam ser empilhadas verticalmente no canto superior direito.  
  
-   Verifique se a configuração vertical é usada somente se tiver outros botões em um alinhamento horizontal a caixa de diálogo.  
  
### <a name="control-standards"></a>Padrões de controle  
  
#### <a name="general"></a>Geral  
  
-   Verifique se, quando possível, há valores padrão para acelerar a interação do usuário e direcionar os usuários para obter um resultado de seguro ou comuns.  
  
-   Verifique se controles padrão se comportam da mesma maneira para que os usuários saibam o que acontece com base na experiência anterior.  
  
#### <a name="label-controls"></a>Controles de rótulo  
  
-   Verifique se cada controle tem um rótulo e que cada rótulo visualmente é emparelhado com seu controle (geralmente dentro de um intervalo de pixel de 4 a 6) e é mais perto de seu controle correspondente que para outros controles.  
  
-   Verifique se que os rótulos são posicionados liberação esquerda com o controle extremidade esquerda se posicionada acima e centralizada horizontalmente, para que a linha de base do rótulo é alinhada com a linha de base de texto de entrada se posicionado à esquerda.  
  
-   Verificar se vários rótulo empilhado e controles de entrada são posicionados à esquerda de um controle, os rótulos são deixados liberação e por uma distância da borda da caixa de diálogo, nunca liberar direita e dos controles a uma distância igual. Pares devem ser distribuídos uniformemente, a menos que precisam de espaçamento adicional para indicar o agrupamento.  
  
#### <a name="input-controls-text-boxes-and-combo-boxes"></a>Controles de entrada (caixas de texto e caixas de combinação)  
  
-   Verifique se que, ao usar a fonte padrão do ambiente, a altura de exibição para as caixas de texto, caixas de combinação e botões são todos os 23 pixels.  
  
-   Se o texto de dica for usado, verifique se que a cor é definida como `Environment.ControlEditHintText` usando o serviço de cor.  
  
-   Se o campo é um campo obrigatório que deve ser identificado como tal, verifique se:  
  
    -   o plano de fundo definido como `Environment.ControlEditRequiredBackground` e o primeiro plano é definido como `Environment.ControlEditRequiredHintText`  
  
    -   há texto de dica dentro do controle que é exibido como **"\<necessário >"**  
  
#### <a name="button-controls"></a>Controles de botão  
  
-   Verifique se botões um tamanho mínimo de 75 x 23 pixels, a menos que acomodar mais texto.  
  
-   Verifique se que botões têm esquerda e direita as margens de 3 a 5 pixels, bem como preenchimento para o conteúdo.  
  
-   É aceitável para usar um pequeno botão quadrado com apenas um botão de reticências **[...]**  nela em vez de um **[procurar...]**  botão (ou uma funcionalidade semelhante). Se usado, verifique se o botão 23 x 23 de tamanho.  
  
-   Se houver mais de um **[procurar...]**  botão em uma caixa de diálogo e, em seguida, verifique a versão abreviada (somente reticências **[...]** ) é usado para todos.  
  
-   Verifique se esse botão de reticências **[...]**  botões não têm um mnemônico. Quando o foco estiver no controle de entrada ao lado dela, uma guia deve mover o foco para o botão de reticências.  
  
-   Verifique se que os links de comando que iniciar interface secundária que captura as entradas de usuário, comandos e botões deve terminar em um botão de reticências **[...]** .  
  
#### <a name="hyperlinks"></a>Hiperlinks  
  
-   Verifique se que um controle de hiperlink nunca pisca em vermelho quando ativo. Este é um indicador de que o serviço de cor não está sendo usada  
  
-   Verifique se as cores do VS usadas são:  
  
    -   `Environment.ControlLinkText`  
  
    -   `Environment.ControlLinkTextHover`  
  
    -   `Environment.ControlLinkTextPressed`  
  
-   Verifique se os hiperlinks aparecem azuis com nenhuma sublinhado, a menos que inserido em um parágrafo.  
  
#### <a name="check-boxes"></a>Caixas de seleção  
  
-   Se uma caixa de seleção tem o texto de várias linhas, verifique se que a caixa esteja alinhada com a primeira linha de texto, não centralizado verticalmente em todas as linhas.  
  
-   Verifique se caixas de seleção sempre indicam uma escolha binária e não leve o usuário ou abrir novas janelas ou páginas.  
  
-   Se uma caixa de seleção apresenta uma opção relacionada a um controle de entrada, verifique se que é posicionado liberação à esquerda e quase sob controle para indicar sua relação.  
  
-   Verifique se a caixa de seleção é **nunca** usado como um meio para permitir todo o conteúdo de uma caixa de diálogo ou página.  
  
#### <a name="group-boxes"></a>Caixas de grupo  
  
-   Verifique se uma caixa de diálogo não tem uma caixa de grupo único dentro dele que contém todo o conteúdo da caixa de diálogo.  
  
-   Verifique se há pelo menos dois controles em cada caixa de grupo.  
  
-   Raramente deve haver mais de duas caixas de grupo em uma caixa de diálogo.  
  
-   Verifique se não há nenhuma caixa de grupo aninhado.  
  
### <a name="icons"></a>Ícones  
  
-   Verifique se ícones aparecem corretamente invertidos no tema escuro.  
  
-   Verifique se que todos os ícones são baseados em conceitos básicos.  
  
-   Verifique se cada ícone é distinta, fácil de reconhecer e não tem mais de dois conceitos (sem modificador status/language).  
  
-   Verifique se o ícone de base aparece centralizado dentro do espaço.  
  
-   Verifique se todos os ícones aparecem legíveis no modo de alto contraste.  
  
-   Verifique se que todas as cores usadas esteja alinhada com os padrões de uso de cor.  
  
-   Verifique se não há nenhum halos (bordas) em torno de ícones. (Se presente, o halo deve corresponder a cor de plano de fundo da interface do usuário adjacente).  
  
### <a name="touch-enabled-ui"></a>Interface do usuário sensíveis ao toque  
  
-   Verifique se controles interativos são grandes o suficiente para ser facilmente touchable - mínimo **23 x 23 pixels** no tamanho  
  
-   Verifique se os controles usados com mais frequência são pelo menos **40 x 40 pixels** em tamanho.  
  
-   Verifique se controles interativos tem pelo menos **5 pixels de espaçamento** entre eles