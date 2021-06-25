---
title: Instalação fora da pasta de extensões com o VSIX v3 | Microsoft Docs
description: Saiba mais sobre como instalar Visual Studio ativos de extensão do SDK fora da pasta de extensões e quais locais são válidos.
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 24b1e1a73ff588e5531eec2025c8a3c9e94760a4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898442"
---
# <a name="install-outside-the-extensions-folder"></a>Instalar fora da pasta de extensões

Começando com Visual Studio 2017 e VSIX v3 (versão 3), os ativos de extensão podem ser instalados fora da pasta de extensões. Atualmente, os seguintes locais estão habilitados como locais de instalação válidos (em que [INSTALLDIR] é mapeado para o diretório de instalação da Visual Studio da instância):

* [INSTALLDIR]\MSBuild
* [INSTALLDIR]\Xml\Schemas
* [INSTALLDIR]\Common7\IDE\PublicAssemblies
* [INSTALLDIR]\Licenses
* [INSTALLDIR]\Common7\IDE\ReferenceAssemblies
* [INSTALLDIR]\Common7\IDE\RemoteDebugger
* [INSTALLDIR]\Common7\IDE\VC\VCTargets (com suporte apenas para o Visual Studio 2017; preterido para o Visual Studio 2019 e posterior)

> [!NOTE]
> O formato VSIX não permite que você instale fora da estrutura de Visual Studio de instalação. 

Para dar suporte à instalação nesses diretórios, o VSIX deve ser instalado "por instância por computador". Isso pode ser habilitado marcando a caixa de seleção "todos os usuários" no designer extension.vsixmanifest:

![verificar todos os usuários](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>Como definir o InstallRoot

Para definir os diretórios de instalação, você pode usar a **janela Propriedades** no Visual Studio. Por exemplo, você pode definir `InstallRoot` a propriedade de uma referência de projeto para um dos locais acima:

![instalar propriedades raiz](media/install-root-properties.png)

Isso adicionará alguns metadados à propriedade correspondente dentro do arquivo `ProjectReference` .csproj do projeto VSIX:

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> Você pode editar o arquivo .csproj diretamente, se preferir.

## <a name="how-to-set-a-subpath-under-the-installroot"></a>Como definir um subcaminho sob InstallRoot

Se você quiser instalar em um subcaminho abaixo do , poderá fazer isso definindo a `InstallRoot` propriedade exatamente como a propriedade `VsixSubPath` `InstallRoot` . Por exemplo, digamos que desejamos que a saída da nossa referência de projeto seja instalada em '[INSTALLDIR]\MSBuild\MyCompany\MySDK\1.0'. Podemos fazer isso facilmente com o designer de propriedade:

![definir subcaminho](media/set-subpath.png)

As alterações .csproj correspondentes terão esta aparência:

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>Informações adicionais

As alterações do designer de propriedade se aplicam a mais do que apenas referências de projeto; você também pode definir os metadados para itens dentro do projeto `InstallRoot` (usando os mesmos métodos descritos acima).
