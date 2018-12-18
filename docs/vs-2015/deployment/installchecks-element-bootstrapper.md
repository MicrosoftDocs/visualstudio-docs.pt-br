---
title: '&lt;InstallChecks&gt; elemento (Bootstrapper) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-deployment
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- <InstallChecks> element [bootstrapper]
ms.assetid: ad329c87-b0ad-4304-84de-ae9496514c42
caps.latest.revision: 25
author: mikejo5000
ms.author: mikejo
manager: wpickett
ms.openlocfilehash: 03f489c22c8912e332f7d01e6ec4ac48aacda30b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49891059"
---
# <a name="ltinstallchecksgt-element-bootstrapper"></a>&lt;InstallChecks&gt; elemento (Bootstrapper)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O `InstallChecks` elemento oferece suporte ao início de uma variedade de testes em relação ao computador local para certificar-se de que todos os pré-requisitos para um aplicativo apropriados foram instalados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
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
 Este é um elemento filho opcional de `InstallChecks`. Para cada instância do `AssemblyCheck`, o bootstrapper irá assegurar que o assembly identificado pelo elemento existe no cache de assembly global (GAC). Ele não contém elementos e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Property`|Necessário. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<comandos > elemento](../deployment/commands-element-bootstrapper.md).|  
|`Name`|Necessário. O nome totalmente qualificado do assembly para verificar.|  
|`PublicKeyToken`|Necessário. A forma abreviada da chave pública associado a esse assembly de nome forte. Todos os assemblies armazenados no GAC devem ter um nome, uma versão e uma chave pública.|  
|`Version`|Necessário. A versão do assembly.<br /><br /> O número de versão tem o formato \< *versão principal*>.\< *versão secundária*>.\< *criar versão*>.\< *versão de revisão*>.|  
|`Language`|Opcional. O idioma de um assembly localizado. O padrão é `neutral`.|  
|`ProcessorArchitecture`|Opcional. O processador do computador direcionado por esta instalação. O padrão é `msil`.|  
  
## <a name="externalcheck"></a>ExternalCheck  
 Este é um elemento filho opcional de `InstallChecks`. Para cada instância do `ExternalCheck`, o bootstrapper executará o programa externo nomeado em um processo separado e armazenar seu código de saída na propriedade indicada pelo `Property`. `ExternalCheck` é útil para a implementação de verificações de dependência complexos, ou quando a única maneira de verificar a existência de um componente for instanciá-la.  
  
 `ExternalCheck` não contém elementos e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Property`|Necessário. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<comandos > elemento](../deployment/commands-element-bootstrapper.md).|  
|`PackageFile`|Necessário. O programa externo para executar. O programa deve ser parte do pacote de distribuição da instalação.|  
|`Arguments`|Opcional. Fornece os argumentos de linha de comando para o executável nomeado pelo `PackageFile`.|  
  
## <a name="filecheck"></a>Não  
 Este é um elemento filho opcional de `InstallChecks`. Para cada instância do `FileCheck`, o bootstrapper determinará se o arquivo nomeado existe e retornar o número de versão do arquivo. Se o arquivo não tiver um número de versão, o bootstrapper define a propriedade nomeada pelo `Property` como 0. Se o arquivo não existir, `Property` não está definida como qualquer valor.  
  
 `FileCheck` não contém elementos e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Property`|Necessário. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<comandos > elemento](../deployment/commands-element-bootstrapper.md).|  
|`FileName`|Necessário. O nome do arquivo a ser localizado.|  
|`SearchPath`|Necessário. O disco ou a pasta na qual procurar o arquivo. Isso deve ser um caminho relativo se `SpecialFolder` é atribuído; caso contrário, ele deve ser um caminho absoluto.|  
|`SpecialFolder`|Opcional. Uma pasta que não tem significado especial para Windows ou a [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. O padrão é interpretar `SearchPath` como um caminho absoluto. Os valores válidos incluem o seguinte:<br /><br /> `AppDataFolder`. A pasta de dados de aplicativo para este [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] específicas para o usuário atual do aplicativo;.<br /><br /> `CommonAppDataFolder`. A pasta de dados de aplicativo usada por todos os usuários.<br /><br /> `CommonFilesFolder`. A pasta arquivos comuns para o usuário atual.<br /><br /> `LocalDataAppFolder`. A pasta de dados para aplicativos não roaming.<br /><br /> `ProgramFilesFolder`. A pasta de arquivos de programas padrão para aplicativos de 32 bits.<br /><br /> `StartUpFolder`. A pasta que contém todos os aplicativos iniciados na inicialização do sistema.<br /><br /> `SystemFolder`. A pasta que contém as DLLs do sistema de 32 bits.<br /><br /> `WindowsFolder`. A pasta que contém a instalação do sistema Windows.<br /><br /> `WindowsVolume`. A unidade ou partição que contém a instalação do sistema Windows.|  
|`SearchDepth`|Opcional. A profundidade no qual Pesquisar subpastas para o arquivo nomeado. A pesquisa é de profundidade. O padrão é 0, o que restringe a pesquisa a pasta de nível superior especificada por `SpecialFolder` e **SearchPath**.|  
  
## <a name="msiproductcheck"></a>MsiProductCheck  
 Este é um elemento filho opcional de `InstallChecks`. Para cada instância do `MsiProductCheck`, o bootstrapper verifica para ver se a instalação do Microsoft Windows Installer especificada foi executada até ser concluído. O valor da propriedade é definido dependendo do estado do produto instalado. Um valor positivo indica que o produto foi instalado, 0 ou -1 indica que não está instalado. (Consulte a função do SDK do Windows Installer MsiQueryFeatureState para obter mais informações.) . Se o Windows Installer não estiver instalado no computador, `Property` não está definido.  
  
 `MsiProductCheck` não contém elementos e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Property`|Necessário. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<comandos > elemento](../deployment/commands-element-bootstrapper.md).|  
|`Product`|Necessário. O GUID para o produto instalado.|  
|`Feature`|Opcional. O GUID de um recurso específico do aplicativo instalado.|  
  
## <a name="registrycheck"></a>RegistryCheck  
 Este é um elemento filho opcional de `InstallChecks`. Para cada instância do `RegistryCheck`, o bootstrapper verifica para ver se a chave do registro especificado existe, ou se ele tem o valor indicado.  
  
 `RegistryCheck` não contém elementos e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Property`|Necessário. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<comandos > elemento](../deployment/commands-element-bootstrapper.md).|  
|`Key`|Necessário. O nome da chave do Registro.|  
|`Value`|Opcional. O nome do valor do registro para recuperar. O padrão é retornar o texto do valor padrão. `Value` deve ser uma cadeia de caracteres ou uma DWORD.|  
  
## <a name="registryfilecheck"></a>RegistryFileCheck  
 Este é um elemento filho opcional de `InstallChecks`. Para cada instância do `RegistryFileCheck`, o bootstrapper recupera a versão do arquivo especificado, primeiro a tentativa de recuperar o caminho para o arquivo de chave do Registro especificada. Isso é particularmente útil se você quiser pesquisar um arquivo em um diretório especificado como um valor no registro.  
  
 `RegistryFileCheck` não contém elementos e tem os seguintes atributos.  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`Property`|Necessário. O nome da propriedade para armazenar o resultado. Essa propriedade pode ser referenciada de um teste sob o `InstallConditions` elemento, que é um filho do `Command` elemento. Para obter mais informações, consulte [ \<comandos > elemento](../deployment/commands-element-bootstrapper.md).|  
|`Key`|Necessário. O nome da chave do Registro. Seu valor é interpretado como o caminho para um arquivo, a menos que o `File` atributo é definido. Se essa chave não existir, `Property` não está definido.|  
|`Value`|Opcional. O nome do valor do registro para recuperar. O padrão é retornar o texto do valor padrão. `Value` deve ser uma cadeia de caracteres.|  
|`FileName`|Opcional. O nome de um arquivo. Se especificado, o valor obtido da chave do registro é considerado um caminho de diretório, e esse nome é anexado a ele. Se não for especificado, o valor retornado do registro deve para ser o caminho completo para um arquivo.|  
|`SearchDepth`|Opcional. A profundidade no qual Pesquisar subpastas para o arquivo nomeado. A pesquisa é de profundidade. O padrão é 0, o que restringe a pesquisa a pasta de nível superior especificada pelo valor da chave do registro.|  
  
## <a name="remarks"></a>Comentários  
 Embora os elementos sob `InstallChecks` definir os testes a serem executados, eles não executá-los. Para executar os testes, você deve criar `Command` elementos sob o `Commands` elemento.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra a `InstallChecks` elemento como ele é usado no arquivo de produto para o [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
```  
<InstallChecks>  
    <ExternalCheck Property="DotNetInstalled" PackageFile="dotnetchk.exe" />  
    <RegistryCheck Property="IEVersion" Key="HKLM\Software\Microsoft\Internet Explorer" Value="Version" />  
</InstallChecks>  
```  
  
## <a name="installconditions"></a>InstallConditions  
 Quando `InstallChecks` são avaliadas, geram propriedades. As propriedades são usadas pelo `InstallConditions` para determinar se um pacote deve instalar, ignorar ou falhar. A seguinte tabela lista o `InstallConditions`:  
  
|||  
|-|-|  
|`FailIf`|Se houver `FailIf` condição for avaliada como true, o pacote falhará. O restante das condições não será avaliado.|  
|`BypassIf`|Se houver `BypassIf` condição for avaliada como true, o pacote será ignorado. O restante das condições não será avaliado.|  
  
## <a name="predefined-properties"></a>Propriedades predefinidas  
 A seguinte tabela lista os `BypassIf` e `FailIf` elementos:  
  
|Propriedade|Observações|Valores possíveis|  
|--------------|-----------|---------------------|  
|`Version9X`|Número de versão de um sistema de operacional Windows 9 X.|4.10 = Windows 98|  
|`VersionNT`|Número de versão de um sistema operacional Windows NT.|ServicePack<br /><br /> 5.0 = Windows 2000<br /><br /> 5.1.0 = Windows XP<br /><br /> 5.1.2 = Windows XP Professional SP2<br /><br /> 5.2.0 = Windows Server 2003|  
|`VersionNT64`|Número de versão de um sistema de operacional de 64 bits com base no Windows NT.|O mesmo como mencionado anteriormente.|  
|`VersionMsi`|Número de versão do serviço Windows Installer.|2.0 = Windows Installer 2.0|  
|`AdminUser`|Especifica se um usuário tem privilégios de administrador em um sistema operacional Windows NT.|0 = sem privilégios de administrador<br /><br /> 1 = privilégios de administrador|  
  
 Por exemplo, para bloquear a instalação em um computador executando o Windows 95, use o código como o seguinte:  
  
```  
<!-- Block install on Windows 95 -->  
    <FailIf Property="Version9X" Compare="VersionLessThan" Value="4.10" String="InvalidPlatform"/>  
```  
  
## <a name="see-also"></a>Consulte também  
 [\<Comandos > elemento](../deployment/commands-element-bootstrapper.md)   
 [Referência de esquema de produto e pacote](../deployment/product-and-package-schema-reference.md)



