---
title: As ferramentas de avaliação para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 94e0e9a3-440c-4943-ad7b-772ed742e034
caps.latest.revision: 4
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4bf1f79cbba948f170849b6f9e89cb2421ceb9cf
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806237"
---
# <a name="evaluation-tools-for-visual-studio"></a>Ferramentas de avaliação para o Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="craftsmanship-checklist-for-visual-studio"></a>Lista de verificação de habilidade para Visual Studio  
 Use esta lista de verificação para avaliar a qualidade da experiência do usuário para obter detalhes de visual e interação.  
  
### <a name="overview"></a>Visão geral  
  
-   Verifique se todos os comandos resultam em comentários que informa aos usuários que os comandos foram realizados.  
  
-   Verifique se todos os elementos de interface do usuário e controles são visíveis em todos os temas e no modo de alto contraste.  
  
-   Verifique se que seleção inativa e ativa sempre são diferenciados, tanto no standard e o modo de alto contraste.  
  
-   Verifique se que o foco esteja sempre visível e aparente.  
  
### <a name="performance"></a>Desempenho  
  
-   Verifique se algum tipo de "ocupado" indicador é mostrado se um comando leva mais de um segundo para ser concluída.  
  
-   Verifique se um comando levar mais de 10 segundos para ser concluída, uma barra de progresso explícito seja determinada (preferencial) ou deixar indeterminada, é exibida.  
  
### <a name="ui-text"></a>Texto da interface do usuário  
  
-   Verificar se todos os rótulos são capitalização de título ou frase e que nenhum texto é totalmente em minúsculas.  
  
    ||Corrigir|Incorreto|  
    |-|-------------|---------------|  
    |**Texto do comando (tudo)**|Diferenciam maiusculas de minúsculas:<br /><br /> **Nome do diretório:**|Nome do diretório:|  
    |**Texto do botão (cliente)**|Capitalização de título:<br /><br /> **[Definir como padrão]**|DEFINIR COMO PADRÃO|  
    |**Texto do botão (online)**|Diferenciam maiusculas de minúsculas:<br /><br /> **[Definir como padrão]**||  
  
-   Verifique se todos os rótulos, exceto os cabeçalhos de grupo e botões, terminam com dois-pontos e precedem o controle com o qual eles estão emparelhados.  
  
-   Verifique se que os links de comando que inicie a interface do usuário para capturar a entrada do usuário, comandos e botões terminar com um sinal de reticências **[...]** .  
  
     Exemplos:  
  
    -   Um **[avançadas...]**  botão em uma caixa de diálogo.  
  
    -   As opções de comando no menu Ferramentas (**Ferramentas > Opções**) não deve obter um sinal de reticências, como iniciar a caixa de diálogo em si é a intenção do comando.  
  
-   Verifique se a interface do usuário não contém nenhum abreviações, exceto para os termos de padrão da indústria. Por exemplo, nem o HTML nem o TCP/IP precisa ser escrito, embora devem OOM (memória insuficiente) e a PII (informações de identificação pessoal).  
  
### <a name="keyboard-access"></a>Acesso pelo teclado  
  
-   Verifique se há uma maneira de realizar cada tarefa com o teclado. Geralmente, isso é feito por meio do acesso do teclado para cada controle, mas para algumas áreas altamente visuais, uma solução alternativa, como vai para a exibição de código é aceitável.  
  
-   Verifique se que você pode pressionar Tab por meio de controles em uma ordem lógica (esquerda para a direita e cima para baixo). Embora essa seja uma prática recomendada para a maioria dos controles, nem todos os controles exigem essa abordagem. Por exemplo, verifique se esse botão de opção controles estão em um grupo com uma única parada de tabulação.  
  
-   Verifique se todos os controles têm rótulos e que cada rótulo tem um mnemônico (as exceções incluem alguns controles não rotulados que podem vir após um controle identificado na guia).  
  
-   Verifique se que não haja nenhum conflito mnemônico.  
  
### <a name="fonts"></a>Fontes  
  
-   Verifique se todas as fontes (detecção facial, tamanho, cor) são usadas de forma consistente e mantêm a hierarquia.  
  
-   Verifique se todos os elementos de interface do usuário usam o serviço de fonte de ambiente. (Consulte [fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md))  
  
     Para verificar se o serviço está sendo usado, vá para **Ferramentas > Opções > fontes e cores**. Na lista suspensa de configurações, escolha a fonte de ambiente e alterar a face de fonte para algo estilística diferentes (como Souza ou revista em quadrinhos Sans) e defina o tamanho como 12 pt. Em seguida, clique em Okey. Talvez você precise reiniciar o IDE, mas a maioria de interface do usuário será alterado imediatamente. Áreas que não receba a alteração de fonte até mesmo na reinicialização não estiver usando a fonte de ambiente.  
  
-   Verifique se que as fontes que são derivados do serviço (por exemplo, texto em negrito ou ampliado) mantenham seu tamanho e a formatação em relação ao texto "normal", quando o tamanho da fonte de ambiente é alterado.  
  
-   Verifique se há bugs sem recorte devido a fontes ampliadas. Fontes que fique recortadas provavelmente são o resultado de controles de altura fixa ou contêineres de altura fixa.  
  
### <a name="dialogs"></a>Caixas de diálogo  
  
-   Verifique se o título da caixa de diálogo é o mesmo que o comando que o iniciou.  
  
-   Verifique se todos os controles padrão são consistentes com o sistema operacional: cor de plano de fundo é padrão e nenhum controle deve ter um estilo de re-modelo especial que os torna um aspecto diferente dos controles padrão.  
  
-   Verifique se as margens dentro do formulário devem ser 12 pixels e devem aparecer uniforme e consistente.  
  
-   Verifique se as caixas de diálogo aparecem centralizadas no shell do IDE ou na janela que é gerado-los.  
  
-   Quando for útil, caixas de diálogo devem ser redimensionáveis. Para caixas de diálogo que são redimensionáveis, verifique se que, após o redimensionamento, os controles apropriados devem redimensionar enquanto outras partes da caixa de diálogo permaneçam constantes.  
  
-   Verifique se que as caixas de diálogo redimensionáveis persistirem qualquer tamanho ajustado pelo usuário (tamanho, localização, expansão dos controles de caixa de diálogo e assim por diante).  
  
-   Verifique não se há nenhum ícone na barra de título.  
  
-   Verifique se que não há nenhum botões minimizar e maximizar na barra de título.  
  
#### <a name="dialog-operation-buttons-vs-client-only"></a>Botões de operação da caixa de diálogo (somente cliente do VS)  
  
-   Verifique se os botões de operação são nesta ordem: **Okey**, **Cancelar**, **aplicar**.  
  
-   Verifique **Okey** e **Cancelar** botões têm o tamanho padrão: 75 x 23 pixels.  
  
-   Verifique **Okey** e **Cancelar** botões são de tamanhos iguais, independentemente do comprimento da cadeia de caracteres.  
  
-   Se o rótulo em um botão de operação requer que o botão seja maior do que o padrão, verifique se que o correspondente **Cancelar** botão é de tamanho igual.  
  
-   Verifique se há um preenchimento de pixel 6 entre os botões e controles associados.  
  
-   Verifique se que o **Okey** e **Cancelar** botões não têm mnemônica (teclas de acesso definidas por uma letra sublinhada).  
  
-   Verifique se um botão (normalmente **Okey**) tem o foco por padrão.  
  
-   Verifique **Esc** cancela a caixa de diálogo  
  
-   Verifique **Enter** executa o botão padrão, se o foco não está em um controle que processa Enter.  
  
-   Verifique se que o **Okey** e **Cancelar** botões são posicionados no canto inferior direito da caixa de diálogo. Em raras exceções, é aceitável para que eles possam ser empilhadas verticalmente no canto superior direito.  
  
-   Verifique se a configuração vertical é usada somente se os outros botões estão em um alinhamento horizontal na caixa de diálogo.  
  
### <a name="control-standards"></a>Padrões de controle  
  
#### <a name="general"></a>Geral  
  
-   Verifique se que, quando possível, existem bons valores padrão para acelerar a interação do usuário e direcionar os usuários em direção a um resultado de seguro ou comuns.  
  
-   Verifique se os controles padrão se comportam da mesma maneira para que os usuários saibam o que acontecerá com base na experiência anterior.  
  
#### <a name="label-controls"></a>Controles de rótulo  
  
-   Verifique se que cada controle tem um rótulo e que cada rótulo visualmente é emparelhado com o seu controle (geralmente dentro de um intervalo de pixel de 4 a 6) e é mais próximo ao seu controle correspondente que para outros controles.  
  
-   Verifique se que os rótulos são posicionados liberação esquerda com o controle de borda esquerda se posicionada acima e centralizada horizontalmente, para que a linha de base do rótulo é alinhada com a linha de base de texto de entrada se posicionado à esquerda.  
  
-   Verifique se que, se vários rótulo empilhado e controles de entrada são posicionados à esquerda de um controle, os rótulos de recuo estão à esquerda e uma distância igual entre a borda da caixa de diálogo, nunca liberar o direito e uma distância igual dos controles. Pares devem ser distribuídos uniformemente, a menos que eles precisam espaçamento adicional para indicar o agrupamento.  
  
#### <a name="input-controls-text-boxes-and-combo-boxes"></a>Controles de entrada (caixas de texto e caixas de combinação)  
  
-   Verifique se que, ao usar a fonte de ambiente padrão, a altura de exibição para as caixas de texto, caixas de combinação e botões são todos os 23 pixels.  
  
-   Se o texto de dica é usado, verifique se que a cor é definida como `Environment.ControlEditHintText` usando o serviço de cor.  
  
-   Se o campo é um campo obrigatório que deve ser identificado como tal, verifique se:  
  
    -   o plano de fundo definido como `Environment.ControlEditRequiredBackground` e primeiro plano é definido como `Environment.ControlEditRequiredHintText`  
  
    -   há texto de dica no controle que aparece como **"\<necessárias >"**  
  
#### <a name="button-controls"></a>Controles de botão  
  
-   Verifique se botões são um tamanho mínimo de 75 x 23 pixels, a menos que acomodar mais texto.  
  
-   Verificar se os botões tem deixado e margens de 3 a 5 pixels, como também o preenchimento para o conteúdo do botão direito do mouse.  
  
-   É aceitável usar um botão quadrado pequeno com apenas uma elipse **[...]**  nele, em vez de um **[procurar...]**  botão (ou uma funcionalidade semelhante). Se usado, verifique se que o botão é 23 x 23 de tamanho.  
  
-   Se houver mais de um **[procurar...]**  botão em uma caixa de diálogo e, em seguida, verifique a versão abreviada (somente reticências **[...]** ) é usada para todos.  
  
-   Verifique se esse botão de reticências **[...]**  botões não têm um mnemônico. Quando o foco estiver no controle de entrada ao lado dela, uma guia deve mover o foco para o botão de reticências.  
  
-   Verifique se que botões, comandos e links de comando que inicie a interface de usuário secundário que captura a entrada de usuário mais deve terminar com um sinal de reticências **[...]** .  
  
#### <a name="hyperlinks"></a>Hiperlinks  
  
-   Verifique se que um controle de hiperlink nunca pisca em vermelho quando ativo. Este é um indicador de que o serviço de cor não está sendo usada  
  
-   Verifique se as cores do VS usadas são:  
  
    -   `Environment.ControlLinkText`  
  
    -   `Environment.ControlLinkTextHover`  
  
    -   `Environment.ControlLinkTextPressed`  
  
-   Verifique se que hiperlinks aparecem em azuis com nenhum sublinhado, a menos que o inserido em um parágrafo.  
  
#### <a name="check-boxes"></a>Caixas de seleção  
  
-   Se uma caixa de seleção tem o texto de várias linhas, verifique se que a caixa se alinha com a primeira linha de texto, não centralizado verticalmente em todas as linhas.  
  
-   Verifique se as caixas de seleção sempre indicam uma escolha binária e não navegue o usuário ou abrir novas janelas ou páginas.  
  
-   Se uma caixa de seleção apresenta uma opção relacionada a um controle de entrada, verifique se ele está posicionado recuo à esquerda e muito próximos sob esse controle para indicar sua relação.  
  
-   Verifique se é uma caixa de seleção **nunca** usado como um meio para permitir todo o conteúdo de uma caixa de diálogo ou página.  
  
#### <a name="group-boxes"></a>Caixas de grupo  
  
-   Verifique se que uma caixa de diálogo não contém uma caixa de grupo único dentro dele que contém todo o conteúdo da caixa de diálogo.  
  
-   Verifique se há pelo menos dois controles dentro de cada caixa de grupo.  
  
-   Raramente deve haver mais de duas caixas de grupo em uma caixa de diálogo.  
  
-   Verifique se que não há nenhuma caixa de grupo aninhado.  
  
### <a name="icons"></a>Ícones  
  
-   Verifique se os ícones aparecem invertidos corretamente quando no tema escuro.  
  
-   Verifique se que todos os ícones são baseados em conceitos básicos.  
  
-   Verifique se cada ícone é distinta, fácil de reconhecer e não contém mais de dois conceitos (sem o modificador de status/idioma).  
  
-   Verifique se o ícone de base aparece centralizado dentro do espaço.  
  
-   Verifique se todos os ícones aparecem legíveis no modo de alto contraste.  
  
-   Verifique se que qualquer cor usada se alinha com padrões de uso de cores.  
  
-   Verifique se que não há nenhum halos (bordas) em torno de ícones. (Se estiver presente, o halo deve corresponder a cor do plano de fundo da interface do usuário adjacente).  
  
### <a name="touch-enabled-ui"></a>Interface do usuário habilitado para toque  
  
-   Verificar se os controles interativos são grandes o suficiente para ser facilmente touchable – mínima **23 x 23 pixels** de tamanho  
  
-   Verifique se os controles usados com mais frequência são pelo menos **40 x 40 pixels** de tamanho.  
  
-   Verifique se tem pelo menos de controles interativos **5 pixels de espaçamento** entre eles

