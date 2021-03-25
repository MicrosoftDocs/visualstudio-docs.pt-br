---
title: Tratamento de erros e valores de retorno | Microsoft Docs
description: Saiba como o SDK do Visual Studio fornece assemblies de interoperabilidade para registrar informações de erro avançadas ao receber uma notificação de erro.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- errors [Visual Studio SDK], handling
- error handling
- return values
ms.assetid: b2d9079d-39a6-438a-8010-290056694b5c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ac9c027623b34afa532f62b4b4c9443f219343e9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075257"
---
# <a name="error-handling-and-return-values"></a>Tratamento de erros e valores de retorno
VSPackages e COM usam a mesma arquitetura para erros. As `SetErrorInfo` `GetErrorInfo` funções e fazem parte da API (interface de programação de aplicativo) do Win32. Qualquer VSPackage no IDE (ambiente de desenvolvimento integrado) pode chamar essas APIs globais do Win32 para registrar informações de erro avançadas ao receber uma notificação de erro. O [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] fornece assemblies de interoperabilidade para gerenciar informações de erro.

## <a name="interop-methods"></a>Métodos de interoperabilidade
 Como uma conveniência, o IDE fornece um método, <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> , para usar em vez de chamar as APIs do Win32. Em uso de código gerenciado <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> . Quando um erro `HRESULT` chega ao nível em que a mensagem de erro deve ser exibida (geralmente, esse é o objeto que implementa um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> manipulador de comando), o IDE usa outro método, <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> , para exibir a caixa de mensagem apropriada. Em código gerenciado, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método.

 Como um implementador VSPackage, seus objetos COM normalmente implementam `ISupportErrorInfo` . A `ISupportErrorInfo` interface garante que as informações de erro avançadas possam se mover verticalmente para cima na cadeia de chamadas. Os objetos que podem ser usados em processos ou em threads devem dar suporte `ISupportErrorInfo` para garantir que as informações de erro avançadas sejam corretamente empacotadas de volta para o chamador.

 Todos os objetos relacionados ao VSPackages e que estão envolvidos na extensão do IDE, incluindo fábricas de editor, editores, hierarquias e serviços oferecidos, devem dar suporte a informações de erro avançadas. Embora o IDE não exija que esses objetos VSPackage sejam implementados `ISupportErrorInfo` , ele é sempre incentivado.

 O IDE é responsável por relatar informações de erro e exibi-las para um usuário de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] sempre que um `HRESULT` é propagado para o IDE. O IDE também é o mecanismo para a criação de `ErrorInfo` objetos.

## <a name="general-guidelines"></a>Diretrizes gerais
 Você pode usar os <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> métodos e para definir e relatar erros que são internos à implementação do VSPackage também. No entanto, como regra geral, siga estas diretrizes para lidar com mensagens de erro em seu VSPackage:

- Implemente `ISupportErrorInfo` em seus objetos com do VSPackage.

- Crie um mecanismo de relatório de erros que chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método em objetos que implementam o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> .

- Deixe o IDE exibir erros para os usuários por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método.

## <a name="error-information-in-the-ide"></a>Informações de erro no IDE
 As regras a seguir indicam como tratar informações de erro no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE:

- Como uma estratégia defensiva para garantir que informações de erro obsoletas não sejam relatadas aos usuários, as funções que chamam o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método devem primeiro chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método. Passe `null` para limpar mensagens de erro armazenadas em cache antes de chamar qualquer coisa que possa definir novas informações de erro.

- As funções que não relatam mensagens de erro diretamente só terão permissão para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método se eles estiverem retornando um erro `HRESULT` . É permitido limpar o `ErrorInfo` na entrada para uma função ou ao retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> . A única exceção a essa regra é quando uma chamada retorna um erro `HRESULT` do qual a parte receptora pode se recuperar explicitamente ou ser ignorada com segurança.

- Qualquer parte que ignora explicitamente um erro `HRESULT` deve chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método com <xref:Microsoft.VisualStudio.VSConstants.S_OK> . Caso contrário, o `ErrorInfo` objeto pode ser acidentalmente usado quando outra parte gerar um erro sem fornecer seus próprios `ErrorInfo` .

- Todos os métodos que originam um erro `HRESULT` são incentivados a chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método para fornecer informações de erro avançadas. Se o retornado `HRESULT` for um `FACILITY_ITF` erro especial, o método será necessário para fornecer um objeto adequado `ErrorInfo` . Se o erro retornado for um erro de sistema padrão (por exemplo,,,, <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY> <xref:Microsoft.VisualStudio.VSConstants.E_ABORT> <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG> <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED> e assim por diante), é aceitável retornar o código de erro sem chamar explicitamente o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método. Como uma estratégia de codificação defensiva, ao originar um erro `HRESULT` (incluindo erros do sistema), sempre chame o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> método, com `ErrorInfo` a descrição da falha em mais detalhes ou `null` .

- Todas as funções que retornam um erro originado por outra chamada devem passar as informações recebidas da chamada com falha no `HRESULT` sem modificar o `ErrorInfo` objeto.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [SetErrorInfo (automação de componente)](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [Interface ISupportErrorInfo](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
