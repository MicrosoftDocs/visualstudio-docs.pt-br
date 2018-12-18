---
title: Visual C++ IntelliSense | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9d7c6414-4e6c-4889-a74c-a6033795eccc
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ced999c20678cc64dc5f96e86070b5f39d5ca2c7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49881671"
---
# <a name="visual-c-intellisense"></a>Visual C++ IntelliSense
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio 2015, o IntelliSense está disponível para arquivos de código único, bem como para arquivos em projetos. Em projetos de plataforma cruzada, alguns recursos do IntelliSense estão disponíveis nos arquivos .cpp e .c no projeto de código compartilhado mesmo quando você está em um contexto Android ou iOS.  
  
## <a name="intellisense-features-in-c"></a>Recursos do IntelliSense em C++  
 IntelliSense é um nome dado a um conjunto de recursos que tornam a codificação mais conveniente. Uma vez que pessoas diferentes têm ideias diferentes sobre o que é conveniente, praticamente todos os recursos do IntelliSense podem ser habilitados ou desabilitados na página de propriedades do **Editor de Texto, C/C++, Avançado**.  
  
 ![Ferramentas, Opções, Editor de Texto, C&#47;C&#43;&#43;, Avançado](../ide/media/sintellisensecpptoolsoptions.PNG "sIntelliSenseCppToolsOptions")  
  
 Você pode usar os itens de menu e os atalhos de teclado mostrados na imagem a seguir para acessar o IntelliSense.  
  
 ![Menu Visual C&#43;&#43; IntelliSense](../ide/media/vs2015-cpp-intellisense-menu.png "vs2015_cpp_intellisense_menu")  
  
### <a name="statement-completion-and-member-list"></a>Lista de membro e preenchimento de declaração  
 Quando você começa a digitar uma palavra-chave, um tipo, uma função, um nome de variável ou outro elemento de programa que o compilador reconhece, o editor se oferece para completar a palavra para você  
  
 Para obter uma lista de ícones e seus significados, consulte [Modo de Exibição de Classe e ícones do Pesquisador de Objetos](../ide/class-view-and-object-browser-icons.md).  
  
 ![Janela Completar Palavra do Visual CC&#43;&#43;](../ide/media/vs2015-cpp-complete-word.png "vs2015_cpp_complete_word")  
  
 Na primeira vez que a lista de membros é invocada, ela mostra apenas membros acessíveis para o contexto atual. Se você usar **Ctrl+J** depois disso, ela mostrará todos os membros, independentemente da acessibilidade. Se você invocá-la uma terceira vez, uma lista ainda maior de elementos do programa será mostrada. Você pode desligar o preenchimento de declaração na página **Opções Gerais do C/C++**.  
  
 ![Lista de membros do Visual C&#43;&#43;](../ide/media/vs2015-cpp-list-members.png "vs2015_cpp_list_members")  
  
### <a name="parameter-help"></a>Ajuda do Parâmetro  
 Quando você digita uma chave de abertura de uma chamada de função ou colchete angular em uma declaração de variável de modelo de classe, o editor mostra uma pequena janela com tipos de parâmetro para cada sobrecarga da função ou do construtor. O parâmetro "atual", com base no local do cursor, está em negrito. Você pode desligar o preenchimento de declaração na página **Opções Gerais do C/C++**.  
  
 ![Ajuda de Parâmetro do Visual C&#43;&#43;](../ide/media/vs-2015-cpp-param-help.png "vs_2015_cpp_param_help")  
  
### <a name="quick-info"></a>Informação Rápida  
 Quando você passa o cursor do mouse sobre uma variável, aparece uma pequena janela embutida que mostra as informações de tipo e o cabeçalho no qual o tipo é definido. Passe o cursor do mouse sobre uma chamada de função para ver a assinatura da função. Você pode desligar Informações Rápidas na página **Editor de Texto, C/C++, Avançado**.  
  
 ![Informações Rápidas do Visual C&#43;&#43;](../ide/media/vs2015-cpp-quickinfo.png "vs2015_cpp_quickInfo")  
  
## <a name="error-squiggles"></a>Linhas onduladas de erro  
 Linhas onduladas em um elemento de programa (variável, palavra-chave, chave, nome do tipo e assim por diante) chamam a atenção para um erro ou erro em potencial no código. Uma linha ondulada verde é exibida quando você escreve uma declaração de encaminhamento para lembrá-lo de que você ainda precisa escrever a implementação. Uma linha ondulada roxa aparece em um projeto compartilhado quando há um erro no código que não está ativo no momento, por exemplo, quando você está trabalhando no contexto do Windows, mas digita algo que seria um erro em um contexto do Android. Uma linha ondulada vermelha indica um erro do compilador ou aviso no código ativo que você precisa resolver.  
  
 ![Linhas onduladas de erro do Visual C&#43;&#43;](../ide/media/vs2015-cpp-error-quiggles.png "vs2015_cpp_error_quiggles")  
  
## <a name="code-colorization-and-fonts"></a>Colorização e fontes de código  
 As fontes e cores padrão podem ser alteradas usando a página de propriedades **Ambiente, Fontes e Cores**. Você pode alterar as fontes para muitas janelas da interface do usuário aqui, não apenas para o editor. As configurações específicas do C++ começam com "C++"; as outras configurações são para todas as linguagens.  
  
## <a name="cross-platform-intellisense"></a>IntelliSense de plataforma cruzada  
 Em um projeto de código compartilhado, alguns recursos do IntelliSense, como linhas onduladas, estão disponíveis, mesmo quando você está trabalhando em um contexto Android. Se você escrever algum código que resultaria em um erro em um projeto inativo, o IntelliSense ainda mostrará linhas onduladas, mas elas estarão em uma cor diferente das linhas onduladas para erros no contexto atual.  
  
 Há um aplicativo OpenGLES configurado para compilar para Android e iOS. A ilustração mostra o código compartilhado que está sendo editado. Na primeira imagem, Android é o projeto ativo:  
  
 ![O projeto Android é o projeto ativo.](../ide/media/intellisensecppcrossplatform.png "IntelliSenseCppCrossPlatform")  
  
 Observe o seguinte:  
  
- O # ramificação else na linha 8 é esmaecida para indicar a região inativa, pois `__ANDROID__` é definido para o projeto Android.  
  
- A variável de saudação na linha 11 é inicializada com o identificador HELLO, que tem uma linha ondulada roxa. Isso ocorre porque nenhum identificador HELLO é definido no projeto iOS atualmente inativo. Embora a linha 11 fosse compilada no projeto Android, ela não seria no iOS. Uma vez que esse é um código compartilhado, que é algo que você deve alterar, embora ele compile na configuração ativa no momento.  
  
- A Linha 12 tem linha ondulada vermelha no identificador BYE; esse identificador não está definido no projeto ativo atualmente selecionado.  
  
  Agora, altere o projeto ativo para iOS.StaticLibrary e observe como as linhas onduladas mudam.  
  
  ![iOS está selecionado como o projeto ativo.](../ide/media/intellisensecppcrossplatform2.png "IntelliSenseCppCrossPlatform2")  
  
  Observe o seguinte:  
  
- A ramificação #ifdef na linha 6 é esmaecida para indicar a região inativa, pois *_ANDROID\\*  \_ não está definido para o projeto do iOS.  
  
- A variável de saudação na linha 11 é inicializada com o identificador HELLO, que agora tem uma linha ondulada vermelha. Isso ocorre porque nenhum identificador HELLO está definido no projeto iOS inativo no momento.  
  
- A linha 12 tem linha ondulada roxa no identificador BYE; esse identificador não está definido no projeto Android.NativeActivity inativo no momento.  
  
## <a name="single-file-intellisense"></a>IntelliSense de arquivo único  
 Ao abrir um arquivo único fora de qualquer projeto, você ainda obtém o IntelliSense. Você pode habilitar ou desabilitar determinados recursos indo para **Editor de Texto, C/C++, Avançado** para ativar ou desativar recursos do IntelliSense. Para configurar o IntelliSense para arquivos únicos que não fazem parte de um projeto, procure **IntelliSense e navegação para arquivos que não são de projeto** na seção **Avançado**. Consulte [Tour guiado do Visual C++](http://msdn.microsoft.com/en-us/499cb66f-7df1-45d6-8b6b-33d94fd1f17c).  
  
 ![IntelliSense de arquivo único do Visual C&#43;&#43;](../ide/media/vs2015-cpp-single-file-intellisense.png "vs2015_cpp_single_file_intellisense")  
  
 Por padrão, IntelliSense de arquivo único usa apenas diretórios de inclusão padrão para localizar arquivos de cabeçalho. Para adicionar mais diretórios, abra o menu de atalho no nó Solução e adicione seu diretório à lista **Depurar Código-Fonte**, como mostra a ilustração a seguir:  
  
 ![Adicionando um caminho a um arquivo de cabeçalho.](../ide/media/intellisensedebugyourcode.jpg "IntelliSenseDebugYourCode")  
  
## <a name="see-also"></a>Consulte também  
 [Usando o IntelliSense](../ide/using-intellisense.md)



