---
title: Tarefa FileClassifier | Microsoft Docs
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
- classifying a resource set to embed in an assembly [WPF MSBuild]
- non-localizable resources [WPF MSBuild], classifying to embed in an assembly
- FileClassifier task [WPF MSBuild]
ms.assetid: 14e03310-fcc0-4bb2-a84d-cda12be66367
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2e0515d4f21993a50ce590df10ca283e6e66b17a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49271437"
---
# <a name="fileclassifier-task"></a>Tarefa FileClassifier
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O <xref:Microsoft.Build.Tasks.Windows.FileClassifier> classifica um conjunto de recursos de origem uma vez que eles serão inseridos em um assembly. Se um recurso não for localizável, ele será inserido no assembly principal do aplicativo; caso contrário, ele será inserido em um assembly satélite.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`CLREmbeddedResource`|Não utilizado.|  
|`CLRResourceFiles`|Não utilizado.|  
|`CLRSatelliteEmbeddedResource`|Não utilizado.|  
|`Culture`|Parâmetro **String** opcional.<br /><br /> Especifica a cultura para o build. Esse valor pode ser **nulo** se o build não for localizável. Se for **nulo**, o valor padrão será o valor em letras minúsculas que **CultureInfo.InvariantCulture** retorna.|  
|`MainEmbeddedFiles`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Especifica os recursos não localizáveis que são inseridos no assembly principal.|  
|`OutputType`|Parâmetro da **cadeia de caracteres** obrigatório.<br /><br /> Especifica o tipo de arquivo no qual inserir os arquivos de origem especificados. Os valores válidos são **exe**, **winexe** ou **library**.|  
|`SatelliteEmbeddedFiles`|Parâmetro de saída opcional **ITaskItem[]**.<br /><br /> Especifica os arquivos localizáveis que são inseridos no assembly satélite para a cultura especificada pelo parâmetro **Culture**.|  
|`SourceFiles`|Parâmetro obrigatório **ITaskItem[]**.<br /><br /> Especifica a lista de arquivos a classificar.|  
  
## <a name="remarks"></a>Comentários  
 Se o parâmetro **Culture** não é definido, todos os recursos especificados usando o parâmetro **SourceFiles** não são localizáveis; caso contrário, eles são localizáveis, a menos que eles estejam associados com um atributo **Localizable** definido como **false**.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir classifica um único arquivo de origem como um recurso e, em seguida, insere-o em um assembly satélite para a cultura Francês canadense (fr-CA).  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask  
    TaskName="Microsoft.Build.Tasks.Windows.FileClassifier"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <ItemGroup>  
    <Resource Include="Resource1.bmp" />  
  </ItemGroup>  
  <Target Name="FileClassifierTask">  
    <FileClassifier  
      SourceFiles="Resource1.bmp"  
      Culture="fr-CA"  
      OutputType="exe" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência MSBuild do WPF](../msbuild/wpf-msbuild-reference.md)   
 [Referência de tarefas](../msbuild/wpf-msbuild-task-reference.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)   
 [Como compilar um aplicativo WPF (WPF)](http://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)



