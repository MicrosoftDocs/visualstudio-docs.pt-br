---
title: 'Erro: O servidor Web foi bloqueado e está bloqueando o verbo DEBUG | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.webdbg_debug_verb_blocked
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 9c8c4812-17db-484d-9c1b-ffd9e3bfef5a
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b85efc44b39485476154d0f41f3261b2aeb1ea7c
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60047196"
---
# <a name="error-the-web-server-has-been-locked-down-and-is-blocking-the-debug-verb"></a>Erro: O servidor Web foi bloqueado e está bloqueando o verbo DEBUG
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Falha ao entrar em um aplicativo Web ou serviço Web XML porque a ferramenta de bloqueio do IIS foi executada e URLScan foi instalado e ativado. Esta condição impede o IIS de receber o verbo DEBUG.  
  
 URLScan é uma ferramenta de segurança que funciona em conjunto com a Ferramenta de Bloqueio do IIS para dar a administradores de site do IIS a capacidade de desativar recursos desnecessários e restringir o tipo de solicitações HTTP que o servidor processará. Ao bloquear solicitações HTTP específicas, a ferramenta de segurança de URLScan impede que as solicitações potencialmente perigosas alcancem o servidor e causem dano.  
  
 Se o seu aplicativo estiver sendo executado no IIS 6.0 no Windows Server 2003, você não precisará executar a ferramenta de bloqueio do IIS porque o IIS 6.0 fornece a mesma funcionalidade.  
  
### <a name="to-enable-debugging-on-a-web-server-with-urlscan-installed"></a>Para habilitar a depuração em um servidor Web com URLScan instalado  
  
1. Localize o arquivo Urlscan.ini. Normalmente, você o localizaria em um diretório que se parece com o seguinte:  
  
     C:\WINNT\System32\Inetsrv\urlscan  
  
2. Crie uma cópia do arquivo e dê o nome de **Urlscan.old**.  
  
3. Abra a cópia original do arquivo Urlscan.ini usando o Bloco de Notas ou o editor de texto de sua escolha.  
  
4. Em Urlscan.ini, localize a seção [AllowVerbs]. Adicione DEBUG à seção [AllowVerbs]. Se você vir ;DEBUG na seção [AllowVerbs], remova o ponto-e-vírgula para remover os comentários do verbo.  
  
5. Localize a seção [DenyVerbs]. Se DEBUG aparecer na seção [DenyVerbs], remova-o.  
  
6. Salve o arquivo.  
  
7. Reinicie o servidor ou reinicie o IIS.  
  
## <a name="see-also"></a>Consulte também  
 [Depurando aplicativos Web: Erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)   
 [Erro: O servidor Web não conseguiu localizar o recurso solicitado](../debugger/error-the-web-server-could-not-find-the-requested-resource.md)
