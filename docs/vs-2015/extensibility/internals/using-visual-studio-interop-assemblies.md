---
title: Usar Assemblies de interoperabilidade do Visual Studio | Microsoft Docs
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
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
caps.latest.revision: 34
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9c47b709d38a9acf84810de7154b270e2b4557ea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794641"
---
# <a name="using-visual-studio-interop-assemblies"></a>Usando assemblies de interoperabilidade do Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Assemblies de interoperabilidade Visual Studio permitem que aplicativos gerenciados acessar as interfaces COM que fornecem extensibilidade do Visual Studio. Há algumas diferenças entre interfaces retas e suas versões de interoperabilidade. Por exemplo, HRESULTs geralmente são representados como valores int e precisam ser manipulados da mesma maneira como exceções e parâmetros (especialmente os parâmetros de saída) são tratados de maneira diferente.  
  
## <a name="handling-hresults-returned-to-managed-code-from-com"></a>Tratamento HRESULTs retornados para o código gerenciado de COM  
 Quando você chama uma interface COM de código gerenciado, examine o valor HRESULT e lançar uma exceção, se necessário. O <xref:Microsoft.VisualStudio.ErrorHandler> classe contém o <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> método, que lança uma exceção de COM, dependendo do valor de HRESULT é passado para ele.  
  
 Por padrão, <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> gera uma exceção sempre que ele é passado um HRESULT que tem um valor menor que zero. Em casos em que tal HRESULTs são valores aceitáveis e nenhuma exceção deverá ser gerada, os valores de HRESULTS adicionais devem ser passados para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> depois que os valores são testados. Se o HRESULT que está sendo testado corresponde a todos explicitamente passados para os valores HRESULT <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>, nenhuma exceção é lançada.  
  
> [!NOTE]
>  O <xref:Microsoft.VisualStudio.VSConstants> classe contém constantes para HRESULTS comuns, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.S_OK> e <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>, e [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] HRESULTS, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> e <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>. <xref:Microsoft.VisualStudio.VSConstants> também fornece o <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> e <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> métodos, que correspondem às macros com êxito e falha no COM.  
  
 Por exemplo, considere a seguinte chamada de função, no qual <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> é um valor de retorno aceitável, mas qualquer outro HRESULT menor que zero representa um erro.  
  
 [!code-csharp[VSSDKHRESULTInformation#1](../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#1)]
 [!code-vb[VSSDKHRESULTInformation#1](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#1)]  
  
 Se existir mais de um valores de retorno aceitáveis, valores adicionais de HRESULT apenas podem ser acrescentados à lista na chamada para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>.  
  
 [!code-csharp[VSSDKHRESULTInformation#2](../../snippets/csharp/VS_Snippets_VSSDK/vssdkhresultinformation/cs/vssdkhresultinformationpackage.cs#2)]
 [!code-vb[VSSDKHRESULTInformation#2](../../snippets/visualbasic/VS_Snippets_VSSDK/vssdkhresultinformation/vb/vssdkhresultinformationpackage.vb#2)]  
  
## <a name="returning-hresults-to-com-from-managed-code"></a>Retornando HRESULTS para COM do código gerenciado  
 Se nenhuma exceção ocorrer, gerenciada retorna código <xref:Microsoft.VisualStudio.VSConstants.S_OK> para a função COM que o chamou. Interoperabilidade COM dá suporte a exceções comuns que são fortemente tipadas em código gerenciado. Por exemplo, um método que recebe um inaceitável `null` argumento gera um <xref:System.ArgumentNullException>.  
  
 Se você não tiver certeza qual exceção ser gerada, mas você sabe o HRESULT que você deseja retornar ao COM, você pode usar o <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> método para gerar uma exceção apropriada. Isso funciona mesmo com um erro não padrão, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>. <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> tenta mapear o HRESULT é passado para ele a uma exceção com rigidez de tipos. Se não for possível, ele lança uma exceção genérica de COM em vez disso. O resultado final é que o HRESULT que você passe para <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> do código gerenciado é retornado para a função COM que o chamou.  
  
> [!NOTE]
>  Exceções de comprometer o desempenho e destinam-se para indicar as condições de programa anormal. As condições que ocorrem com frequência devem ser tratada em linha, em vez de uma exceção gerada.  
  
## <a name="iunknown-parameters-passed-as-type-void"></a>Parâmetros de IUnknown passados como tipo void * *  
 Procure [out] os parâmetros que são definidos como tipo `void **` no COM a interface, mas que são definidas como `[``iid_is``]` no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Às vezes, uma interface COM gera uma `IUnknown` objeto e a interface COM, em seguida, passa como tipo `void **`. Essas interfaces são especialmente importantes porque se a variável for definida como [out] no IDL, em seguida, a `IUnknown` objeto é contado por referência com o `AddRef` método. Um vazamento de memória ocorre se o objeto não é manipulado corretamente.  
  
> [!NOTE]
>  Um `IUnknown` objeto criado pela interface COM e retornados em uma variável [out] faz com que um vazamento de memória se não for explicitamente liberado.  
  
 Métodos gerenciados que lidar com esses objetos devem ser tratadas <xref:System.IntPtr> como um ponteiro para um `IUnknown` do objeto e, em seguida, chamar o <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> método para obter o objeto. O chamador deve, em seguida, converter o valor retornado para qualquer tipo é apropriado. Quando o objeto não é necessário, chame <xref:System.Runtime.InteropServices.Marshal.Release%2A> liberá-la.  
  
 A seguir está um exemplo de chamada a <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A> método e tratamento de `IUnknown` objeto corretamente:  
  
```  
MyClass myclass;  
Object object;  
IntPtr pObj;  
Guid iid = Typeof(MyClass).Guid;  
int hr = windowFrame.QueryViewInterface(ref iid, out pObj);     
if (NativeMethods.Succeeded(hr))   
{  
    try   
    {  
        object = Marshal.GetObjectForIUnknown(pObj);  
        myclass = object;  
    }  
    finally   
    {  
        Marshal.Release(pObj);  
    }  
}  
else   
{  
    // error calling QueryViewInterface  
}  
```  
  
> [!NOTE]
>  Os métodos a seguir são conhecidos para transmitir `IUnknown` ponteiros do objeto como tipo <xref:System.IntPtr>. Tratá-los conforme descrito nesta seção.  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>  
  
## <a name="optional-out-parameters"></a>Opcional [parâmetros out]  
 Procure os parâmetros que são definidos como [out] o tipo de dados (`int`, `object`e assim por diante) no COM a interface, mas que são definidos como matrizes do mesmo tipo de dados no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Alguns COM interfaces, como <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>, tratar [out] parâmetros como opcional. Se um objeto não é necessário, essas interfaces COM retornam um `null` ponteiro como o valor desse parâmetro em vez de criar o objeto [out]. Esse comportamento é esperado. Para essas interfaces, `null` ponteiros são considerados como parte do comportamento correto do VSPackage, e nenhum erro será retornado.  
  
 Porque o CLR não permite que o valor de um parâmetro [out] para ser `null`, parte do que o comportamento padrão dessas interfaces não está disponível diretamente no código gerenciado. O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] métodos de assembly de interoperabilidade para interfaces afetados contornar o problema definindo os parâmetros relevantes como matrizes, como o CLR permite a passagem de `null` matrizes.  
  
 Implementações gerenciadas desses métodos devem colocar um `null` matriz para o parâmetro quando não há nada a ser retornado. Caso contrário, crie uma matriz de um elemento do tipo correto e coloque o valor retornado na matriz.  
  
 Gerenciado os métodos que recebem informações de interfaces com opcional [out] os parâmetros recebem o parâmetro como uma matriz. Basta examine o valor do primeiro elemento da matriz. Se não for `null`, trate o primeiro elemento, como se fosse o parâmetro original.  
  
## <a name="passing-constants-in-pointer-parameters"></a>Constantes de passagem em parâmetros de ponteiro  
 Procure os parâmetros que são definidas como [in] ponteiros na interface COM, mas que são definidos como um <xref:System.IntPtr> digite o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Um problema semelhante ocorre quando uma interface COM transmite um valor especial, como 0, -1 ou – 2, em vez de um ponteiro de objeto. Ao contrário de [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)], o CLR não permite constantes ser convertido como objetos. Em vez disso, o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] assembly de interoperabilidade define o parâmetro como um <xref:System.IntPtr> tipo.  
  
 Implementações gerenciadas desses métodos devem tirar proveito do fato de que o <xref:System.IntPtr> classe tem ambos `int` e `void *` construtores para criar um <xref:System.IntPtr> de um objeto ou uma constante de inteiro, conforme apropriado.  
  
 Gerenciado os métodos que recebem <xref:System.IntPtr> parâmetros desse tipo devem usar o <xref:System.IntPtr> digite operadores de conversão para lidar com os resultados. Primeiro, converta a <xref:System.IntPtr> para `int` e testá-lo em constantes de inteiro relevantes. Se não há valores corresponderem, convertê-lo em um objeto do tipo necessário e continuar.  
  
 Para obter exemplos de isso, consulte <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>.  
  
## <a name="ole-return-values-passed-as-out-parameters"></a>OLE retornam valores passados como [parâmetros out]  
 Procure por métodos que têm uma `retval` valor de retorno na interface COM, mas que têm um `int` valor de retorno e um adicional [out] do parâmetro de matriz na [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade. Deve ficar claro que esses métodos exigem tratamento especial, porque o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] protótipos de método do assembly de interoperabilidade tem um parâmetro a mais que os métodos de interface COM.  
  
 Várias interfaces COM que lidam com a atividade de OLE enviar informações sobre o status OLE volta para o programa de chamada armazenado no `retval` retornar o valor da interface. Em vez de usar um valor de retorno correspondente [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] métodos do assembly de interoperabilidade enviar as informações de volta para o programa de chamada armazenado em um [out] o parâmetro de matriz.  
  
 Gerenciado implementações dos métodos a seguir devem criar uma matriz de elemento único, do mesmo tipo como o parâmetro [out] e colocá-lo no parâmetro. O valor do elemento da matriz deve ser o mesmo que o apropriada COM `retval`.  
  
 Métodos gerenciados que chamam as interfaces desse tipo devem obter o primeiro elemento da matriz [out]. Esse elemento pode ser tratado como se fosse um `retval` retornar valor de interface COM correspondente.  
  
## <a name="see-also"></a>Consulte também  
 [Interoperação com código não gerenciado](http://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)

