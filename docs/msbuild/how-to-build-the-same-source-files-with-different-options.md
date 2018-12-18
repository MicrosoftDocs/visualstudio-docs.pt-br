---
title: Como compilar os mesmos arquivos de origem com opções diferentes | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- source files, building with different options
- MSBuild, properties
- project properties, modifying
- Hello World example [Visual Studio]
ms.assetid: d14f1212-ddd9-434f-b138-f840011b0fb2
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e80252582f93c995330f9c586a56e2f8f2c4e6a3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49897167"
---
# <a name="how-to-build-the-same-source-files-with-different-options"></a>Como criar os mesmos arquivos de origem com opções diferentes
Quando compila projetos, frequentemente você compila os mesmos componentes com opções de build diferente. Por exemplo, é possível criar um build de depuração com informações de símbolo ou um build de versão sem nenhuma informação de símbolo, mas com otimizações habilitadas. Ou você pode compilar um projeto para ser executado em uma plataforma específica, como x86 ou [!INCLUDE[vcprx64](../extensibility/internals/includes/vcprx64_md.md)]. Em todos esses casos, a maioria das opções de build permanecem as mesmas, apenas algumas opções são alteradas para controlar a configuração de build. Com [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], você usa propriedades e condições para criar as diferentes configurações de build.  
  
## <a name="use-properties-to-modify-projects"></a>Usar propriedades para modificar projetos  
 O elemento `Property` define uma variável que é referenciada várias vezes em um arquivo de projeto, como o local de um diretório temporário ou para definir os valores de propriedades que são usadas em várias configurações, como um build de Depuração e um build de Versão. Para saber mais sobre propriedades, confira [Propriedades do MSBuild](../msbuild/msbuild-properties.md).  
  
 Você pode usar propriedades para alterar a configuração de seu build sem precisar alterar o arquivo de projeto. O atributo `Condition` do elemento `Property` e do elemento `PropertyGroup` permite alterar o valor de propriedades. Para obter mais informações sobre as condições de [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)], consulte [Condições](../msbuild/msbuild-conditions.md).  
  
#### <a name="to-set-a-group-of-properties-based-on-another-property"></a>Para definir um grupo de propriedades com base em outra propriedade  
  
-   Use um atributo `Condition` em um elemento `PropertyGroup`, semelhante ao seguinte:  
  
    ```xml  
    <PropertyGroup Condition="'$(Flavor)'=='DEBUG'">  
        <DebugType>full</DebugType>  
        <Optimize>no</Optimize>  
    </PropertyGroup>  
    ```  
  
#### <a name="to-define-a-property-based-on-another-property"></a>Para definir uma propriedade com base em outra propriedade  
  
-   Use um atributo `Condition` em um elemento `Property`, semelhante ao seguinte:  
  
    ```xml  
    <DebugType Condition="'$(Flavor)'=='DEBUG'">full</DebugType>  
    ```  
  
## <a name="specify-properties-on-the-command-line"></a>Especificar propriedades na linha de comando  
 Quando o arquivo de projeto é escrito para aceitar várias configurações, você precisa ter a capacidade de alterar essas configurações sempre que compilar o projeto. O [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] fornece essa capacidade, permitindo que propriedades sejam especificadas na linha de comando usando o comutador **-property** ou **-p**.  
  
#### <a name="to-set-a-project-property-at-the-command-line"></a>Para definir uma propriedade de projeto na linha de comando  
  
-   Use a opção **-property** com a propriedade e o valor da propriedade. Por exemplo:  
  
    ```cmd  
    msbuild file.proj -property:Flavor=Debug  
    ```  
  
    ou  
  
    ```cmd  
    Msbuild file.proj -p:Flavor=Debug  
    ```  
  
#### <a name="to-specify-more-than-one-project-property-at-the-command-line"></a>Para especificar mais de uma propriedade de projeto na linha de comando  
  
- Use a opção **-property** ou **-p** várias vezes com a propriedade e os valores de propriedade ou use uma opção **-property** ou **-p** e separe várias propriedades com ponto e vírgula (;). Por exemplo:  
  
  ```cmd  
  msbuild file.proj -p:Flavor=Debug;Platform=x86  
  ```  
  
  ou
  
  ```cmd  
  msbuild file.proj -p:Flavor=Debug -p:Platform=x86  
  ```  
  
  Variáveis de ambiente também são tratadas como propriedades e são incorporadas automaticamente por [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)]. Para obter mais informações sobre como usar variáveis de ambiente, confira [Como usar variáveis de ambiente em um build](../msbuild/how-to-use-environment-variables-in-a-build.md).  
  
  O valor da propriedade especificado na linha de comando tem precedência sobre qualquer valor definido para a mesma propriedade no arquivo de projeto e o valor no arquivo de projeto tem precedência sobre o valor em uma variável de ambiente.  
  
  É possível alterar esse comportamento usando o atributo `TreatAsLocalProperty` em uma marca de projeto. Para nomes de propriedades listados com esse atributo, o valor da propriedade especificado na linha de comando não tem precedência sobre o valor no arquivo de projeto. Veja um exemplo mais adiante neste tópico.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código seguinte, o projeto "Hello World", contém dois novos grupos de propriedade que podem ser usados para criar um build de Depuração e um build de Versão.  
  
 Para compilar a versão de depuração do projeto, digite:  
  
```cmd  
msbuild consolehwcs1.proj -p:flavor=debug  
```  
  
 Para compilar a versão comercial do projeto, digite:  
  
```cmd  
msbuild consolehwcs1.proj -p:flavor=retail  
```  
  
```xml  
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
  
```cmd  
msbuild colortest.proj -t:go -property:Color=Green  
```  
  
```xml  
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
[MSBuild](../msbuild/msbuild.md)  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Referência do MSBuild](../msbuild/msbuild-reference.md)   
 [Elemento Project (MSBuild)](../msbuild/project-element-msbuild.md)