---
title: Instalando fora da pasta de extensões com VSIX v3 | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 8476b300974d66efc60f647c897ec6892191e7fa
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31136766"
---
# <a name="installing-outside-the-extensions-folder"></a>Instalando fora da pasta de extensões

Começando com o Visual Studio de 2017 e VSIX v3 (versão 3), agora há suporte para a instalação de ativos de extensão fora da pasta extensões. Atualmente, os locais a seguir estejam habilitados como locais de instalação válido (onde [INSTALLDIR] é mapeado para o diretório de instalação da instância do Visual Studio):

* \MSBuild [INSTALLDIR]
* [INSTALLDIR] \XML\Schemas.
* \Common7\IDE\PublicAssemblies [INSTALLDIR]
* \Licenses [INSTALLDIR]
* \Common7\IDE\ReferenceAssemblies [INSTALLDIR]
* \Common7\IDE\RemoteDebugger [INSTALLDIR]
* \Common7\IDE\VC\VCTargets [INSTALLDIR]

>**Observação:** o formato do VSIX não permite a instalação de fora da estrutura de pasta de instalação do VS.

Para dar suporte à instalação para esses diretórios, VSIX deve ser instalado "por instância por máquina". Isso pode ser habilitado, marcando a caixa de seleção "todos os usuários" no designer de extension.vsixmanifest:

![Verifique todos os usuários](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>Como definir a Raiz_da_instalação

Para definir os diretórios de instalação, você pode usar o **propriedades** janela no Visual Studio. Por exemplo, você pode definir o `InstallRoot` propriedade de uma referência de projeto para um dos locais acima:

![instalar as propriedades de raiz](media/install-root-properties.png)

Isso adicionará alguns metadados correspondentes `ProjectReference` propriedade dentro o VSIX arquivo do projeto. csproj:

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

>**Observação:** você pode editar o arquivo. csproj diretamente, se você preferir.

## <a name="how-to-set-a-subpath-under-the-installroot"></a>Como definir um subcaminho sob o Raiz_da_instalação

Se você gostaria de instalar um subcaminho sob o `InstallRoot`, você pode fazer isso definindo o `VsixSubPath` propriedade assim o `InstallRoot` propriedade. Por exemplo, digamos que queremos que a saída da nossa referência de projeto para instalar ' [INSTALLDIR]\MSBuild\MyCompany\MySDK\1.0'. Podemos fazer isso facilmente com o designer de propriedade:

![subcaminho do conjunto](media/set-subpath.png)

As alterações. csproj correspondente serão assim:

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>Informações adicionais

As alterações de propriedade designer se aplicam a mais do que apenas as referências do projeto; Você pode definir o `InstallRoot` metadados para os itens dentro de seu projeto (usando os métodos descritos acima).
