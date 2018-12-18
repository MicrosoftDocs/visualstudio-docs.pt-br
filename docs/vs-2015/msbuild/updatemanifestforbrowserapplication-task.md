---
title: Tarefa UpdateManifestForBrowserApplication | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- UpdateManifestForBrowserApplication task [WPF MSBuild]
- adding the <hostInBrowser /> element to the application manifest [WPF MSBuild]
- building XBAP projects [WPF MSBuild]
- UpdateManifestForBrowserApplication task [WPF MSBuild], parameters
ms.assetid: 653339f7-654b-4d64-a26a-5c9f27036895
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 4d1549616dcaa2ec998e242c5d39821baabfa39b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49219980"
---
# <a name="updatemanifestforbrowserapplication-task"></a>Tarefa UpdateManifestForBrowserApplication
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A tarefa <xref:Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication> é executada para adicionar o elemento **\<hostInBrowser />** para o manifesto do aplicativo (*projectname*.exe.manifest) quando um projeto [!INCLUDE[TLA#tla_xbap](../includes/tlasharptla-xbap-md.md)] é compilado.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`ApplicationManifest`|Parâmetro obrigatório **ITaskItem[]**.<br /><br /> Especifica o caminho e o nome do arquivo de manifesto do aplicativo ao qual você deseja adicionar o elemento `<hostInBrowser />`.|  
|`HostInBrowser`|Parâmetro **Booliano** opcional.<br /><br /> Especifica se deseja ou não modificar o manifesto do aplicativo para incluir o elemento **\<hostInBrowser />**. Se for **true**, um novo elemento `<`**hostInBrowser />** será incluído no elemento **\<entryPoint />**. Observe que a inclusão do elemento é cumulativa: se um elemento **\<hostInBrowser />** já existe, ele não é removido nem substituído. Em vez disso, um elemento **\<hostInBrowser />** adicional é criado. Se for **false**, o manifesto do aplicativo não será modificado.|  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[TLA2#tla_xbap#plural](../includes/tla2sharptla-xbapsharpplural-md.md)] são executadas usando a implantação [!INCLUDE[TLA#tla_clickonce](../includes/tlasharptla-clickonce-md.md)] e, portanto, devem ser publicadas com suporte a implantação e manifestos de aplicativo. [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] usa a [Tarefa GenerateApplicationManifest](http://msdn2.microsoft.com/library/6wc2ccdc.aspx) para gerar um manifesto do aplicativo.  
  
 Em seguida, para configurar um aplicativo para ser hospedado de um navegador, um elemento adicional, **\<hostInBrowser />**, deve ser adicionado ao manifesto do aplicativo, conforme mostrado no exemplo a seguir:  
  
```  
<!--MyXBAPApplication.exe.manifest-->  
<?xml version="1.0" encoding="utf-8"?>  
<asmv1:assembly ... >  
    <asmv1:assemblyIdentity ... />  
    <application />  
    <entryPoint>  
      ...  
      <hostInBrowser xmlns="urn:schemas-microsoft-com:asm.v3" />  
    </entryPoint>  
  ...  
/>  
```  
  
 A tarefa <xref:Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication> é executada quando um projeto [!INCLUDE[TLA2#tla_xbap](../includes/tla2sharptla-xbap-md.md)] é compilado para adicionar o elemento `<hostInBrowser />`.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como garantir que o elemento `<hostInBrowser />` seja incluído em um arquivo de manifesto do aplicativo.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.UpdateManifestForBrowserApplication"  
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="UpdateManifestForBrowserApplicationTask">  
    <UpdateManifestForBrowserApplication  
      ApplicationManifest="MyXBAPApplication.exe.manifest"  
      HostInBrowser="true" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência MSBuild do WPF](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Compilando um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [Visão geral dos aplicativos de navegador XAML do WPF](http://msdn.microsoft.com/library/3a7a86a8-75d5-4898-96b9-73da151e5e16)



