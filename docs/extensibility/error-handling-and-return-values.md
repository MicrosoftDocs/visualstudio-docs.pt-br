---
title: Tratamento de erros e valores de retorno | Microsoft Docs
description: Saiba como o Visual Studio SDK fornece assemblies de interop para registrar informações de erro rich ao receber uma notificação de erro.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: ef33936e3dc36d98cc88b1285aa0b198a84cbd59
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898312"
---
# <a name="error-handling-and-return-values"></a>Tratamento de erros e valores de retorno
VSPackages e COM usam a mesma arquitetura para erros. As funções e fazem parte da API (interface de programação `SetErrorInfo` `GetErrorInfo` de aplicativo) win32. Qualquer VSPackage no IDE (ambiente de desenvolvimento integrado) pode chamar essas APIs globais do Win32 para registrar informações de erro rich ao receber uma notificação de erro. O [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] fornece assemblies de interop para gerenciar informações de erro.

## <a name="interop-methods"></a>Métodos de interop
 Como uma conveniência, o IDE fornece um método, , para usar em <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> vez de chamar as APIs do Win32. No código gerenciado, use <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> . Quando um erro chega ao nível em que a mensagem de erro deve ser exibida (geralmente é o objeto que implementa um manipulador de comandos), o IDE usa outro método, , para exibir a caixa de mensagem `HRESULT` <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> apropriada. No código gerenciado, use o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método .

 Como um implementador vsPackage, seus objetos COM normalmente implementam `ISupportErrorInfo` . A `ISupportErrorInfo` interface garante que as informações de erro rich possam ser movimentadas verticalmente para cima na cadeia de chamada. Os objetos que podem ser usados entre processos ou threads devem dar suporte para garantir que as informações de erro rich sejam devidamente empacotadas de volta `ISupportErrorInfo` para o chamador.

 Todos os objetos relacionados ao VSPackages e que estão envolvidos na extensão do IDE, incluindo fábricas de editores, editores, hierarquias e serviços oferecidos, devem dar suporte a informações de erro rich. Embora o IDE não exige que esses objetos VSPackage implementem `ISupportErrorInfo` , ele é sempre incentivado.

 O IDE é responsável por relatar informações de erro e exibi-los a um usuário do sempre que um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] `HRESULT` é propagado para o IDE. O IDE também é o mecanismo para criar `ErrorInfo` objetos.

## <a name="general-guidelines"></a>Diretrizes gerais
 Você também pode usar os métodos e para definir e relatar erros internos <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> à implementação do VSPackage. No entanto, como regra geral, siga estas diretrizes para lidar com mensagens de erro em seu VSPackage:

- Implemente `ISupportErrorInfo` em seus objetos COM do VSPackage.

- Crie um mecanismo de relatório de erros que chama <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> o método em objetos que implementam <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> .

- Deixe o IDE exibir erros aos usuários por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> método .

## <a name="error-information-in-the-ide"></a>Informações de erro no IDE
 As regras a seguir indicam como tratar informações de erro no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] IDE:

- Como uma estratégia de defesa para garantir que as informações de erro stale não são relatadas aos usuários, as funções que chamam o método devem <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ReportErrorInfo%2A> primeiro chamar o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> . Passe para `null` limpar mensagens de erro armazenadas em cache antes de chamar qualquer coisa que possa definir novas informações de erro.

- Funções que não relatam diretamente mensagens de erro só poderão chamar o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> se retornarem um erro `HRESULT` . É permitido limpar o na entrada para uma função `ErrorInfo` ou ao retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> . A única exceção a essa regra é quando uma chamada retorna um erro do qual a parte receptora pode se recuperar explicitamente `HRESULT` ou ignorar com segurança.

- Qualquer parte que ignore explicitamente um erro `HRESULT` deve chamar o método com <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> <xref:Microsoft.VisualStudio.VSConstants.S_OK> . Caso contrário, o objeto poderá ser usado acidentalmente quando outra parte gerar um erro `ErrorInfo` sem fornecer seu próprio `ErrorInfo` .

- Todos os métodos que originam um erro são incentivados a `HRESULT` chamar o método para fornecer informações de erro <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> rich. Se o retornado `HRESULT` for um erro `FACILITY_ITF` especial, o método será necessário para fornecer um objeto `ErrorInfo` apropriado. Se o erro retornado for um erro padrão do sistema (por exemplo, , , , e assim por diante). É aceitável retornar o código de erro sem chamar explicitamente <xref:Microsoft.VisualStudio.VSConstants.E_OUTOFMEMORY> <xref:Microsoft.VisualStudio.VSConstants.E_ABORT> o método <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG> <xref:Microsoft.VisualStudio.VSConstants.E_UNEXPECTED> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> . Como uma estratégia de codificação de defesa, ao originar um erro (incluindo erros do sistema), sempre chame o método , seja com a descrição da falha em mais `HRESULT` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.SetErrorInfo%2A> detalhes ou `ErrorInfo` `null` .

- Todas as funções que retornam um erro originado por outra chamada devem passar as informações recebidas da chamada com falha no sem `HRESULT` modificar o `ErrorInfo` objeto.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [SetErrorInfo (Automação de Componentes)](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-seterrorinfo)
- [GetErrorInfo](/previous-versions/windows/desktop/api/oleauto/nf-oleauto-geterrorinfo)
- [ISupportErrorInfo Interface](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-isupporterrorinfo)
