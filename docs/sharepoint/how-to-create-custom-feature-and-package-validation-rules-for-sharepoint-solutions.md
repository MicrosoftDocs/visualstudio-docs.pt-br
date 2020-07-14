---
title: 'Soluções do SharePoint: criar recurso personalizado, regras de validação de pacote'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
- SharePoint development in Visual Studio, validation rules
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f731b6af2ada8caddb84be5561d7f6dc304e7bbd
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016908"
---
# <a name="how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions"></a>Como criar regras de validação de pacotes e recursos personalizados para soluções do SharePoint
  Você pode criar regras de validação personalizadas para verificar o pacote de solução gerado pelo Visual Studio. Você pode executar a validação completa em um recurso ou pacote inteiro selecionando **validar** no menu de contexto de um pacote ou recurso no **PackagingExplorer**. A validação parcial é executada quando você adiciona novos itens de projeto do SharePoint ou recursos ao projeto para determinar se o pacote ou recurso estaria em um estado válido.

### <a name="to-create-a-custom-package-validation-rule"></a>Para criar uma regra de validação de pacote personalizada

1. Crie um projeto de biblioteca de classes.

2. Adicione referências aos assemblies a seguir:

    - Microsoft. VisualStudio. SharePoint

    - System. ComponentModel. composição

3. Crie uma classe que implemente uma das seguintes interfaces:

    - Para criar uma regra de validação de pacote, implemente a <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> interface.

    - Para criar uma regra de validação de recurso, implemente a <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> interface.

4. Adicione o <xref:System.ComponentModel.Composition.ExportAttribute> à classe. Esse atributo permite que o Visual Studio descubra e carregue sua regra de validação. Passe o <xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule> <xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule> tipo ou para o construtor de atributo.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como criar uma regra de validação de recurso personalizada.

 [!code-vb[SPExtensibility.FeatureValidation#1](../sharepoint/codesnippet/VisualBasic/featurevalidation/extension/customvalidationrule.vb#1)]
 [!code-csharp[SPExtensibility.FeatureValidation#1](../sharepoint/codesnippet/CSharp/featurevalidation/extension/customfeaturevalidationrule.cs#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint.

- System. ComponentModel. composição.

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
