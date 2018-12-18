---
title: Quando criar tipos de projeto | Microsoft Docs
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
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 021a4d5e527ca7a22ecd984805b9fbec547531ee
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801661"
---
# <a name="when-to-create-project-types"></a>Quando criar tipos de projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Criar um novo tipo de projeto oferece uma base para a personalização [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para seus usuários. No entanto, criar um novo tipo de projeto não é necessário para todos os [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] personalizações. As diretrizes a seguir devem ajudá-lo a determinar se um novo tipo de projeto é necessário para seu cenário.  
  
## <a name="create-a-new-project-type"></a>Criar um novo tipo de projeto  
 Você deve criar um tipo de projeto se você quiser personalizar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para atuar em uma ou mais das seguintes maneiras:  
  
-   Participa na compilação, implantar, configurações e controle de origem.  
  
-   Oferecem suporte à depuração.  
  
-   Exibir itens de projeto no **Gerenciador de soluções**.  
  
-   Use o **Abrir projeto** ou **novo projeto** caixa de diálogo.  
  
-   Suporte a aninhamento de projeto.  
  
## <a name="extend-an-existing-project-type"></a>Estender um tipo de projeto existente  
 Você talvez queira criar um novo tipo de projeto que pode usar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] das seguintes maneiras para modificar ou estender o comportamento de um tipo de projeto existente, por exemplo, modificando o processo de compilação para [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] projetos:  
  
-   Trabalhar com vários arquivos como uma única unidade.  
  
-   Exiba um único arquivo como uma hierarquia de subitens.  
  
-   Exiba um contexto de comando em torno de editores.  
  
-   Exiba um contexto de serviço para os editores.  
  
## <a name="use-an-existing-project-type"></a>Usar um tipo de projeto existente  
 Criar um novo projeto, às vezes, não é necessário. A tabela a seguir mostra as tarefas que você não precisa criar um tipo de projeto para.  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Manipulando comandos|Qualquer VSPackage pode lidar com comandos.|  
|Criação de um editor|Editores personalizados podem ser registrados. Para obter mais informações, consulte [editores e documentos Windows](http://msdn.microsoft.com/en-us/603625e1-62b6-413a-bc44-089346e166bc).|  
|Proprietário do windows|Você pode criar janelas de ferramenta e o documento sem adicionar um novo tipo de projeto.|  
|Expondo propriedades na janela Propriedades|Todos os objetos podem expor propriedades.|  
  
## <a name="create-a-project-subtype"></a>Criar um subtipo de projeto  
 Você pode usar os subtipos de projeto para estender um tipo de projeto gerenciado sem precisar criar um novo tipo de projeto. Subtipos de projeto usam agregação COM para estender projetos gerenciados escritos em Microsoft [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ou [!INCLUDE[csprcs](../../includes/csprcs-md.md)]. Com a agregação de COM, você pode reutilizar grande parte da implementação do sistema de projeto gerenciado e ainda personalizar para um cenário específico por meio de agregação e o uso de interfaces de suporte. Para obter mais informações sobre os subtipos de projeto, consulte [subtipos do projeto](../../extensibility/internals/project-subtypes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Windows de documento e editores](http://msdn.microsoft.com/en-us/603625e1-62b6-413a-bc44-089346e166bc)   
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)

