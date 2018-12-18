---
title: Práticas recomendadas para implementar um plug-in de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5bcbe41bc0b5cd6c348463426fe8bb97a38ac308
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742351"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>Práticas recomendadas para implementar um plug-in de controle do código-fonte
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os seguintes detalhes técnicos podem ajudá-lo com confiança implementar um plug-in de controle de fonte [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="memory-management-issues"></a>Problemas de gerenciamento de memória  
 Na maioria dos casos, o ambiente de desenvolvimento integrado (IDE), que é o chamador, libera e aloca memória. O plug-in de controle de origem retorna cadeias de caracteres e outros itens em buffers alocados pelo chamador. As exceções são observadas nas descrições de funções específicas em que eles ocorrem.  
  
## <a name="arrays-of-file-names"></a>Matrizes de nomes de arquivo  
 Quando uma matriz de arquivos for passada, ele não é passado como uma matriz de nomes de arquivo de contígua. Ele é passado como uma matriz de ponteiros para nomes de arquivo. Por exemplo, nos [SccGet](../extensibility/sccget-function.md), os nomes de arquivo são passados pela `lpFileNames` parâmetro, onde `lpFileNames` é, na verdade, um ponteiro para um `char **`. `lpFileNames`[0] é um ponteiro para o primeiro nome, `lpFileNames`[1] é um ponteiro para o nome do segundo e assim por diante.  
  
## <a name="large-model"></a>Modelo grande  
 Todos os ponteiros são de 32 bits, mesmo em sistemas operacionais de 16 bits.  
  
## <a name="fully-qualified-paths"></a>Caminhos totalmente qualificados  
 Em que os nomes de arquivos ou diretórios são especificados como argumentos, eles devem ser caminhos totalmente qualificados ou caminhos UNC, sem barras invertidas finais. É responsabilidade do controle de fonte de plug-in para traduzir para caminhos relativos, se o que é um requisito de sistema de controle de origem subjacente.  
  
## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>Especifique um caminho totalmente qualificado para a DLL registrada  
 O IDE não mais carrega DLLs de caminhos relativos (por exemplo,.\NewProvider.dll). Deve ser especificado um caminho completo da DLL (por exemplo, C:\Providers\NewProvider.dll). Esse requisito reforça a segurança do IDE, impedindo que o carregamento de DLLs de controle de origem de não autorizado ou delegadas.  
  
## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>Procure um existente VSSCI plug-in quando você instala o plug-in de controle de origem  
 Um usuário que planeja instalar o plug-in de controle de origem talvez já tenha um código-fonte controle existente plug-in instalado no computador. O programa de instalação (instalação) para o plug-in que você criar deve determinar se há valores existentes para as chaves de registro relevantes. Se essas chaves já estiverem definidas, seu programa de instalação deve perguntar ao usuário se registre seu plug-in como o controle de fonte padrão plug-in e substituir aquele que já está instalado.  
  
## <a name="error-result-codes-and-reporting"></a>Códigos de resultado de erro e emissão de relatórios  
 O `SCC_OK` retornar o código para uma função de controle do código-fonte indica que a operação foi bem-sucedida para todos os arquivos. Se a operação falhar, ele deve retornar o último código de erro.  
  
 A regra para emissão de relatórios é que, se ocorrer um erro no IDE, o IDE é responsável por relatá-las. Se ocorrer um erro no sistema de controle de origem, o plug-in de controle do código-fonte é responsável por relatá-las. Por exemplo, "nenhum arquivo está atualmente selecionado" seria informado pelo IDE, ao passo que "Este arquivo já fez check-out" seria informada pelo plug-in.  
  
## <a name="the-context-structure"></a>A estrutura de contexto  
 Durante a chamada para o [SccInitialize](../extensibility/sccinitialize-function.md), o chamador passa a `ppvContext` parâmetro, que é um identificador não inicializado para um nulo. O plug-in de controle do código-fonte pode ignorar esse parâmetro ou pode alocar uma estrutura de qualquer tipo e colocam um ponteiro para essa estrutura no ponteiro passado. O IDE não compreende essa estrutura, mas ele passa um ponteiro para essa estrutura em todas as outras chamadas no plug-in. Isso fornece informações de cache de um contexto valioso para o plug-in que ele pode usar para manter informações de estado global que persiste entre chamadas de função sem o uso de variáveis globais. O plug-in é responsável por liberar a estrutura em uma chamada para o [SccUninitialize](../extensibility/sccuninitialize-function.md).  
  
 Se os conjuntos de plug-in a `SCC_CAP_REENTRANT` bit na [SccInitialize](../extensibility/sccinitialize-function.md) (especificamente, no `lpSccCaps` parâmetro), várias estruturas de contexto são usadas para acompanhar todos os projetos que estão abertos.  
  
## <a name="bitflags-and-other-command-options"></a>Sinalizadores de bit e outras opções de comando  
 Para cada comando, como o [SccGet](../extensibility/sccget-function.md), o IDE pode especificar várias opções que alteram o comportamento do comando.  
  
 A API dá suporte a configuração de determinadas opções pelo IDE através de `fOptions` parâmetro. Essas opções são descritas em [sinalizadores de bit usados por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md) junto com os comandos que afetam a eles. Em geral, estas são opções para o qual o usuário não será avisado.  
  
 Mais opções de configuração configurável pelo usuário não são definidas dessa maneira, porque eles variam amplamente entre plug-ins de controle de origem. Portanto, o mecanismo recomendado é um **avançado** botão. Por exemplo, na **Obtenha** caixa de diálogo, o IDE exibirá apenas as informações que ele entende, mas ele também exibe um **avançado** botão se o plug-in tem opções para este comando. Quando o usuário clica o **Advanced** botão, as chamadas IDE a [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) para habilitar o plug-in para solicitar ao usuário informações, como os sinalizadores de bit ou um valor de data/hora de controle do código-fonte. O plug-in retorna essas informações em uma estrutura que é passada de volta durante o `SccGet` comando.  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)   
 [Criar um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md)

