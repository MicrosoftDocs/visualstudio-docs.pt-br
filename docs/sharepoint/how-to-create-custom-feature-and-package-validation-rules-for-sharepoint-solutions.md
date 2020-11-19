---
title: Criar validações de recursos e pacotes para soluções do SharePoint
titleSuffix: ''
description: Crie regras de validação personalizadas para verificar o pacote de solução gerado pelo Visual Studio ou para verificar um recurso inteiro.
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 8f76abeee6ace851025a29ce6d85b894bf479dfa
ms.sourcegitcommit: 86e98df462b574ade66392f8760da638fe455aa0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2020
ms.locfileid: "94903683"
---
# <a name="create-feature-and-package-validations-for-sharepoint-solutions"></a>Criar validações de recursos e pacotes para soluções do SharePoint

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

## <a name="see-also"></a>Confira também
- [Estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
