---
title: 'Como: exibir documentos de Script | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Script Explorer
ms.assetid: 8b621e53-4508-4b4a-9995-70995b0b9ac8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5bfa273f98cebdf61f865e03a02c9b2d5f22bfa9
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31474723"
---
# <a name="how-to-view-script-documents"></a>Como exibir documentos de script
Em versões anteriores do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], os arquivos de script do lado do cliente gerados do script do lado do servidor eram exibidos na janela Explorador de Script. A janela Explorador de Script estava geralmente oculta, de modo que a disponibilidade de script do lado do cliente não era sempre óbvia.  
  
 No [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)], os arquivos de script do lado do cliente gerados do script do lado do servidor aparecem no Gerenciador de Soluções, que é visível por padrão. A janela Explorador de Script foi eliminada.  
  
 Os arquivos de script do lado do cliente são visíveis apenas quando você está no modo de depuração ou modo de interrupção. Eles aparecem no **documentos de Script** nó.  
  
 Os arquivos de script do lado do servidor são sempre visíveis. Eles aparecem no  **\<nome de caminho do site >** nó. O nome do nó é semelhante a este exemplo: `c:\...\Website2\`  
  
### <a name="to-view-a-server-side-script-document"></a>Para exibir um documento de script do lado do servidor  
  
1.  Em **Solution Explorer**, abra o  **\<nome de caminho do site >** nó.  
  
2.  Clique duas vezes no arquivo de script que deseja exibir.  
  
     O arquivo de script do lado do servidor é aberto em uma janela de origem.  
  
### <a name="to-view-a-client-side-script-document"></a>Para exibir um documento de script do lado do cliente  
  
1.  Em **Solution Explorer**, abra o **documentos de Script** nó.  
  
2.  Clique duas vezes no arquivo de script que deseja exibir.  
  
     O arquivo de script do lado do cliente é aberto em uma janela de origem.  
  
## <a name="see-also"></a>Consulte também  
 [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)