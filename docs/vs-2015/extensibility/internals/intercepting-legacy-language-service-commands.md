---
title: Interceptar comandos do serviço de linguagem herdado | Microsoft Docs
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
- commands, intercepting language service
- language services, intercepting commands
ms.assetid: eea69f03-349c-44bb-bd4f-4925c0dc3e55
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 41d89e2947cbd7bf1087f8dfa0ecffdd75033171
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51752989"
---
# <a name="intercepting-legacy-language-service-commands"></a>Interceptando comandos do serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], você pode ter os comandos de interceptação do serviço de linguagem que trataria a exibição de texto. Isso é útil para o comportamento específico do idioma que não gerencia a exibição de texto. Você pode interceptar esses comandos, adicionando um ou mais filtros de comando para a exibição de texto de seu serviço de linguagem.  
  
## <a name="getting-and-routing-the-command"></a>Obtendo e roteamento de comando  
 Um filtro de comando é um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> objeto que monitora a determinadas sequências de caracteres ou comandos de tecla. Você pode associar mais de um filtro de comando com uma exibição única de texto. Cada modo de exibição de texto mantém uma cadeia de comando filtros. Depois de criar um novo filtro de comando, você adiciona o filtro da cadeia para a exibição de texto apropriado.  
  
 Chame o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> para adicionar o filtro de comando para a cadeia. Quando você chama <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.AddCommandFilter%2A>, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] retorna outro filtro de comando para o qual você pode passar os comandos que não lidar com o seu filtro de comando.  
  
 Você tem as seguintes opções para manipulação de comando:  
  
- Lidar com o comando e, em seguida, passe o comando para o próximo filtro de comando na cadeia.  
  
- Lidar com o comando e não passam o comando para o próximo filtro de comando.  
  
- Não lidam com o comando, mas transmitir o comando para o próximo filtro de comando.  
  
- Ignore o comando. Não tratá-la no filtro atual e não a passar para o próximo filtro.  
  
  Para obter informações sobre quais comandos deve lidar com seu serviço de linguagem, consulte [comandos importantes para filtros do serviço de linguagem](../../extensibility/internals/important-commands-for-language-service-filters.md).

