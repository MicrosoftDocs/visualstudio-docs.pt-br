---
title: Criando instâncias de projeto usando fábricas de projeto | Microsoft Docs
description: Saiba como criar instâncias de classe de projeto usando fábricas de projeto no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project factories
- projects [Visual Studio SDK], project factories
ms.assetid: 94c90012-8669-459c-af8e-307ac242c8c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 40b7c3fbe5b5b7fd59fe0e57376290181f3e9a20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056787"
---
# <a name="create-project-instances-by-using-project-factories"></a>Criar instâncias de projeto usando fábricas de projeto
Tipos de projeto em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usar uma *fábrica de projetos* para criar instâncias de objetos de projeto. Uma fábrica de projetos é semelhante a uma fábrica de classes padrão para objetos COM de Cocriação. No entanto, os objetos do projeto não são cocriáveis; Eles só podem ser criados usando uma fábrica de projetos.

 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE chama a fábrica de projetos implementada em seu VSPackage quando um usuário carrega um projeto existente ou cria um novo projeto no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . O novo objeto de projeto fornece ao IDE informações suficientes para popular **Gerenciador de soluções**. O novo objeto de projeto também fornece as interfaces necessárias para dar suporte a todas as ações de interface do usuário relevantes iniciadas pelo IDE.

 Você pode implementar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> interface em uma classe em seu projeto. Normalmente, ele reside em seu próprio módulo.

 Os projetos que dão suporte à agregação por um proprietário devem persistir uma chave de proprietário em seu arquivo de projeto. Quando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> método é chamado em um projeto com uma chave de proprietário, o projeto de propriedade converte sua chave de proprietário em um GUID de fábrica do projeto, em seguida, chama o `CreateProject` método neste alocador de projeto para fazer a criação real.

## <a name="create-an-owned-project"></a>Criar um projeto de propriedade
 Um proprietário cria um projeto de propriedade em duas fases:

1. Chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.PreCreateForOwner%2A> método. Isso dá ao projeto de propriedade uma oportunidade de criar um objeto de projeto agregado com base no controle de entrada `IUnknown` . O projeto de propriedade passa o `IUnknown` objeto interno e agregado de volta para o projeto de proprietário. Isso dá ao projeto de propriedade uma chance de armazenar o interno `IUnknown` .

2. Chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory.InitializeForOwner%2A> método. O projeto de propriedade faz toda a sua instanciação quando esse método é chamado em vez de chamar `IVsProjectFactory::CreateProject` , como seria o caso de projetos que não são de propriedade. A enumeração de entrada `VSOWNEDPROJECTOBJECT` normalmente é o projeto de propriedade agregada. O projeto de propriedade pode usar essa variável para determinar se seu objeto de projeto já foi criado (cookie não é igual a NULL) ou deve ser criado (cookie é igual a NULL).

   Os tipos de projeto são identificados por um GUID de projeto exclusivo, semelhante ao CLSID de um objeto COM coformativo. Normalmente, uma fábrica de projetos lida com a criação de instâncias de um único tipo de projeto, embora seja possível ter uma fábrica de projetos com mais de um GUID de tipo de projeto.

   Os tipos de projeto são associados a uma extensão de nome de arquivo específica. Quando um usuário tenta abrir um arquivo de projeto existente ou tenta criar um novo projeto clonando um modelo, o IDE usa a extensão no arquivo para determinar o GUID do projeto correspondente.

   Assim que o IDE determina se ele deve criar um novo projeto ou abrir um projeto existente de um tipo específico, o IDE usa as informações no registro do sistema em **[HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\8.0\Projects]** para descobrir qual VSPackage implementa a fábrica de projetos necessária. O IDE carrega esse VSPackage. No <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage.SetSite%2A> método, o VSPackage deve registrar sua fábrica de projetos com o IDE chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes.RegisterProjectType%2A> método.

   O método principal da `IVsProjectFactory` interface é <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory.CreateProject%2A> , que deve lidar com dois cenários: abrir um projeto existente e criar um novo projeto. A maioria dos projetos armazena seu estado de projeto em um arquivo de projeto. Normalmente, novos projetos são criados fazendo uma cópia do arquivo de modelo passado para o `CreateProject` método e, em seguida, abrindo a cópia. Os projetos existentes são instanciados abrindo diretamente o arquivo de projeto passado para o `CreateProject` método. O `CreateProject` método pode exibir recursos adicionais da interface do usuário conforme necessário.

   Um projeto também pode usar nenhum arquivo e, em vez disso, armazenar o estado do projeto em um mecanismo de armazenamento diferente do sistema de arquivos, como um banco de dados ou servidor Web. Nesse caso, o parâmetro de nome de arquivo passado para o `CreateProject` método não é, na verdade, um caminho do sistema de arquivos, mas uma cadeia de caracteres exclusiva — uma URL — para identificar os dados do projeto. Você não precisa copiar os arquivos de modelo que são passados para `CreateProject` para disparar a sequência de construção apropriada a ser executada.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsOwnedProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>
- [Lista de verificação: criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
