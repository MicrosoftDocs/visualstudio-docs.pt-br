---
title: Texto da interface do usuário e a Ajuda do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 52260b2cd401f8cdbd3a94704ab29db2f64fdc6d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49842229"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Texto da interface do usuário e a Ajuda do Visual Studio
##  <a name="BKMK_UITextAndTerminology"></a> Terminologia e o texto de interface do usuário  
 Texto compreensível é crucial para a interface de usuário efetivada. Os usuários de software tendem a leitura de rótulos em primeiro lugar, ou seja, aqueles mais relevantes para concluir a tarefa em questão. Texto estático é lido com menos frequência. Plano para os usuários iniciar suas sessões de trabalho com uma verificação rápida de toda a janela, seguida por uma leitura da interface do usuário nesta ordem aproximado:  
  
1.  Controles interativos no Centro  
  
2.  Botões de confirmação  
  
3.  Controles interativos encontrados em outro lugar  
  
4.  Instruções principais  
  
5.  Explicações complementares  
  
6.  Título da janela  
  
7.  Outro texto estático no corpo principal  
  
### <a name="usage-patterns-for-ui-text"></a>Padrões de uso para o texto da interface do usuário  
  
#### <a name="title-bar-text"></a>Texto da barra de título  
 Texto da barra de título deve corresponder o comando que é gerado a interface do usuário.  
  
#### <a name="instructional-text-helper-text"></a>Texto de instrução (texto auxiliar)  
 Algumas caixas de diálogo, é útil fornecer instruções principais proeminentes para explicar o que fazer na janela ou na página. Às vezes, isso é conhecido como "texto auxiliar".  
  
##### <a name="writing-style-rules-for-helper-text"></a>Escrever regras de estilo para o texto do auxiliar  
  
-   Não explicam o óbvio. A menos que seja absolutamente necessário, não inclua texto de instrução.  
  
-   Texto de instrução sempre é colocado na parte superior da caixa de diálogo e deve se referir à tarefa que está sendo executada.  
  
-   Precisamente explica aos usuários o que precisam. Evite a redundância e a comunicação excessiva.  
  
-   Examine cada janela e eliminar as instruções e palavras duplicadas.  
  
-   Mantenha o texto de instrução curto. Se saber é necessário para determinados usuários ou cenários, em seguida, forneça um link para um tópico de online conceitual detalhado.  
  
-   Escreva o texto para que contém o peso de cada palavra e é necessária.  
  
-   Siga as diretrizes da Microsoft existente para [texto de Interface do usuário](/windows/desktop/uxguide/text-ui) e [estilo e tom](/windows/desktop/uxguide/text-style-tone).  
  
#### <a name="supplemental-instructions"></a>Instruções complementares  
 Instruções complementares fornecem informações adicionais que ajuda o usuário a entender os controles ou agrupamentos de controle. Isso também pode incluir texto de dica necessário para compreender qual formato o controle de entrada está esperando. Use instruções complementares com moderação. Reservá-los para casos em que é provável que o usuário não compreenda totalmente as implicações da opção que eles estão fazendo.  
  
 ![Texto suplementar no Visual Studio](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "b_SupplementalText1 0601")  
  
 **Texto suplementar no Visual Studio**  
  
 ![Texto suplementar no Visual Studio](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "c_SupplementalText2 0601")  
  
 **Texto suplementar no Visual Studio**  
  
#### <a name="infotips"></a>InfoTips  
 Muitas vezes, o texto de instrução pode ser muito demorado para posicionar no local na interface do usuário ou pode ser útil somente para novos usuários, pareçam resíduos para usuários experientes. Nesse caso, o texto das instruções informativas deve ser colocado como uma dica de ferramenta em uma InfoDica.  
  
 InfoTips deve ser colocado perto os controles que eles estão relacionados e devem usar o ícone de InfoDica específico, que é discreto ainda notável.  
  
 ![InfoDica no Visual Studio](../../extensibility/ux-guidelines/media/0601-d_infotip.png "d_InfoTip 0601")  
  
 **Exemplo de uma InfoDica no Visual Studio**  
  
##### <a name="writing-style-rules-for-infotips"></a>Regras de estilo de escrita para InfoTips  
  
-   Grave InfoTips como frases completas. Eles exigem a verbos específicos, diferenciam maiusculas de minúsculas e pontuação final.  
  
-   Use InfoTips para complementar sua instrução principal ou informações. Se você estiver usando apenas palavras diferentes para declarar novamente a ideia principal, não será necessário uma InfoDica.  
  
-   Manter InfoTips curto e bonito. Use palavras pequenas e sem formatação, linguagem cotidiana que dá suporte e incentivo para o usuário.  
  
-   Siga as diretrizes da Microsoft existente para [texto de Interface do usuário](/windows/desktop/uxguide/text-ui) e [estilo e tom](/windows/desktop/uxguide/text-style-tone).  
  
#### <a name="control-labels"></a>Rótulos de controle  
 Rótulos de controle devem ser curta e concisa e siga as [diretrizes de área de trabalho do Windows para controles](/windows/desktop/uxguide/controls).  
  
 Para obter mais informações sobre o formato do rótulo de controle e o posicionamento dentro da interface do usuário, consulte [Layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).  
  
#### <a name="help-links"></a>Links de ajuda  
 Links de Ajuda pode ser posicionado dentro do texto de instrução ou no corpo da interface do usuário. Eles podem ser links de Ajuda ou abrem caixas de diálogo internas.  
  
##### <a name="visual-style-rules-for-help-links"></a>Regras de estilo visual para links de ajuda  
  
-   Use as cores de ambiente correta de hiperlinks. Um hiperlink corretamente com estilo não piscará brevemente vermelho quando clicado. Se você vir isso, é uma indicação de que as cores de ambiente não estão sendo usadas.  
  
-   Sublinhados só devem ser usados em foco ou quando o link é incorporado em um parágrafo.  
  
-   Para obter mais informações sobre estilos visuais e interação de hiperlinks, consulte botões e hiperlinks.  
  
##### <a name="writing-style-rules-for-help-links"></a>Regras de estilo de escrita para links de ajuda  
  
-   Ao iniciar as caixas de diálogo, manter os padrões para elipses: nenhum botão de reticências de navegação, elipses, se a tarefa requer adicional da interface do usuário.  
  
     ![Link de Ajuda no Visual Studio](../../extensibility/ux-guidelines/media/0601-e_helplink.png "e_HelpLink 0601")  
  
     **Um sinal de reticências (...) em um link de ajuda indica que a tarefa exigirá adicional da interface do usuário.**  
  
-   Links não deve começar com "Saiba", isso não é a intenção do usuário. O usuário deseja responder uma pergunta específica, não receberá uma educação geral.  
  
-   Links de ajuda de frase, de modo que eles a pergunta que o tópico responderá.  
  
     Incorreto:  
     "Saiba mais sobre os preços de serviços móveis do Windows Azure"  
  
     Corrigi:  
     "Quais opções de preços estão disponíveis para serviços móveis do Windows Azure?"  
  
-   Nunca use *clique em...*  para o texto do link.  
  
-   Nunca vincular apenas a palavra "aqui". Isso é problemático para alguns leitores de tela, que serão de voz apenas a palavra com hiperlink.  
  
     Incorreto:  
     "Para obter informações sobre serviços móveis do Windows Azure **aqui**"  
  
     Corrigi:  
     "Quais opções de preços estão disponíveis para serviços móveis do Windows Azure?"  
  
-   Para obter mais informações sobre o estilo de escrita correto para links de Ajuda, consulte o [diretrizes de área de trabalho do Windows para obter ajuda](/windows/desktop/uxguide/winenv-help).  
  
#### <a name="hint-text"></a>Texto de dica  
 Texto de dica é exibido como uma marca d'água em um controle ou abaixo do controle. A formatação correta será aplicada usando o token VSColors apropriado, `Environment.GrayText`.  
  
 Ele pode aparecer em um número de formulários.  
  
-   Em vez do rótulo de controle:  
  
     ![Dica de texto no Visual Studio](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "f_HintText1 0601")  
  
-   Com um verbo, fornecendo instruções:  
  
     ![Dica de texto no Visual Studio](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "g_HintText2 0601")  
  
-   Com o texto que indica uma entrada necessária:  
  
     ![Dica de texto no Visual Studio](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "h_HintText3 0601")  
  
#### <a name="watermark-text"></a>Texto de marca d'água  
 Em uma superfície de design vazio, o texto deve indicar o que fazer, bem como fornecem links para abrir outras janelas relacionadas, se apropriado:  
  
 ![Texto do Visual Studio de marca d'água](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "i_WatermarkText 0601")  
  
 **Exemplo de texto de marca d'água no Visual Studio**  
  
### <a name="common-terminology"></a>Terminologia comum  
  
|Termo|Explicação|Comentário|  
|----------|-----------------|-------------|  
|Entrar / sair|Verbos usados como sinônimos com a web para a representação de autenticação em uma propriedade da web. Dentro de clientes, nós usamos isso vez como uma noção de nível superior para a assinatura dentro e fora de conexão de usuário do IDE, que representa uma identidade de nível superior que fornece recursos de nível mais altos, como o roaming e licenciamento que não estão disponíveis com todas as outras conexões.|O usuário do IDE é o único recurso que deve representar uma entrada / sair verbo, porque ele representa o usuário do IDE de nível superior.|  
|Conectar / desconectar|Use em lugares onde um recurso mantém uma única conexão a um serviço online.|Gerenciador de servidores, onde você pode ter apenas uma conexão do Azure Active Directory por vez, é um exemplo de como conectar/desconectar.|  
|Adicionar / remover|Não-destrutiva. Use quando estiver adicionando ou removendo algo em uma lista.|A caixa de diálogo de lista de servidores do Gerenciador de Conexão do TFS é um exemplo de como adicionar ou remover.|  
|Excluir|Destrutiva. Use somente quando o elemento que está sendo removido será permanentemente descartado ou excluído do disco.|Geralmente requer um prompt de "Excluir" se o resultado é excluir um arquivo de disco.|  
  
## <a name="error-messages"></a>Mensagens de erro  
  
### <a name="overview"></a>Visão geral  
 Erros acontecem. Definindo as limitações em que o usuário pode fazer é uma primeira etapa sensata impedindo que mensagens de erro podem ser evitados. No entanto, quando ocorre um erro, uma mensagem de erro bem escrito pode percorrem um longo caminho em direção a atenuar o problema. Mensagens de erro são possivelmente um dos tipos mais importantes de notificação de que o usuário vê, porque eles são síncronos e indicam um problema que precisa ser resolvido. Mensagens de erro mal-escrito deixarem os usuários sobre suas próprias para decidir a causa dos erros e quaisquer possíveis soluções.  
  
 Os usuários podem parar prestando atenção para o uso excessivo ou confuso mensagens de erro, portanto, a experiência de gravação de mensagens somente é necessário que adicionam valor ao usuário. Se a mensagem é simplesmente uma notificação, em seguida, use uma apresentação alternativa.  
  
### <a name="rules-for-creating-an-error-message"></a>Regras para criar uma mensagem de erro  
  
-   Ao construir mensagens de erro, escolha o nível de erro apropriada para o público-alvo. Tenha como objetivo resumos simples que fornecem uma ação que o usuário pode executar, se aplicável. Não o estado de qualquer coisa que o usuário não precisa saber.  
  
-   Fornece assistência construtivo. É mais fácil de ler e agir em uma mensagem de erro que contém a instrução.  
  
-   Não use negativas duplas.  
  
-   Executar os dois um automatizados e um manual gramática e ortografia verificar qualquer mensagem de erro que você escreve.  
  
-   Para mensagens de erro complexas, evite comunicações sequenciais. Nunca use uma conexão de F1 para a mensagem de erro. A mensagem em si deve ser suficiente.  
  
-   Use o ícone correto.  
  
-   Faça perguntas fácil de entender e usar os botões que têm opções claras, como "Excluir" e "Cancelar".  
  
-   Para avisos, ser claro sobre qual será a consequência de continuar. Os botões devem indicar a consequência.  
  
-   Para erros, descrevem o que o usuário pode fazer para corrigir o problema. Botões devem ser ações ou dizer "Fechar". Não use um botão de "Okey" para uma mensagem de erro.  
  
-   Algumas perguntas se perguntar ao construir uma mensagem de erro:  
  
    -   O usuário pode descobrir como resolver o problema com este erro sozinho?  
  
    -   O usuário usa o mesmo vocabulário que esse erro?  
  
    -   É esse erro ambigious ou compartilhados em várias situações? Nesse caso, como você orientar os usuários para a solução que precisam?  
  
#### <a name="build-errors"></a>Erros de compilação  
 Como o Visual Studio é uma ferramenta de desenvolvimento de software, muitos de seus componentes têm uma compilação, convertendo, codificação ou etapa para converter o trabalho do desenvolvedor em formato binário. Essas conversões podem causar erros quando o compilador não pode processar arquivos criados incorretamente ou quando as opções do compilador não foram definidas corretamente.  
  
 Usuários do Visual Studio podem gastar um número enorme de horas de desenvolvimento Resolvendo erros de compilação. Esse tempo de resolução aumenta quando erros têm dependências ou quando as mensagens de erro são mal escritas, que pode dificultar descobrir a origem do erro.  
  
 Os erros de compilação melhores são aquelas que não ocorrem em primeiro lugar, razão pela qual o Visual Studio fornece preenchimento automático e rabisca do IntelliSense. Os validadores de esquema e ferramentas semelhantes fornecem o mesmo tipo de comentários. Esses mecanismos proativamente orientam o usuário para construir o código bem formado, pois isso reduz a chance de erros de compilação.  
  
 O Visual Studio fornece uma janela de ferramentas em que os usuários podem ler e percorrer os erros que ocorreram em suas janelas de documento. Atalhos de teclado são fornecidos para que o usuário possa rapidamente grandes quantidades de código de navegar e ir diretamente para o local do problema. Visual Studio também permite que cada erro de build estar vinculado a uma determinada identificação de palavra-chave/contexto de ajuda para que o usuário pode ir diretamente para um tópico da Ajuda que fornece informações mais detalhadas sobre o erro.  
  
 Erros de compilação claras e concisas de gravação:  
  
-   **Use uma linguagem simples** que explica o problema com pouca ou nenhuma jargão do compilador. O texto de um erro de compilação não deve ser excessivamente técnico.  
  
-   **Descrever as possíveis causas.** Por exemplo, "faltando dois pontos entre a propriedade e o valor no ' (propriedade): (valor)' declaração."  
  
-   Fornecer detalhes sobre possíveis correções. Se não houver espaço suficiente, detalhes adicionais podem ser colocados para o tópico da Ajuda correspondente.  
  
### <a name="components-of-a-well-written-error-message"></a>Componentes de uma mensagem de erro bem escrito  
  
#### <a name="use-the-shell-dialog-service-for-error-messages"></a>Use o serviço de caixa de diálogo do shell para mensagens de erro.  
 Usando o serviço de caixa de diálogo de shell permite controlar a aparência da mensagem, fontes em particular, sem grandes alterações aos elementos individuais. Use o **IErrorInfo** mecanismos e relatá-los usando **IVsUIShell::SetErrorInfo/ReportErrorInfo**.  
  
#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>Escolha uma apresentação de notificação efetivo e apropriado.  
 Use uma caixa de diálogo modal com um aviso crítico se uma ação imediata é necessária para evitar a perda de dados (notificação síncrona). Ícones críticos são reservados para situações em que a mensagem sem leitura fechando pode levar a consequências negativas. Perda de dados é uma situação crítica que requer uma resposta de nível de alarme. Uso excessivo do ícone crítico desensitizes que os usuários façam sua importância. Se a mensagem de erro é informativa por natureza, considere alternativas para uma caixa de diálogo modal (notificação assíncrona).  
  
#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>Fornece uma explicação limpa e sucinta por que o problema ocorreu em vez de uma explicação técnica.  
 Sobrecarregar os usuários com detalhes técnicos a explicação os tornará mais provável ignorar as mensagens de erro. Exemplos de mensagens boa:  
  
-   "Não é possível abrir o arquivo solicitado."  
  
-   "Não é possível conectar à Internet."  
  
#### <a name="provide-information-about-how-to-fix-the-problem"></a>Fornecem informações sobre como corrigir o problema.  
 As sugestões de usuário de como corrigir o problema da oferta. Ser honesto com o usuário se não houver nenhuma sugestão. Fornece links diretos para fontes online alternativos, como o suporte técnico ou suporte da comunidade. Tente apontar os usuários a informações online específicas pertinentes ao problema. Para uma ID de erro, considere a vinculação de usuários a um thread de discussão sobre esse erro específico. Exemplos de mensagens boa:  
  
-   "Certifique-se de que você está conectado à Internet e tente a operação novamente."  
  
-   "Certifique-se de que o arquivo existe e se você tem permissão para abri-lo."  
  
#### <a name="write-a-message-that-is-short-and-to-the-point"></a>Grave uma mensagem que é curto e para o ponto.  
 Uma mensagem de erro pode notificar, explicar e oferecem uma solução mas ainda ser ignorado se ele está muito prolixo. Uma solução é usar divulgação progressiva com um botão de detalhes. Por exemplo, dê uma breve descrição/solução e, em seguida, colocar mais detalhes em um botão de detalhes. Se os usuários optar por ler mais informações sobre o erro, eles podem fazer isso.  
  
 O idioma da mensagem deve ser:  
  
-   **Domínio apropriado.** Use linguagem que entenderá o usuário. Mesmo que nossos clientes estão os desenvolvedores, eles geralmente não têm o contexto e a terminologia que nós temos.  
  
-   **Específico.** Evite texto vago e dar nomes específicos e os locais dos objetos envolvidos. Por exemplo, uma mensagem de erro como "o caractere é inválido" não é útil. O caractere? "Arquivo não encontrado". Qual arquivo?  
  
-   **Cortês.** Não culpe o usuário ou torná-los se sentir tolos. Evite linguagem ofensiva ou hostil (kill, executar, encerrar, fatal, inválida). Evite texto em maiusculas, que é normalmente visto como shouting e não está tão legível. Não use o humor.  
  
-   **Corrigi.** Use a gramática e ortografia correta (mesmo em Alfas). Erros de digitação são capricho e embaraçoso.  
  
-   **Contextualmente apropriadas.** Use o texto do botão apropriado. Evite o botão "Okey" e em vez disso, use "Continuar" ou "Sim/não".  
  
### <a name="error-message-examples"></a>Exemplos de mensagem de erro  
  
|Bom|incorreta|  
|----------|---------|  
|"O número discado não está mais no serviço. Verifique o número e discar novamente ou discar 0 para o operador."|-"Erro (449): número inválido"<br />-"Esse erro de exceção sem tratamento indica que a operação foi concluída com êxito."<br /><br /> ![Mensagem de erro inválido no Visual Studio](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "a_ErrorDialog 0602")|  
  
## <a name="accessing-help"></a>Acessando a Ajuda  
  
### <a name="overview"></a>Visão geral  
 Além de documentação no MSDN, um usuário do Visual Studio tem vários pontos de acesso para ajudar o usuário enquanto estiver na interface do usuário. Para garantir que esses pontos de acesso estejam consistentemente disponíveis, as equipes de recursos precisam tirar proveito do sistema de ajuda oferecido pelo ambiente. Esses pontos de acesso são:  
  
-   **Texto suplementar e das instruções nas caixas de diálogo.** Texto estático que fornece a direção ou explicação, na interface do usuário disponível em passe o mouse sobre um ícone de InfoDica ou superfície.  
  
-   **Ajuda de F1** (editor). No editor do Visual Studio, um usuário pode confiar que a qualquer momento pressionando F1 abrirá um tópico de ajuda específico para a seleção atual. Certifique-se de que tópicos associados F1 são apropriados e informativos.  
  
-   **Hiperlinks para tópicos de Ajuda.** Um hiperlink dentro de uma caixa de diálogo, a janela de ferramentas ou a superfície de design que inicia um tópico para ajudar o usuário a aprender mais sobre uma tecnologia, recurso ou obter informações sobre como realizar uma tarefa.  
  
-   **Mecanismos de interface do usuário de auxiliar, como marcas inteligentes e caixas de diálogo de criação.** Esses mecanismos ajudam o usuário a compreender um elemento de interface do usuário ou facilitam uma tarefa, como marcas inteligentes ou caixas de diálogo do construtor.  
  
-   **Botões de Ajuda da interface do usuário** (preterido). Um indicador visível na barra de título que fornece acesso para o tópico da Ajuda F1 relacionado.  
  
### <a name="text"></a>Texto  
  
#### <a name="instructional-and-supplemental-text-in-dialogs"></a>Texto suplementar e das instruções nas caixas de diálogo  
 Caixas de diálogo que dão suporte a tarefas complexas, pode haver a necessidade de dar o texto de instrução dentro da interface do usuário, geralmente na parte superior da caixa de diálogo ou próximo controles complexos. Ver [interface do usuário do texto e a terminologia](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) para obter detalhes sobre 1&gt;Writing.  
  
#### <a name="infotips"></a>InfoTips  
 Muitas vezes, o texto com instrução pode ser muito demorado para posicionar em vigor na interface do usuário ou pode ser útil somente para novos usuários, pareçam resíduos para usuários experientes. Nesse caso, o texto das instruções informativas deve ser colocado como uma dica de ferramenta em uma InfoDica.  
  
 InfoTips deve ser colocado perto os controles que eles estão relacionados e devem usar o ícone de InfoDica específico, que é discreto ainda notável.  
  
 ![InfoDica no Visual Studio](../../extensibility/ux-guidelines/media/0601-d_infotip.png "d_InfoTip 0601")  
  
 **Exemplo de uma InfoDica no Visual Studio**  
  
### <a name="interactive-help-mechanisms"></a>Mecanismos de ajuda interativos  
  
#### <a name="f1-help"></a>F1 Ajuda  
 Ajuda F1 é necessária em um editor ou a superfície de design, mas não em outro lugar no ambiente do Visual Studio.  
  
#### <a name="hyperlinks-to-help-topics"></a>Hiperlinks para tópicos de ajuda  
 Hiperlinks podem ser usados para executar uma ação, navegar dentro do IDE ou iniciar a Ajuda em um navegador. Ver [interface do usuário do texto e a terminologia](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) para obter detalhes sobre a linguagem e 07.10.01 botões e hiperlinks para diretrizes visual e layout.  
  
#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>Ajuda [?] botões em barras de título da caixa de diálogo (preteridas)  
 Geralmente, os botões de Ajuda [?] na barra de título das caixas de diálogo são preteridos. Tópicos de interface do usuário não fazem mais parte de nosso modelo de documento e, portanto, talvez não haja um tópico relevante para vincular a. Essencialmente, o botão da barra de título era a mesma coisa que ajuda F1, e que não é mais necessário nas caixas de diálogo. Em alguns casos, isso pode ainda ser usado como um indicador de que há mais informações processuais ou conceituais, embora os hiperlinks são mais comumente usados na interface do usuário mais recente.  
  
##### <a name="dialogs-created-through-the-environment"></a>Caixas de diálogo criadas por meio do ambiente  
 Muitas caixas de diálogo de shell são criadas por meio de **VBDialogBoxParam** função. Essa função compartilhada foi atualizada para auxiliar na movimentação a **ajudar** botão na caixa de diálogo para o **?** botão, mantendo uma arquitetura que é com versões anteriores compatível e extensível.  
  
 Especificamente, o **VBDialogBoxParam** função analisa o modelo de caixa de diálogo para um botão cuja ID é **IDHELP** (9) ou o rótulo é **ajuda** ou **& Ajuda**. Se um botão de ajuda for encontrado, ele está oculto e o **WS_EX_CONTEXTHELP** estilo é adicionado à caixa de diálogo, o que coloca o **?** botão na barra de título da caixa de diálogo.  
  
 Quando a caixa de diálogo é criada, ele envia o proc. caixa de diálogo para uma pilha e invoca a caixa de diálogo com um procedimento de caixa de diálogo pré-processando denominado **DialogPreProc**. Quando o **?** botão é clicado, ele envia uma **WM_SYSCOMMAND** dos **SC_CONTEXTHELP** na caixa de diálogo. O **DialogPreProc** captura esse comando e o altera para um **WM_HELP** mensagem, que é passada para o procedimento original. a caixa de diálogo  
  
 A maioria das caixas de diálogo ambiente criado tem um botão de ajuda na caixa de diálogo. Quando a caixa de diálogo é exibida, o botão Ajuda é ocultada automaticamente e somente o **?** botão funciona. Se o **?** botão nunca é removida ou alterada no Windows, essa solução permite que você rapidamente mover de volta para os botões de ajuda originais.  
  
 Essa solução faz quatro suposições que poderiam causar bugs:  
  
- Botão de Ajuda da caixa de diálogo estiver **IDHELP** (9).  
  
- A caixa de diálogo parece correta quando o botão Ajuda estiver oculto.  
  
- A caixa de diálogo não substitui sua winproc.  
  
- A caixa de diálogo não será inserida dentro de outra caixa de diálogo.  
  
  Se a caixa de diálogo reside no msenv e não usar **VBDialogBoxParam**, investigue aproveitando **VBDialogBoxParam** antes de implementar seu próprio manipulador.  
  
##### <a name="dialogs-created-through-other-packages"></a>Caixas de diálogo criadas por meio de outros pacotes  
 Você pode implementar sua própria solução para caixas de diálogo que residem fora do msenv. Para uma classe de caixa de diálogo compartilhadas em seu VSPackage, considere mover o botão à barra de título ou implementar um manipulador em cada caixa de diálogo. O código a seguir é um esqueleto de uma implementação para ajudar você a começar:  
  
```  
struct DLGPROCITEM  
{  
    FARPROC proc; // The info used to create the dialog.  
    DLGPROCITEM* procPrev;  
};  
  
DLGPROCITEM* g_dlgProcStack = NULL;  
  
// A dialog starter/wrapper function is used to push the new  
// dialog proc to the top of our dialog proc stack.  
  
int SomeDialogStarterFunction(hinst, id, proc, etc)  
{  
    if (g_dlgProcStack == NULL)  
    {  
        g_dlgProcStack = new DLGPROCITEM;  
        g_dlgProcStack->procPrev = NULL;  
    }  
    else  
    {  
        DLGPROCITEM* procItem = new DLGPROCITEM;  
        g_dlgProcStack->procPrev = g_dlgProcStack;  
        g_dlgProcStack = procItem;  
    }  
}  
  
// Pop this dialog proc off the dialog proc stack.  
  
DialogBoxIndirectParam...(...)  
{  
    DLGPROCITEM* procItem = g_dlgProcStack->procPrev;  
    delete g_dlgProcStack;  
    g_dlgProcStack = procItem;  
}  
  
// A wrapper dialog procedure will allow us to capture the  
// SC_CONTEXTHELP button on the title bar from Windows and  
// forward it as a simple WM_HELP message back to the dialog.  
  
INT_PTR CALLBACK DialogPreProc(HWND hwndDlg, UINT uMsg,  
    WPARAM wParam, LPARAM lParam)  
{  
    if (uMsg == WM_SYSCOMMAND && wParam == SC_CONTEXTHELP)  
    {  
        uMsg = WM_HELP;  
        wParam = 0;  
        lParam = 0;  
    }  
    return CallWindowProc((WNDPROC)g_dlgProcStack->proc,  
        hwndDlg, uMsg, wParam, lParam);  
}  
```  
  
##### <a name="help-buttons-in-managed-code"></a>Botões de Ajuda em código gerenciado  
 Substituindo o comportamento de padrão do botão da barra de ajuda janela título é fácil em código gerenciado. Abaixo está um aplicativo de demonstração completo que demonstra esse comportamento. Em essência, você precisa substituir seu formulário **WndProc** solicitações de método e, em seguida, incêndio desativar a Ajuda de F1 quando um **SC_CONTEXTHELP** mensagem é interceptada.  
  
```  
using System;  
using System.Windows.Forms;  
  
public class HelpForm : Form  
{  
    private const int SC_CONTEXTHELP = 0xF180;  
    private const int WM_SYSCOMMAND = 0x0112;  
  
    public HelpForm()  
    {  
        this.ClientSize = new System.Drawing.Size(300, 250);  
        this.HelpButton = true;  
        this.MaximizeBox = false;  
        this.MinimizeBox = false;  
        this.Name = "HelpForm";  
        this.Text = "Help Form";  
    }  
  
    protected override void WndProc(ref Message m)  
    {  
        if (m.Msg == WM_SYSCOMMAND && SC_CONTEXTHELP == (int)m.WParam)  
            ShowHelp();  
        else  
            base.WndProc(ref m);  
    }  
  
    private void ShowHelp()  
    {  
        MessageBox.Show("F1 Help goes here.");  
    }  
  
     [STAThread]  
    static void Main()  
    {  
        Application.EnableVisualStyles();  
        Application.EnableRTLMirroring();  
        Application.Run(new HelpForm());  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Fontes e formatação para o Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)   
 [Layout para o Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md)   
 [Notificações e progresso do Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)