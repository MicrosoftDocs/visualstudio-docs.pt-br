---
title: Registrando extensões do .NET Framework | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- Add References dialog box, registering extensions of the .NET Framework
- MSBuild, registering extensions of the .NET Framework
- .NET Framework extensions, registering
ms.assetid: deee6f53-ea87-4b88-a120-bea589822e03
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 0017255b67042a7e42b54325b24512a295ebeaf5
ms.sourcegitcommit: 5b767247b3d819a99deb0dbce729a0562b9654ba
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2018
ms.locfileid: "39180146"
---
# <a name="register-extensions-of-the-net-framework"></a>Registrar extensões do .NET Framework
Você pode desenvolver um assembly que estende uma versão específica do .NET Framework. Para habilitar o assembly a ser exibido na caixa de diálogo **Adicionar Referências** do Visual Studio, você deve adicionar a pasta que contém o Registro do sistema.  
  
 Por exemplo, suponha que a empresa Trey Research desenvolveu uma biblioteca que estende o .NET Framework 4 e deseja que os assemblies de biblioteca apareçam na caixa de diálogo **Adicionar Referências** quando um projeto for voltado para o .NET Framework 4. Suponha também que os assemblies são de 32 bits em execução em um computador de 32 bits ou assemblies de 64 bits que são executados em um computador de 64 bits e que eles serão instalados na pasta *C:\TreyResearch\Extensions4\\*.  
  
 Registre essa pasta usando essa chave: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\**. Forneça o seguinte valor padrão para a chave: **C:\TreyResearch\Extensions4**.  
  
> [!NOTE]
>  O número de build da versão do .NET Framework pode ser diferente.  
  
 Para registrar um assembly de 32 bits em um computador de 64 bits, use o nó Wow6432, por exemplo: **HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\v4.0.21006\AssemblyFoldersEx\TreyResearch\\**.  
  
### <a name="see-also"></a>Consulte também  
 [Integração com o Visual Studio](../msbuild/visual-studio-integration-msbuild.md)