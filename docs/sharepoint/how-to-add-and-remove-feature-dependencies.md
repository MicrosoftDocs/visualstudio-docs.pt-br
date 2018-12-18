---
title: 'Como: adicionar e remover dependências de recurso | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- MICROSOFT.VISUALSTUDIO.SHAREPOINT.DESIGNERS.CUSTOMDEPENDENCYWINDOW
- VS.SHAREPOINTTOOLS.RAD.FEATUREDESIGNERDEPENDENCY
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, features
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a7a61ff71b5ed8caa8ad50dff71957bee20b955a
ms.sourcegitcommit: 30f653d9625ba763f6b58f02fb74a24204d064ea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2018
ms.locfileid: "36757986"
---
# <a name="how-to-add-and-remove-feature-dependencies"></a>Como: adicionar e remover dependências de recurso
  O recurso do SharePoint pode depender de outros recursos de funcionalidade ou dados. Nesses casos, você pode marcar esses outros recursos como dependências para o recurso. Dessa forma, o servidor do SharePoint assegura que os recursos dependentes são ativados antes do recurso é ativado.  
  
## <a name="add-dependencies"></a>Adicionar dependências  
 Você pode adicionar outros recursos em sua solução como dependências. Dessa forma, você pode garantir que os recursos necessários são instalados e ativados antes do recurso é instalado.  
  
#### <a name="to-add-a-dependency-on-a-feature-in-the-solution"></a>Para adicionar uma dependência em um recurso na solução
  
1.  Abra o Designer de recursos, expanda o **dependências de ativação do recurso** nó e, em seguida, escolha o **Add** botão.  
  
2.  No **adicionar dependências de ativação do recurso** diálogo caixa, escolha o **adicionar uma dependência de recursos na solução** botão de opção, escolha o título do recurso que você deseja adicionar como uma dependência e, em seguida, Escolha o **adicionar** botão.  
  
     Você pode adicionar mais de um recurso ao escolher vários títulos ao escolher o **Ctrl** chave.  
  
## <a name="addi-custom-dependencies"></a>Dependências de Addi personalizadas  
 Você pode adicionar recursos que já foram implantados em um servidor do SharePoint como uma dependência. Dessa forma, o processo de ativação do SharePoint verifica para ter certeza de que todos os recursos dependentes são ativados antes do recurso está instalado.  
  
#### <a name="to-add-a-dependency-by-the-feature-id"></a>Para adicionar uma dependência pela ID de recurso
  
1.  Abra o Designer de recursos, expanda o **dependências de ativação do recurso** nó e, em seguida, escolha o **Add** botão.  
  
2.  No **adicionar dependências de ativação do recurso** diálogo caixa, escolha o **adicionar uma dependência personalizada** botão de opção.  
  
3.  No **ID do recurso** texto, digite o GUID para o recurso que você deseja marcar como uma dependência de ativação e, em seguida, escolha o **Add** botão.  
  
## <a name="edit-custom-dependencies"></a>Editar dependências personalizadas  
 Você pode editar dependências personalizadas que você adicionou anteriormente. No entanto, os recursos dependentes que estão em sua solução também podem apenas ser removida, não editado.  
  
#### <a name="to-change-a-dependency-on-a-feature-in-the-solution"></a>Para alterar uma dependência em um recurso na solução
  
1.  Abra o Designer de recursos e, em seguida, expanda o **dependências de ativação do recurso** nó.  
  
2.  Escolha o nome do recurso que você deseja editar e, em seguida, escolha o **editar** botão.  
  
3.  No **Editar dependência de ativação de recurso personalizado** caixa de diálogo, altere o título, a ID de recurso ou a descrição e, em seguida, escolha o **enviar** botão.  
  
## <a name="remove-dependencies"></a>Remova as dependências  
  
#### <a name="to-remove-a-dependency-on-a-feature-in-the-solution"></a>Para remover uma dependência em um recurso na solução
  
1.  No Designer de recursos, expanda o **dependências de ativação do recurso** nó, escolha o nome do recurso que você deseja remover e, em seguida, escolha o **remover** botão.  
  
## <a name="see-also"></a>Consulte também
 [Criar recursos do SharePoint](../sharepoint/creating-sharepoint-features.md)   
 [Como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md)   
 [Como: adicionar e remover itens de recursos do SharePoint](../sharepoint/how-to-add-and-remove-items-to-sharepoint-features.md)  
  
