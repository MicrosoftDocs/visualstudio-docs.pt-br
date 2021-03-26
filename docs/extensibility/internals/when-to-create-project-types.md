---
title: Quando criar tipos de projeto | Microsoft Docs
description: Saiba como determinar se um novo tipo de projeto é necessário para personalizar o Visual Studio para seus usuários.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, conditions for creating
ms.assetid: 26adc860-ee4a-4f5c-95e1-e41b207dd7e6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 427c35a03f9d0cb11667ca9eaf88f144d018f620
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074295"
---
# <a name="when-to-create-project-types"></a>Quando criar tipos de projeto
A criação de um novo tipo de projeto fornece uma base para personalizar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] os usuários. No entanto, a criação de um novo tipo de projeto não é necessária para todas as [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] personalizações. As diretrizes a seguir devem ajudá-lo a determinar se um novo tipo de projeto é necessário para seu cenário.

## <a name="create-a-new-project-type"></a>Criar um novo tipo de projeto
 Você deve criar um tipo de projeto se quiser personalizar [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o para agir de uma ou mais das seguintes maneiras:

- Participe de compilação, implantação, configurações e controle do código-fonte.

- Oferecer suporte à depuração.

- Exibir itens de projeto no **Gerenciador de soluções**.

- Use a caixa de diálogo **Abrir projeto** ou **novo projeto** .

- Suporte a aninhamento de projetos.

## <a name="extend-an-existing-project-type"></a>Estender um tipo de projeto existente
 Talvez você queira criar um novo tipo de projeto que possa ser usado [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] nas seguintes maneiras de modificar ou estender o comportamento de um tipo de projeto existente, por exemplo, modificar o processo de compilação para [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] projetos:

- Trabalhe com vários arquivos como uma única unidade.

- Exibir um único arquivo como uma hierarquia de subitens.

- Exiba um contexto de comando em volta de editores.

- Exibir um contexto de serviço para editores.

## <a name="use-an-existing-project-type"></a>Usar um tipo de projeto existente
 Às vezes, a criação de um novo projeto não é necessária. A tabela a seguir mostra as tarefas para as quais você não precisa criar um tipo de projeto.

|Tarefa|Descrição|
|----------|-----------------|
|Manipulando comandos|Qualquer VSPackage pode manipular comandos.|
|Criando um editor|Editores personalizados podem ser registrados. Para obter mais informações, consulte [janelas de documentos e editores](/previous-versions/bb165691(v=vs.100)).|
|Janelas proprietárias|Você pode criar as janelas de ferramentas e de documentos sem adicionar um novo tipo de projeto.|
|Expondo Propriedades no janela Propriedades|Todos os objetos podem expor propriedades.|

## <a name="create-a-project-subtype"></a>Criar um subtipo de projeto
 Você pode usar subtipos de projeto para estender um tipo de projeto gerenciado sem precisar criar um novo tipo de projeto. Os subtipos de projeto usam agregação COM para estender projetos gerenciados escritos na Microsoft [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] ou [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] . Com a agregação COM, você pode reutilizar grande parte da implementação do sistema de projeto gerenciado e ainda Personalizar para um cenário específico por meio da agregação e do uso de interfaces de suporte. Para obter mais informações sobre subtipos de projeto, consulte [subtipos de projeto](../../extensibility/internals/project-subtypes.md).

## <a name="see-also"></a>Confira também
- [Documentar janelas e editores](/previous-versions/bb165691(v=vs.100))
- [Lista de verificação: Criando tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Hierarquias no Visual Studio](../../extensibility/internals/hierarchies-in-visual-studio.md)