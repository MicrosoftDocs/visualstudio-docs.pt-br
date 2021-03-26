---
title: Implementando um plug-in de controle do código-fonte-práticas recomendadas
description: Examine esses detalhes técnicos para ajudá-lo a implementar de forma confiável um plug-in de controle do código-fonte no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, best practices
- best practices, source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: 85e73b73-29dc-464f-8734-ed308742c435
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d64f195d13aca75b3b037ff14401395c03bd3d29
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097351"
---
# <a name="best-practices-for-implementing-a-source-control-plug-in"></a>Práticas recomendadas para implementar um plug-in de controle do código-fonte
Os detalhes técnicos a seguir podem ajudá-lo a implementar de maneira confiável um plug-in de controle do código-fonte no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

## <a name="memory-management-issues"></a>Problemas de gerenciamento de memória
 Na maioria dos casos, o IDE (ambiente de desenvolvimento integrado), que é o chamador, libera e aloca memória. O plug-in de controle do código-fonte retorna cadeias de caracteres e outros itens em buffers alocados pelo chamador. As exceções são observadas em descrições de funções específicas em que ocorrem.

## <a name="arrays-of-file-names"></a>Matrizes de nomes de arquivo
 Quando uma matriz de arquivos é passada, ela não é passada como uma matriz contígua de nomes de arquivo. Ele é passado como uma matriz de ponteiros para nomes de arquivo. Por exemplo, no [SccGet](../extensibility/sccget-function.md), os nomes de arquivo são passados pelo `lpFileNames` parâmetro, onde `lpFileNames` é, na verdade, um ponteiro para um `char **` . `lpFileNames`[0] é um ponteiro para o primeiro nome, `lpFileNames` [1] é um ponteiro para o segundo nome e assim por diante.

## <a name="large-model"></a>Modelo grande
 Todos os ponteiros são 32 bits, mesmo em sistemas operacionais de 16 bits.

## <a name="fully-qualified-paths"></a>Caminhos totalmente qualificados
 Quando os nomes de arquivo ou diretórios são especificados como argumentos, eles devem ser caminhos totalmente qualificados ou caminhos UNC, sem as barras invertidas finais. É responsabilidade do plug-in de controle do código-fonte para traduzi-los para caminhos relativos, se isso for um requisito do sistema de controle do código-fonte subjacente.

## <a name="specify-a-fully-qualified-path-for-the-registered-dll"></a>Especifique um caminho totalmente qualificado para a DLL registrada
 O IDE não carrega mais DLLs de caminhos relativos (por exemplo, *.\NewProvider.dll*). Um caminho completo da DLL deve ser especificado (por exemplo, *C:\Providers\NewProvider.dll*). Esse requisito reforça a segurança do IDE, impedindo o carregamento de DLLs de controle do código-fonte não autorizadas ou representadas.

## <a name="check-for-an-existing-vssci-plug-in-when-you-install-your-source-control-plug-in"></a>Verificar um plug-in VSSCI existente ao instalar o plug-in de controle do código-fonte
 Um usuário que planeja instalar seu plug-in de controle do código-fonte pode já ter um plug-in de controle do código-fonte existente instalado no computador. O programa de instalação (instalação) do plug-in que você cria deve determinar se há valores existentes para as chaves de registro relevantes. Se essas chaves já estiverem definidas, o programa de instalação deverá solicitar ao usuário que Registre seu plug-in como o plug-in de controle do código-fonte padrão e substitua aquele que já está instalado.

## <a name="error-result-codes-and-reporting"></a>Relatórios e códigos de resultado de erro
 O `SCC_OK` código de retorno para uma função de controle do código-fonte indica que a operação foi bem-sucedida para todos os arquivos. Se a operação falhar, espera-se retornar o último código de erro encontrado.

 A regra de relatório é que, se ocorrer um erro no IDE, o IDE será responsável por reportá-lo. Se ocorrer um erro no sistema de controle do código-fonte, o plug-in de controle do código-fonte será responsável por reportá-lo. Por exemplo, **nenhum arquivo está selecionado no momento** seria relatado pelo IDE, enquanto que o **check-out já foi** reportado pelo plug-in.

## <a name="the-context-structure"></a>A estrutura de contexto
 Durante a chamada para o [SccInitialize](../extensibility/sccinitialize-function.md), o chamador passa o `ppvContext` parâmetro, que é um identificador não inicializado para um void. O plug-in de controle do código-fonte pode ignorar esse parâmetro ou pode alocar uma estrutura de qualquer tipo e colocar um ponteiro para essa estrutura no ponteiro passado. O IDE não entende essa estrutura, mas passa um ponteiro para essa estrutura em todas as outras chamadas no plug-in. Isso fornece informações valiosas de cache de contexto para o plug-in que ele pode usar para manter as informações de estado global que persistem entre chamadas de função sem usar variáveis globais. O plug-in é responsável por liberar a estrutura em uma chamada para o [SccUninitialize](../extensibility/sccuninitialize-function.md).

 Se o plug-in definir o `SCC_CAP_REENTRANT` bit no [SccInitialize](../extensibility/sccinitialize-function.md) (especificamente, no `lpSccCaps` parâmetro), várias estruturas de contexto serão usadas para rastrear todos os projetos que estão abertos.

## <a name="bitflags-and-other-command-options"></a>Bitflags e outras opções de comando
 Para cada comando, como o [SccGet](../extensibility/sccget-function.md), o IDE pode especificar muitas opções que alteram o comportamento do comando.

 A API dá suporte à configuração de determinadas opções pelo IDE por meio do `fOptions` parâmetro. Essas opções são descritas em [Bitflags usadas por comandos específicos](../extensibility/bitflags-used-by-specific-commands.md) junto com os comandos que eles afetam. Em geral, essas são opções para as quais o usuário não será solicitado.

 A maioria das opções de configuração configuráveis pelo usuário não são definidas dessa maneira, pois elas variam muito entre os plug-ins de controle do código-fonte. Portanto, o mecanismo recomendado é um botão **avançado** . Por exemplo, na caixa de diálogo **obter** , o IDE exibe apenas as informações que ele entende, mas também exibe um botão **avançado** se o plug-in tiver opções para esse comando. Quando o usuário clica no botão **avançado** , o IDE chama o [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md) para habilitar o plug-in de controle do código-fonte para solicitar informações ao usuário, como bitflags ou uma data/hora. O plug-in retorna essas informações em uma estrutura que é passada de volta durante o `SccGet` comando.

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [Criar um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md)
