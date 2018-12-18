---
title: Solucionando problemas de snippets | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IntelliSense Code Snippets, troubleshooting
- troubleshooting IntelliSense Code Snippets
- troubleshooting Visual Basic, IntelliSense Code Snippets
ms.assetid: 7b6dd40e-2f78-4b50-8e68-41fac1bcb81e
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4fff2767c962cf6899840e54bff798bae1f9e202
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49304805"
---
# <a name="troubleshooting-snippets"></a>Solucionando problemas de snippets
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Normalmente, problemas com snippets de código IntelliSense são causados por dois problemas: um arquivo de snippet corrompido ou conteúdo inválido no arquivo de snippet.  
  
## <a name="common-problems"></a>Problemas comuns  
  
### <a name="the-snippet-cannot-be-dragged-from-file-explorer-to-a-visual-studio-source-file"></a>O snippet não pode ser arrastado do Explorador de Arquivos para um arquivo de origem do Visual Studio  
  
-   Talvez o XML no arquivo de snippet esteja corrompido. O **Editor XML** em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pode localizar problemas na estrutura XML.  
  
-   Talvez o arquivo de snippet pode não estar em conformidade com o esquema de snippet. O **Editor XML** em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] pode localizar problemas na estrutura XML.  
  
### <a name="the-code-has-compiler-errors-that-are-not-highlighted"></a>O código tem erros de compilador que não estão realçados  
  
-   Talvez esteja faltando uma referência de projeto. Examine a documentação sobre o snippet. Se a referência não for encontrada no computador, será necessário instalá-la. Inserir um snippet deve adicionar ao projeto quaisquer referências necessárias. Se o snippet estiver sem as informações de referência, isso pode ser relatado ao criador do snippet como um erro.  
  
-   Talvez uma variável esteja indefinida. Variáveis indefinidas em um snippet devem ser realçadas. Caso contrário, isso pode ser relatado ao criador do snippet como um erro.  
  
## <a name="see-also"></a>Consulte também  
 [Snippets de código](../ide/code-snippets.md)



