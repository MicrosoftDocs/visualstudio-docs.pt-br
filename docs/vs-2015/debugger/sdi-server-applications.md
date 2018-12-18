---
title: Aplicativos de servidor SDI | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- SDI server applications
- SDI server applications, debugging
ms.assetid: 09713718-1376-4753-b119-26f36639693e
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea0497c7d20c0102aff3bc77cdecf87d1525a82c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752393"
---
# <a name="sdi-server-applications"></a>Aplicativos de servidor SDI
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você estiver depurando um aplicativo de servidor SDI, você deve especificar `/Embedding` ou `/Automation` na **argumentos de linha de comando** propriedade no *projeto* caixa de diálogo páginas de propriedades para C/C++, c#, ou Projetos do Visual Basic.  
  
 Com esses argumentos de linha de comando, o depurador pode iniciar o aplicativo de servidor como se tivesse sido iniciado de um contêiner. Iniciar o contêiner do Gerenciador de Programas ou do Gerenciador de Arquivos fará com que o contêiner use a instância do servidor iniciada no depurador.  
  
## <a name="finding-the-command-line-arguments-property"></a>Localizando a propriedade Argumentos de Linha de Comando  
 Para acessar o *projeto* caixa de diálogo páginas de propriedades, clique em seu projeto no Gerenciador de soluções e escolha Propriedades no menu de atalho. Para localizar a propriedade Argumentos de linha de comando, expanda a categoria Propriedades de Configuração e clique na página Depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Depuração de COM e ActiveX](../debugger/com-and-activex-debugging.md)   
 [Como depurar servidores COM](../debugger/how-to-debug-com-servers.md)



