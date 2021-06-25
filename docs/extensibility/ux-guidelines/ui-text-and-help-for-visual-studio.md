---
title: Texto da interface do usuário e Ajuda para Visual Studio | Microsoft Docs
description: Saiba mais sobre o texto e a terminologia da interface do usuário usados nas informações da Ajuda para Visual Studio.
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 40b128c5e95c70457d92843e620b4aa072c409ba
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899427"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Texto de interface do usuário e Ajuda para Visual Studio
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a> Texto e terminologia da interface do usuário
 O texto compreensível é crucial para a interface do usuário efetiva. Os usuários de software tendem a ler rótulos primeiro, ou seja, aqueles mais relevantes para concluir a tarefa em questão. O texto estático é lido com menos frequência. Planeje que os usuários iniciem suas sessões de trabalho com uma verificação rápida de toda a janela, seguida por uma leitura da interface do usuário nesta ordem aproximada:

1. Controles interativos no centro

2. Botões de commit

3. Controles interativos encontrados em outro lugar

4. Instruções principais

5. Explicações complementares

6. Título da janela

7. Outro texto estático no corpo principal

### <a name="usage-patterns-for-ui-text"></a>Padrões de uso para texto da interface do usuário

#### <a name="title-bar-text"></a>Texto da barra de título
 O texto da barra de título deve corresponder ao comando que gerou a interface do usuário.

#### <a name="instructional-text-helper-text"></a>Texto de instrução (texto auxiliar)
 Em alguns diálogos, é útil fornecer instruções principais em destaque para explicar o que fazer na janela ou na página. Às vezes, isso é chamado de "texto auxiliar".

##### <a name="writing-style-rules-for-helper-text"></a>Escrevendo regras de estilo para texto auxiliar

- Não explique o óbvio. A menos que seja absolutamente necessário, não inclua texto de instrução.

- O texto de instrução sempre é colocado na parte superior da caixa de diálogo e deve se referir à tarefa que está sendo executada.

- Explique precisamente aos usuários o que eles precisam fazer. Evite comunicação excessiva e redundância.

- Revise cada janela e elimine palavras e instruções duplicadas.

- Mantenha o texto de instrução curto. Se mais informações são necessárias para determinados usuários ou cenários, forneça um link para um tópico online conceitual detalhado.

- Escreva seu texto para que cada palavra mantenha o peso e seja necessário.

- Siga as diretrizes existentes da Microsoft para [Interface do Usuário texto](/windows/desktop/uxguide/text-ui) e estilo [e tom.](/windows/desktop/uxguide/text-style-tone)

#### <a name="supplemental-instructions"></a>Instruções complementares
 As instruções complementares fornecem informações adicionais que ajudam o usuário a entender os controles ou os grupos de controle. Isso também pode incluir o texto de dica necessário para entender qual formato o controle de entrada está esperando. Use instruções complementares com moderação. Reserve-os para casos em que é provável que o usuário não entenda totalmente as ramificações da escolha que está fazendo.

 ![Captura de tela mostrando o Internet Explorer opções com texto complementar abaixo dele que descreve o impacto da alteração das configurações de opção.](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Texto complementar em Visual Studio**

 ![Captura de tela da caixa de diálogo Escolher Controle do Código-Fonte Visual Studio texto suplementar que descreve cada uma das opções do sistema de controle do código-fonte.](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Texto complementar em Visual Studio**

#### <a name="infotips"></a>InfoTips
 Geralmente, o texto de instrução pode ser muito longo para ser posicionado in-locar na interface do usuário ou pode ser útil somente para novos usuários, se sentido como uma confusão para usuários experientes. Nesse caso, o texto instrucional/informacional deve ser colocado como uma dica de ferramenta em uma InfoTip.

 As InfoTips devem ser colocadas perto dos controles aos quais estão relacionadas e devem usar o ícone infotip específico, que é discreto, mas perceptível.

 ![InfoTip no Visual Studio](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Exemplo de uma InfoTip no Visual Studio**

##### <a name="writing-style-rules-for-infotips"></a>Escrevendo regras de estilo para InfoTips

- Escreva InfoTips como frases completas. Eles exigem verbos específicos, caso de frase e pontuação final.

- Use InfoTips para complementar suas instruções ou informações principais. Se você estiver apenas usando palavras diferentes para reestado a ideia principal, não precisará de uma InfoTip.

- Mantenha o InfoTips curto e bom. Use palavras pequenas e linguagem simples e diárias que dá suporte e incentiva o usuário.

- Siga as diretrizes existentes da Microsoft para [Interface do Usuário texto](/windows/desktop/uxguide/text-ui) e estilo [e tom.](/windows/desktop/uxguide/text-style-tone)

#### <a name="control-labels"></a>Rótulos de controle
 Os rótulos de controle devem ser curtos, concisos e seguir as diretrizes da Área de [Trabalho do Windows para Controles](/windows/desktop/uxguide/controls).

 Para obter mais informações sobre o formato e o posicionamento do rótulo de controle na interface do usuário, consulte [Layout para Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).

#### <a name="help-links"></a>Links de ajuda
 Os links de ajuda podem ser colocados dentro do texto de instrução ou no corpo da interface do usuário. Eles podem ser links para Ajuda ou iniciar diálogos internos.

##### <a name="visual-style-rules-for-help-links"></a>Regras de estilo visual para links de Ajuda

- Use as cores corretas do ambiente para hiperlinks. Um hiperlink com estilo adequado não piscará rapidamente em vermelho quando clicado. Se você vir isso, será uma indicação de que as cores do ambiente não estão sendo usadas.

- Sublinhados só devem ser usados ao passar o mouse ou quando o link é inserido em um parágrafo.

- Para obter informações mais detalhadas sobre estilos visuais e de interação para hiperlinks, consulte Botões e hiperlinks.

##### <a name="writing-style-rules-for-help-links"></a>Escrevendo regras de estilo para links de Ajuda

- Ao iniciar diálogos, mantenha os padrões para reellipses: sem reellipses para navegação, relipes se a tarefa exigir interface do usuário adicional.

     ![Link de ajuda Visual Studio](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **Uma reellipse (...) em um link da Ajuda indica que a tarefa exigirá interface do usuário adicional.**

- Os links não devem começar com "Learn", pois essa não é a intenção do usuário. O usuário deseja responder a uma pergunta específica, não receber uma educação geral.

- Links de ajuda de frase para que eles fazem a pergunta que o tópico responderá.

     Incorreto: "Saiba mais sobre os preços de Mobile Services Windows Azure"

     Correto: "Quais opções de preço estão disponíveis para o Windows Azure Mobile Services?"

- Nunca use *Clique...* para o texto do link.

- Nunca vincule apenas a palavra "aqui". Isso é problemático para alguns leitores de tela, que dará voz apenas à palavra hiperlinkada.

     Incorreto: "Encontre informações sobre o Windows Azure Mobile Services **aqui"**

     Correto: "Quais opções de preço estão disponíveis para o Windows Azure Mobile Services?"

- Para obter mais informações sobre o estilo de escrita correto para links de Ajuda, consulte As diretrizes da Área de [Trabalho do Windows para Ajuda](/windows/desktop/uxguide/winenv-help).

#### <a name="hint-text"></a>Texto da dica
 O texto da dica aparece como uma marca-d'água dentro de um controle ou abaixo do controle . A formatação correta será aplicada usando o token VSColors apropriado, `Environment.GrayText` .

 Ele pode aparecer em vários formulários.

- No lugar do rótulo de controle:

     ![Captura de tela de um controle de lista listada com texto de dica no lugar do rótulo de controle que lê "Pesquisar Gerenciador de Soluções (Ctrl+;)".](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- Com um verbo, dando instruções:

     ![Captura de tela de uma caixa de texto com texto de dica no controle que indica "Insira seu nome".](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- Com texto indicando uma entrada necessária:

     ![Captura de tela de uma caixa de texto com texto de dica no controle que diz " \< Obrigatório \> ".](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>Texto de marca-d'água
 Em uma superfície de design vazia, o texto deve indicar o que fazer, bem como fornecer links para abrir outras janelas relacionadas, se apropriado:

 ![Texto de marca-d'água Visual Studio](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **Exemplo de texto de marca-d'água Visual Studio**

### <a name="common-terminology"></a>Terminologia comum

|Termo|Explicação|Comentário|
|----------|-----------------|-------------|
|Entrar/Sair|Verbos usados sinônimos com a Web para representar a autenticação em uma propriedade da Web. Nos clientes, usamos isso uma vez como uma noção de nível superior para entrar e sair da conexão de usuário do IDE, que representa uma identidade de nível superior que fornece funcionalidades de nível superior, como roaming e licenciamento que não estão disponíveis com todas as outras conexões.|O Usuário do IDE é o único recurso que deve representar um verbo de entrar/sair, pois ele representa o usuário do IDE de nível superior.|
|Conectar/desconectar|Use em locais em que um recurso mantém uma única conexão com um serviço online.|Gerenciador de Servidores, em que você só pode ter uma conexão ativa do Azure por vez, é um exemplo de Conectar/Desconectar.|
|Adicionar/remover|Não destrutiva. Use ao adicionar ou remover algo de uma lista.|A caixa de Gerenciador de Conexões lista de servidores do TFS é um exemplo de Adicionar/Remover.|
|Excluir|Destrutivo. Use somente quando o elemento que está sendo removido for descartado permanentemente ou excluído do disco.|"Excluir" geralmente requer um prompt se o resultado estiver excluindo um arquivo do disco.|

## <a name="error-messages"></a>Mensagens de erro

### <a name="overview"></a>Visão geral
 Ocorrem erros. Definir limitações sobre o que o usuário pode fazer é uma primeira etapa razoável para evitar mensagens de erro evitadas. No entanto, quando ocorre um erro, uma mensagem de erro bem escrita pode ir muito longe para atenuar o problema. As mensagens de erro são, indiscutivelmente, um dos tipos mais importantes de notificação que o usuário vê, pois são síncronas e indicam um problema que precisa ser resolvido. Mensagens de erro mal escritas deixam os usuários por conta própria para decidir a causa dos erros e quaisquer soluções possíveis.

 Os usuários podem parar de prestar atenção a mensagens de erro sobreutilizadas ou confusas, portanto, escreva apenas as mensagens necessárias que agregam valor à experiência do usuário. Se a mensagem for simplesmente uma notificação, use uma apresentação alternativa.

### <a name="rules-for-creating-an-error-message"></a>Regras para criar uma mensagem de erro

- Ao construir mensagens de erro, escolha o nível de erro apropriado para o público-alvo. Visa resumos simples que fornecem uma ação que o usuário pode tomar, se aplicável. Não estado nada que o usuário não precise saber.

- Forneça assistência construtiva. É mais fácil ler e agir em uma mensagem de erro que contém instruções.

- Não use negativos duplos.

- Execute uma verificação automática e manual de gramática e ortografia em qualquer mensagem de erro que você escrever.

- Para mensagens de erro complexas, evite comunicações sequenciais. Nunca use uma conexão F1 para a mensagem de erro. A mensagem em si deve ser suficiente.

- Use o ícone correto.

- Faça perguntas fáceis de entender e usar botões que têm opções claras, como "Excluir" e "Cancelar".

- Para avisos, seja claro sobre qual será a consequência de continuar. Os botões devem indicar a consequência.

- Para erros, descreva o que o usuário pode fazer para corrigir o problema. Os botões devem ser ações ou dizer "Fechar". Não use um botão "OK" para uma mensagem de erro.

- Algumas perguntas a fazer a si mesmo ao construir uma mensagem de erro:

  - O usuário pode descobrir como resolver o problema apenas com esse erro?

  - O usuário usa o mesmo vocabulário que esse erro?

  - Esse erro é ambíguo ou compartilhado em várias situações? Se sim, como você orienta os usuários para a solução de que eles precisam?

#### <a name="build-errors"></a>Erros de compilação
 Como Visual Studio é uma ferramenta de desenvolvimento de software, muitos de seus componentes têm uma etapa de compilação, conversão ou codificação para converter o trabalho do desenvolvedor em formato binário. Essas conversões podem causar erros quando o compilador não pode processar arquivos criado incorretamente ou quando as opções do compilador não foram definidas corretamente.

 Visual Studio usuários podem gastar um grande número de horas de desenvolvimento resolvendo erros de build. Esse tempo de resolução aumenta quando os erros têm dependências ou quando as mensagens de erro são mal escritas, o que pode dificultar a descoberta da origem do erro.

 Os melhores erros de build são aqueles que não ocorrem em primeiro lugar, e é por isso que Visual Studio fornece alternâncias AutoComplete e IntelliSense. Validadores de esquema e ferramentas semelhantes fornecem o mesmo tipo de comentários. Esses mecanismos orientam proativamente o usuário a construir código bem formado, diminuindo a chance de erros de build.

 Visual Studio fornece uma janela de ferramentas em que os usuários podem ler e navegar pelos erros ocorridos em suas janelas de documentos. Atalhos de teclado são fornecidos para que o usuário possa navegar rapidamente por grandes quantidades de código e ir diretamente para o local do problema. Visual Studio também permite que cada erro de build seja vinculado a uma ID de contexto/palavra-chave de Ajuda específica para que o usuário possa ir diretamente para um tópico de Ajuda que fornece informações mais detalhadas sobre o erro.

 Escreva erros de build claros e concisos:

- **Use linguagem simples** que explique o problema com pouco ou nenhum jargão do compilador. O texto de um erro de build não deve ser muito técnico.

- **Delinear possíveis causas.** Por exemplo, "Faltando dois-pontos entre a propriedade e o valor na declaração '(property) : (value)'."

- Dê detalhes sobre possíveis correções. Se não houver espaço suficiente, detalhes adicionais poderão ser colocados no tópico de Ajuda correspondente.

### <a name="components-of-a-well-written-error-message"></a>Componentes de uma mensagem de erro bem escrita

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>Use o serviço de diálogo shell para mensagens de erro.
 Usar o serviço de diálogo do shell permite controlar a aparência da mensagem, fontes em particular, sem alterações importantes em elementos individuais. Use os **mecanismos IErrorInfo** e reporte-os usando **IVsUIShell::SetErrorInfo/ReportErrorInfo**.

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>Escolha uma apresentação de notificação eficaz e apropriada.
 Use uma caixa de diálogo modal com um aviso crítico se uma ação imediata for necessária para evitar a perda de dados (notificação síncrona). Ícones críticos são reservados para situações em que fechar a mensagem sem lê-la pode levar a consequências negativas. A perda de dados é uma situação crítica que requer uma resposta de nível de alarme. O uso excessivo do ícone crítico alimente os usuários para sua importância. Se a mensagem de erro for informacional por natureza, considere alternativas a uma caixa de diálogo modal (notificação assíncrona).

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>Forneça uma explicação simples e sucinta do motivo pelo qual o problema ocorreu em vez de uma explicação técnica.
 Sobrecarregar usuários com detalhes técnicos na explicação os torna mais prováveis de ignorar mensagens de erro. Exemplos de boas mensagens:

- "Não é possível abrir o arquivo solicitado."

- "Não é possível se conectar à Internet."

#### <a name="provide-information-about-how-to-fix-the-problem"></a>Forneça informações sobre como corrigir o problema.
 Ofereça ao usuário sugestões de como corrigir o problema. Seja ofensivo com o usuário se não houver sugestões. Forneça links diretos para fontes online alternativas, como suporte técnico ou suporte à comunidade. Tente apontar os usuários para informações online específicas pertinentes ao problema. Para uma ID de erro, considere vincular usuários a um thread de discussão sobre esse erro específico. Exemplos de boas mensagens:

- "Certifique-se de que você está conectado à Internet e tente essa operação novamente."

- "Certifique-se de que o arquivo existe e se você tem permissão para abri-lo."

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>Escreva uma mensagem curta e até o ponto.
 Uma mensagem de erro pode notificar, explicar e oferecer uma solução, mas ainda será ignorada se for muito wordy. Uma solução é usar a divulgação progressiva com um botão de detalhes. Por exemplo, dê uma breve descrição/solução e, em seguida, coloque mais detalhes em um botão de detalhes. Se os usuários optarem por ler mais informações sobre o erro, eles poderão fazer isso.

 O idioma na mensagem deve ser:

- **Apropriado para o domínio.** Use o idioma que o usuário entenderá. Embora nossos clientes sejam desenvolvedores, eles geralmente não têm o contexto e a terminologia que temos.

- **Específico.** Evite palavras vaga e dê nomes e locais específicos de objetos envolvidos. Por exemplo, uma mensagem de erro como "caractere inválido" não é útil. Qual caractere? "Arquivo não encontrado." Qual arquivo?

- **Educado.** Não tenha culpado o usuário nem faça com que eles se sintam estúpidos. Evite a linguagem hostil ou ofensiva (Kill, execute, Terminate, fatal, ilegal). Evite texto em maiúsculas, que geralmente é visto como gritar e não é tão legível. Não use humor.

- **Correto.** Use a grafia e a gramática corretas (mesmo em Alfas). Erros de grafia são constrangedoras e incorretas.

- **Contextual apropriado.** Use o texto do botão apropriado. Evite o botão "OK" e, em vez disso, use "Continue" ou "yes/no".

### <a name="error-message-examples"></a>Exemplos de mensagem de erro

|Satisfatório|Incorreto|
|----------|---------|
|"O número que você está discado não está mais em serviço. Verifique o número e disque novamente ou disque 0 para o operador. "|-"Erro (449): número inválido"<br />-"Esse erro de exceção sem tratamento indica que a operação foi concluída com êxito".<br /><br /> ![Mensagem de erro inadequada no Visual Studio](../../extensibility/ux-guidelines/media/0602-a_errordialog.png "0602-a_ErrorDialog")|

## <a name="accessing-help"></a>Acessando a ajuda

### <a name="overview"></a>Visão geral
 Além da documentação no MSDN, um usuário do Visual Studio tem vários pontos de acesso para auxiliar o usuário na interface do usuário. Para garantir que esses pontos de acesso estejam consistentemente disponíveis, as equipes de recursos precisam aproveitar o sistema de ajuda oferecido pelo ambiente. Estes pontos de acesso são:

- **Texto instrutivo e suplementar em caixas de diálogo.** Texto estático que fornece direção ou explicação, na superfície da interface do usuário ou disponível ao passar o mouse sobre um ícone de InfoTip.

- **Ajuda F1** (somente editor). No editor do Visual Studio, um usuário pode confiar que, a qualquer momento, pressionar F1 abrirá um tópico da ajuda específico da seleção atual. Verifique se os tópicos associados a F1 são apropriados e informativos.

- **Hiperlinks para tópicos da ajuda.** Um hiperlink em uma caixa de diálogo, janela de ferramentas ou superfície de design que inicia um tópico para ajudar o usuário a aprender mais sobre uma tecnologia, capacidade ou informações sobre como realizar uma tarefa.

- **Mecanismos de interface do usuário auxiliares, como marcas inteligentes e caixas de diálogo de construção.** Esses mecanismos ajudam o usuário a compreender um elemento de interface do usuário ou a facilitar uma tarefa, como marcas inteligentes ou caixas de diálogo de construtor.

- **Botões de ajuda da interface do usuário** (preterido). Um indicador visível na barra de título que fornece acesso ao tópico de ajuda F1 relacionado.

### <a name="text"></a>Texto

#### <a name="instructional-and-supplemental-text-in-dialogs"></a>Texto instrutivo e suplementar em caixas de diálogo
 Em caixas de diálogo que dão suporte a tarefas complexas, pode haver a necessidade de fornecer texto de instrução dentro da interface do usuário, geralmente na parte superior da caixa de diálogo ou controles quase complexos. Consulte a [terminologia e o texto da interface do usuário](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) para obter detalhes sobre como escrever estilo.

#### <a name="infotips"></a>InfoTips
 Muitas vezes, o texto instrutivo pode ser muito demorado para ser posicionado na interface do usuário ou pode ser útil apenas para novos usuários, como confusão aos usuários experientes. Nesse caso, o texto instrutivo/informativo deve ser colocado como uma dica de ferramenta em um InfoTip.

 InfoTips deve ser posicionado próximo aos controles aos quais eles estão relacionados e deve usar o ícone de InfoTip específico, que é discreto, ainda perceptível.

 ![InfoTip no Visual Studio](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Exemplo de um InfoTip no Visual Studio**

### <a name="interactive-help-mechanisms"></a>Mecanismos de ajuda interativa

#### <a name="f1-help"></a>Ajuda F1
 A ajuda F1 é necessária em um editor ou superfície de design, mas não em outro lugar no ambiente do Visual Studio.

#### <a name="hyperlinks-to-help-topics"></a>Hiperlinks para tópicos da ajuda
 Os hiperlinks podem ser usados para executar uma ação, navegar dentro do IDE ou iniciar a ajuda em um navegador. Consulte o [texto e a terminologia da interface do usuário](../../extensibility/ux-guidelines/ui-text-and-help-for-visual-studio.md#BKMK_UITextAndTerminology) para obter detalhes sobre os botões de idioma e 07.10.01 e hiperlinks para Visual e diretrizes de layout.

#### <a name="help--buttons-in-dialog-title-bars-deprecated"></a>Botões da ajuda [?] nas barras de título da caixa de diálogo (preterido)
 Na maior parte, os botões da ajuda [?] na barra de título das caixas de diálogo são preteridos. Os tópicos da interface do usuário não fazem mais parte do nosso modelo de documento e, portanto, pode não haver um tópico relevante para vincular. Essencialmente, o botão da barra de título foi o mesmo que a ajuda F1, e isso não é mais necessário em caixas de diálogo. Em alguns casos, isso ainda pode ser usado como um indicador de que há mais informações conceituais ou de procedimento disponíveis, embora os hiperlinks sejam mais comumente usados na interface do usuário mais recente.

##### <a name="dialogs-created-through-the-environment"></a>Caixas de diálogo criadas por meio do ambiente
 Muitas caixas de diálogo de shell são criadas por meio da função **VBDialogBoxParam** . Esta função compartilhada foi atualizada para ajudar a mover o botão **ajuda** da caixa de diálogo para o **?** ao reter uma arquitetura que é compatível com versões anteriores e extensível.

 Especificamente, a função **VBDialogBoxParam** examina o modelo de caixa de diálogo para um botão cuja ID é **IDHELP** (9) ou o rótulo é **ajuda** ou **&ajuda**. Se um botão de ajuda for encontrado, ele ficará oculto e o estilo de **WS_EX_CONTEXTHELP** será adicionado à caixa de diálogo, que colocará o **?** na barra de título da caixa de diálogo.

 Quando a caixa de diálogo é criada, ela envia por push o procedimento de caixa de diálogo para uma pilha e invoca a caixa de diálogo com um procedimento de caixa de diálogo de pré-processamento chamado **DialogPreProc**. Quando o **?** o botão é clicado, ele envia uma **WM_SYSCOMMAND** de **SC_CONTEXTHELP** para a caixa de diálogo. O **DialogPreProc** captura esse comando e o altera para uma **WM_HELP** mensagem, que é passada para o procedimento de caixa de diálogo original.

 A maioria das caixas de diálogo criadas pelo ambiente tem um botão ajuda na caixa de diálogo. Quando a caixa de diálogo é exibida, o botão ajuda é ocultado automaticamente e apenas o **?** botão funciona. Se o **?** o botão é removido ou alterado no Windows, essa solução permite que você avance rapidamente para os botões de ajuda originais.

 Essa solução faz quatro suposições que podem causar bugs:

- O botão ajuda da caixa de diálogo é **IDHELP** (9).

- A caixa de diálogo parece correta quando o botão ajuda está oculto.

- A caixa de diálogo não substitui seu que WinProc.

- A caixa de diálogo não está inserida dentro de outra caixa de diálogo.

  Se a caixa de diálogo residir em msenv e não usar **VBDialogBoxParam**, investigue aproveitando o **VBDialogBoxParam** antes de implementar seu próprio manipulador.

##### <a name="dialogs-created-through-other-packages"></a>Caixas de diálogo criadas por meio de outros pacotes
 Você pode implementar sua própria solução para caixas de diálogo que residem fora do msenv. Para uma classe de diálogo compartilhada em seu VSPackage, considere mover o botão para a barra de título ou implementar um manipulador em cada caixa de diálogo. O código a seguir é um esqueleto de uma implementação para ajudá-lo a começar:

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

##### <a name="help-buttons-in-managed-code"></a>Botões de ajuda no código gerenciado
 Substituir o comportamento padrão do botão de ajuda da barra de título da janela é fácil no código gerenciado. Veja abaixo um aplicativo de demonstração completo que demonstra esse comportamento. Em essência, você precisa substituir o método **WndProc** do seu formulário e, em seguida, disparar as solicitações de ajuda F1 quando uma mensagem de **SC_CONTEXTHELP** for interceptada.

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

## <a name="see-also"></a>Confira também
- [Fontes e formatação para Visual Studio](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md)
- [Layout para Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md)
- [Notificações e progresso do Visual Studio](../../extensibility/ux-guidelines/notifications-and-progress-for-visual-studio.md)
