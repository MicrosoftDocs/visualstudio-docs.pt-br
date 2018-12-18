---
title: Tarefa SignFile | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#SignFile
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, SignFile task
- SignFile task [MSBuild]
ms.assetid: edef1819-ddeb-4e09-95de-fc7063ba9388
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 849c82fe11e4440c4b3394532ceecfe30ef57253
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49206397"
---
# <a name="signfile-task"></a>Tarefa SignFile
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Assina o arquivo especificado usando o certificado especificado.  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa `SignFile`.  
  
 Observe que os certificados SHA-256 são permitidos apenas em computadores que tenham o .NET 4.5 e superior.  
  
> [!WARNING]
>  A partir do Visual Studio 2013 Atualização 3, essa tarefa tem uma nova assinatura que permite que você especifique a versão da estrutura de destino do arquivo. Você é incentivado a usar a nova assinatura sempre que possível, pois o processo do MSBuild usa hashes SHA-256 somente quando a estrutura de destino for .NET 4.5 ou superior. Se a estrutura de destino for .NET 4.0 ou abaixo, o hash SHA-256 não será usado.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`CertificateThumbprint`|Parâmetro `String` obrigatório.<br /><br /> Especifica o certificado a ser usado para a assinatura. Esse certificado deve estar no repositório pessoal do usuário atual.|  
|`SigningTarget`|Parâmetro <xref:Microsoft.Build.Framework.ITaskItem> obrigatório.<br /><br /> Especifica os arquivos a serem assinados com o certificado.|  
|`TimestampUrl`|Parâmetro `String` opcional.<br /><br /> Especifica a URL de um servidor de carimbo de data/hora.|  
|`TargetFrameworkVersion`|A versão do .NET Framework que é usada para o destino.|  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Tarefa de Classe Base](../msbuild/task-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `SignFile` para assinar os arquivos especificados na coleção de itens `FilesToSign` com o certificado especificado pela propriedade `Certificate`.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <FileToSign Include="File.exe" />  
    </ItemGroup>  
    <PropertyGroup>  
        <Certificate>Cert.cer</Certificate>  
    </PropertyGroup>  
    <Target Name="Sign">  
        <SignFile  
            CertificateThumbprint="$(CertificateThumbprint)"  
            SigningTarget="@(FileToSign)"   
            TargetFrameworkVersion="v4.5" />  
    </Target>  
</Project>  
```  
  
> [!NOTE]
>  A impressão digital do certificado é o hash SHA-1 do certificado. Para obter mais informações, consulte [Obter o hash SHA-1 de um certificado de autoridade de certificação raiz confiável](http://msdn.microsoft.com/en-us/dd641990-9a88-4228-a245-017797131a87).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `Exec` para assinar os arquivos especificados na coleção de itens `FilesToSign` com o certificado especificado pela propriedade `Certificate`. Você pode usar isso para assinar arquivos do Windows Installer durante o processo de compilação.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <ItemGroup>  
        <FileToSign Include="File.msi" />  
    </ItemGroup>  
    <PropertyGroup>  
        <Certificate>Cert.cer</Certificate>  
    </PropertyGroup>  
    <Target Name="Sign">  
        <Exec Command="signtool.exe sign /f CertFile /p Password "@(FileToSign)" "/>  
        <SignFile  
            CertificateThumbprint="$(CertificateThumbprint)"  
            SigningTarget="@(FileToSign)"   
            TargetFrameworkVersion="v4.0" />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Tarefas](../msbuild/msbuild-tasks.md)



