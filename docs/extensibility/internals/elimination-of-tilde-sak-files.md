---
title: Eliminação de ~ SAK arquivos | Microsoft Docs
description: Saiba mais sobre a eliminação de arquivos ~ SAK da API de plug-in de controle do código-fonte 1,2 e como eles foram substituídos por sinalizadores de recurso e novas funções.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- temporary files
- ~sak files
- source control plug-ins, ~SAK files
ms.assetid: 5277b5fa-073b-4bd1-8ba1-9dc913aa3c50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf0f8bc567a097d4bb7d400f829489c517e9a68f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061232"
---
# <a name="elimination-of-sak-files"></a>Eliminação de ~ SAK arquivos
Na API de plug-in de controle do código-fonte 1,2, os arquivos *~ Sak* foram substituídos por sinalizadores de funcionalidade e novas funções que detectam se um plug-in de controle do código-fonte dá suporte ao arquivo *MSSCCPRJ* e aos checkouts compartilhados.

## <a name="sak-files"></a>~ Arquivos SAK
O Visual Studio .NET 2003 criou arquivos temporários prefixados com *~ Sak*. Esses arquivos são usados para determinar se um plug-in de controle do código-fonte dá suporte a:

- O arquivo *MSSCCPRJ. SCC* .

- Vários check-outs (compartilhados).

Para plug-ins que dão suporte a funções avançadas fornecidas na API de plug-in de controle do código-fonte 1,2, o IDE pode detectar esses recursos sem criar os arquivos temporários por meio do uso de novos recursos, sinalizadores e funções, detalhados nas seções a seguir.

## <a name="new-capability-flags"></a>Novos sinalizadores de capacidade
 `SCC_CAP_SCCFILE`

 `SCC_CAP_MULTICHECKOUT`

## <a name="new-functions"></a>Novas funções
- [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md)

- [SccIsMultiCheckoutEnabled](../../extensibility/sccismulticheckoutenabled-function.md)

 Se um plug-in de controle do código-fonte der suporte a vários check-outs (compartilhados), ele declara a `SCC_CAP_MULTICHECKOUT` funcionalidade e implementa a `SccIsMultiCheckOutEnabled` função. Essa função é chamada sempre que uma operação de check-out ocorre em qualquer um dos projetos de origem controlada.

 Se um plug-in de controle do código-fonte der suporte à criação e ao uso de um arquivo *MSSCCPRJ. SCC* , ele declara o `SCC_CAP_SCCFILE` recurso e implementa o [SccWillCreateSccFile](../../extensibility/sccwillcreatesccfile-function.md). Essa função é chamada com uma lista de arquivos. A função retorna `TRUE' or 'FALSE` para cada arquivo para indicar se o Visual Studio deve usar um arquivo *MSSCCPRJ. SCC* para ele. Se o plug-in de controle do código-fonte optar por não oferecer suporte a esses novos recursos e funções, ele poderá usar a seguinte chave do registro para desabilitar a criação desses arquivos:

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl]DoNotCreateTemporaryFilesInSourceControl**  =  *DWORD: 00000001*

> [!NOTE]
> Se essa chave do registro for definida como *DWORD: 00000000*, ela será equivalente à chave que está sendo inexistente e o Visual Studio ainda tentará criar os arquivos temporários. No entanto, se a chave do registro for definida como *DWORD: 00000001*, o Visual Studio não tentará criar os arquivos temporários. Em vez disso, ele pressupõe que o plug-in de controle do código-fonte não oferece suporte ao arquivo *MSSCCPRJ. SCC* e não oferece suporte a check-outs compartilhados.

## <a name="see-also"></a>Confira também
- [O que há de novo na API de plug-in de controle do código-fonte versão 1,2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
