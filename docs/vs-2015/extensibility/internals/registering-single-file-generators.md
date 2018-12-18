---
title: Registrar geradores de arquivo único | Microsoft Docs
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
- registration, custom tools
- custom tools, defining registry settings
ms.assetid: db7592c0-1273-4843-9617-6e2ddabb6ca8
caps.latest.revision: 17
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8e601b3fcf8bd702c1bc6cde427766d0f107e6bd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780978"
---
# <a name="registering-single-file-generators"></a>Registrando geradores de arquivo único
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Para disponibilizar uma ferramenta personalizada no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], você deve registrá-lo tão [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] pode instanciá-la e a associa a um tipo de projeto específico.  
  
### <a name="to-register-a-custom-tool"></a>Para registrar uma ferramenta personalizada  
  
1.  Registrar a DLL de ferramenta personalizada ou no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] registro local ou no registro do sistema, sob HKEY_CLASSES_ROOT.  
  
     Por exemplo, eis aqui as informações de registro gerenciado MSDataSetGenerator ferramenta personalizada, que vem com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]:  
  
    ```  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\CLSID\{E76D53CC-3D4F-40A2-BD4D-4F3419755476}]  
    @="COM+ class: Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "InprocServer32"="C:\\WINDOWS\\system32\\mscoree.dll"  
    "ThreadingModel"="Both"  
    "Class"="Microsoft.VSDesigner.CodeGenerator.TypedDataSourceGenerator.DataSourceGeneratorWrapper"  
    "Assembly"="Microsoft.VSDesigner, Version=14.0.0.0, Culture=Neutral, PublicKeyToken=b03f5f7f11d50a3a"  
    ```  
  
2.  Criar uma chave do registro no desejado [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] hive em geradores\\*GUID* onde *GUID* é o GUID definido pelo sistema de projeto específico do idioma ou o serviço. O nome da chave se torna o nome programático da sua ferramenta personalizada. A chave de ferramenta personalizada tem os seguintes valores:  
  
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
  
    [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\14.0\Generators\{e6fdf8b0-f3d1-11d4-8576-0002a516ece8}\MSDataSetGenerator]  
    @="Microsoft J# Code Generator for XSD"  
    "CLSID"="{E76D53CC-3D4F-40a2-BD4D-4F3419755476}"  
    "GeneratesDesignTimeSource"=dword:00000001  
    ```  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator>   
 [Implementando geradores de arquivo único](../../extensibility/internals/implementing-single-file-generators.md)   
 [Determinando o Namespace padrão de um projeto](../../misc/determining-the-default-namespace-of-a-project.md)   
 [Expor tipos aos Designers visuais](../../extensibility/internals/exposing-types-to-visual-designers.md)   
 [Introdução ao objeto BuildManager](http://msdn.microsoft.com/en-us/50080ec2-c1c9-412c-98ef-18d7f895e7fa)

