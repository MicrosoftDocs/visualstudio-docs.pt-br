---
title: 'Como: Adicionar e remover dependências de recursos | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
f1_keywords:
- MICROSOFT.VISUALSTUDIO.SHAREPOINT.DESIGNERS.CUSTOMDEPENDENCYWINDOW
- VS.SHAREPOINTTOOLS.RAD.FEATUREDESIGNERDEPENDENCY
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c318a7dc4672a10e993d0149ec77e7f94679d465
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014773"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>Como: Adicionar e remover dependências de recursos
  O recurso do SharePoint pode depender de outros recursos de funcionalidade ou dados. Nesses casos, você pode marcar esses outros recursos como dependências para seu recurso. Dessa forma, o servidor do SharePoint garante que os recursos dependentes sejam ativados antes que o recurso seja ativado.

## <a name="add-dependencies"></a>Adicionar dependências
 Você pode adicionar outros recursos em sua solução como dependências. Dessa forma, você pode verificar se os recursos necessários estão instalados e ativados antes de o recurso ser instalado.

#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>Para adicionar uma dependência em um recurso na solução

1. Abra o designer de recursos, expanda o nó **dependências de ativação de recurso** e escolha o botão **Adicionar** .

2. Na caixa de diálogo **Adicionar dependências de ativação de recurso** , escolha a opção **Adicionar uma dependência nos recursos na solução** , escolha o título do recurso que você deseja adicionar como uma dependência e, em seguida, escolha o botão **Adicionar** .

     Você pode adicionar mais de um recurso escolhendo vários títulos ao escolher a tecla **Ctrl** .

## <a name="addi-custom-dependencies"></a>Por dependências personalizadas
 Você pode adicionar recursos que já estão implantados em um servidor do SharePoint como uma dependência. Dessa forma, o processo de ativação do SharePoint verifica se todos os recursos dependentes são ativados antes da instalação do recurso.

#### <a name="to-add-a-dependency-by-the-feature-id"></a>Para adicionar uma dependência pela ID do recurso

1. Abra o designer de recursos, expanda o nó **dependências de ativação de recurso** e escolha o botão **Adicionar** .

2. Na caixa de diálogo **Adicionar dependências de ativação de recurso** , escolha o botão **Adicionar uma opção de dependência personalizada** .

3. Na caixa de texto **ID do recurso** , insira o GUID do recurso que você deseja marcar como uma dependência de ativação e, em seguida, escolha o botão **Adicionar** .

## <a name="edit-custom-dependencies"></a>Editar dependências personalizadas
 Você pode editar as dependências personalizadas que você adicionou anteriormente. No entanto, os recursos dependentes que estão em sua solução só podem ser removidos, não editados.

#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>Para alterar uma dependência em um recurso na solução

1. Abra o designer de recursos e, em seguida, expanda o nó **dependências de ativação do recurso** .

2. Escolha o nome do recurso que você deseja editar e, em seguida, escolha o botão **Editar** .

3. Na caixa de diálogo **Editar dependência de ativação de recurso personalizado** , altere o título, a ID do recurso ou a descrição e, em seguida, escolha o botão **Enviar** .

## <a name="remove-dependencies"></a>Remover dependências

#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>Para remover uma dependência de um recurso na solução

1. No designer de recursos, expanda o nó **dependências de ativação de recurso** , escolha o nome do recurso que você deseja remover e, em seguida, escolha o botão **remover** .

## <a name="see-also"></a>Consulte também
- [Criar recursos do SharePoint](../sharepoint/creating-sharepoint-features.md)
- [Como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md)
- [Como: Adicionar e remover itens para recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)
