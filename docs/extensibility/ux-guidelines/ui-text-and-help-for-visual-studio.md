---
title: Texto e ajuda da interface do usuário para o Visual Studio | Microsoft Docs
description: Saiba mais sobre o texto da interface do usuário e a terminologia usada nas informações de ajuda do Visual Studio.
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e8747d07-6c90-46cc-b425-55b589f7e9e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8635907b5c0190165855378fa692fb9abca4b0ec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105052652"
---
# <a name="ui-text-and-help-for-visual-studio"></a>Texto de interface do usuário e Ajuda para Visual Studio
## <a name="ui-text-and-terminology"></a><a name="BKMK_UITextAndTerminology"></a> Texto e terminologia da interface do usuário
 O texto abrangente é crucial para a interface do usuário efetiva. Os usuários de software tendem a ler os rótulos primeiro, ou seja, aqueles mais relevantes para a conclusão da tarefa em questão. O texto estático é lido com menos frequência. Planeje que os usuários iniciem suas sessões de trabalho com uma verificação rápida de toda a janela, seguida de uma leitura da interface do usuário nessa ordem aproximada:

1. Controles interativos no centro

2. Botões de confirmação

3. Controles interativos encontrados em outro lugar

4. Instruções principais

5. Explicações suplementares

6. Título da janela

7. Outro texto estático no corpo principal

### <a name="usage-patterns-for-ui-text"></a>Padrões de uso para texto da interface do usuário

#### <a name="title-bar-text"></a>Texto da barra de título
 O texto da barra de título deve corresponder ao comando que gerou a interface do usuário.

#### <a name="instructional-text-helper-text"></a>Texto instrutivo (texto auxiliar)
 Em algumas caixas de diálogo, é útil fornecer instruções principais importantes para explicar o que fazer na janela ou na página. Isso às vezes é chamado de "texto auxiliar".

##### <a name="writing-style-rules-for-helper-text"></a>Escrevendo regras de estilo para texto auxiliar

- Não explique o óbvio. A menos que seja absolutamente necessário, não inclua texto de instrução.

- O texto de instrução sempre é colocado na parte superior da caixa de diálogo e deve se referir à tarefa que está sendo executada.

- Explique precisamente aos usuários o que eles precisam fazer. Evite a comunicação e a redundância excessivas.

- Examine cada janela e elimine palavras e instruções duplicadas.

- Mantenha o texto de instrução curto. Se mais informações forem necessárias para determinados usuários ou cenários, forneça um link para um tópico online conceitual detalhado.

- Escreva seu texto para que todas as palavras contenham peso e sejam necessárias.

- Siga as diretrizes da Microsoft existentes para texto e [estilo](/windows/desktop/uxguide/text-style-tone)de [interface do usuário](/windows/desktop/uxguide/text-ui) e Tom.

#### <a name="supplemental-instructions"></a>Instruções complementares
 As instruções complementares fornecem informações adicionais que ajudam o usuário a entender controles ou controlar agrupamentos. Isso também pode incluir o texto de dica necessário para entender o formato esperado pelo controle de entrada. Use instruções suplementares com moderação. Reserve-los para casos em que é provável que o usuário não entenda totalmente as ramificações da escolha que estão fazendo.

 ![Captura de tela mostrando o botão Opções do Internet Explorer com texto suplementar abaixo dele que descreve o impacto da alteração das configurações de opção.](../../extensibility/ux-guidelines/media/0601-b_supplementaltext1.png "0601-b_SupplementalText1")

 **Texto complementar no Visual Studio**

 ![Captura de tela da caixa de diálogo escolher controle do código-fonte no Visual Studio mostrando texto suplementar que descreve cada uma das opções do sistema de controle do código-fonte.](../../extensibility/ux-guidelines/media/0601-c_supplementaltext2.png "0601-c_SupplementalText2")

 **Texto complementar no Visual Studio**

#### <a name="infotips"></a>InfoTips
 Geralmente, o texto de instrução pode ser muito longo para ser posicionado no local na interface do usuário ou pode ser útil apenas para novos usuários, como confusão para usuários experientes. Nesse caso, o texto instrutivo/informativo deve ser colocado como uma dica de ferramenta em um InfoTip.

 InfoTips deve ser posicionado próximo aos controles aos quais eles estão relacionados e deve usar o ícone de InfoTip específico, que é discreto, ainda perceptível.

 ![InfoTip no Visual Studio](../../extensibility/ux-guidelines/media/0601-d_infotip.png "0601-d_InfoTip")

 **Exemplo de um InfoTip no Visual Studio**

##### <a name="writing-style-rules-for-infotips"></a>Escrevendo regras de estilo para InfoTips

- Escrever InfoTips como sentenças completas. Eles exigem verbos específicos, maiúsculas e minúsculas e pontuação final.

- Use InfoTips para complementar sua instrução ou informações principais. Se você estiver usando apenas palavras diferentes para refazer a ideia principal, não precisará de um InfoTip.

- Mantenha o InfoTips curto e docente. Use palavras pequenas e linguagem simples e diária que suporte e incentiva o usuário.

- Siga as diretrizes da Microsoft existentes para texto e [estilo](/windows/desktop/uxguide/text-style-tone)de [interface do usuário](/windows/desktop/uxguide/text-ui) e Tom.

#### <a name="control-labels"></a>Rótulos de controle
 Os rótulos de controle devem ser curtos, concisos e seguir as [diretrizes de área de trabalho do Windows para controles](/windows/desktop/uxguide/controls).

 Para obter mais informações sobre o formato do rótulo de controle e o posicionamento na interface do usuário, consulte [layout do Visual Studio](../../extensibility/ux-guidelines/layout-for-visual-studio.md).

#### <a name="help-links"></a>Links de ajuda
 Os links de ajuda podem ser colocados no texto de instruções ou no corpo da interface do usuário. Eles podem ser links para ajudar ou iniciar caixas de diálogo internas.

##### <a name="visual-style-rules-for-help-links"></a>Regras de estilo visual para links de ajuda

- Use as cores de ambiente corretas para hiperlinks. Um hiperlink com estilo adequado não piscará brevemente quando for clicado. Se você vir isso, é uma indicação de que as cores do ambiente não estão sendo usadas.

- Sublinhados só devem ser usados em foco ou quando o link é inserido em um parágrafo.

- Para obter informações mais detalhadas sobre o Visual e estilos de interação para hiperlinks, consulte botões e hiperlinks.

##### <a name="writing-style-rules-for-help-links"></a>Escrevendo regras de estilo para links de ajuda

- Ao iniciar caixas de diálogo, mantenha os padrões para reticências: não há reticências para navegação, reticências se a tarefa exigir interface do usuário adicional.

     ![Link de ajuda no Visual Studio](../../extensibility/ux-guidelines/media/0601-e_helplink.png "0601-e_HelpLink")

     **Uma elipse (...) em um link de ajuda indica que a tarefa exigirá uma interface do usuário adicional.**

- Os links não devem começar com "Learn", pois isso não é a intenção do usuário. O usuário deseja responder a uma pergunta específica, não receber uma educação geral.

- A frase ajuda links para que eles façam a pergunta que o tópico responderá.

     Incorreto: "Saiba mais sobre o preço dos serviços móveis do Windows Azure"

     Correto: "quais opções de preços estão disponíveis para os serviços móveis do Windows Azure?"

- Nunca use *Click...* para o texto do link.

- Nunca vincule apenas a palavra "aqui". Isso é problemático para alguns leitores de tela, que receberão a voz apenas da palavra vinculada.

     Incorreto: "localizar informações sobre os serviços móveis do Windows Azure **aqui**"

     Correto: "quais opções de preços estão disponíveis para os serviços móveis do Windows Azure?"

- Para obter mais informações sobre o estilo de escrita correto para links de ajuda, consulte a [orientação da área de trabalho do Windows para obter ajuda](/windows/desktop/uxguide/winenv-help).

#### <a name="hint-text"></a>Texto de dica
 O texto de dica aparece como uma marca-d ' água dentro de um controle ou abaixo do controle. A formatação correta será aplicada usando o token VSColors apropriado, `Environment.GrayText` .

 Ele pode aparecer em vários formulários.

- No lugar do rótulo de controle:

     ![Captura de tela de um controle suspenso com texto de dica no lugar do rótulo de controle que lê "Pesquisar Gerenciador de Soluções (Ctrl +;)".](../../extensibility/ux-guidelines/media/0601-f_hinttext1.png "0601-f_HintText1")

- Com um verbo, fornecendo instruções:

     ![Captura de tela de uma caixa de texto com texto de dica no controle que lê "Insira seu nome".](../../extensibility/ux-guidelines/media/0601-g_hinttext2.png "0601-g_HintText2")

- Com texto indicando uma entrada necessária:

     ![Captura de tela de uma caixa de texto com texto de dica no controle que lê " \< obrigatório \> ".](../../extensibility/ux-guidelines/media/0601-h_hinttext3.png "0601-h_HintText3")

#### <a name="watermark-text"></a>Texto da marca d' água
 Em uma superfície de design vazia, o texto deve indicar o que fazer, bem como fornecer links para abrir outras janelas relacionadas, se apropriado:

 ![Texto de marca d' água no Visual Studio](../../extensibility/ux-guidelines/media/0601-i_watermarktext.png "0601-i_WatermarkText")

 **Exemplo de texto de marca d' água no Visual Studio**

### <a name="common-terminology"></a>Terminologia comum

|Termo|Explicação|Comentário|
|----------|-----------------|-------------|
|Entrar/sair|Os verbos usaram como sinônimos com a Web para representar a autenticação em uma propriedade da Web. Nos clientes, usamos isso uma vez como uma noção de nível superior para entrar e sair da conexão de usuário do IDE, que representa uma identidade de nível superior que fornece recursos de nível superior, como roaming e licenciamento que não estão disponíveis com todas as outras conexões.|O usuário do IDE é o único recurso que deve representar um verbo de entrada/saída, pois representa o usuário do IDE de nível superior.|
|Conectar/desconectar|Use em locais onde um recurso mantém uma única conexão com um serviço online.|Gerenciador de Servidores, em que você pode ter apenas uma conexão ativa do Azure por vez, é um exemplo de conectar/desconectar.|
|Adicionar/remover|Não destrutivo. Use ao adicionar ou remover algo de uma lista.|A caixa de diálogo lista de servidores do Gerenciador de conexões do TFS é um exemplo de adicionar/remover.|
|Excluir|Destrui. Use somente quando o elemento que está sendo removido for descartado permanentemente ou excluído do disco.|"Excluir" geralmente requer um prompt se o resultado estiver excluindo um arquivo do disco.|

## <a name="error-messages"></a>Mensagens de erro

### <a name="overview"></a>Visão geral
 Ocorreram erros. A definição de limitações sobre o que o usuário pode fazer é uma primeira etapa sensata na prevenção de mensagens de erro podem ser evitados. No entanto, quando ocorre um erro, uma mensagem de erro bem escrita pode dar um longo caminho para atenuar o problema. As mensagens de erro são, sem dúvida, um dos tipos mais importantes de notificação que o usuário vê, pois elas são síncronas e indicam um problema que precisa ser resolvido. Mensagens de erro mal gravadas deixam os usuários por conta própria para decidir a causa dos erros e de quaisquer soluções possíveis.

 Os usuários podem parar de prestar atenção às mensagens de erro mais usadas ou confusas; portanto, grave somente as mensagens necessárias que agregam valor à experiência do usuário. Se a mensagem for simplesmente uma notificação, use uma apresentação alternativa.

### <a name="rules-for-creating-an-error-message"></a>Regras para criar uma mensagem de erro

- Ao construir mensagens de erro, escolha o nível de erro apropriado para o público. Objetivo para resumos diretos que fornecem uma ação que o usuário pode tomar, se aplicável. Não declare nada que o usuário não precise saber.

- Forneça assistência construtivas. É mais fácil ler e agir em uma mensagem de erro que contém instruções.

- Não use negativos duplos.

- Realize uma verificação de gramática automatizada e manual e de ortografia em qualquer mensagem de erro que você escrever.

- Para mensagens de erro complexas, evite comunicações sequenciais. Nunca use uma conexão F1 para a mensagem de erro. A mensagem em si deve ser suficiente.

- Use o ícone correto.

- Faça perguntas fáceis de entender e Use botões com opções claras, como "excluir" e "Cancelar".

- Para avisos, fique claro sobre o que a consequência de continuar será. Os botões devem indicar a consequência.

- Para erros, descreva o que o usuário pode fazer para corrigir o problema. Os botões devem ser ações ou dizer "fechar". Não use um botão "OK" para uma mensagem de erro.

- Algumas perguntas a serem feitas ao construir uma mensagem de erro:

  - O usuário pode descobrir como resolver o problema com esse erro sozinho?

  - O usuário usa o mesmo vocabulário que esse erro?

  - Esse erro é ambigious ou compartilhado em várias situações? Em caso afirmativo, como você orienta os usuários para a solução de que precisam?

#### <a name="build-errors"></a>Erros de compilação
 Como o Visual Studio é uma ferramenta de desenvolvimento de software, muitos de seus componentes têm uma etapa de compilação, conversão ou codificação para converter o trabalho do desenvolvedor em formato binário. Essas conversões podem causar erros quando o compilador não pode processar arquivos criados incorretamente ou quando as opções do compilador não foram definidas corretamente.

 Os usuários do Visual Studio podem gastar um enorme número de horas de desenvolvimento Resolvendo erros de compilação. Esse tempo de resolução aumenta quando os erros têm dependências ou quando mensagens de erro são mal gravadas, o que pode dificultar a descoberta da origem do erro.

 Os melhores erros de compilação são aqueles que não ocorrem em primeiro lugar, motivo pelo qual o Visual Studio fornece preenchimento automático e linha ondulada do IntelliSense. Os validadores de esquema e ferramentas semelhantes fornecem o mesmo tipo de comentário. Esses mecanismos orientam proativamente o usuário a construir código bem formado, diminuindo a chance de erros de compilação.

 O Visual Studio fornece uma janela de ferramentas onde os usuários podem ler e navegar pelos erros que ocorreram em suas janelas de documentos. Os atalhos de teclado são fornecidos para que o usuário possa navegar rapidamente por grandes quantidades de código e ir diretamente para o local do problema. O Visual Studio também permite que cada erro de compilação seja vinculado a uma determinada palavra-chave/ID de contexto da ajuda para que o usuário possa ir diretamente para um tópico da ajuda que fornece informações mais detalhadas sobre o erro.

 Grave erros de Build claros e concisos:

- **Use linguagem simples** que explica o problema com pouco ou nenhum jargão do compilador. O texto de um erro de compilação não deve ser muito técnico.

- **Contorno de possíveis causas.** Por exemplo, "faltam dois-pontos entre a propriedade e o valor na declaração ' (Propriedade): (valor) '."

- Forneça detalhes sobre possíveis correções. Se não houver espaço suficiente, os detalhes adicionais poderão ser colocados no tópico da ajuda correspondente.

### <a name="components-of-a-well-written-error-message"></a>Componentes de uma mensagem de erro bem escrita

#### <a name="use-the-shell-dialog-service-for-error-messages"></a>Use o serviço de caixa de diálogo do Shell para mensagens de erro.
 O uso do serviço de diálogo do Shell permite controlar a aparência da mensagem, as fontes em particular, sem alterações importantes em elementos individuais. Use os mecanismos **IErrorInfo** e denuncie-os usando **IVsUIShell:: SetErrorInfo/ReportErrorInfo**.

#### <a name="choose-an-effective-and-appropriate-notification-presentation"></a>Escolha uma apresentação de notificação eficaz e apropriada.
 Use uma caixa de diálogo modal com um aviso crítico se uma ação imediata for necessária para evitar a perda de dados (notificação síncrona). Os ícones críticos são reservados para situações em que o fechamento da mensagem sem lê-la pode levar a consequências negativas. A perda de dados é uma situação crítica que requer uma resposta em nível de alarme. O uso excessivo do ícone crítico desensitizes os usuários à sua importância. Se a mensagem de erro for informativa por natureza, considere alternativas para uma caixa de diálogo modal (notificação assíncrona).

#### <a name="provide-a-clean-succinct-explanation-of-why-the-problem-occurred-rather-than-a-technical-explanation"></a>Forneça uma explicação clara e sucinta de por que o problema ocorreu em vez de uma explicação técnica.
 Sobrecarregar os usuários com detalhes técnicos na explicação irá torná-los mais prováveis de ignorar mensagens de erro. Exemplos de boas mensagens:

- "Não é possível abrir o arquivo solicitado".

- "Não é possível se conectar à Internet".

#### <a name="provide-information-about-how-to-fix-the-problem"></a>Forneça informações sobre como corrigir o problema.
 Ofereça ao usuário sugestões de como corrigir o problema. Seja honesto com o usuário se não houver nenhuma sugestão. Forneça links diretos para fontes online alternativas, como suporte técnico ou suporte da Comunidade. Tente apontar os usuários para informações online específicas pertinentes ao problema. Para obter uma ID de erro, considere vincular usuários a um thread de discussão sobre esse erro específico. Exemplos de boas mensagens:

- "Verifique se você está conectado à Internet e repita a operação."

- "Verifique se o arquivo existe e se você tem permissão para abri-lo".

#### <a name="write-a-message-that-is-short-and-to-the-point"></a>Escreva uma mensagem curta e até o ponto.
 Uma mensagem de erro pode notificar, explicar e oferecer uma solução, mas ainda será ignorada se for uma palavra muito grande. Uma solução é usar a divulgação progressiva com um botão detalhes. Por exemplo, dê uma breve descrição/solução e, em seguida, coloque mais detalhes em um botão detalhes. Se os usuários optarem por ler mais informações sobre o erro, eles poderão fazer isso.

 O idioma na mensagem deve ser:

- **Apropriado ao domínio.** Use o idioma que o usuário entenderá. Embora nossos clientes sejam desenvolvedores, eles geralmente não têm o contexto e a terminologia que temos.

- **Determinados.** Evite palavras vagas e forneça nomes específicos e locais de objetos envolvidos. Por exemplo, uma mensagem de erro como "caractere inválido" não é útil. Qual caractere? "Arquivo não encontrado." Qual arquivo?

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
