---
title: 'Como: Especifique uma URL de suporte para pré-requisitos individuais em uma implantação de ClickOnce | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- ClickOnce deployment, URLs
ms.assetid: 590742c3-a286-4160-aa75-7a441bb2207b
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f272f1b7a8fc970ab616ba1c02e815cbb6ecb568
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60059130"
---
# <a name="how-to-specify-a-support-url-for-individual-prerequisites-in-a-clickonce-deployment"></a>Como: Especifique uma URL de suporte para pré-requisitos individuais em uma implantação do ClickOnce
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantação pode testar para um número de pré-requisitos que devem estar disponíveis no computador cliente para o [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo seja executado. Isso inclui a versão mínima necessária do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)], a versão do sistema operacional e todos os assemblies que devem ser pré-instalados no cache de assembly global (GAC). [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)], no entanto, não é possível instalar qualquer um desses pré-requisitos em si; Se um pré-requisito não for encontrado, ele simplesmente interrompe a instalação e exibe uma caixa de diálogo explicando por que a instalação falhou.  
  
 Há dois métodos para instalar os pré-requisitos. Você pode instalá-los usando um aplicativo bootstrapper. Como alternativa, você pode especificar uma URL de suporte para pré-requisitos individuais, que é exibida aos usuários na caixa de diálogo se o pré-requisito não for encontrado. A página referenciada por essa URL pode conter links para instruções de instalação dos pré-requisitos necessários. Se um aplicativo não especificar uma URL de suporte para um pré-requisito individual, [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] exibirá a URL de suporte especificada no manifesto de implantação para o aplicativo como um todo, se ele está definido.  
  
 Embora [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], Mage.exe e MageUI.exe podem todos ser usados para gerar [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] implantações, nenhuma dessas ferramentas diretamente suporte à especificação de uma URL de suporte para pré-requisitos individuais. Este documento descreve como modificar sua implantação manifesto do aplicativo e manifesto de implantação para incluí-las dão suporte a URLs.  
  
### <a name="specifying-a-support-url-for-an-individual-prerequisite"></a>Especificando uma URL de suporte para um pré-requisito individual  
  
1. Abra o manifesto do aplicativo (o arquivo. manifest) para sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo em um editor de texto.  
  
2. Para obter um pré-requisito de sistema operacional, adicione a `supportUrl` de atributo para o `dependentOS` elemento:  
  
    ```  
     <dependency>  
        <dependentOS supportUrl="http://www.adatum.com/MyApplication/wrongOSFound.htm">  
          <osVersionInfo>  
            <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" servicePackMinor="0" />  
          </osVersionInfo>  
        </dependentOS>  
      </dependency>  
    ```  
  
3. Para obter um pré-requisito para uma determinada versão do common language runtime, adicione a `supportUrl` de atributo para o `dependentAssembly` entrada que especifica a dependência de tempo de execução de linguagem comum:  
  
    ```  
      <dependency>  
        <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/wrongClrVersionFound.htm">  
          <assemblyIdentity name="Microsoft.Windows.CommonLanguageRuntime" version="4.0.30319.0" />  
        </dependentAssembly>  
      </dependency>  
    ```  
  
4. Para um pré-requisito para um assembly que deve ser pré-instalados no cache de assembly global, defina as `supportUrl` para o `dependentAssembly` elemento que especifica o assembly necessário:  
  
    ```  
      <dependency>  
        <dependentAssembly dependencyType="preRequisite" allowDelayedBinding="true" supportUrl=" http://www.adatum.com/MyApplication/missingSampleGACAssembly.htm">  
          <assemblyIdentity name="SampleGACAssembly" version="5.0.0.0" publicKeyToken="04529dfb5da245c5" processorArchitecture="msil" language="neutral" />  
        </dependentAssembly>  
      </dependency>  
    ```  
  
5. Opcional. Para aplicativos destinados ao .NET Framework 4, abra o manifesto de implantação (o arquivo. Application) para sua [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] aplicativo em um editor de texto.  
  
6. Para obter um pré-requisito do .NET Framework 4, adicione a `supportUrl` de atributo para o `compatibleFrameworks` elemento:  
  
    ```  
    <compatibleFrameworks  xmlns="urn:schemas-microsoft-com:clickonce.v2" supportUrl="http://adatum.com/MyApplication/CompatibleFrameworks.htm">  
      <framework targetVersion="4.0" profile="Client" supportedRuntime="4.0.30319" />  
      <framework targetVersion="4.0" profile="Full" supportedRuntime="4.0.30319" />  
    </compatibleFrameworks>  
    ```  
  
7. Depois que você alterou manualmente o manifesto do aplicativo, você deve assinar novamente o manifesto do aplicativo usando seu certificado digital, em seguida, atualizar e assinar novamente o manifesto de implantação. Você deve usar o Mage.exe ou MageUI.exe SDK das ferramentas para realizar essa tarefa, como regenerar esses arquivos usando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] apaga as alterações manuais. Para obter mais informações sobre como usar Mage.exe assinar novamente os manifestos, consulte [como: Assinar novamente os manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md).  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 A URL de suporte não é exibida na caixa de diálogo se o aplicativo é marcado para ser executado em confiança parcial.  
  
## <a name="see-also"></a>Consulte também  
 [Mage.exe (Manifest Generation and Editing Tool)](http://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [Passo a passo: Implantando um aplicativo ClickOnce manualmente](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)   
 [\<compatibleFrameworks > elemento](../deployment/compatibleframeworks-element-clickonce-deployment.md)   
 [ClickOnce e Authenticode](../deployment/clickonce-and-authenticode.md)   
 [Pré-requisitos de implantação de aplicativos](../deployment/application-deployment-prerequisites.md)
