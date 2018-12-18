---
title: Detalhes de tempo de execução do controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], runtime details
ms.assetid: 1acd30e0-f98c-4bde-b9cd-4076845887df
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b972218258ded1ebf2f9f606927ba351e77afa01
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130306"
---
# <a name="source-control-runtime-details"></a>Detalhes de tempo de execução de controle do código-fonte
Um projeto é adicionado ao controle de origem quando o usuário adiciona um arquivo no projeto ao controle de origem ou por meio de um controlador de automação, como um assistente. Um projeto não especificar para si mesmo que está sob controle do código-fonte; Ele dá suporte ao controle de origem, mas deve ser adicionado a ele manualmente.  
  
## <a name="registering-with-a-source-control-package"></a>Registrando um pacote de controle de origem  
 Quando um arquivo em seu projeto é adicionado ao controle de origem, o ambiente chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A> para fornecer a você quatro cadeias de caracteres opacas que são usadas como cookies pelo sistema de controle de origem. Armazene essas cadeias de caracteres no arquivo de projeto. Essas cadeias de caracteres devem ser passadas para o Stub de controle de origem (o componente do Visual Studio que gerencia pacotes de controle de origem) na inicialização do tipo de projeto chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>. Isso carrega o pacote de controle de origem sucessivamente e encaminha a chamada para sua implementação de `IVsSccManager2::RegisterSccProject`.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2.RegisterSccProject%2A>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2.SetSccLocation%2A>   
 [Oferecer suporte ao controle do código-fonte](../../extensibility/internals/supporting-source-control.md)