---
title: Interceptar comandos do serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 669d03043ad36ad1e96084cb4cc8833ab20f0998
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832845"
---
# <a name="intercepting-legacy-language-service-commands"></a>Interceptando comandos do serviço de linguagem herdado
Com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], você pode ter os comandos de interceptação do serviço de linguagem que trataria a exibição de texto. Isso é útil para o comportamento específico do idioma que não gerencia a exibição de texto. Você pode interceptar esses comandos, adicionando um ou mais filtros de comando para a exibição de texto de seu serviço de linguagem.  
  
## <a name="getting-and-routing-the-command"></a>Obtendo e roteamento de comando  
 Um filtro de comando é um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto que monitora a determinadas sequências de caracteres ou comandos de tecla. Você pode associar mais de um filtro de comando com uma exibição única de texto. Cada modo de exibição de texto mantém uma cadeia de comando filtros. Depois de criar um novo filtro de comando, você adiciona o filtro da cadeia para a exibição de texto apropriado.  
  
 Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para adicionar o filtro de comando para a cadeia. Quando você chama <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] retorna outro filtro de comando para o qual você pode passar os comandos que não lidar com o seu filtro de comando.  
  
 Você tem as seguintes opções para manipulação de comando:  
  
- Lidar com o comando e, em seguida, passe o comando para o próximo filtro de comando na cadeia.  
  
- Lidar com o comando e não passam o comando para o próximo filtro de comando.  
  
- Não lidam com o comando, mas transmitir o comando para o próximo filtro de comando.  
  
- Ignore o comando. Não tratá-la no filtro atual e não a passar para o próximo filtro.  
  
  Para obter informações sobre quais comandos deve lidar com seu serviço de linguagem, consulte [comandos importantes para filtros do serviço de linguagem](../../extensibility/internals/important-commands-for-language-service-filters.md).