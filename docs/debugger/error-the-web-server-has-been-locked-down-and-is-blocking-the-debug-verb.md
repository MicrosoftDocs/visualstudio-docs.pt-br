---
title: Erro-o servidor Web foi bloqueado e está bloqueando o verbo de depuração | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.webdbg_debug_verb_blocked
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugger, Web application errors
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: abef1edefad63e340170e7934f4ad87cce268e46
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460358"
---
# <a name="error-the-web-server-has-been-locked-down-and-is-blocking-the-debug-verb"></a>Erro: o servidor Web foi bloqueado e está bloqueando o verbo DEBUG
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

## <a name="see-also"></a>Veja também
- [Depurando aplicativos Web: erros e solução de problemas](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
- [Erro: o servidor Web não pôde localizar o recurso solicitado](../debugger/error-the-web-server-could-not-find-the-requested-resource.md)