---
title: Parâmetro de Assembly de interoperabilidade do Visual Studio Marshaling | Microsoft Docs
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
- troubleshooting Visual Studio SDK interop assemblies
- interop assemblies, parameter marshaling
- interop assemblies, troubleshooting
ms.assetid: 89123eae-0fef-46d5-bd36-3d2a166b14e3
caps.latest.revision: 24
manager: douge
ms.openlocfilehash: e18667adb48f565f73acc14f5012f9c96283efe9
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49195007"
---
# <a name="visual-studio-interop-assembly-parameter-marshaling"></a>Parâmetro de Assembly de interoperabilidade do Visual Studio de Marshaling
Os VSPackages são escritos em código gerenciado pode ter que chamar ou ser chamado pelo código COM não gerenciado. Normalmente, os argumentos de método são transformados ou marshaling, automaticamente pelo marshaler de interoperabilidade. No entanto, às vezes, argumentos não podem ser transformados de uma maneira simples. Nesses casos, os parâmetros de protótipo do método de assembly de interoperabilidade são usados para corresponder ao máximo os parâmetros da função COM. Para obter mais informações, consulte [Marshaling de interoperabilidade](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a).  
  
## <a name="general-suggestions"></a>Sugestões gerais  
  
##### <a name="read-the-reference-documentation"></a>Leia a documentação de referência  
 É uma maneira eficaz para detectar problemas de interoperabilidade ler a documentação de referência para cada método.  
  
 A documentação de referência para cada método contém três seções relevantes:  
  
-   O [!INCLUDE[vcprvc](../includes/vcprvc-md.md)] protótipo de função COM.  
  
-   O protótipo do método de assembly de interoperabilidade.  
  
-   Uma lista de parâmetros COM e uma breve descrição de cada um.  
  
##### <a name="look-for-differences-between-the-two-prototypes"></a>Procure as diferenças entre os dois protótipos  
 A maioria dos problemas de interoperabilidade derivam de incompatibilidades entre a definição de um determinado tipo em uma interface COM e a definição do mesmo tipo no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] assemblies de interoperabilidade. Por exemplo, considere a diferença na capacidade de passar um `null` valor em um parâmetro [out]. Você deve examinar as diferenças entre os dois protótipos e considerar suas ramificações para os dados que está sendo passados.  
  
##### <a name="read-the-parameter-definitions"></a>Ler as definições de parâmetro  
 Ler as definições de parâmetro. O COM é menos rigorosa do que o common language runtime (CLR) sobre a combinação de diferentes tipos de dados em um único parâmetro. O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] interfaces COM aproveitarem ao máximo essa flexibilidade. Qualquer parâmetro que pode passar ou exigem um valor não padrão ou o tipo de dados, como um valor constante em um parâmetro de ponteiro, deve ser descrito como tal na documentação.  
  
### <a name="iunknown-objects-passed-as-type-void"></a>IUnknown objetos passados como tipo void * *  
 Procure [out] os parâmetros que são definidos como tipo `void **` no COM a interface, mas que são definidas como `[``iid_is``]` no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade.  
  
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
  
### <a name="optional-out-parameters"></a>Opcional [parâmetros out]  
 Procure os parâmetros que são definidos como [out] o tipo de dados (`int`, `object`e assim por diante) no COM a interface, mas que são definidos como matrizes do mesmo tipo de dados no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Alguns COM interfaces, como <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2.GetCfgs%2A>, tratar [out] parâmetros como opcional. Se um objeto não é necessário, essas interfaces COM retornam um `null` ponteiro como o valor desse parâmetro em vez de criar o objeto [out]. Esse comportamento é esperado. Para essas interfaces, `null` ponteiros são considerados como parte do comportamento correto do VSPackage, e nenhum erro será retornado.  
  
 Porque o CLR não permite que o valor de um parâmetro [out] para ser `null`, parte do que o comportamento padrão dessas interfaces não está disponível diretamente no código gerenciado. O [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] métodos de assembly de interoperabilidade para interfaces afetados contornar o problema definindo os parâmetros relevantes como matrizes, como o CLR permite a passagem de `null` matrizes.  
  
 Implementações gerenciadas desses métodos devem colocar um `null` matriz para o parâmetro quando não há nada a ser retornado. Caso contrário, crie uma matriz de um elemento do tipo correto e coloque o valor retornado na matriz.  
  
 Gerenciado os métodos que recebem informações de interfaces com opcional [out] os parâmetros recebem o parâmetro como uma matriz. Basta examine o valor do primeiro elemento da matriz. Se não for `null`, trate o primeiro elemento, como se fosse o parâmetro original.  
  
### <a name="passing-constants-in-pointer-parameters"></a>Constantes de passagem em parâmetros de ponteiro  
 Procure os parâmetros que são definidas como [in] ponteiros na interface COM, mas que são definidos como um <xref:System.IntPtr> digite o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade.  
  
 Um problema semelhante ocorre quando uma interface COM transmite um valor especial, como 0, -1 ou – 2, em vez de um ponteiro de objeto. Ao contrário de [!INCLUDE[vcprvc](../includes/vcprvc-md.md)], o CLR não permite constantes ser convertido como objetos. Em vez disso, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] assembly de interoperabilidade define o parâmetro como um <xref:System.IntPtr> tipo.  
  
 Implementações gerenciadas desses métodos devem tirar proveito do fato de que o <xref:System.IntPtr> classe tem ambos `int` e `void *` construtores para criar um <xref:System.IntPtr> de um objeto ou uma constante de inteiro, conforme apropriado.  
  
 Gerenciado os métodos que recebem <xref:System.IntPtr> parâmetros desse tipo devem usar o <xref:System.IntPtr> digite operadores de conversão para lidar com os resultados. Primeiro, converta a <xref:System.IntPtr> para `int` e testá-lo em constantes de inteiro relevantes. Se não há valores corresponderem, convertê-lo em um objeto do tipo necessário e continuar.  
  
 Para obter exemplos de isso, consulte <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenSpecificEditor%2A>.  
  
### <a name="ole-return-values-passed-as-out-parameters"></a>OLE retornam valores passados como [parâmetros out]  
 Procure por métodos que têm uma `retval` valor de retorno na interface COM, mas que têm um `int` valor de retorno e um adicional [out] do parâmetro de matriz na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] protótipo do método de assembly de interoperabilidade. Deve ficar claro que esses métodos exigem tratamento especial, porque o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] protótipos de método do assembly de interoperabilidade tem um parâmetro a mais que os métodos de interface COM.  
  
 Várias interfaces COM que lidam com a atividade de OLE enviar informações sobre o status OLE volta para o programa de chamada armazenado no `retval` retornar o valor da interface. Em vez de usar um valor de retorno correspondente [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] métodos do assembly de interoperabilidade enviar as informações de volta para o programa de chamada armazenado em um [out] o parâmetro de matriz.  
  
 Gerenciado implementações dos métodos a seguir devem criar uma matriz de elemento único, do mesmo tipo como o parâmetro [out] e colocá-lo no parâmetro. O valor do elemento da matriz deve ser o mesmo que o apropriada COM `retval`.  
  
 Métodos gerenciados que chamam as interfaces desse tipo devem obter o primeiro elemento da matriz [out]. Esse elemento pode ser tratado como se fosse um `retval` retornar valor de interface COM correspondente.  
  
## <a name="see-also"></a>Consulte também  
 [Marshaling de interoperabilidade](http://msdn.microsoft.com/en-us/a95fdb76-7c0d-409e-a77e-0349b1ea1490)   
 [Marshaling de interoperabilidade](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)   
 [Solucionando problemas de interoperabilidade](http://msdn.microsoft.com/library/b324cc1e-b03c-4f39-aea6-6a6d5bfd0e37)   
 [VSPackages gerenciados](../misc/managed-vspackages.md)