---
title: Tarefa GenerateBootstrapper | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateBootstrapper
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateBootstrapper task
- GenerateBootstrapper task [MSBuild]
ms.assetid: ca3ba2c6-d2ea-41f2-b7e3-0fc2b0730460
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 85ea10b956069415198feb74be8c9e546ecc7ff8
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54769217"
---
# <a name="generatebootstrapper-task"></a>Tarefa GenerateBootstrapper
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Fornece uma forma automatizada de detectar, baixar e instalar um aplicativo e seus pré-requisitos. Atua como um único instalador que integra os diferentes instaladores de todos os componentes que compõem um aplicativo.  
  
## <a name="task-parameters"></a>Parâmetros da tarefa  
 A tabela a seguir descreve os parâmetros da tarefa `GenerateBootstrapper`.  
  
- `ApplicationFile`  
  
   Parâmetro `String` opcional.  
  
   Especifica o arquivo que o bootstrapper usará para iniciar a instalação do aplicativo após todos os pré-requisitos terem sido instalados. Um erro de build ocorrerá se nenhum dos parâmetros `BootstrapperItems` ou `ApplicationFile` for especificado.  
  
- `ApplicationName`  
  
   Parâmetro `String` opcional.  
  
   Especifica o nome do aplicativo que o bootstrapper instalará. Esse nome aparecerá na interface do usuário que o bootstrapper usa durante a instalação.  
  
- `ApplicationRequiresElevation`  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, o componente será executado com permissões elevadas quando for instalado em um computador de destino.  
  
- `ApplicationUrl`  
  
   Parâmetro `String` opcional.  
  
   Especifica o local da Web que está hospedando o instalador do aplicativo.  
  
- `BootstrapperComponentFiles`  
  
   Parâmetro de saída `String[]` opcional.  
  
   Especifica o local interno dos arquivos do pacote do bootstrapper.  
  
- `BootstrapperItems`  
  
   Parâmetro opcional <xref:Microsoft.Build.Framework.ITaskItem>`[]`.  
  
   Especifica os produtos a serem inseridos no bootstrapper. Os itens passados para esse parâmetro devem ter a seguinte sintaxe:  
  
  ```  
  <BootstrapperItem  
      Include="ProductCode">  
      <ProductName>  
          ProductName  
      </ProductName>  
  </BootstrapperItem>  
  ```  
  
   O atributo `Include` é usado para representar o nome de um pré-requisito que deve ser instalado. Os metadados do item `ProductName` são opcionais e serão usados pelo mecanismo de build como um nome amigável caso o pacote não possa ser encontrado. Esses itens não são parâmetros de entrada de [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] obrigatórios, a menos que nenhum `ApplicationFile` seja especificado. Você precisa incluir um item para cada pré-requisito que precisar ser instalado para seu aplicativo.  
  
   Um erro de build ocorrerá se nenhum dos parâmetros `BootstrapperItems` ou `ApplicationFile` for especificado.  
  
- `BootstrapperKeyFile`  
  
   Parâmetro de saída `String` opcional.  
  
   Especifica a localização interna de setup.exe  
  
- `ComponentsLocation`  
  
   Parâmetro `String` opcional.  
  
   Especifica um local no qual o bootstrapper deverá procurar os pré-requisitos de instalação a serem instalados. Esse parâmetro pode ter os seguintes valores:  
  
  - `HomeSite`: indica que o pré-requisito está sendo hospedado pelo fornecedor do componente.  
  
  - `Relative`: indica que o pré-requisito está no mesmo local que o aplicativo.  
  
  - `Absolute`: indica que todos os componentes serão encontrados em uma URL centralizada. Esse valor deve ser usado em conjunto com o parâmetro de entrada `ComponentsUrl`.  
  
    Se `ComponentsLocation` não for especificado, `HomeSite` será usado por padrão.  
  
- `ComponentsUrl`  
  
   Parâmetro `String` opcional.  
  
   Especifica a URL que contém os pré-requisitos de instalação.  
  
- `CopyComponents`  
  
   Parâmetro `Boolean` opcional.  
  
   Se for `true`, o bootstrapper copiará todos os arquivos de saída para o caminho especificado no parâmetro `OutputPath`. Os valores do parâmetro `BootstrapperComponentFiles` devem ser baseados nesse caminho. Se for `false`, os arquivos não serão copiados e o valores de `BootstrapperComponentFiles` serão baseados no valor do parâmetro `Path`.  O valor padrão desse parâmetro é `true`.  
  
- `Culture`  
  
   Parâmetro `String` opcional.  
  
   Especifica a cultura a ser usada para a interface do usuário do bootstrapper e os pré-requisitos de instalação. Se a cultura especificada estiver indisponível, a tarefa usará o valor do parâmetro `FallbackCulture`.  
  
- `FallbackCulture`  
  
   Parâmetro `String` opcional.  
  
   Especifica a cultura secundária a ser usada para a interface do usuário do bootstrapper e os pré-requisitos de instalação.  
  
- `OutputPath`  
  
   Parâmetro `String` opcional.  
  
   Especifica o local para o qual copiar setup.exe e todos os arquivos do pacote.  
  
- `Path`  
  
   Parâmetro `String` opcional.  
  
   Especifica o local de todos os pacotes de pré-requisitos disponíveis.  
  
- `SupportUrl`  
  
   Parâmetro `String` opcional.  
  
   Especifica a URL a ser fornecida caso a instalação do bootstrapper falhe  
  
- `Validate`  
  
   Parâmetro `Boolean` opcional.  
  
   Se for `true`, o bootstrapper executará a validação do XSD nos itens de entrada do bootstrapper especificados. O valor padrão desse parâmetro é `false`.  
  
## <a name="remarks"></a>Comentários  
 Além dos parâmetros listados acima, essa tarefa herda parâmetros da classe <xref:Microsoft.Build.Tasks.TaskExtension>, que herda da classe <xref:Microsoft.Build.Utilities.Task>. Para obter uma lista desses parâmetros adicionais e suas descrições, consulte [Classe base TaskExtension](../msbuild/taskextension-base-class.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa a tarefa `GenerateBootstrapper` para instalar um aplicativo que deve ter o [!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)] instalado como pré-requisito.  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <BootstrapperFile Include="Microsoft.Net.Framework.2.0">  
            <ProductName>Microsoft .NET Framework 2.0</ProductName>  
        </BootstrapperFile>  
    </ItemGroup>  
  
    <Target Name="BuildBootstrapper">  
        <GenerateBootstrapper  
            ApplicationFile="WindowsApplication1.application"  
            ApplicationName="WindowsApplication1"  
            ApplicationUrl="http://mycomputer"  
            BootstrapperItems="@(BootstrapperFile)"  
            OutputPath="C:\output" />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tarefas](../msbuild/msbuild-tasks.md)   
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)
