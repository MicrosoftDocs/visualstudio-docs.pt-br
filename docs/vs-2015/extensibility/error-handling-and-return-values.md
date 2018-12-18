---
title: Tratamento de erros e valores de retorno | Microsoft Docs
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
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: d55dea94e55e676a1ca37b46bcaa35a2a7a508e1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51728171"
---
# <a name="error-handling-and-return-values"></a>Tratamento de erro e valores retornados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os VSPackages e COM usam a mesma arquitetura de erros. O `SetErrorInfo` e `GetErrorInfo` funções fazem parte da interface de programação de aplicativo (API) do Win32. Qualquer VSPackage no ambiente de desenvolvimento integrado (IDE) pode chamar essas APIs do Win32 global para informações de erros de registro ao receber uma notificação de erro. O [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] fornece assemblies de interoperabilidade para gerenciar informações de erro.  
  
## <a name="interop-methods"></a>Métodos de interoperabilidade  
 Como uma conveniência, o IDE fornece um método, <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>, para usar em vez de chamar as APIs do Win32. Em uso de código gerenciado <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A>. Quando um erro `HRESULT` chega no nível em que a mensagem de erro deve ser exibida (geralmente, esse é o objeto implementando um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> manipulador de comando), o IDE usa outro método, <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A>, para exibir a caixa de mensagem apropriado. Em uso de código gerenciado a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método.  
  
 Como um implementador de VSPackage, seus objetos COM normalmente implementam `ISupportErrorInfo`. O `ISupportErrorInfo` interface garante que as informações de erros podem mover verticalmente a cadeia de chamada. Devem dar suporte a objetos que podem ser usados em processos ou threads `ISupportErrorInfo` para garantir que as informações de erros completa corretamente por marshaling para o chamador.  
  
 Todos os objetos que estão relacionados a VSPackages e que estão envolvidos em estender o IDE, incluindo as fábricas de editor, editores, hierarquias e oferecidos serviços, devem dar suporte a informações de erros. Embora o IDE não exija esses objetos de VSPackage implementar `ISupportErrorInfo`, sempre é incentivado.  
  
 O IDE é responsável por relatar as informações de erro e exibi-los para um usuário do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] sempre que um `HRESULT` é propagada para o IDE. O IDE também é o mecanismo para a criação de `ErrorInfo` objetos.  
  
## <a name="general-guidelines"></a>Diretrizes gerais  
 Você pode usar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> métodos para definir e relatar erros que são internos a implementação do VSPackage. No entanto, como regra geral, siga estas diretrizes para lidar com mensagens de erro no VSPackage:  
  
-   Implementar `ISupportErrorInfo` em seus objetos COM VSPackage.  
  
-   Criar um erro relatando o mecanismo que chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método em objetos que implementam <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>.  
  
-   Deixar o IDE exibir erros aos usuários por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método.  
  
## <a name="error-information-in-the-ide"></a>Informações de erro no IDE  
 As regras a seguir indicam como lidar com informações de erro no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE:  
  
-   Como uma estratégia de defesa para garantir que informações sobre o erro obsoletos não é relatado para os usuários, funções que chamam a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método deve chamar primeiro o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método. Passe `null` limpar mensagens de erro armazenado em cache antes de chamar qualquer coisa que pode definir novas informações de erro.  
  
-   Funções que reportam diretamente mensagens de erro são permitidas apenas para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método se eles estão retornando um erro `HRESULT`. É permitido para limpar os `ErrorInfo` na entrada para uma função ou ao retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK>. A única exceção a essa regra é quando uma chamada retornará um erro `HRESULT` do qual a parte destinatária pode recuperar explicitamente ou ignorar com segurança.  
  
-   Qualquer parte que ignore explicitamente um erro `HRESULT` deve chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método com <xref:Microsoft.VisualStudio.VSConstants.S_OK>. Caso contrário, o `ErrorInfo` objeto pode ser acidentalmente usado quando o outro participante gera um erro sem fornecer suas próprias `ErrorInfo`.  
  
-   Todos os métodos que se originam de um erro `HRESULT` são incentivados a chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método para fornecer informações de erros. Se retornado `HRESULT` é um especial `FACILITY_ITF` erro e, em seguida, o método é necessário para fornecer apropriadas `ErrorInfo`objeto. Se o erro retornado é um erro de sistema padrão (por exemplo, <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY>, <xref:Microsoft.VisualStudio.VSConstants.E_ABORT>, <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>, <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED>e assim por diante.) é aceitável retornar o código de erro sem chamar explicitamente o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método. Como uma estratégia de codificação defensiva, quando um erro de origem `HRESULT` (incluindo erros de sistema), sempre chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método, com `ErrorInfo` descrevendo a falha em mais detalhes, ou `null`.  
  
-   Todas as funções que retornam um erro que originou por outra chamada deve passar as informações que foram recebidas de falha do chamam na `HRESULT` sem modificar o `ErrorInfo` objeto.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [SetErrorInfo (automação de componente)](http://msdn.microsoft.com/en-us/8eaacfac-fc37-4eaa-870b-10b99d598d66)   
 [GetErrorInfo](http://msdn.microsoft.com/en-us/03317526-8c4f-4173-bc10-110c8112676a)   
 [Interface ISupportErrorInfo](http://msdn.microsoft.com/en-us/42d33066-36b4-4a5b-aa5d-46682e560f32)

