---
title: Eliminação de ~ SAK arquivos | Microsoft Docs
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
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 930ee0690e14431298461f50387a94dd4bb0ce7d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780458"
---
# <a name="elimination-of-sak-files"></a>Eliminação de arquivos ~SAK
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Na fonte de controle de plug-in API 1.2, o ~ arquivos SAK foram substituídos por novas funções que detectam se um plug-in de controle de origem dá suporte a arquivo MSSCCPRJ e check-outs compartilhados e de sinalizadores de recurso.  
  
## <a name="sak-files"></a>~ Arquivos SAK  
 Visual Studio .NET 2003 criado arquivos temporários, prefixados com ~ SAK. Esses arquivos são usados para determinar se um plug-in de controle de origem dá suporte a:  
  
- MSSCCPRJ. Arquivos SCC.  
  
- Vários checkouts (compartilhados).  
  
  Para plug-ins que dão suporte a funções avançadas fornecidas a fonte de controle de plug-in API 1.2, o IDE pode detectar esses recursos sem criar os arquivos temporários com o uso de novos recursos, sinalizadores e funções, detalhadas nas seções a seguir.  
  
## <a name="new-capability-flags"></a>Novos sinalizadores de recurso  
 `SCC_CAP_SCCFILE`  
  
 `SCC_CAP_MULTICHECKOUT`  
  
## <a name="new-functions"></a>Novas funções  
 [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)  
  
 [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)  
  
 Se um plug-in de controle de origem dá suporte a vários check-outs (compartilhados) e, em seguida, ele declara a `SCC_CAP_MULTICHECKOUT` funcionalidade e implementa o `SccIsMultiCheckOutEnabled` função. Essa função é chamada sempre que uma operação de check-out ocorre em qualquer um dos projetos de controle do código-fonte.  
  
 Se um plug-in de controle de origem dá suporte à criação e ao uso de um MSSCCPRJ. Arquivos SCC, em seguida, ele declara a `SCC_CAP_SCCFILE` funcionalidade e implementa as [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md). Essa função é chamada com uma lista de arquivos. A função retorna `TRUE/FALSE` para cada arquivo indicar se o Visual Studio deve usar um MSSCCPRJ. Arquivos SCC para ele. Se o plug-in de controle do código-fonte optar por não dar suporte a esses novos recursos e funções, ele pode usar a seguinte chave do registro para desabilitar a criação desses arquivos:  
  
 [HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateTemporaryFilesInSourceControl" = DWORD: 00000001  
  
> [!NOTE]
>  Se essa chave do registro é definida como DWORD: 00000000, é equivalente à chave que está sendo inexistente e Visual Studio ainda tenta criar arquivos temporários. No entanto, se a chave do registro é definida como DWORD: 00000001, o Visual Studio não tentará criar os arquivos temporários. Em vez disso, ele pressupõe que o plug-in de controle do código-fonte não dá suporte a MSSCCPRJ. Arquivo de SCC e não oferece suporte a check-outs compartilhados.  
  
## <a name="see-also"></a>Consulte também  
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

