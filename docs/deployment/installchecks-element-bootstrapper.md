---
title: '&lt;&gt;Elemento InstallChecks (Bootstrapper) | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <InstallChecks> element [bootstrapper]
ms.assetid: ad329c87-b0ad-4304-84de-ae9496514c42
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c7ba4da072a586bdc09993b77200a769be3940ab
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536299"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;&gt;Elemento InstallChecks (Bootstrapper)
O `InstallChecks` elemento dá suporte à inicialização de uma variedade de testes em relação ao computador local para garantir que todos os pré-requisitos apropriados para um aplicativo tenham sido instalados.

## <a name="syntax"></a>Sintaxe

```xml
<InstallChecks>
    <AssemblyCheck
        Property
        Name
        PublicKeyToken
        Version
        Language
        ProcessorArchitecture
    />
    <RegistryCheck
        Property
        Key
        Value
    />
    <ExternalCheck
        PackageFile
        Property
        Arguments
    />
    <FileCheck
        Property
        FileName
        SearchPath
        SpecialFolder
        SearchDepth
    />
    <MsiProductCheck
        Property
        Product
        Feature
    />
    <RegistryFileCheck
        Property
        Key
        Value
        FileName
        SearchDepth
    />
</InstallChecks>
```

## <a name="assemblycheck"></a>AssemblyCheck
 Esse elemento é um elemento filho opcional de `InstallChecks` . Para cada instância do `AssemblyCheck` , o bootstrapper garantirá que o assembly identificado pelo elemento exista no GAC (cache de assembly global). Ele não contém nenhum elemento e tem os atributos a seguir.

|Atributo|Descrição|
|---------------|-----------------|
|`Property`|Obrigatórios. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<Commands> elemento](../deployment/commands-element-bootstrapper.md).|
|`Name`|Obrigatórios. O nome totalmente qualificado do assembly a ser verificado.|
|`PublicKeyToken`|Obrigatórios. A forma abreviada da chave pública associada a esse assembly com nome forte. Todos os assemblies armazenados no GAC devem ter um nome, uma versão e uma chave pública.|
|`Version`|Obrigatórios. A versão do assembly.<br /><br /> O número de versão tem o formato \<*major version*> . \<*minor version*> . \<*build version*> . \<*revision version*> .|
|`Language`|Opcional. O idioma de um assembly localizado. O padrão é `neutral`.|
|`ProcessorArchitecture`|Opcional. O processador do computador de destino desta instalação. O padrão é `msil`.|

## <a name="externalcheck"></a>ExternalCheck
 Esse elemento é um elemento filho opcional de `InstallChecks` . Para cada instância do `ExternalCheck` , o bootstrapper executará o programa externo nomeado em um processo separado e armazenará seu código de saída na propriedade indicada por `Property` . `ExternalCheck`é útil para implementar verificações de dependência complexas ou quando a única maneira de verificar a existência de um componente é instanciá-lo.

 `ExternalCheck`Não contém elementos e tem os seguintes atributos.

|Atributo|Descrição|
|---------------|-----------------|
|`Property`|Obrigatórios. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<Commands> elemento](../deployment/commands-element-bootstrapper.md).|
|`PackageFile`|Obrigatórios. O programa externo a ser executado. O programa deve fazer parte do pacote de distribuição da instalação.|
|`Arguments`|Opcional. Fornece argumentos de linha de comando para o executável nomeado por `PackageFile` .|

## <a name="filecheck"></a>FileCheck
 Esse elemento é um elemento filho opcional de `InstallChecks` . Para cada instância do `FileCheck` , o bootstrapper determinará se o arquivo nomeado existe e retornará o número de versão do arquivo. Se o arquivo não tiver um número de versão, o bootstrapper definirá a propriedade nomeada `Property` como 0. Se o arquivo não existir, `Property` não será definido como qualquer valor.

 `FileCheck`Não contém elementos e tem os seguintes atributos.

| Atributo | Descrição |
|-----------------| - |
| `Property` | Obrigatórios. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<Commands> elemento](../deployment/commands-element-bootstrapper.md). |
| `FileName` | Obrigatórios. O nome do arquivo a ser localizado. |
| `SearchPath` | Obrigatórios. O disco ou a pasta na qual procurar o arquivo. Esse deve ser um caminho relativo se `SpecialFolder` for atribuído; caso contrário, ele deve ser um caminho absoluto. |
| `SpecialFolder` | Opcional. Uma pasta que tem significância especial para o Windows ou para o [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] . O padrão é interpretar `SearchPath` como um caminho absoluto. Os valores válidos incluem os seguintes:<br /><br /> `AppDataFolder`. A pasta de dados do aplicativo para este [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] aplicativo; específica para o usuário atual.<br /><br /> `CommonAppDataFolder`. A pasta de dados de aplicativo usada por todos os usuários.<br /><br /> `CommonFilesFolder`. A pasta Arquivos comuns para o usuário atual.<br /><br /> `LocalDataAppFolder`. A pasta de dados para aplicativos que não são de roaming.<br /><br /> `ProgramFilesFolder`. A pasta arquivos de programas padrão para aplicativos de 32 bits.<br /><br /> `StartUpFolder`. A pasta que contém todos os aplicativos iniciados na inicialização do sistema.<br /><br /> `SystemFolder`. A pasta que contém DLLs de sistema de 32 bits.<br /><br /> `WindowsFolder`. A pasta que contém a instalação do sistema do Windows.<br /><br /> `WindowsVolume`. A unidade ou partição que contém a instalação do sistema do Windows. |
| `SearchDepth` | Opcional. A profundidade na qual Pesquisar subpastas para o arquivo nomeado. A pesquisa é de profundidade-primeiro. O padrão é 0, o que restringe a pesquisa para a pasta de nível superior especificada por `SpecialFolder` e **SearchPath**. |

## <a name="msiproductcheck"></a>MsiProductCheck
 Esse elemento é um elemento filho opcional de `InstallChecks` . Para cada instância do `MsiProductCheck` , o bootstrapper verifica se a instalação do Microsoft Windows Installer especificada foi executada até ser concluída. O valor da propriedade é definido dependendo do estado do produto instalado. Um valor positivo indica que o produto está instalado, 0 ou-1 indica que ele não está instalado. (Consulte a função Windows Installer SDK MsiQueryFeatureState para obter mais informações.) . Se Windows Installer não estiver instalado no computador, `Property` não será definido.

 `MsiProductCheck`Não contém elementos e tem os seguintes atributos.

|Atributo|Descrição|
|---------------|-----------------|
|`Property`|Obrigatórios. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<Commands> elemento](../deployment/commands-element-bootstrapper.md).|
|`Product`|Obrigatórios. O GUID do produto instalado.|
|`Feature`|Opcional. O GUID de um recurso específico do aplicativo instalado.|

## <a name="registrycheck"></a>RegistryCheck
 Esse elemento é um elemento filho opcional de `InstallChecks` . Para cada instância do `RegistryCheck` , o bootstrapper verifica se a chave do Registro especificada existe ou se tem o valor indicado.

 `RegistryCheck`Não contém elementos e tem os seguintes atributos.

|Atributo|Descrição|
|---------------|-----------------|
|`Property`|Obrigatórios. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<Commands> elemento](../deployment/commands-element-bootstrapper.md).|
|`Key`|Obrigatórios. O nome da chave do Registro.|
|`Value`|Opcional. O nome do valor do registro a ser recuperado. O padrão é retornar o texto do valor padrão. `Value`deve ser uma cadeia de caracteres ou uma DWORD.|

## <a name="registryfilecheck"></a>RegistryFileCheck
 Esse elemento é um elemento filho opcional de `InstallChecks` . Para cada instância do `RegistryFileCheck` , o bootstrapper recupera a versão do arquivo especificado, primeiro tentando recuperar o caminho para o arquivo da chave do Registro especificada. Isso é particularmente útil se você quiser pesquisar um arquivo em um diretório especificado como um valor no registro.

 `RegistryFileCheck`Não contém elementos e tem os seguintes atributos.

|Atributo|Descrição|
|---------------|-----------------|
|`Property`|Obrigatórios. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<Commands> elemento](../deployment/commands-element-bootstrapper.md).|
|`Key`|Obrigatórios. O nome da chave do Registro. Seu valor é interpretado como o caminho para um arquivo, a menos que o `File` atributo seja definido. Se essa chave não existir, `Property` não será definida.|
|`Value`|Opcional. O nome do valor do registro a ser recuperado. O padrão é retornar o texto do valor padrão. `Value`deve ser uma cadeia de caracteres.|
|`FileName`|Opcional. O nome de um arquivo. Se especificado, o valor obtido da chave do registro será considerado um caminho de diretório e esse nome será anexado a ele. Se não for especificado, o valor retornado do registro será considerado o caminho completo de um arquivo.|
|`SearchDepth`|Opcional. A profundidade na qual Pesquisar subpastas para o arquivo nomeado. A pesquisa é de profundidade-primeiro. O padrão é 0, o que restringe a pesquisa para a pasta de nível superior especificada pelo valor da chave do registro.|

## <a name="remarks"></a>Comentários
 Embora os elementos abaixo `InstallChecks` definam os testes a serem executados, eles não os executam. Para executar os testes, você deve criar `Command` elementos abaixo do `Commands` elemento.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra o `InstallChecks` elemento como ele é usado no arquivo do produto para o .NET Framework.

```xml
<InstallChecks>
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />
</InstallChecks>
```

## <a name="installconditions"></a>InstallConditions
 Quando `InstallChecks` são avaliados, eles produzem propriedades. As propriedades são usadas pelo `InstallConditions` para determinar se um pacote deve ser instalado, ignorado ou reprovado. A tabela a seguir lista o `InstallConditions` :

|Condição|Descrição|
|-|-|
|`FailIf`|Se qualquer `FailIf` condição for avaliada como true, o pacote falhará. O restante das condições não será avaliado.|
|`BypassIf`|Se qualquer `BypassIf` condição for avaliada como true, o pacote será ignorado. O restante das condições não será avaliado.|

## <a name="predefined-properties"></a>Propriedades predefinidas
 A tabela a seguir lista `BypassIf` os `FailIf` elementos e:

|Propriedade|Observações|Valores possíveis|
|--------------|-----------|---------------------|
|`Version9X`|Número de versão de um sistema operacional Windows 9X.|4,10 = Windows 98|
|`VersionNT`|Número de versão de um sistema operacional baseado no Windows NT.|Major.Minor.ServicePack<br /><br /> 5,0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|
|`VersionNT64`|Número de versão de um sistema operacional baseado no Windows NT de 64 bits.|O mesmo mencionado anteriormente.|
|`VersionMsi`|Número de versão do serviço de Windows Installer.|2,0 = Windows Installer 2,0|
|`AdminUser`|Especifica se um usuário tem privilégios de administrador em um sistema operacional baseado no Windows NT.|0 = sem privilégios de administrador<br /><br /> 1 = privilégios de administrador|

 Por exemplo, para bloquear a instalação em um computador que executa o Windows 95, use um código como o seguinte:

```xml
<!-- Block install on Windows 95 -->
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>
```

## <a name="see-also"></a>Confira também
- [\<Commands>elementos](../deployment/commands-element-bootstrapper.md)
- [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)