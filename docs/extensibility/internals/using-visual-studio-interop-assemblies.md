---
title: Usando Assemblies de interoperabilidade do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, interop assemblies
- interop assemblies, Visual Studio
- managed VSPackages, interop assemblies
ms.assetid: 1043eb95-4f0d-4861-be21-2a25395b3b3c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ca0ff9a75d72bc723b767a43f12123094a520644
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31146813"
---
# <a name="using-visual-studio-interop-assemblies"></a>Usando Assemblies de interoperabilidade do Visual Studio
Assemblies de interoperabilidade do Visual Studio permitem que aplicativos gerenciados acessar as interfaces COM que fornecem a extensibilidade do Visual Studio. Há algumas diferenças entre as interfaces normais e suas versões de interoperabilidade. Por exemplo, HRESULTs são geralmente representados como valores de int e precisam ser manipulados da mesma maneira como exceções e parâmetros (especialmente os parâmetros de saída) são tratados de forma diferente.  
  
## <a name="handling-hresults-returned-to-managed-code-from-com"></a>Tratamento HRESULTs retornados ao código gerenciado do COM  
 Quando você chama uma interface COM de código gerenciado, examine o valor HRESULT e lançar uma exceção se necessário. O <xref:Microsoft.VisualStudio.ErrorHandler> classe contém o <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> método, que gera uma exceção de COM, dependendo do valor de HRESULT passados para ele.  
  
 Por padrão, <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> gera uma exceção sempre que é passado um HRESULT que tem um valor menor que zero. Em casos onde tais HRESULTs são valores aceitáveis e nenhuma exceção deve ser gerada, os valores de HRESULTS adicionais devem ser passados para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A> depois que os valores são testados. Se o HRESULT que está sendo testado corresponde a quaisquer valores HRESULT passados explicitamente para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>, nenhuma exceção é lançada.  
  
> [!NOTE]
>  O <xref:Microsoft.VisualStudio.VSConstants> classe contém constantes para os HRESULTS comuns, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.S_OK> e <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL>, e [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] HRESULTS, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA> e <xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>. <xref:Microsoft.VisualStudio.VSConstants> também fornece o <xref:Microsoft.VisualStudio.ErrorHandler.Succeeded%2A> e <xref:Microsoft.VisualStudio.ErrorHandler.Failed%2A> métodos que correspondem às macros êxito e falha no COM.  
  
 Por exemplo, considere a seguinte chamada de função, na qual <xref:Microsoft.VisualStudio.VSConstants.E_NOTIMPL> é um valor de retorno aceitável, mas qualquer outro HRESULT menor que zero representa um erro.  
  
 [!code-vb[VSSDKHRESULTInformation#1](../../extensibility/internals/codesnippet/VisualBasic/using-visual-studio-interop-assemblies_1.vb)]
 [!code-csharp[VSSDKHRESULTInformation#1](../../extensibility/internals/codesnippet/CSharp/using-visual-studio-interop-assemblies_1.cs)]  
  
 Se existir mais de um aceitáveis valores de retorno, valores adicionais de HRESULT apenas podem ser anexados à lista na chamada para <xref:Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure%2A>.  
  
 [!code-vb[VSSDKHRESULTInformation#2](../../extensibility/internals/codesnippet/VisualBasic/using-visual-studio-interop-assemblies_2.vb)]
 [!code-csharp[VSSDKHRESULTInformation#2](../../extensibility/internals/codesnippet/CSharp/using-visual-studio-interop-assemblies_2.cs)]  
  
## <a name="returning-hresults-to-com-from-managed-code"></a>Retornando HRESULTS para COM do código gerenciado  
 Se nenhuma exceção ocorrer, gerenciados código retorna <xref:Microsoft.VisualStudio.VSConstants.S_OK> para a função COM que o chamou. Interoperabilidade COM oferece suporte a exceções comuns que são fortemente tipadas no código gerenciado. Por exemplo, um método que recebe um inaceitável `null` argumento lança um <xref:System.ArgumentNullException>.  
  
 Se você não tiver certeza de qual exceção a ser lançada, mas você sabe o HRESULT que você deseja retornar ao COM, você pode usar o <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> método para lançar uma exceção apropriada. Isso funciona mesmo com um erro não padrão, por exemplo, <xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>. <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> tenta mapear o HRESULT passado a uma exceção fortemente tipada. Se não for possível, ele lança uma exceção COM genéricos em vez disso. O resultado final é que o HRESULT que você passar para <xref:System.Runtime.InteropServices.Marshal.ThrowExceptionForHR%2A> de código gerenciado é retornado para a função COM que o chamou.  
  
> [!NOTE]
>  Exceções de comprometem o desempenho e são destinadas para indicar as condições de programa anormal. Condições que ocorrem com frequência devem ser manipulada embutida, em vez de uma exceção lançada.  
  
## <a name="iunknown-parameters-passed-as-type-void"></a>Parâmetros de IUnknown passados como tipo void * *  
 Procure [os parâmetros que são definidos como tipo out] `void **` no COM interface, mas que são definidos como `[``iid_is``]` no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Às vezes, uma interface COM gera um `IUnknown` objeto e a interface COM, em seguida, passa como tipo `void **`. Essas interfaces são especialmente importantes porque se a variável for definida como [out] em IDL, em seguida, o `IUnknown` objeto é contado por referência com o `AddRef` método. Um vazamento de memória ocorre se o objeto não é manipulado corretamente.  
  
> [!NOTE]
>  Um `IUnknown` objeto criado pela interface do COM e retornados em uma variável [out] faz com que um vazamento de memória se não for liberado explicitamente.  
  
 Métodos gerenciados que lidar com esses objetos devem tratar <xref:System.IntPtr> como um ponteiro para um `IUnknown` do objeto e, em seguida, chamar o <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> método para obter o objeto. O chamador deve, em seguida, converter o valor de retorno para o tipo é apropriado. Quando o objeto não for necessário, chame <xref:System.Runtime.InteropServices.Marshal.Release%2A> para liberá-lo.  
  
 A seguir está um exemplo de chamada a <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A> tratamento e o método de `IUnknown` objeto corretamente:  
  
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
>  Os métodos a seguir são conhecidos como passar `IUnknown` ponteiros de objeto como tipo <xref:System.IntPtr>. Tratá-los, conforme descrito nesta seção.  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.CreateProject%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.QueryViewInterface%2A>  
  
-   <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2.get_CfgType%2A>  
  
## <a name="optional-out-parameters"></a>Opcional [parâmetros out]  
 Procure os parâmetros que são definidos como [out] o tipo de dados (`int`, `object`, e assim por diante) no COM interface, mas que são definidos como matrizes do tipo de dados no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Alguns COM interfaces, como <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>, tratar [out] parâmetros como opcional. Se um objeto não é necessário, essas interfaces COM retornam um `null` ponteiro como o valor desse parâmetro em vez de criar o objeto [out]. Esse comportamento é esperado. Para essas interfaces, `null` ponteiros são considerados como parte do comportamento correto do VSPackage e nenhum erro será retornado.  
  
 Porque o CLR não permite que o valor de um parâmetro [out] para ser `null`, não é parte do comportamento dessas interfaces diretamente disponível no código gerenciado. O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] métodos de assembly de interoperabilidade para interfaces afetados contornar o problema definindo os parâmetros relevantes como matrizes porque o CLR permite a passagem de `null` matrizes.  
  
 Implementações gerenciadas desses métodos devem colocar um `null` matriz para o parâmetro quando não há nada a ser retornado. Caso contrário, crie uma matriz de um elemento do tipo correto e colocar o valor de retorno na matriz.  
  
 Gerenciado métodos que recebem informações de interfaces com opcional [out] os parâmetros recebem o parâmetro como uma matriz. Basta examine o valor do primeiro elemento da matriz. Se não for `null`, trate o primeiro elemento como se fosse o parâmetro original.  
  
## <a name="passing-constants-in-pointer-parameters"></a>Constantes de passagem em parâmetros de ponteiro  
 Procure os parâmetros que são definidos como [in] ponteiros na interface COM, mas que são definidos como um <xref:System.IntPtr> digite o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Um problema semelhante ocorre quando uma interface COM transmite um valor especial, como 0, -1 ou -2, em vez de um ponteiro de objeto. Ao contrário de [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)], o CLR não permite constantes ser convertidos em objetos. Em vez disso, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] assembly de interoperabilidade define o parâmetro como um <xref:System.IntPtr> tipo.  
  
 Gerenciado implementações dos métodos a seguir devem tirar proveito do fato de que o <xref:System.IntPtr> classe tem ambos `int` e `void *` construtores para criar um <xref:System.IntPtr> de um objeto ou uma constante inteira, conforme apropriado.  
  
 Gerenciado métodos que recebem <xref:System.IntPtr> parâmetros desse tipo devem usar o <xref:System.IntPtr> digite operadores de conversão para lidar com os resultados. Primeiro, converta o <xref:System.IntPtr> para `int` e testá-lo em constantes de inteiro relevantes. Se nenhum valor corresponder, convertê-lo em um objeto do tipo necessário e continue.  
  
 Para obter exemplos de isso, consulte <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>.  
  
## <a name="ole-return-values-passed-as-out-parameters"></a>OLE retornar valores passados como [parâmetros out]  
 Procure métodos que têm um `retval` o valor de retorno na interface COM, mas que têm um `int` retornar valor e um [parâmetro de matriz em out] adicionais a [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] protótipo do método de assembly de interoperabilidade. Deve ficar claro que esses métodos requerem tratamento especial porque o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] protótipos de método do assembly de interoperabilidade tem um parâmetro mais que os métodos de interface COM.  
  
 Interfaces COM muitos que lidam com a atividade OLE enviar informações sobre o status OLE volta para o programa de chamada armazenado no `retval` retornar o valor da interface. Em vez de usar um valor de retorno correspondente [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] métodos de assembly de interoperabilidade enviar as informações de volta para o programa de chamada armazenado em um [out] o parâmetro de matriz.  
  
 Implementações gerenciadas desses métodos devem criar uma matriz de elemento único do mesmo tipo que o parâmetro [out] e colocá-la no parâmetro. O valor do elemento da matriz deve ser o mesmo que o apropriado COM `retval`.  
  
 Métodos gerenciados que chamam as interfaces desse tipo devem obter o primeiro elemento de matriz [out]. Esse elemento pode ser tratado como se fosse um `retval` valor de retorno da interface COM correspondente.  
  
## <a name="see-also"></a>Consulte também  
 [Interoperação com código não gerenciado](/dotnet/framework/interop/index)