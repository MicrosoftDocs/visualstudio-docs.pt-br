---
title: Como modificar arquivos Web.Config para instrumentar e analisar aplicativos Web ASP .NET dinamicamente compilados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a92e5692-2183-4ae3-9431-b067c6a7aab4
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 521da3263d3ea893613bf3b5211763230d07c67f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830984"
---
# <a name="how-to-modify-webconfig-files-to-instrument-and-profile-dynamically-compiled-aspnet-web-applications"></a>Como modificar arquivos Web.Config para instrumentar e criar perfil de Aplicativos Web ASP.NET compilados dinamicamente
Você pode usar o método de instrumentação das Ferramentas de Criação de Perfil do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] para coletar dados de tempo detalhados, dados de alocação de memória do .NET e dados de tempo de vida do objeto do .NET de aplicativos Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] dinamicamente compilados.  

 Este tópico descreve como modificar o arquivo de configuração *web.config* para habilitar a instrumentação e a criação de perfil de aplicativos Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)].  

> [!NOTE]
>  Não é necessário modificar o arquivo *web.config* quando você usa o método de criação de perfil por amostragem ou quando você deseja instrumentar um módulo [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] pré-compilado.  

 A raiz de um arquivo *web.config* é o elemento **configuration**. Para instrumentar e criar o perfil de um aplicativo Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] compilado dinamicamente, é necessário adicionar ou modificar os seguintes elementos:  

- Um elemento **configuration/runtime/assemblyBinding/dependentAssembly** que identifica o assembly Microsoft.VisualStudio.Enterprise.ASPNetHelper que controla a criação de perfil. O elemento **dependentAssembly** contém dois elementos filho: **assemblyIdentity** e **codeBase**.  

- Um elemento **configuration/system.web/compilation** que identifica a etapa de compilação pós-processamento do criador de perfil do assembly de destino.  

- Dois elementos **add** que identificam o local das Ferramentas de Criação de Perfil são adicionados à seção **configuration/appSettings**.  

  Recomendamos a criação de uma cópia do arquivo *web.config* original que pode ser usada para restaurar a configuração do aplicativo.  

### <a name="to-add-the-aspnethelper-assembly-as-a-configurationruntimeassemblybindingdependentassembly-element"></a>Para adicionar o assembly ASPNetHelper como um elemento configuration/runtime/assemblyBinding/dependentAssembly  

1. Se necessário, adicione o elemento **runtime** como um elemento filho do elemento **configuration**. Caso contrário, vá para a próxima etapa.  

    O elemento **runtime** não tem atributos. O elemento **configuration** pode ter apenas um elemento filho **runtime**.  

2. Se necessário, adicione o elemento **assemblyBinding** como um elemento filho do elemento **runtime**. Caso contrário, vá para a próxima etapa.  

    O elemento **runtime** pode ter apenas um elemento **assemblyBinding**.  

3. Adicione os seguintes nomes de atributo e valor ao elemento **assemblyBinding**:  


   | Nome do atributo | Valor do Atributo |
   |----------------|--------------------------------------|
   | **Xmlns** | **urn:schemas-microsoft-com:asm.v1** |


4. Adicione um elemento **dependentAssembly** como um elemento filho do elemento **assemblyBinding**.  

    O elemento **dependentAssembly** não tem atributos.  

5. Adicione um elemento **assemblyIdentity** como um filho do elemento **dependentAssembly**.  

6. Adicione os seguintes nomes de atributo e valores ao elemento **assemblyIdentity**:  


   | Nome do atributo | Valor do Atributo |
   |--------------------| - |
   | **name** | **Microsoft.VisualStudio.Enterprise.ASPNetHelper** |
   | **PublicKeyToken** | **b03f5f7f11d50a3a** |
   | **culture** | **Neutral** |


7. Adicione um elemento **codeBase** como um filho do elemento **dependentAssembly**.  

8. Adicione os seguintes nomes de atributo e valores ao elemento **codeBase**:  

   |Nome do atributo|Valor do Atributo|  
   |--------------------|---------------------|  
   |**version**|**10.0.0.0**|  
   |**href**|`PathToASPNetHelperDll`|  

    `PathToASPNetHelperDll` é a URL do arquivo da Microsoft.VisualStudio.Enterprise.ASPNetHelper.dll. Se o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] estiver instalado no local padrão, o valor **href** deverá ser `C:/Program%20Files/Microsoft%20Visual%20Studio%202010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL`  

```xml  
    <configuration>  
        <runtime>  
            <assemblyBinding   
                xmlns="urn:schemas-microsoft-com:asm.v1"  
            >  
                <dependentAssembly>  
                    <assemblyIdentity name="Microsoft.VisualStudio.Enterprise.ASPNetHelper"   
                        publicKeyToken="b03f5f7f11d50a3a"
                        culture="neutral"   
                    />  
                    <codeBase   
                        version="10.0.0.0"  
                        href="file:///C:/Program%20Files/Microsoft%20Visual%20Studio%2010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL"   
                    />  
                </dependentAssembly>  
            </assemblyBinding>  
        </runtime>  
```  

### <a name="to-add-the-profiler-post-process-step-to-the-configurationsystemwebcompilation-element"></a>Para adicionar a etapa de pós-processamento do criador de perfil ao elemento configuration/system.web/compilation  

1.  Se necessário, adicione o elemento **system.web** como um elemento filho do elemento **configuration**. Caso contrário, vá para a próxima etapa.  

     O elemento **system.web** não tem atributos. O elemento **configuration** pode ter apenas um elemento filho **system.web**.  

2.  Se necessário, adicione o elemento **compilation** como um elemento filho do elemento **system.web**. Caso contrário, vá para a próxima etapa.  

     O elemento **system.web** pode ter apenas um elemento filho **compilation**.  

3.  Remova todos os atributos existentes do elemento **compilation** e adicione os seguintes nomes de atributo e valor:  

    |Nome do atributo|Valor do Atributo|  
    |--------------------|---------------------|  
    |**assemblyPostProcessorType**|**Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter, Microsoft.VisualStudio.Enterprise.ASPNetHelper, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a**|  

```xml  
    <configuration>  
        <runtime>  
        . . .  
        </runtime>  
        <system.web>  
            <compilation  
                assemblyPostProcessorType="Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter,  
                    Microsoft.VisualStudio.Enterprise.ASPNetHelper,  
                    Version=10.0.0.0,  
                    Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"   
            />  
        </system.web>  
    <configuration>  
```  

### <a name="to-add-profiler-location-settings-to-the-configurationappsettings-element"></a>Para adicionar configurações de local do Criador de Perfil ao elemento configuration/appSettings  

1. Se necessário, adicione o elemento **appSettings** como um elemento filho do elemento **configuration**. Caso contrário, vá para a próxima etapa.  

    O elemento **appSettings** não tem atributos. O elemento **configuration** pode ter apenas um elemento filho **appSettings**.  

2. Adicione um elemento **add** como um filho do elemento **appSettings**.  

3. Adicione os seguintes nomes de atributo e valores ao elemento **add**:  


   | Nome do atributo | Valor do Atributo |
   |----------------| - |
   | **key** | **Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation** |
   | **value** | `PerformanceToolsFolder` **\VSInstr.Exe** |


4. Adicione outro elemento **add** como um filho do elemento **appSettings**.  

5. Adicione os seguintes nomes de atributo e valores a esse elemento **add**:  

   |Nome do atributo|Valor do Atributo|  
   |--------------------|---------------------|  
   |**key**|**Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools**|  
   |**value**|`PerformanceToolsFolder`|  

    `PerformanceToolsFolder` é o caminho dos arquivos executáveis do criador de perfil. Se o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] estiver instalado no local padrão, o valor será **C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools**  

```xml  
    <configuration>  
        <runtime>  
        . . .  
        </runtime>  
        . . .  
        <system.web>  
        </system.web>  
        <appSettings>  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\vsinstr.exe"  
        />  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\"  
            />  
        </appSettings>  
    </configuration>  
```  

## <a name="example"></a>Exemplo  
 A seguir há um arquivo *web.config* completo que habilita a instrumentação e criação de perfil de aplicativos Web [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] compilados dinamicamente. Este exemplo presume que não havia outras configurações no arquivo antes de qualquer modificação.  

```xml  
<?xml version="1.0"?>  
    <configuration>  
        <runtime>  
            <assemblyBinding   
                xmlns="urn:schemas-microsoft-com:asm.v1"  
            >  
                <dependentAssembly>  
                    <assemblyIdentity   
                        name="Microsoft.VisualStudio.Enterprise.ASPNetHelper"   
                        publicKeyToken="b03f5f7f11d50a3a"  
                        culture="neutral"   
                    />  
                    <codeBase   
                        version="10.0.0.0"  
                        href="file:///C:/Program%20Files/Microsoft%20Visual%20Studio%2010.0/Common7/IDE/PrivateAssemblies/Microsoft.VisualStudio.Enterprise.ASPNetHelper.DLL"   
                    />  
                </dependentAssembly>  
            </assemblyBinding>  
        </runtime>  
        <system.web>  
            <compilation  
                assemblyPostProcessorType="Microsoft.VisualStudio.Enterprise.Common.AspPerformanceInstrumenter,  
                    Microsoft.VisualStudio.Enterprise.ASPNetHelper,  
                    Version=10.0.0.0,  
                    Culture=neutral,  
                    PublicKeyToken=b03f5f7f11d50a3a"   
            />  
        </system.web>  
        <appSettings>  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrLocation"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\vsinstr.exe"  
            />  
            <add  
                key="Microsoft.VisualStudio.Enterprise.AspNetHelper.VsInstrTools"  
                value="C:\Program Files\Microsoft Visual Studio 10.0\Team Tools\Performance Tools\"  
            />  
        </appSettings>  
    </configuration>  

```  

## <a name="see-also"></a>Consulte também  
 [Como instrumentar um aplicativo do ASP.NET compilado dinamicamente e coletar dados de tempo detalhados](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-app-and-collect-timing-data.md)   
 [Como instrumentar um aplicativo do ASP.NET compilado dinamicamente e coletar dados de memória](../profiling/how-to-instrument-a-dynamically-compiled-aspnet-web-application-and-collect-memory-data.md)