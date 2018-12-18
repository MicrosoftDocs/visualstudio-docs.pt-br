---
title: Como limitar a instrumentação a funções específicas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, limiting instrumentation to functions
ms.assetid: bd98d6bf-2560-4eba-b063-2facb09f87c4
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 042ef6ef7a562f03f84184a86944a93f99c1d13e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49815150"
---
# <a name="how-to-limit-instrumentation-to-specific-functions"></a>Como limitar a instrumentação a funções específicas
Você pode limitar a instrumentação e a coleta de dados a uma ou mais funções ao definir opções na página **Avançado** da **Sessão de Desempenho** ou nas páginas de propriedades de binário de destino:  
  
- Se você especificar as funções na página de propriedades de sessão de desempenho, somente aquelas funções serão instrumentadas em todos os binários instrumentados da sessão.  
  
- Se você especificar as funções na página de propriedades de um binário de destino, apenas as funções que estão naquele binário específico serão instrumentadas. As funções em outros binários do desempenho são instrumentadas como de costume.  
  
  Só há suporte para limitar a coleta de dados dessa maneira quando o método de criação de perfil de instrumentação está selecionado.  
  
> [!NOTE]
>  Você também pode usar a página **Avançado** das páginas de propriedades da **Sessão de Desempenho** para definir outras opções que estão disponíveis para as ferramentas de instrumentação de linha de comando das Ferramentas de Criação de Perfil [VSInstr](../profiling/vsinstr.md).  
  
### <a name="to-limit-instrumentation-to-specific-functions-in-a-performance-session"></a>Para limitar a instrumentação a funções específicas em uma sessão de desempenho  
  
1. No **Gerenciador de Desempenho**, clique com o botão direito do mouse no nome da sessão e, em seguida, clique em **Propriedades**.  
  
    A caixa de diálogo **Páginas de Propriedades** é exibida.  
  
2. Na caixa de diálogo **Páginas de Propriedades**, clique em **Avançado**.  
  
3. Na caixa de texto **Opções de instrumentação adicionais**, use a seguinte sintaxe para digitar o nome das funções que você deseja instrumentar:  
  
    **/include:** `FuncSpec` **[;** `FuncSpec` **]** `...`  
  
    `FuncSpec` é o nome do namespace e da função. Ele tem o formato `Namespace`**::**`FunctionName`. Use um ponto e vírgula para separar várias funções. Use um asterisco (\*) para especificar um curinga para um ou mais caracteres. Por exemplo, **/include:MyNS::\\*** especifica todas as funções no namespace MyNS.  
  
   > [!NOTE]
   >  Para listar as funções em um binário, abra uma janela de prompt de comando no diretório de instalação das Ferramentas de Criação de Perfil (normalmente, o diretório \Team Tools\Performance Tools no diretório de instalação do [!INCLUDE[vsprvsts](../code-quality/includes/vsprvsts_md.md)]) e, em seguida, digite **vsinstr /DumpFuncs**  
  
### <a name="to-limit-instrumentation-to-specific-functions-in-a-binary"></a>Para limitar a instrumentação a funções específicas em um binário  
  
1. No **Gerenciador de Desempenho**, localize o nome do binário no nó **Destinos** da sessão de desempenho.  
  
2. Clique com botão direito do mouse no nome do binário e, em seguida, clique em **Propriedades**.  
  
    A caixa de diálogo **Páginas de Propriedades** é exibida.  
  
3. Na caixa de diálogo **Páginas de Propriedades**, clique em **Avançado**.  
  
4. Na caixa de texto **Opções de instrumentação adicionais**, use a seguinte sintaxe para digitar o nome das funções que você deseja instrumentar:  
  
    **/include:** `FuncSpec` **[;** `FuncSpec` **]** `...`  
  
    `FuncSpec` é o nome do namespace e da função. Ele tem o formato `Namespace`**::**`FunctionName`. Use um ponto e vírgula para separar várias funções. Use um asterisco (\*) para especificar um curinga para um ou mais caracteres. Por exemplo, **/include:MyNS::\\*** especifica todas as funções no namespace MyNS.  
  
   > [!NOTE]
   >  Para listar as funções em um binário, abra uma janela de prompt de comando no diretório de instalação das Ferramentas de Criação de Perfil (normalmente, o diretório \Team Tools\Performance Tools no diretório de instalação do [!INCLUDE[vsprvsts](../code-quality/includes/vsprvsts_md.md)]) e, em seguida, digite **vsinstr /DumpFuncs**  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de dados de controle](../profiling/controlling-data-collection.md)   
 [Como limitar a instrumentação a DLLs específicas](../profiling/how-to-limit-instrumentation-to-specific-dlls.md)   
 [Como especificar opções de instrumentação adicionais](../profiling/how-to-specify-additional-instrumentation-options.md)