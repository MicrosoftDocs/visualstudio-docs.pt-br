---
title: Suporte a formulários em fluxos de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, workflows
- workflows [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 27e8ab6651c6838de92b8a3d83311ebd47fabcbb
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296184"
---
# <a name="form-support-in-workflows"></a>Suporte de formulário nos fluxos de trabalho
  Quatro tipos de formulários podem ser usados em um fluxo de trabalho: associação, inicialização, tarefa e modificação. Esses tipos de formulário podem ser baseados em um formulário ASPX ou em um formulário do InfoPath. O nível de suporte que [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] fornece para um formulário específico depende de vários fatores, que são descritos nas tabelas a seguir. Para obter mais informações sobre os tipos de formulário de fluxo de trabalho, consulte [visão geral de formulários de fluxo de trabalho](http://go.microsoft.com/fwlink/?LinkId=185228).  
  
## <a name="xml-refactoring"></a>Refatoração de XML
 Quando você adiciona um formulário de associação ou o início do ASPX para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] item de projeto de fluxo de trabalho [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] automaticamente refatora o XML do fluxo de trabalho *Elements. XML* arquivo para manter o atributo que se refere à associação ou o formulário de inicialização em sincronização sempre que o caminho de implantação ou o nome do formulário é atualizado ou o formulário é excluído. No entanto, quando você usar outros tipos de formulário em um fluxo de trabalho, como um formulário de tarefa ou de modificação, o *Elements. XML* arquivo não é refatorado.  
  
## <a name="form-support-in-new-visual-studio-workflows"></a>Suporte de formulário nos novos fluxos de trabalho do Visual Studio
 A seguinte tabela lista [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] suporte para tipos de forma diferente em formulários ASPX ou InfoPath nos fluxos de trabalho que são criados no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
|Tipo de formulário|Fluxo de trabalho criado no Visual Studio com um formulário ASPX|Fluxo de trabalho criado no Visual Studio usando um formulário do InfoPath|  
|---------------|---------------------------------------------------------|-----------------------------------------------------------------|  
|Associação|-Um formulário de associação ASPX pode ser adicionado ao fluxo de trabalho usando o **formulário de associação de fluxo de trabalho** modelo de item.<br />-A *Elements. XML* arquivo do fluxo de trabalho é refatorado quando o formulário for adicionado, renomeado ou excluído, ou quando seu caminho de implantação é alterado.<br />-Para obter mais informações, consulte [instruções passo a passo: Criando um fluxo de trabalho com associação e formulários de iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md).|-Não há nenhum modelo de formulário do InfoPath associação no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].<br />-Não há nenhuma integração entre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e Designer do InfoPath.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.|  
|Iniciação|-Um formulário de inicialização ASPX pode ser adicionado ao fluxo de trabalho usando o **formulário de iniciação do fluxo de trabalho** modelo de item.<br />-A *Elements. XML* arquivo do fluxo de trabalho é refatorado quando o formulário for adicionado, renomeado ou excluído, ou quando seu caminho de implantação é alterado.<br />-Para obter mais informações, consulte [instruções passo a passo: Criando um fluxo de trabalho com associação e formulários de iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md).|-Não há nenhum modelo de formulário do InfoPath associação no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].<br />-Não há nenhuma integração entre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e Designer do InfoPath.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.|  
|Tarefa|-Nenhum modelo de formulário de tarefa ASPX está disponível em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Você deve criar uma página de aplicativo e adicione o código a ele.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.<br />-Para obter mais informações, consulte [formulários de tarefa de fluxo de trabalho (SharePoint Foundation)](http://go.microsoft.com/fwlink/?LinkId=187674)|-Não há nenhum modelo de formulário de tarefa do InfoPath em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].<br />-Não há nenhuma integração entre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e Designer do InfoPath.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.|  
|Modificação|-Nenhum modelo de formulário de modificação de ASPX está disponível em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Para adicionar um formulário de modificação, você deve criar uma página de aplicativo e adicione o código a ele.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado. Você deve editar manualmente-lo conforme apropriado.<br />-Para obter mais informações, consulte [formulários de modificação de fluxo de trabalho (SharePoint Foundation)](http://go.microsoft.com/fwlink/?LinkId=187675)|-Não há nenhum modelo de formulário do InfoPath modificação no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].<br />-Não há nenhuma integração entre [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e Designer do InfoPath.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.|  
  
## <a name="form-support-in-imported-sharepoint-reusable-workflows"></a>Suporte a formulários em SharePoint reutilizáveis fluxos de trabalho
 A seguinte tabela lista [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] suporte para tipos de forma diferente em formulários ASPX ou do InfoPath nos fluxos de trabalho reutilizáveis do SharePoint que são importados para [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
|Tipo de formulário|Fluxo de trabalho reutilizável que tem uma forma ASPX importada do SharePoint Designer|Fluxo de trabalho reutilizável que tem um formulário do InfoPath importado do SharePoint Designer|  
|---------------|-------------------------------------------------------------------------------| - |  
|Associação|-O formulário é referenciado na *Elements. XML* arquivo do fluxo de trabalho.<br />-A *Elements. XML* arquivo do fluxo de trabalho é refatorado quando o formulário for renomeado ou excluído, ou quando seu caminho de implantação é alterado.|-O formulário é importado, mas não referenciado na *Elements. XML* do fluxo de trabalho.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.|  
|Iniciação|-O formulário é referenciado pelo fluxo de trabalho na *Elements. XML* arquivo do fluxo de trabalho.<br />-A *Elements. XML* arquivo do fluxo de trabalho é refatorado quando o formulário for renomeado ou excluído, ou quando seu caminho de implantação é alterado.|-O formulário é importado, mas não referenciado na *Elements. XML* do fluxo de trabalho.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado. **Observação:** regras e propriedades devem ser adicionadas e alteradas para este cenário funcione.|  
|Tarefa|-O formulário é referenciado na *Elements. XML* arquivo do fluxo de trabalho.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado.|-O formulário é importado, mas não referenciado na *Elements. XML* do fluxo de trabalho.<br />-A *Elements. XML* arquivo do fluxo de trabalho não é refatorado. **Observação:** regras e propriedades devem ser adicionadas e alteradas para este cenário funcione.|  
|Modificação|Não aplicável. Não não possível criar formulários de modificação de ASPX no SharePoint Designer.|Não aplicável. Formulários de modificação do InfoPath não não possível criar no SharePoint Designer, exceto para o fluxo de trabalho de servidor do SharePoint interno, que não está incluído no arquivo. wsp quando o fluxo de trabalho é exportado.|  
  
## <a name="see-also"></a>Consulte também
 [Passo a passo: Criar um fluxo de trabalho com formulários de associação e iniciação](../sharepoint/walkthrough-creating-a-workflow-with-association-and-initiation-forms.md)   
 [Criar soluções de fluxo de trabalho do SharePoint](../sharepoint/creating-sharepoint-workflow-solutions.md)   
 [Importar itens de um site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)  
  
  
