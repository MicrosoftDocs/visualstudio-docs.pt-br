---
title: Visão geral das propriedades de documento personalizadas
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], custom properties
- custom document properties
- document-level customizations [Office development in Visual Studio], custom properties
- Office documents [Office development in Visual Studio], custom properties
- _AssemblyLocation property
- _AssemblyName property
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 23d0aa3b065a05b1c85b54e7889c4fe1bac4af7a
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671515"
---
# <a name="custom-document-properties-overview"></a>Visão geral das propriedades de documento personalizadas

Quando você compila um projeto de nível de documento, o Visual Studio adiciona duas propriedades personalizadas para o documento no projeto: \_AssemblyLocation e \_AssemblyName. Quando um usuário abre um documento, verifica se o aplicativo do Microsoft Office para essas propriedades de documento personalizadas. Se existirem no documento, o aplicativo carrega o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)], que inicia a personalização. Para obter mais informações, consulte [soluções de arquitetura do Office no Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md).

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="assemblyname"></a>\_AssemblyName

Esta propriedade contém o CLSID de uma interface no componente de carregador de solução do Office da [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]. O valor CLSID é 4E3C66D5 - 58D 4-491E-A7D4-64AF99AF6E8B. Você nunca deve alterar esse valor.

## <a name="assemblylocation"></a>\_AssemblyLocation

Esta propriedade contém uma cadeia de caracteres que fornece detalhes sobre o manifesto de implantação para a personalização. Para obter mais informações sobre manifestos, consulte [manifestos do aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md).

 Valor da propriedade The_AssemblyLocation pode ter formatos diferentes, dependendo de como a solução é implantada:

- Se a solução for publicada para ser instalado a partir de um site da Web, o caminho UNC ou uma unidade de CD ou USB, a propriedade assemblylocation tem o formato *DeploymentManifestPath*|*SolutionID*. A cadeia de caracteres a seguir está um exemplo:

     file://deployserver/MyShare/ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9

- Se você estiver em execução ou depurar a solução do Visual Studio, a propriedade assemblylocation tem o formato *DeploymentManifestName*|*SolutionID*| vstolocal. A cadeia de caracteres a seguir está um exemplo:

     ExcelWorkbook1.vsto|74744e4b-e4d6-41eb-84f7-ad20346fe2d9|vstolocal

  O *SolutionID* é um GUID que o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] usa para identificar a solução. O *SolutionID* é gerado automaticamente quando você compila o projeto. O **vstolocal** termo indica para o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] que o assembly deve ser carregado na mesma pasta que o documento.

## <a name="see-also"></a>Consulte também

- [Arquitetura de soluções do Office no Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)
- [Arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md)
- [Manifestos de aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md)
- [Como: publicar uma solução do Office usando o ClickOnce](https://msdn.microsoft.com/2b6c247e-bc04-4ce4-bb64-c4e79bb3d5b8)
- [Como: criar e modificar propriedades de documento personalizadas](../vsto/how-to-create-and-modify-custom-document-properties.md)
