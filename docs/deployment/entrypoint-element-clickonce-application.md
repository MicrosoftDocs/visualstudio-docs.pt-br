---
title: '&lt;ponto de entrada&gt; elemento (aplicativo ClickOnce) | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- urn:schemas-microsoft-com:asm.v2#commandLine
- urn:schemas-microsoft-com:asm.v2#entryPoint
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- <entryPoint> element [ClickOnce application manifest]
- manifests [ClickOnce], entryPoint element
ms.assetid: 10ad3083-10c1-4189-a870-9bba2eab244f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 56996f83f0ac8d9e7b2bce81ab7e2c8e13faee52
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934620"
---
# <a name="ltentrypointgt-element-clickonce-application"></a>&lt;ponto de entrada&gt; elemento (aplicativo ClickOnce)
Identifica o assembly que deve ser executado quando isso [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo é executado em um computador cliente.  

## <a name="syntax"></a>Sintaxe  

```xml  
<entryPoint  
   name  
>  
   <assemblyIdentity  
      name  
      version  
      processorArchitecture  
      language  
   />  
   <commandLine  
      file  
      parameters  
   />  
   <customHostRequired />  
   <customUX />  
</entryPoint>  
```  

## <a name="elements-and-attributes"></a>Elementos e atributos  
 O `entryPoint` elemento é necessário e está no `urn:schemas-microsoft-com:asm.v2` namespace. Pode haver apenas um `entryPoint` elemento definido em um manifesto de aplicativo.  

 O `entryPoint` elemento tem o seguinte atributo.  

|Atributo|Descrição|  
|---------------|-----------------|  
|`name`|Opcional. Esse valor não é usado pelo .NET Framework.|  

 `entryPoint` tem os seguintes elementos.  

## <a name="assemblyidentity"></a>assemblyIdentity  
 Necessário. A função de `assemblyIdentity` e seus atributos é definida no [ \<assemblyIdentity > elemento](../deployment/assemblyidentity-element-clickonce-application.md).  

 O `processorArchitecture` atributo desse elemento e o `processorArchitecture` atributo definido no `assemblyIdentity` em outro lugar no aplicativo de manifesto deve corresponder.  

## <a name="commandline"></a>linha de comando  
 Necessário. Deve ser um filho de `entryPoint` elemento. Ele não tem elementos filho e tem os seguintes atributos.  


| Atributo | Descrição |
|--------------| - |
| `file` | Necessário. Uma referência local para o assembly de inicialização para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. Esse valor não pode conter barra (/) ou barra invertida (\\) separadores de caminho. |
| `parameters` | Necessário. Descreve a ação a ser tomada com o ponto de entrada. O único valor válido é `run`; se uma cadeia de caracteres em branco for fornecida, `run` será assumido. |

## <a name="customhostrequired"></a>customHostRequired  
 Opcional. Se for incluído, especifica que essa implantação contém um componente que será implantado dentro de um host personalizado e não é um aplicativo autônomo.  

 Se esse elemento estiver presente, o `assemblyIdentity` e `commandLine` elementos não também devem estar presentes. Se elas forem, [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] irá gerar um erro de validação durante a instalação.  

 Este elemento tem atributos não e nenhum filho.  

## <a name="customux"></a>customUX  
 Opcional. Especifica que o aplicativo está instalado e mantido por um instalador personalizado e não cria uma entrada de menu Iniciar, atalhos ou adicionar ou remover programas de entrada.  

```xml  
<customUX xmlns="urn:schemas-microsoft-com:clickonce.v1" />  
```  

 Um aplicativo que inclui o elemento customUX deve fornecer um instalador personalizado que usa o <xref:System.Deployment.Application.InPlaceHostingManager> classe para executar operações de instalação. Um aplicativo com este elemento não pode ser instalado clicando duas vezes em seu manifesto ou setup.exe bootstrapper de pré-requisito. O instalador personalizado pode criar entradas do menu Iniciar, atalhos e entradas de adicionar ou remover programas. Se o instalador personalizado não cria uma entrada de adicionar ou remover programas, ele deve armazenar o identificador de assinatura fornecido pelo <xref:System.Deployment.Application.GetManifestCompletedEventArgs.SubscriptionIdentity%2A> propriedade e habilite o usuário para desinstalar o aplicativo mais tarde, chamando o <xref:System.Deployment.Application.InPlaceHostingManager.UninstallCustomUXApplication%2A> método. Para obter mais informações, consulte [instruções passo a passo: Criando um instalador personalizado para um aplicativo ClickOnce](../deployment/walkthrough-creating-a-custom-installer-for-a-clickonce-application.md).  

## <a name="remarks"></a>Comentários  
 Este elemento identifica o assembly e ponto de entrada para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo.  

 Não é possível usar `commandLine` para passar parâmetros para seu aplicativo em tempo de execução. Você pode acessar parâmetros de cadeia de caracteres de consulta para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] implantação a partir do aplicativo <xref:System.AppDomain>. Para obter mais informações, consulte [como: recuperar informações de cadeia de caracteres de consulta em um aplicativo ClickOnce Online](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md).  

## <a name="example"></a>Exemplo  
 O exemplo de código a seguir ilustra uma `entryPoint` elemento em um manifesto de aplicativo para um [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo. Este exemplo de código é parte de um exemplo maior fornecido para o [manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md) tópico.  

```xml  
<!-- Identify the main code entrypoint. -->  
<!-- This code runs the main method in an executable assembly. -->  
  <entryPoint>  
    <assemblyIdentity   
      name="MyApplication"   
      version="1.0.0.0"  
      language="neutral"  
      processorArchitecture="x86" />  
    <commandLine file="MyApplication.exe" parameters="" />  
  </entryPoint>  
```  

## <a name="see-also"></a>Consulte também  
 [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)
