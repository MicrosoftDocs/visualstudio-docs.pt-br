---
title: Propriedades do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, properties
ms.assetid: 962912ac-8931-49bf-a88c-0200b6e37362
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3c8835dab5ca866762a7d2b0e6cad1d0d80726b0
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48879181"
---
# <a name="msbuild-properties"></a>propriedades MSBuild
Propriedades são pares nome-valor que podem ser usados para configurar compilações. Propriedades são úteis para passar valores para tarefas, avaliar condições e armazenar os valores que serão referenciados em todo o arquivo de projeto.  
  
## <a name="define-and-reference-properties-in-a-project-file"></a>Definir e referenciar propriedades em um arquivo de projeto  
 As propriedades são declaradas com a criação de um elemento que tem o nome da propriedade como um filho de um elemento [PropertyGroup](../msbuild/propertygroup-element-msbuild.md). Por exemplo, o XML a seguir cria uma propriedade chamada `BuildDir` que tem um valor de `Build`.  
  
```xml  
<PropertyGroup>  
    <BuildDir>Build</BuildDir>  
</PropertyGroup>  
```  
  
 Em todo o arquivo de projeto, as propriedades são referenciadas usando a sintaxe $(\<PropertyName>). Por exemplo, a propriedade no exemplo anterior é referenciada usando $(BuildDir).  
  
 Os valores de propriedade podem ser alterados redefinindo a propriedade. A propriedade `BuildDir` pode receber um novo valor usando este XML:  
  
```xml  
<PropertyGroup>  
    <BuildDir>Alternate</BuildDir>  
</PropertyGroup>  
```  
  
 Todas as propriedades são avaliadas na ordem em que aparecem no arquivo de projeto. O novo valor de `BuildDir` deve ser declarado depois que o valor antigo for atribuído.  
  
## <a name="reserved-properties"></a>Propriedades reservadas  
 O MSBuild reserva alguns nomes de propriedade para armazenar informações sobre o arquivo de projeto e os binários do MSBuild. Essas propriedades são referenciadas com a notação $ como qualquer outra propriedade. Por exemplo, $(MSBuildProjectFile) retorna o nome de arquivo completo do arquivo de projeto, incluindo a extensão de nome de arquivo.  
  
 Para saber mais, confira [Como referenciar o nome ou o local do arquivo de projeto](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md) e [Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md).  
  
## <a name="environment-properties"></a>Propriedades de ambiente  
 Você pode referenciar variáveis de ambiente em arquivos de projeto da mesma maneira que as propriedades reservadas. Por exemplo, para usar a variável de ambiente `PATH` em seu arquivo de projeto, use $(Path). Se o projeto contiver uma definição de propriedade que tem o mesmo nome que uma propriedade de ambiente, a propriedade no projeto substituirá o valor da variável de ambiente.  
  
 Cada projeto do MSBuild tem um bloco de ambiente isolado: apenas observa, lê e grava em seu próprio bloco.  O MSBuild somente lê as variáveis de ambiente quando ele inicializa a coleção de propriedades, antes de o arquivo de projeto ser avaliado ou criado. Depois disso, as propriedades de ambiente são estáticas, ou seja, cada ferramenta gerada começa com os mesmos nomes e valores.  
  
 Para obter o valor atual de variáveis de ambiente em uma ferramenta gerada, use as [Funções de propriedade](../msbuild/property-functions.md) System.Environment.GetEnvironmentVariable. O método preferido, entretanto, é usar o parâmetro de tarefa <xref:Microsoft.Build.Utilities.ToolTask.EnvironmentVariables%2A>. As propriedades de ambiente definidas nesta matriz de cadeia de caracteres podem ser passadas para a ferramenta gerada sem afetar as variáveis de ambiente do sistema.  
  
> [!TIP]
>  Nem todas as variáveis de ambiente são lidas para se tornarem propriedades iniciais. Qualquer variável de ambiente cujo nome não seja um nome de propriedade do MSBuild válido, como "386", será ignorada.  
  
 Para obter mais informações, confira [Como usar variáveis de ambiente em um build](../msbuild/how-to-use-environment-variables-in-a-build.md).  
  
## <a name="registry-properties"></a>Propriedades de Registro  
 Leia valores de registro do sistema usando a sintaxe a seguir, em que `Hive` é o hive do Registro (por exemplo, **HKEY_LOCAL_MACHINE**), `Key` é o nome da chave, `SubKey` é o nome da subchave e `Value` é o valor da subchave.  
  
```xml  
$(registry:Hive\MyKey\MySubKey@Value)  
```  
  
 Para obter o valor da subchave padrão, omita o `Value`.  
  
```xml  
$(registry:Hive\MyKey\MySubKey)  
```  
  
 Esse Registro pode ser usado para inicializar uma propriedade de build. Por exemplo, para criar uma propriedade de build que representa a home page do navegador da Web do Visual Studio, use este código:  
  
```xml  
<PropertyGroup>  
  <VisualStudioWebBrowserHomePage>  
    $(registry:HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\WebBrowser@HomePage)  
  </VisualStudioWebBrowserHomePage>  
<PropertyGroup>  
```  
  
## <a name="global-properties"></a>Propriedades globais  
 O MSBuild permite a definição de propriedades na linha de comando com o uso da opção **-property** (ou **-p**). Esses valores de propriedades globais substituem os valores de propriedade que são definidos no arquivo de projeto. Isso inclui propriedades de ambiente, mas não inclui propriedades reservadas, que não podem ser alteradas.  
  
 O exemplo a seguir define a propriedade `Configuration` global como `DEBUG`.  
  
```cmd  
msbuild.exe MyProj.proj -p:Configuration=DEBUG  
```  
  
 As propriedades globais também podem ser definidas ou modificadas para projetos filho em um build de vários projetos usando o atributo `Properties` da tarefa do MSBuild. As propriedades globais também são encaminhadas para projetos filho, a menos que o atributo `RemoveProperties` da tarefa MSBuild seja usado para especificar a lista de propriedades que não devem ser encaminhadas. Para saber mais, confira [Tarefa do MSBuild](../msbuild/msbuild-task.md).
  
 Se você especificar uma propriedade usando o atributo `TreatAsLocalProperty` em uma marca de projeto, esse valor da propriedade global não substituirá o valor da propriedade que é definido no arquivo de projeto. Para obter mais informações, confira [Elemento Project (MSBuild)](../msbuild/project-element-msbuild.md) e [Como criar os mesmos arquivos de origem com opções diferentes](../msbuild/how-to-build-the-same-source-files-with-different-options.md).  
  
## <a name="property-functions"></a>Funções de propriedade  
 A partir do .NET Framework versão 4, você pode usar funções de propriedade para avaliar seus scripts do MSBuild. Você pode ler a hora do sistema, comparar cadeias de caracteres, combinar expressões regulares e executar outras ações no script de build sem usar as tarefas do MSBuild.  
  
 Você pode usar métodos de cadeia de caracteres (instância) para operar qualquer valor da propriedade e pode chamar os métodos estáticos de muitas classes de sistema. Por exemplo, você pode definir uma propriedade de build com a data de hoje da seguinte maneira.  
  
```xml  
<Today>$([System.DateTime]::Now.ToString("yyyy.MM.dd"))</Today>  
```  
  
 Para obter mais informações e uma lista de funções de propriedade, confira [Funções de propriedade](../msbuild/property-functions.md).  
  
## <a name="create-properties-during-execution"></a>Criar propriedades durante a execução  
 As propriedades posicionadas fora dos elementos `Target` são valores atribuídos durante a fase de avaliação de um build. Durante a fase de execução subsequente, as propriedades podem ser criadas ou modificadas das seguintes maneiras:  
  
-   Uma propriedade pode ser emitida por qualquer tarefa. Para emitir uma propriedade, o elemento [Task](../msbuild/task-element-msbuild.md) deve ter um elemento filho [Output](../msbuild/output-element-msbuild.md) que tem um atributo `PropertyName`.  
  
-   Uma propriedade pode ser emitida pela tarefa [CreateProperty](../msbuild/createproperty-task.md). Esse uso é preterido.  
  
-   A partir do .NET Framework 3.5, os elementos `Target` podem conter elementos `PropertyGroup` que podem conter declarações de propriedade.  
  
## <a name="store-xml-in-properties"></a>Armazenar o XML em propriedades  
 As propriedades podem conter XML arbitrário, que pode ajudar a passar valores para tarefas ou exibir informações de log. O exemplo a seguir mostra a propriedade `ConfigTemplate`, que tem um valor que contém o XML e outras referências de propriedade. [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] substitui as referências de propriedade usando seus respectivos valores de propriedade. Os valores de propriedade são atribuídos na ordem em que aparecem. Portanto, nesse exemplo, `$(MySupportedVersion)`, `$(MyRequiredVersion)` e `$(MySafeMode)` já devem ter sido definidos.  
  
```xml  
  
<PropertyGroup>  
    <ConfigTemplate>  
        <Configuration>  
            <Startup>  
                <SupportedRuntime  
                    ImageVersion="$(MySupportedVersion)"  
                    Version="$(MySupportedVersion)"/>  
                <RequiredRuntime  
                    ImageVersion="$(MyRequiredVersion)"  
                    Version="$(MyRequiredVersion)"  
                    SafeMode="$(MySafeMode)"/>  
            </Startup>  
        </Configuration>  
    </ConfigTemplate>  
</PropertyGroup>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)  
 [MSBuild](../msbuild/msbuild.md)  
 [Como usar variáveis de ambiente em um build](../msbuild/how-to-use-environment-variables-in-a-build.md)   
 [Como referenciar o nome ou o local do arquivo de projeto](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)   
 [Como criar os mesmos arquivos de origem com opções diferentes](../msbuild/how-to-build-the-same-source-files-with-different-options.md)   
 [Propriedades reservadas e conhecidas do MSBuild](../msbuild/msbuild-reserved-and-well-known-properties.md)   
 [Elemento Property (MSBuild)](../msbuild/property-element-msbuild.md)
