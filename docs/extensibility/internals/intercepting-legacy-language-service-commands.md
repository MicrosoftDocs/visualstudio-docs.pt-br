---
title: Interceptando comandos do serviço de idioma herdado | Microsoft Docs
description: Saiba como usar filtros de comando no Visual Studio para interceptar comandos de serviço de idioma herdado e adicionar comportamento específico de idioma.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8d7af9ff4a8f04382cff4999b8c57549f3da3db7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074666"
---
# <a name="intercepting-legacy-language-service-commands"></a>Interceptando comandos do serviço de linguagem herdado
Com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o, você pode fazer com que o serviço de linguagem intercepte os comandos que o modo de exibição de texto manipularia. Isso é útil para o comportamento específico de um idioma que a exibição de texto não gerencia. Você pode interceptar esses comandos adicionando um ou mais filtros de comando à exibição de texto do seu serviço de idioma.

## <a name="getting-and-routing-the-command"></a>Obter e rotear o comando
 Um filtro de comando é um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto que monitora determinadas sequências de caracteres ou comandos de chave. Você pode associar mais de um filtro de comando a uma única exibição de texto. Cada exibição de texto mantém uma cadeia de filtros de comando. Depois de criar um novo filtro de comando, você adiciona o filtro à cadeia para a exibição de texto apropriada.

 Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para adicionar o filtro de comando à cadeia. Quando você chama <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> , [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] retorna outro filtro de comando para o qual você pode passar os comandos que o filtro de comando não manipula.

 Você tem as seguintes opções para manipulação de comandos:

- Manipule o comando e, em seguida, passe o comando para o próximo filtro de comando na cadeia.

- Manipule o comando e não passe o comando para o próximo filtro de comando.

- Não manipule o comando, mas passe o comando para o próximo filtro de comando.

- Ignore o comando. Não o manipule no filtro atual e não o passe para o próximo filtro.

  Para obter informações sobre quais comandos seu serviço de idioma deve manipular, consulte [comandos importantes para filtros de serviço de idioma](../../extensibility/internals/important-commands-for-language-service-filters.md).
