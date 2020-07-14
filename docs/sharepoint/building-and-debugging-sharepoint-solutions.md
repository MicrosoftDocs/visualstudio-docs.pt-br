---
title: Criando e Depurando soluções do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, building and debugging
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e4b34df23c8cb612d72fed108a6c0aecbf57875c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016364"
---
# <a name="build-and-debug-sharepoint-solutions"></a>Compilar e depurar soluções do SharePoint
  Em geral, a criação e a depuração de soluções do SharePoint são as mesmas que a criação e a depuração de outros tipos de projetos no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Os tópicos nesta seção explicam as diferenças que existem.

## <a name="project-output-for-sharepoint-solutions"></a>Saída do projeto para soluções do SharePoint
 A criação de soluções do SharePoint cria assemblies e um arquivo de pacote de solução (*. wsp*). A tabela a seguir mostra os locais desses arquivos durante uma compilação.

|Compilar item|Pasta de saída|
|----------------|-------------------|
|Assembly, banco de dados do programa (*. pdb*) e arquivos *. wsp* .|* \<ProjectName> \bin\Debug* ou * \<ProjectName> \bin\Release*|
|Arquivos de item de projeto do SharePoint.|* \<ProjectName> \pkg\debug* ou * \<ProjectName> \pkg\release*|
|Compilar arquivos intermediários.|* \<ProjectName> \obj\debug* ou * \<ProjectName> \obj\release*|
|Empacotar arquivos intermediários.|* \<ProjectName> \pkgobj\debug* ou * \<ProjectName> \pkgobj\release*|

## <a name="build-sharepoint-solutions"></a>Criar soluções do SharePoint
 Para criar soluções do SharePoint, o computador de desenvolvimento deve ter a versão correta do SharePoint Server instalada. Caso contrário, criar soluções do SharePoint é o mesmo que criar outros tipos de projetos no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Para obter mais informações, consulte [como compilar soluções do SharePoint](../sharepoint/how-to-build-sharepoint-solutions.md).

## <a name="debug-and-test-sharepoint-solutions"></a>Soluções de depuração e teste do SharePoint
 Antes da depuração, [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] o copia o pacote *. wsp* para o servidor do SharePoint, ativa o site e os recursos no escopo da Web e, em alguns casos, inicia o projeto. Em outros casos, talvez seja necessário abrir o projeto manualmente. Para obter mais informações, consulte [solucionar problemas de soluções do SharePoint](../sharepoint/troubleshooting-sharepoint-solutions.md) e [depurar soluções do SharePoint](../sharepoint/debugging-sharepoint-solutions.md).

## <a name="debug-and-verify-sharepoint-solutions-by-using-azure-devops-services-features"></a>Depurar e verificar soluções do SharePoint usando Azure DevOps Services recursos
 Azure DevOps Services recursos como o teste de unidade e o IntelliTrace permitem identificar problemas com mais precisão nas soluções do SharePoint. A criação de perfil permite que você localize e identifique áreas problemáticas de desempenho em suas soluções do SharePoint. Para obter mais informações, consulte [verificando e Depurando o código do SharePoint](../sharepoint/verifying-and-debugging-sharepoint-code.md) e [criando o perfil do desempenho de aplicativos do SharePoint](../sharepoint/profiling-the-performance-of-sharepoint-applications.md).

## <a name="security-during-the-build-process"></a>Segurança durante o processo de compilação
 Para empacotar ou implantar soluções do SharePoint, o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] deve ter permissão para copiar arquivos para o servidor do SharePoint. Você deve executar o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] como um processo elevado e sua conta de usuário deve ser um administrador de conjuntos de sites no servidor do SharePoint. Além disso, você deve especificar se seu projeto é uma solução em área restrita ou uma solução de farm. Para obter mais informações, consulte [diferenças entre as soluções de área restrita e de farm](../sharepoint/differences-between-sandboxed-and-farm-solutions.md).

## <a name="using-the-clean-command"></a>Usando o comando limpar
 Quando uma solução do SharePoint é instalada em um servidor do SharePoint para depuração, o comando **limpar** não desinstala a solução. Em vez disso, você deve desativar os recursos por meio da configuração do SharePoint.

## <a name="see-also"></a>Consulte também
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Procurar conexões do SharePoint usando Gerenciador de Servidores](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
