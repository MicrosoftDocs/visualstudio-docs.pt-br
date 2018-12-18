---
title: Registrar geradores de arquivo único | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a2e65a1ef3db913223d9248797d1cf4bd9c9ded6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49875990"
---
# <a name="registering-single-file-generators"></a>Registrando geradores de arquivo único
Para disponibilizar uma ferramenta personalizada no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], você deve registrá-lo tão [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] pode instanciá-la e a associa a um tipo de projeto específico.  
  
### <a name="to-register-a-custom-tool"></a>Para registrar uma ferramenta personalizada  
  
1. Registrar a DLL de ferramenta personalizada ou no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] registro local ou no registro do sistema, sob HKEY_CLASSES_ROOT.  
  
    Por exemplo, eis aqui as informações de registro gerenciado MSDataSetGenerator ferramenta personalizada, que vem com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]:  
  
   ```  
   [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]  
   @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
   "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"  
   "ThreadingModel"="Both"  
   "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
   "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"  
   ```  
  
2. Criar uma chave do registro no desejado [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] hive em geradores\\*GUID* onde *GUID* é o GUID definido pelo sistema de projeto específico do idioma ou o serviço. O nome da chave se torna o nome programático da sua ferramenta personalizada. A chave de ferramenta personalizada tem os seguintes valores:  
  
   -   (Padrão)  
  
        Opcional. Fornece uma descrição amigável da ferramenta personalizada. Esse parâmetro é opcional, mas recomendado.  
  
   -   CLSID  
  
        Necessário. Especifica o identificador da biblioteca de classes do componente COM que implementa <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>.  
  
   -   GeneratesDesignTimeSource  
  
        Necessário. Indica se os tipos de arquivos gerados por essa ferramenta personalizada são disponibilizados aos designers visuais. O valor desse parâmetro precisa ser (zero) 0 para tipos não disponíveis aos designers visuais ou 1 (um) para os tipos disponíveis para designers visuais.  
  
   > [!NOTE]
   >  Você deve registrar a ferramenta personalizada separadamente para cada idioma para o qual você deseja que a ferramenta personalizada esteja disponível.  
  
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
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>   
 [Implementando geradores de arquivo único](../../extensibility/internals/implementing-single-file-generators.md)   
 [Expor tipos aos Designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)   
 [Introdução ao objeto BuildManager](https://msdn.microsoft.com/library/50080ec2-c1c9-412c-98ef-18d7f895e7fa)