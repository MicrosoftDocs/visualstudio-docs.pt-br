---
title: Como compilar os mesmos arquivos de origem com opções diferentes | Microsoft Docs
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
- source files, building with different options
- MSBuild, properties
- project properties, modifying
- Hello World example [Visual Studio]
ms.assetid: d14f1212-ddd9-434f-b138-f840011b0fb2
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: c46d0577d19a3b3ad0fcd150f33d400e76d550d3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830997"
---
# <a name="how-to-build-the-same-source-files-with-different-options"></a>Como compilar os mesmos arquivos de origem com opções diferentes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando compila projetos, frequentemente você compila os mesmos componentes com opções de build diferente. Por exemplo, é possível criar um build de depuração com informações de símbolo ou um build de versão sem nenhuma informação de símbolo, mas com otimizações habilitadas. Ou você pode compilar um projeto para ser executado em uma plataforma específica, como x86 ou [!INCLUDE[vcprx64](../includes/vcprx64-md.md)]. Em todos esses casos, a maioria das opções de build permanecem as mesmas, apenas algumas opções são alteradas para controlar a configuração de build. Com [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)], você usa propriedades e condições para criar as diferentes configurações de build.  
  
## <a name="using-properties-to-modify-projects"></a>Usando propriedades para modificar projetos  
 O elemento `Property` define uma variável que é referenciada várias vezes em um arquivo de projeto, como o local de um diretório temporário ou para definir os valores de propriedades que são usadas em várias configurações, como um build de Depuração e um build de Versão. Para obter mais informações sobre as propriedades, consulte [Propriedades do MSBuild](msbuild-properties1.md).  
  
 Você pode usar propriedades para alterar a configuração de seu build sem precisar alterar o arquivo de projeto. O atributo `Condition` do elemento `Property` e do elemento `PropertyGroup` permite alterar o valor de propriedades. Para obter mais informações sobre as condições de [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)], consulte [Condições](../msbuild/msbuild-conditions.md).  
  
#### <a name="to-set-a-group-of-properties-based-on-another-property"></a>Para definir um grupo de propriedades com base em outra propriedade  
  
-   Use um atributo `Condition` em um elemento `PropertyGroup`, semelhante ao seguinte:  
  
    ```  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
    ```  
  
#### <a name="to-define-a-property-based-on-another-property"></a>Para definir uma propriedade com base em outra propriedade  
  
-   Use um atributo `Condition` em um elemento `Property`, semelhante ao seguinte:  
  
    ```  
    <DebugType Condition="'$(Flavor)'=='DEBUG'">full</DebugType>  
    ```  
  
## <a name="specifying-properties-on-the-command-line"></a>Especificando propriedades na linha de comando  
 Quando o arquivo de projeto é escrito para aceitar várias configurações, você precisa ter a capacidade de alterar essas configurações sempre que compilar o projeto. O [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] fornece essa capacidade, permitindo que propriedades sejam especificadas na linha de comando usando o comutador **/property** ou **/p**.  
  
#### <a name="to-set-a-project-property-at-the-command-line"></a>Para definir uma propriedade de projeto na linha de comando  
  
-   Use o comutador **/property** com a propriedade e o valor da propriedade. Por exemplo:  
  
    ```  
    msbuild file.proj /property:Flavor=Debug  
    ```  
  
     - ou –  
  
    ```  
    Msbuild file.proj /p:Flavor=Debug  
    ```  
  
#### <a name="to-specify-more-than-one-project-property-at-the-command-line"></a>Para especificar mais de uma propriedade de projeto na linha de comando  
  
- Use o comutador **/property** ou **/p** várias vezes com a propriedade e os valores de propriedade ou use um comutador **/property** ou **/p** e separe várias propriedades com ponto e vírgula (;). Por exemplo:  
  
  ```  
  msbuild file.proj /p:Flavor=Debug;Platform=x86  
  ```  
  
   - ou –  
  
  ```  
  msbuild file.proj /p:Flavor=Debug /p:Platform=x86  
  ```  
  
  Variáveis de ambiente também são tratadas como propriedades e são incorporadas automaticamente por [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)]. Para obter mais informações sobre o uso de variáveis de ambiente, consulte [Como usar variáveis de ambiente em um build](../msbuild/how-to-use-environment-variables-in-a-build.md).  
  
  O valor da propriedade especificado na linha de comando tem precedência sobre qualquer valor definido para a mesma propriedade no arquivo de projeto e o valor no arquivo de projeto tem precedência sobre o valor em uma variável de ambiente.  
  
  É possível alterar esse comportamento usando o atributo `TreatAsLocalProperty` em uma marca de projeto. Para nomes de propriedades listados com esse atributo, o valor da propriedade especificado na linha de comando não tem precedência sobre o valor no arquivo de projeto. Veja um exemplo mais adiante neste tópico.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código seguinte, o projeto "Hello World", contém dois novos grupos de propriedade que podem ser usados para criar um build de Depuração e um build de Versão.  
  
 Para compilar a versão de depuração do projeto, digite:  
  
```  
msbuild consolehwcs1.proj /p:flavor=debug  
```  
  
 Para compilar a versão comercial do projeto, digite:  
  
```  
msbuild consolehwcs1.proj /p:flavor=retail  
```  
  
```  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <!-- Sets the default flavor of an environment variable called   
    Flavor is not set or specified on the command line -->  
    <PropertyGroup>  
        <Flavor Condition="'$(Flavor)'==''">DEBUG</Flavor>  
    </PropertyGroup>  
  
    <!-- Define the DEBUG settings -->  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
  
    <!-- Define the RETAIL settings -->  
    <PropertyGroup Condition="'$(Flavor)'=='RETAIL'">  
        <DebugType>pdbonly</DebugType>  
        <Optimize>yes</Optimize>  
    </PropertyGroup>  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldCS</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using input files  
        of type CSFile -->  
        <CSC  Sources = "@(CSFile)"  
            DebugType="$(DebugType)"  
            Optimize="$(Optimize)"  
            OutputAssembly="$(appname).exe" >  
  
            <!-- Set the OutputAssembly attribute of the CSC  
            task to the name of the executable file that is   
            created -->  
            <Output TaskParameter="OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como usar o atributo `TreatAsLocalProperty`. A propriedade `Color` tem um valor de `Blue` no arquivo de projeto e `Green` na linha de comando. Com `TreatAsLocalProperty="Color"` na marca de projeto, a propriedade de linha de comando (`Green`) não substitui a propriedade definida no arquivo de projeto (`Blue`).  
  
 Para compilar o projeto, digite o seguinte comando:  
  
```  
msbuild colortest.proj /t:go /property:Color=Green  
```  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
ToolsVersion="4.0" TreatAsLocalProperty="Color">  
  
    <PropertyGroup>  
        <Color>Blue</Color>  
    </PropertyGroup>  
  
    <Target Name="go">  
        <Message Text="Color: $(Color)" />  
    </Target>  
</Project>  
  
<!--  
  Output with TreatAsLocalProperty="Color" in project tag:  
     Color: Blue  
  
  Output without TreatAsLocalProperty="Color" in project tag:  
     Color: Green  
-->  
```  
  
## <a name="see-also"></a>Consulte também  
[MSBuild](msbuild.md)  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Elemento Project (MSBuild)](../msbuild/project-element-msbuild.md)


