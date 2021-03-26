---
title: Instalando fora da pasta extensões com o VSIX v3 | Microsoft Docs
description: Saiba mais sobre como instalar ativos de extensão do SDK do Visual Studio fora da pasta extensões e quais locais são válidos.
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2fecad421cca4cdf4644add5e5e7c7a6af4a23c0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073021"
---
# <a name="install-outside-the-extensions-folder"></a>Instalar fora da pasta de extensões

A partir do Visual Studio 2017 e do VSIX v3 (versão 3), os ativos de extensão podem ser instalados fora da pasta extensões. Atualmente, os seguintes locais estão habilitados como locais de instalação válidos (onde [INSTALLDIR] está mapeado para o diretório de instalação da instância do Visual Studio):

* [INSTALLDIR] \MSBuild
* [INSTALLDIR] \Xml\Schemas
* [INSTALLDIR] \Common7\IDE\PublicAssemblies
* [INSTALLDIR] \Licenses
* [INSTALLDIR] \Common7\IDE\ReferenceAssemblies
* [INSTALLDIR] \Common7\IDE\RemoteDebugger
* [INSTALLDIR] \Common7\IDE\VC\VCTargets (somente com suporte para o Visual Studio 2017; preterido para o Visual Studio 2019 e posterior)

> [!NOTE]
> O formato VSIX não permite que você instale fora da estrutura de pastas de instalação do Visual Studio. 

Para dar suporte à instalação nesses diretórios, o VSIX deve ser instalado "por instância por máquina". Isso pode ser habilitado marcando a caixa de seleção "todos os usuários" no designer de extensão. vsixmanifest:

![verificar todos os usuários](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>Como definir o InstallRoot

Para definir os diretórios de instalação, você pode usar a janela **Propriedades** no Visual Studio. Por exemplo, você pode definir a `InstallRoot` propriedade de uma referência de projeto para um dos locais acima:

![instalar Propriedades raiz](media/install-root-properties.png)

Isso adicionará alguns metadados à propriedade correspondente `ProjectReference` dentro do arquivo. csproj do projeto VSIX:

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> Você pode editar o arquivo. csproj diretamente, se preferir.

## <a name="how-to-set-a-subpath-under-the-installroot"></a>Como definir um subcaminho sob o InstallRoot

Se você quiser instalar o em um subcaminho sob o `InstallRoot` , poderá fazer isso definindo a `VsixSubPath` Propriedade exatamente como a `InstallRoot` propriedade. Por exemplo, digamos que queremos que a saída de nossa referência de projeto seja instalada em ' [INSTALLDIR] \MSBuild\MyCompany\MySDK\1.0 '. Podemos fazer isso facilmente com o designer de propriedade:

![definir subcaminho](media/set-subpath.png)

As alterações. csproj correspondentes terão a seguinte aparência:

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>Informações adicionais

As alterações do designer de propriedade se aplicam a mais do que apenas referências de projeto; Você também pode definir os `InstallRoot` metadados para os itens dentro do seu projeto (usando os mesmos métodos descritos acima).
