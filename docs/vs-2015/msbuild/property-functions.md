---
title: Funções de propriedade | Microsoft Docs
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
- MSBuild, property functions
ms.assetid: 2253956e-3ae0-4bdc-9d3a-4881dfae4ddb
caps.latest.revision: 35
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0194de0a9f14186dc02b17564c77b1b2bc7441be
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49920164"
---
# <a name="property-functions"></a>Funções de propriedade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Nas versões .NET Framework 4 e 4.5, as funções de propriedade podem ser usadas para avaliar scripts MSBuild. As funções de propriedade podem ser usadas sempre que as propriedades forem exibidas. Ao contrário das tarefas, as funções de propriedade podem ser usadas fora dos destinos e são avaliadas antes de qualquer destino ser executado.  
  
 Sem o uso de tarefas MSBuild, você pode ler a hora do sistema, comparar cadeias de caracteres, combinar expressões regulares e executar outras ações no script de compilação. O MSBuild tentará converter a cadeia de caracteres em número e número em cadeia de caracteres, além de fazer outras conversões, conforme necessário.  
  
 **Neste tópico:**  
  
-   [Sintaxe da função de propriedade](#BKMK_Syntax)  
  
    -   [Funções de propriedade de cadeia de caracteres](#BKMK_String)  
  
    -   [Funções de propriedade estática](#BKMK_Static)  
  
    -   [Chamando métodos de instância em propriedades estáticas](#BKMK_InstanceMethods)  
  
    -   [Funções de Propriedade de MSBuild](#BKMK_PropertyFunctions)  
  
-   [Funções de propriedade aninhadas](#BKMK_Nested)  
  
-   [MSBuild DoesTaskHostExist](#BKMK_DoesTaskHostExist)  
  
-   [MSBuild GetDirectoryNameOfFileAbove](#BKMK_GetDirectoryNameOfFileAbove)  
  
-   [MSBuild GetRegistryValue](#BKMK_GetRegistryValue)  
  
-   [MSBuild GetRegistryValueFromView](#BKMK_GetRegistryValueFromView)  
  
-   [MSBuild MakeRelative](#BKMK_MakeRelative)  
  
-   [MSBuild ValueOrDefault](#BKMK_ValueOrDefault)  
  
##  <a name="BKMK_Syntax"></a> Sintaxe da função de propriedade  
 Três tipos de funções de propriedade estão listados abaixo. Cada função possui uma sintaxe diferente:  
  
-   Funções de propriedade de cadeia de caracteres (instância)  
  
-   Funções de propriedade estática  
  
-   Funções de propriedade MSBuild  
  
###  <a name="BKMK_String"></a> Funções de propriedade de cadeia de caracteres  
 Todos os valores de propriedade de compilação são apenas valores de cadeia de caracteres. Você pode usar métodos de cadeia (instância) para operar em qualquer valor de propriedade. Por exemplo, você pode extrair o nome da unidade (os três primeiros caracteres) de uma propriedade de compilação que representa um caminho completo usando este código:  
  
 `$(ProjectOutputFolder.Substring(0,3))`  
  
###  <a name="BKMK_Static"></a> Funções de propriedade estática  
 No seu script de compilação, você pode acessar propriedades e métodos estáticos de muitas classes de sistema. Para obter o valor de uma propriedade estática, use a seguinte sintaxe, em que *Class* é o nome da classe do sistema e *Property* é o nome da propriedade.  
  
 `$([Class]::Property)`  
  
 Por exemplo, você pode usar o seguinte código para definir uma propriedade de compilação para a data e hora atual.  
  
 `<Today>$([System.DateTime]::Now)</Today>`  
  
 Para chamar um método estático, use a seguinte sintaxe, em que *Class* é o nome da classe de sistema, *Method* é o nome do método e *(Parameters)* é a lista de parâmetros para o método:  
  
 `$([Class]::Method(Parameters))`  
  
 Por exemplo, para definir uma propriedade de compilação para um novo GUID, você pode usar este script:  
  
 `<NewGuid>$([System.Guid]::NewGuid())</NewGuid>`  
  
 Em funções de propriedade estática, você pode usar qualquer método estático ou propriedade destas classes de sistema:  
  
- System.Byte  
  
- System.Char  
  
- System.Convert  
  
- System.DateTime  
  
- System.Decimal  
  
- System.Double  
  
- System.Enum  
  
- System.Guid  
  
- System.Int16  
  
- System.Int32  
  
- System.Int64  
  
- System.IO.Path  
  
- System.Math  
  
- System.UInt16  
  
- System.UInt32  
  
- System.UInt64  
  
- System.SByte  
  
- System.Single  
  
- System.String  
  
- System.StringComparer  
  
- System.TimeSpan  
  
- System.Text.RegularExpressions.Regex  
  
- Microsoft.Build.Utilities.ToolLocationHelper  
  
  Você pode usar também as seguintes propriedades e métodos estáticos:  
  
- System.Environment::CommandLine  
  
- System.Environment::ExpandEnvironmentVariables  
  
- System.Environment::GetEnvironmentVariable  
  
- System.Environment::GetEnvironmentVariables  
  
- System.Environment::GetFolderPath  
  
- System.Environment::GetLogicalDrives  
  
- System.IO.Directory::GetDirectories  
  
- System.IO.Directory::GetFiles  
  
- System.IO.Directory::GetLastAccessTime  
  
- System.IO.Directory::GetLastWriteTime  
  
- System.IO.Directory::GetParent  
  
- System.IO.File::Exists  
  
- System.IO.File::GetCreationTime  
  
- System.IO.File::GetAttributes  
  
- System.IO.File::GetLastAccessTime  
  
- System.IO.File::GetLastWriteTime  
  
- System.IO.File::ReadAllText  
  
###  <a name="BKMK_InstanceMethods"></a> Chamando métodos de instância em propriedades estáticas  
 Se você acessar uma propriedade estática que retorna uma instância de objeto, poderá invocar métodos de instância desse objeto. Para invocar um método de instância, use a seguinte sintaxe, em que *Class* é o nome de classe de sistema, *Property* é o nome da propriedade, *Method* é o nome do método e *(Parameters)* é a lista de parâmetros para o método:  
  
 `$([Class]::Property.Method(Parameters))`  
  
 O nome da classe deve ser totalmente qualificado com o namespace.  
  
 Por exemplo, você pode usar o seguinte código para definir uma propriedade de compilação para a data atual.  
  
 `<Today>$([System.DateTime]::Now.ToString("yyyy.MM.dd"))</Today>`  
  
###  <a name="BKMK_PropertyFunctions"></a> Funções de Propriedade de MSBuild  
 Vários métodos estáticos em sua compilação podem ser acessados para fornecer aritmética, lógica de bit a bit e suporte a caracteres de escape. Você pode acessar esses métodos usando a seguinte sintaxe, em que *Method* é o nome do método e *Parameters* é a lista de parâmetros para o método.  
  
 `$([MSBuild]::Method(Parameters))`  
  
 Por exemplo, para adicionar duas propriedades com valores numéricos, use o código a seguir.  
  
 `$([MSBuild]::Add($(NumberOne), $(NumberTwo))`  
  
 Aqui está uma lista de funções da propriedade MSBuild:  
  
|Assinatura da função|Descrição|  
|------------------------|-----------------|  
|double Add(double a, double b)|Adicionar dois duplos.|  
|long Add(long a, long b)|Adicionar dois longos.|  
|double Subtract(double a, double b)|Subtrair dois duplos.|  
|long Subtract(long a, long b)|Subtrair dois longos.|  
|double Multiply(double a, double b)|Multiplicar dois duplos.|  
|long Multiply(long a, long b)|Multiplicar dois longos.|  
|double Divide(double a, double b)|Dividir dois duplos.|  
|long Divide(long a, long b)|Dividir dois longos.|  
|double Modulo(double a, double b)|Modular dois duplos.|  
|long Modulo(long a, long b)|Modular dois longos.|  
|string Escape(string unescaped)|Escapar a cadeia de caracteres de acordo com a regras de escape do MSBuild.|  
|string Unescape(string escaped)|Deixar sem escape a cadeia de caracteres de acordo com a regras de escape do MSBuild.|  
|int BitwiseOr(int first, int second)|Realiza um `OR` bit a bit no primeiro e segundo (first &#124; second).|  
|int BitwiseAnd(int first, int second)|Realizar um bit a bit `AND` no primeiro e segundo (primeiro e segundo).|  
|int BitwiseXor(int first, int second)|Realizar um bit a bit `XOR` no primeiro e segundo (primeiro ^ segundo).|  
|int BitwiseNot(int first)|Realizar um bit a bit `NOT` (~primeiro).|  
  
##  <a name="BKMK_Nested"></a> Funções de propriedade aninhadas  
 Você pode combinar funções de propriedade para formar funções mais complexas, como mostra o exemplo a seguir.  
  
 `$([MSBuild]::BitwiseAnd(32,   $([System.IO.File]::GetAttributes(tempFile))))`  
  
 Este exemplo retorna o valor dos bits (32 ou 0) do <xref:System.IO.FileAttributes>`Archive` do arquivo dado pelo caminho `tempFile`. Observe que os valores dos dados enumerados não podem aparecer por nome nas funções de propriedade. O valor numérico (32) deve ser usado em seu lugar.  
  
 Metadados também podem aparecer em funções de propriedade aninhadas. Para obter mais informações, consulte [Envio em lote](../msbuild/msbuild-batching.md).  
  
##  <a name="BKMK_DoesTaskHostExist"></a> MSBuild DoesTaskHostExist  
 A função de propriedade `DoesTaskHostExist` no MSBuild retorna se um host de tarefas está instalado atualmente para os valores de tempo de execução e arquitetura especificados.  
  
 Essa função de propriedade tem a seguinte sintaxe:  
  
```  
$[MSBuild]::DoesTaskHostExist(string theRuntime, string theArchitecture)  
```  
  
##  <a name="BKMK_GetDirectoryNameOfFileAbove"></a> MSBuild GetDirectoryNameOfFileAbove  
 A função da propriedade `GetDirectoryNameOfFileAbove` procura por um arquivo nos diretórios acima do diretório atual no caminho.  
  
 Essa função de propriedade tem a seguinte sintaxe:  
  
```  
$[MSBuild]::GetDirectoryNameOfFileAbove(string ThePath, string TheFile)  
```  
  
 O código a seguir mostra um exemplo dessa sintaxe.  
  
```  
<Import Project="$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))\EnlistmentInfo.props" Condition=" '$([MSBuild]::GetDirectoryNameOfFileAbove($(MSBuildThisFileDirectory), EnlistmentInfo.props))' != '' " />  
```  
  
##  <a name="BKMK_GetRegistryValue"></a> MSBuild GetRegistryValue  
 A função da propriedade `GetRegistryValue` do MSBuild retorna o valor de uma chave de registro. Essa função usa dois argumentos, o nome da chave e o nome do valor, e retorna o valor do registro. Se você não especificar um nome de valor, o valor padrão será retornado.  
  
 Os exemplos a seguir mostram como a função é usada:  
  
```  
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, ``))                                  // default value  
$([MSBuild]::GetRegistryValue(`HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\10.0\Debugger`, `SymbolCacheDir`))  
$([MSBuild]::GetRegistryValue(`HKEY_LOCAL_MACHINE\SOFTWARE\(SampleName)`, `(SampleValue)`))             // parens in name and value  
  
```  
  
##  <a name="BKMK_GetRegistryValueFromView"></a> MSBuild GetRegistryValueFromView  
 A função de propriedade `GetRegistryValueFromView` do MSBuild obtém os dados de registro do sistema, dados a chave do registro, o valor e uma ou mais exibições de registro solicitada. A chave e o valor são pesquisados em cada exibição do registo em ordem até serem encontrados.  
  
 A sintaxe para essa função de propriedade é:  
  
 [MSBuild\]::GetRegistryValueFromView(string keyName, string valueName, object defaultValue, params object[] views)  
  
 O sistema operacional Windows de 64 bits mantém uma chave de registro HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node que apresenta uma exibição do registro HKEY_LOCAL_MACHINE\SOFTWARE para aplicativos de 32 bits.  
  
 Por padrão, um aplicativo de 32 bits em execução no WOW64 acessa a exibição do registro de 32 bits e um aplicativo de 64 bits acessa a exibição do registro de 64 bits.  
  
 As seguintes exibições de registro estão disponíveis:  
  
|Exibição do registro|Definição|  
|-------------------|----------------|  
|RegistryView.Registry32|A exibição do registro do aplicativo de 32 bits.|  
|RegistryView.Registry64|A exibição do registro do aplicativo de 64 bits.|  
|RegistryView.Default|A exibição do registro que corresponde ao processo em que o aplicativo está sendo executado.|  
  
 Confira o exemplo abaixo.  
  
 `$([MSBuild]::GetRegistryValueFromView('HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SDKs\Silverlight\v3.0\ReferenceAssemblies', 'SLRuntimeInstallPath', null, RegistryView.Registry64, RegistryView.Registry32))`  
  
 obtém os dados de SLRuntimeInstallPath da chave ReferenceAssemblies, procurando primeiro na exibição do registro de 64 bits e depois na exibição do registro de 32 bits.  
  
##  <a name="BKMK_MakeRelative"></a> MSBuild MakeRelative  
 A função de propriedade `MakeRelative` do MSBuild retorna o caminho relativo do segundo caminho relativo ao primeiro caminho. Cada caminho pode ser um arquivo ou pasta.  
  
 Essa função de propriedade tem a seguinte sintaxe:  
  
```  
$[MSBuild]::MakeRelative($(FileOrFolderPath1), $(FileOrFolderPath2))  
```  
  
 O código a seguir mostra um exemplo dessa sintaxe.  
  
```xml  
<PropertyGroup>  
    <Path1>c:\users\</Path1>  
    <Path2>c:\users\username\</Path2>  
</PropertyGroup>  
  
<Target Name = "Go">  
    <Message Text ="$([MSBuild]::MakeRelative($(Path1), $(Path2)))" />  
    <Message Text ="$([MSBuild]::MakeRelative($(Path2), $(Path1)))" />  
</Target>  
  
<!--  
Output:  
   username\  
   ..\  
-->  
```  
  
##  <a name="BKMK_ValueOrDefault"></a> MSBuild ValueOrDefault  
 A função de propriedade `ValueOrDefault` do MSBuild retorna o primeiro argumento, a menos que seja nulo ou esteja vazio. Se o primeiro argumento for nulo ou estiver vazio, a função retornará o segundo argumento.  
  
 Os exemplos a seguir mostram como essa função é usada.  
  
```  
<Project ToolsVersion="4.0" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <Value1>$([MSBuild]::ValueOrDefault(`$(UndefinedValue)`, `a`))</Value1>  
        <Value2>$([MSBuild]::ValueOrDefault(`b`, `$(Value1)`))</Value2>  
    </PropertyGroup>  
  
    <Target Name="MyTarget">  
        <Message Text="Value1 = $(Value1)" />  
        <Message Text="Value2 = $(Value2)" />  
    </Target>  
</Project>  
  
<!--  
Output:   
  Value1 = a  
  Value2 = b  
-->  
```

## <a name="see-also"></a>Consulte também
[Propriedades do MSBuild](msbuild-properties1.md)   
[Visão geral do MSBuild](msbuild.md)


