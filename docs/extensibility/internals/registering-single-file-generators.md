---
title: Registrando geradores de arquivo único | Microsoft Docs
description: Saiba como registrar uma ferramenta personalizada no Visual Studio para instanciá-la e associá-la a um tipo de projeto específico.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ee110defb06d308c017230a36cebc2b04b3c63b9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062675"
---
# <a name="registering-single-file-generators"></a>Registrando geradores de arquivo único
Para disponibilizar uma ferramenta personalizada no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , você deve registrá-la para que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] possa instanciá-la e o associe a um determinado tipo de projeto.

### <a name="to-register-a-custom-tool"></a>Para registrar uma ferramenta personalizada

1. Registre a DLL de ferramenta personalizada no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Registro local ou no registro do sistema, em HKEY_CLASSES_ROOT.

    Por exemplo, aqui estão as informações de registro da ferramenta personalizada MSDataSetGenerator gerenciada, que vem com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] :

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"
   "ThreadingModel"="Both"
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"
   ```

2. Crie uma chave do registro no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Hive desejado em GUID de geradores, \\  em que *GUID* é o GUID definido pelo serviço ou sistema de projeto do idioma específico. O nome da chave se torna o nome programático de sua ferramenta personalizada. A chave de ferramenta personalizada tem os seguintes valores:

   - (Padrão)

        Opcional. Fornece uma descrição amigável da ferramenta personalizada. Esse parâmetro é opcional, mas recomendado.

   - CLSID

        Obrigatórios. Especifica o identificador da biblioteca de classes do componente COM que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> .

   - GeneratesDesignTimeSource

        Obrigatórios. Indica se os tipos de arquivos produzidos por essa ferramenta personalizada são disponibilizados para designers visuais. O valor desse parâmetro precisa ser (zero) 0 para tipos não disponíveis para designers visuais ou (um) 1 para tipos disponíveis para designers visuais.

   > [!NOTE]
   > Você deve registrar a ferramenta personalizada separadamente para cada idioma para o qual você deseja que a ferramenta personalizada esteja disponível.

    Por exemplo, o MSDataSetGenerator se registra uma vez para cada idioma:

   ```
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{164b10b9-b200-11d0-8c61-00a0c91e29d5}\MSDataSetGenerator]
   @="Microsoft VB Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001

   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{fae04ec1-301f-11d3-bf4b-00c04f79efbc}\MSDataSetGenerator]
   @="Microsoft C# Code Generator for XSD"
   "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"
   "GeneratesDesignTimeSource"=dword:00000001
   ```

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>
- [Implementando geradores de arquivo único](../../extensibility/internals/implementing-single-file-generators.md)
- [Expondo tipos para designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)
- [Introdução ao objeto BuildManager](/previous-versions/8f9kffa8(v=vs.140))