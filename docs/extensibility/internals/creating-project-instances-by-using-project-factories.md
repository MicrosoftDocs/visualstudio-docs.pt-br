---
title: Criar instâncias de projetos usando fábricas de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bfde36f5e2b4854dbcee494ddd83ff4610982530
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54936912"
---
# <a name="create-project-instances-by-using-project-factories"></a>Criar instâncias de projetos usando fábricas de projeto
Tipos de projeto em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usar um *fábrica de projeto* para criar instâncias de objetos do projeto. Uma fábrica de projeto é semelhante a uma fábrica de classes padrão para objetos cocreatable do COM. No entanto, os objetos do projeto não são cocreatable; eles só podem ser criados usando uma fábrica de projeto.  
  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE chama a fábrica de projeto implementada no VSPackage quando um usuário carrega um projeto existente ou cria um novo projeto no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. O novo objeto de projeto fornece o IDE com informações suficientes para preencher **Gerenciador de soluções**. O novo objeto de projeto também fornece as interfaces necessárias para dar suporte a todas as ações relevantes de interface do usuário iniciadas pelo IDE.  
  
 Você pode implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> interface em uma classe em seu projeto. Normalmente, residem em seu próprio módulo.  
  
 Projetos que dão suporte ao que está sendo agregada por um proprietário devem manter uma chave de proprietário no seu arquivo de projeto. Quando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> método é chamado em um projeto com uma chave de proprietário, o projeto de propriedade converte sua chave de proprietário para uma fábrica de projeto, GUID, em seguida, chama o `CreateProject` método nesta fábrica de projeto para fazer a criação real.  
  
## <a name="create-an-owned-project"></a>Criar um projeto de propriedade  
 Um proprietário cria um projeto de propriedade em duas fases:  
  
1. Chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A> método. Isso fornece o propriedade projeto uma oportunidade para criar um objeto de projeto agregado com base em como o controle de entrada `IUnknown`. O projeto de propriedade passa interno `IUnknown` e o objeto agregado para o projeto proprietário. Isso fornece a propriedade project a oportunidade de armazenar interno `IUnknown`.  
  
2. Chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A> método. O projeto de propriedade faz todos os seu instanciação quando este método é chamado em vez de chamar `IVsProjectFactory::CreateProject` como seria o caso para projetos que não são de propriedade. A entrada `VSOWNEDPROJECTOBJECT` enumeração normalmente é o projeto de propriedade agregado. O projeto de propriedade pode usar essa variável para determinar se seu objeto de projeto já foi criado (cookie não é igual a NULL) ou deve ser criado (cookie igual a NULL).  
  
   Tipos de projeto são identificados por um GUID, semelhante ao CLSID de um objeto COM cocreatable exclusivo do projeto. Normalmente, um projeto factory manipula a criação de instâncias de um tipo de projeto único, embora seja possível ter uma fábrica de projeto lidar com mais de um GUID de tipo de projeto.  
  
   Tipos de projeto são associados com uma extensão de nome de arquivo específico. Quando um usuário tenta abrir um arquivo de projeto existente ou tenta criar um novo projeto por meio da clonagem de um modelo, o IDE usa a extensão no arquivo para determinar o GUID do projeto correspondente.  
  
   Assim que o IDE determina se ele deve criar um novo projeto ou abra um projeto existente de um tipo específico, o IDE usa as informações no registro do sistema em **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]**  para encontrar qual VSPackage implementa a fábrica de projeto necessários. O IDE carrega esse VSPackage. No <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método, o VSPackage deverá registrar sua fábrica de projeto no IDE chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A> método.  
  
   O principal método o `IVsProjectFactory` interface é <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A>, que deve lidar com dois cenários: abrir um projeto existente e criar um novo projeto. A maioria dos projetos armazena seu estado de projeto em um arquivo de projeto. Normalmente, os novos projetos são criados por fazer uma cópia do arquivo de modelo passada para o `CreateProject` método e, em seguida, abrindo a cópia. Projetos existentes são instanciados por meio diretamente a abertura do arquivo de projeto passado para `CreateProject` método. O `CreateProject` método pode exibir os recursos adicionais da interface do usuário para o usuário conforme necessário.  
  
   Um projeto pode também não usar nenhum arquivo e, em vez disso, armazenar seu estado de projeto em um mecanismo de armazenamento que não seja o sistema de arquivos, como um servidor Web ou um banco de dados. Nesse caso, o parâmetro de nome do arquivo passado para o `CreateProject` método não é, na verdade, um caminho de sistema de arquivos, mas uma cadeia de caracteres exclusiva — uma URL — para identificar os dados do projeto. Você não precisa copiar os arquivos de modelo que são passados para `CreateProject` para disparar a sequência de construção apropriado a ser executado.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>   
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)