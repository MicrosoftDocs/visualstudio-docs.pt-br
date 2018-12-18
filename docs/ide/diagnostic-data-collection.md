---
title: Dados de diagnóstico e logs gerados pelo sistema
ms.date: 05/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
author: gewarren
ms.author: michma
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f55d8a0f32886ed477026e298ed2c8c5d6e26f16
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34478288"
---
# <a name="system-generated-logs-collected-by-visual-studio"></a>Logs gerados pelo sistema coletados pelo Visual Studio

O Visual Studio coleta logs gerados pelo sistema para corrigir problemas e melhorar a qualidade do produto por meio do [Programa de Aperfeiçoamento da Experiência do Usuário do Visual Studio](visual-studio-experience-improvement-program.md). Este artigo fornece algumas informações sobre os tipos de dados que coletamos e como eles são usados. Também fornece dicas sobre como os autores de extensão podem evitar a divulgação acidental de informações pessoais ou confidenciais.

## <a name="types-of-collected-data"></a>Tipos de dados coletados

O Visual Studio coleta logs gerados pelo sistema sobre falhas, travamentos, falta de resposta da interface do usuário e alto uso da CPU ou de memória. Também coletamos informações sobre os erros encontrados durante a instalação ou o uso do produto. Os dados coletados variam de acordo com o erro e podem incluir rastreamentos de pilha, despejos de memória e informações de exceção:

- Para alto uso da CPU e falta de resposta, são coletados rastreamentos de pilha de threads relevantes do Visual Studio.

- Para casos em que os rastreamentos de pilha de alguns threads não são suficientes para determinar a causa raiz do problema, por exemplo, falhas, travamentos ou alto uso de memória, coletamos um *despejo* de memória. O despejo representa o estado do processo durante o erro.

- Para condições de erro inesperadas, por exemplo, uma exceção ao tentar fazer uma gravação em um arquivo em disco, coletamos informações sobre a exceção. As informações incluem o nome da exceção, o rastreamento de pilha do thread no qual ocorreu a exceção, a mensagem associada à exceção e outras informações relevantes à exceção específica.

   O seguinte exemplo de dados coletados mostra um nome de exceção, um rastreamento de pilha e uma mensagem de exceção:

   ```text
   "Reserved.DataModel.Fault.Exception.TypeString": "System.IO.IOException",
   "Reserved.DataModel.Fault.Exception.StackTrace": "System.IO.__Error.WinIOError(Int32,String)\r\n
   System.IO.FileStream.Init(String,FileMode,FileAccess,Int32,Boolean,FileShare,Int32,FileOptions,SECURITY_ATTRIBUTES,String,Boolean,Boolean,Boolean)\r\n
   System.IO.FileStream..ctor(String,FileMode,FileAccess,FileShare,Int32,FileOptions,String,Boolean,Boolean,Boolean)\r\nSystem.IO.StreamWriter.CreateFile(String,Boolean,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean,Encoding,Int32,Boolean)\r\n
   System.IO.StreamWriter..ctor(String,Boolean)\r\n
   System.IO.File.CreateText(String)\r\n
   Microsoft.VisualStudio.Setup.Services.FileSystem.CreateText(String,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.WriteChannelManifest(IChannelManifest,String,String)\r\n
   Microsoft.VisualStudio.Setup.Cache.ChannelManifestRepository.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.Cache.CacheManager.AddChannel(ChannelManifestPair,Boolean)\r\n
   Microsoft.VisualStudio.Setup.ChannelManager.\<UpdateAsync>d__37.MoveNext()\r\n”,
   "Reserved.DataModel.Fault.Exception.Message": " The process cannot access the file 'C:\\Users\\[UserName]\\AppData\\Local\\Microsoft\\VisualStudio\\Packages\\_Channels\\4CB340F5\\channelManifest.json' because it is being used by another process."
   ```

## <a name="how-we-use-system-generated-logs"></a>Como usamos os logs gerados pelo sistema

O fluxo de trabalho para determinar a causa raiz do erro varia conforme o tipo de erro e sua severidade.

### <a name="error-classification"></a>Classificação de erros

Com base nos logs, os erros são classificados e contados a fim de priorizar sua investigação. Por exemplo, podemos descobrir que “System.IO.\__Error.WinIOError” em “System.IO.FileStream.Init” ocorreu 500 vezes na versão \<x> do produto, e tem a maior taxa de ocorrência nessa versão.

### <a name="work-items-for-tracking"></a>Itens de trabalho para acompanhamento

Itens de trabalho para erros individuais priorizados são criados e atribuídos aos engenheiros para investigação. Esses itens de trabalho normalmente contêm informações de classificação, prioridade e diagnóstico relevantes ao tipo de erro. Essas informações são obtidas dos logs gerados pelo sistema coletados sobre o erro. Por exemplo, um item de trabalho sobre uma falha pode conter o rastreamento de pilha no qual a falha está ocorrendo.

### <a name="error-investigation"></a>Investigação de erros

Os engenheiros usam as informações disponíveis em um item de trabalho para determinar a causa de um erro. Em alguns casos, eles precisam de mais informações do que está presente no item de trabalho; nesse caso, eles se referem ao log original gerado pelo sistema que foi coletado. Por exemplo, um engenheiro pode inspecionar um despejo de memória para entender uma falha de produto.

## <a name="tips-for-extension-authors"></a>Dicas para autores de extensão

Os autores de extensão devem limitar a exposição de informações pessoais não usando informações pessoais ou outras informações confidenciais nos nomes de módulos, tipos e métodos. Em caso de falha ou condição de erro semelhante com esse código na pilha, essas informações são coletadas como parte dos logs gerados pelo sistema.

## <a name="opt-out-of-data-collection"></a>Recusar a coleta de dados

Considerando a finalidade dos dados que coletamos e as restrições de acesso e retenção, recomendamos que você use as configurações de privacidade padrão para o Visual Studio e o Windows. No entanto, você pode [recusar](../ide/visual-studio-experience-improvement-program.md#opt-in-or-out) o Programa de Aperfeiçoamento da Experiência do Visual Studio. Para recusar a coleta de logs gerados pelo sistema para todos os programas, confira [Diagnóstico, comentários e privacidade no Windows 10](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy). As opções podem variar de acordo com a versão do Windows que você está usando.

## <a name="see-also"></a>Consulte também

- [Programa de Aperfeiçoamento da Experiência do Usuário do Visual Studio](visual-studio-experience-improvement-program.md)
- [Diagnóstico, comentários e privacidade no Windows 10](https://privacy.microsoft.com/windows-10-feedback-diagnostics-and-privacy)