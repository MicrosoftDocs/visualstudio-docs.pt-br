---
title: Informações de HRESULT em código gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, HRESULT information
- HRESULT, managed VSPackages
ms.assetid: 0795ee94-17a8-4327-bf57-27cd5e312a4c
caps.latest.revision: 29
manager: douge
ms.openlocfilehash: 08d14f1155838e53321224280a69e7a76bf07b52
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911844"
---
# <a name="hresult-information-in-managed-code"></a>Informações de HRESULT em código gerenciado
A interação entre código gerenciado e COM pode causar problemas quando os valores de retorno HRESULT forem encontrados.  
  
 Em uma interface COM, um valor de retorno HRESULT pode executar essas funções:  
  
- Fornecer informações de erro (por exemplo, <xref:Microsoft.VisualStudio.VSConstants.E_INVALIDARG>).  
  
- Fornecer informações de status sobre o comportamento normal do programa.  
  
  Quando chama COM código gerenciado, HRESULTs podem causar esses problemas:  
  
- Funções COM que retornam valores HRESULT menor que zero (códigos de falha) geram exceções.  
  
- OS métodos com regularmente retornam duas ou mais códigos de sucesso diferentes, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.S_OK> ou <xref:Microsoft.VisualStudio.VSConstants.S_FALSE>, não podem ser diferenciadas.  
  
  Porque muitos dos [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] funções COM retornará valores HRESULT menor que zero ou retornam códigos de sucesso diferentes, o [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] assemblies de interoperabilidade foram gravados para que as assinaturas de método são preservadas. Todos os [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] métodos de interoperabilidade são de `int` tipo. Valores HRESULT são passados por meio da camada de interoperabilidade sem alteração e sem gerar exceções.  
  
  Como uma função COM retorna um HRESULT para o método gerenciado que faz a chamada, o método de chamada deve verificar o HRESULT e lançar exceções conforme necessário.  
  
## <a name="handling-hresults-returned-to-managed-code-from-com"></a>Tratamento HRESULTs retornados para o código gerenciado de COM  
 Quando você chama uma interface COM de código gerenciado, examine o valor HRESULT e lançar uma exceção, se necessário. O <xref:Microsoft.VisualStudio.ErrorHandler> classe contém o <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> método, que lança uma exceção de COM, dependendo do valor de HRESULT é passado para ele.  
  
 Por padrão, <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> gera uma exceção sempre que ele é passado um HRESULT que tem um valor menor que zero. Em casos em que tal HRESULTs são valores aceitáveis e nenhuma exceção deverá ser gerada, os valores de HRESULTS adicionais devem ser passados para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> depois que os valores são testados. Se o HRESULT que está sendo testado corresponde a todos explicitamente passados para os valores HRESULT <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>, nenhuma exceção é lançada.  
  
> [!NOTE]
>  O <xref:Microsoft.VisualStudio.VSConstants> classe contém constantes para HRESULTS comuns, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.S_OK> e <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>, e [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] HRESULTS, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> e <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>. <xref:Microsoft.VisualStudio.VSConstants> também fornece o <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> e <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> métodos, que correspondem às macros com êxito e falha no COM.  
  
 Por exemplo, considere a seguinte chamada de função, no qual <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> é um valor de retorno aceitável, mas qualquer outro HRESULT menor que zero representa um erro.  
  
 [!code-csharp[VSSDKHRESULTInformation#1](../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#1)]
 [!code-vb[VSSDKHRESULTInformation#1](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#1)]  
  
 Se existir mais de um valores de retorno aceitáveis, valores adicionais de HRESULT apenas podem ser acrescentados à lista na chamada para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>.  
  
 [!code-csharp[VSSDKHRESULTInformation#2](../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#2)]
 [!code-vb[VSSDKHRESULTInformation#2](../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#2)]  
  
## <a name="returning-hresults-to-com-from-managed-code"></a>Retornando HRESULTS para COM do código gerenciado  
 Se nenhuma exceção ocorrer, gerenciada retorna código <xref:Microsoft.VisualStudio.VSConstants.S_OK> para a função COM que o chamou. Interoperabilidade COM dá suporte a exceções comuns que são fortemente tipadas em código gerenciado. Por exemplo, um método que recebe um inaceitável `null` argumento gera um <xref:System.ArgumentNullException>.  
  
 Se você não tiver certeza qual exceção ser gerada, mas você sabe o HRESULT que você deseja retornar ao COM, você pode usar o <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> método para gerar uma exceção apropriada. Isso funciona mesmo com um erro não padrão, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>. <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> tenta mapear o HRESULT é passado para ele a uma exceção com rigidez de tipos. Se não for possível, ele lança uma exceção genérica de COM em vez disso. O resultado final é que o HRESULT que você passe para <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> do código gerenciado é retornado para a função COM que o chamou.  
  
> [!NOTE]
>  Exceções de comprometer o desempenho e destinam-se para indicar as condições de programa anormal. As condições que ocorrem com frequência devem ser tratada em linha, em vez de uma exceção gerada.  
  
## <a name="see-also"></a>Consulte também  
 [VSPackages gerenciados](../misc/managed-vspackages.md)   
 [Interoperação com código não gerenciado](http://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)   
 [Como: mapear HRESULTs e exceções](http://msdn.microsoft.com/library/610b364b-2761-429d-9c4a-afbc3e66f1b9)   
 [Compilando componentes COM para interoperação](http://msdn.microsoft.com/en-us/7a2c657a-cfef-40f0-bed3-7c2c0ac4abdf)   
 [VSPackages gerenciados](../misc/managed-vspackages.md)