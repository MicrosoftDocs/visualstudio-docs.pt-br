---
title: Como atualizar projetos para a versão atual das ferramentas do Azure | Microsoft Docs
description: Saiba como atualizar um projeto do Azure no Visual Studio para a versão atual das ferramentas do Azure
author: ghogen
manager: douge
assetId: 1d64070a-078d-468a-87f4-e6715de6475f
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 11/18/2016
ms.author: ghogen
ms.openlocfilehash: c5fb70f2dd09338dd2e2f6b01cb60bf2be0cdbdd
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001306"
---
# <a name="how-to-upgrade-projects-to-the-current-version-of-the-azure-tools-for-visual-studio"></a>Como atualizar projetos para a versão atual das Ferramentas do Azure para Visual Studio
## <a name="overview"></a>Visão geral
Depois de instalar a versão atual das ferramentas do Azure (ou uma versão anterior mais recente que 1.6), todos os projetos que foram criados usando ferramentas do Azure versão anterior à 1.6 (novembro de 2011) serão atualizados automaticamente assim que você abri-los. Se você criou projetos usando a versão de 1.6 (novembro de 2011) dessas ferramentas e você ainda tiver a versão instalada, você pode abrir esses projetos na versão mais antiga e posteriormente decidir se deseja atualizá-los.

## <a name="how-your-project-changes-when-you-upgrade-it"></a>Como o projeto muda quando você o atualiza
Se um projeto é atualizado automaticamente ou especifique que você deseja atualizá-lo, seu projeto será modificado para funcionar com as versões atuais de determinados assemblies e algumas propriedades também são alteradas, conforme descrito nesta seção. Se seu projeto exigir outras alterações para ser compatível com a versão mais recente das ferramentas, você deve fazer essas alterações manualmente.

* O arquivo Web. config para funções web e o arquivo App. config para funções de trabalho são atualizados para referenciar a versão mais recente do diagnosticmonitoirtracelistener.
* Os assemblies storageclient, Microsoft.WindowsAzure.Diagnostics.dll e Microsoft.WindowsAzure.ServiceRuntime.dll são atualizados para as novas versões.
* Perfis de publicação que foram armazenados no arquivo de projeto do Azure (. ccproj) são movidos para um arquivo separado, com a extensão. azurePubxml, além de **publicar** subdiretório.
* Algumas propriedades no perfil de publicação são atualizadas para dar suporte a recursos novos e alterados. **AllowUpgrade** é substituído por **DeploymentReplacementMethod** porque você pode atualizar um serviço de nuvem implantado simultaneamente ou incrementalmente.
* A propriedade **UseIISExpressByDefault** é adicionada e definida como false para que o servidor web que é usado para depurar não mudará automaticamente de serviços de informações da Internet (IIS) para o IIS Express. O IIS Express é o servidor de web padrão para projetos que são criados com as versões mais recentes das ferramentas.
* Se o cache do Azure estiver hospedado em uma ou mais das funções do seu projeto, algumas propriedades na definição de serviço (arquivo. csdef) e a configuração de serviço (arquivo. cscfg) são alteradas quando um projeto é atualizado. Se o projeto usa o pacote NuGet de Caching do Azure, o projeto é atualizado para a versão mais recente do pacote. Você deve abrir o arquivo Web. config e verifique se que a configuração do cliente foi mantida corretamente durante o processo de atualização. Se você adicionar as referências aos assemblies de cliente de cache do Azure sem usar o pacote do NuGet, esses assemblies não serão atualizados; Você deve atualizar manualmente essas referências para as novas versões.

> [!IMPORTANT]
> Para F# projetos, você deve atualizar manualmente as referências aos assemblies do Azure para que eles fazem referência as versões mais recentes desses assemblies.
> 
> 

### <a name="how-to-upgrade-an-azure-project-to-the-current-release"></a>Como atualizar um projeto do Azure para a versão atual
1. Instale a versão atual das ferramentas do Azure na instalação do Visual Studio que você deseja usar para o projeto atualizado e, em seguida, abra o projeto que você deseja atualizar. Se o projeto foi criado com ferramentas do Azure versão anterior à 1.6 (novembro de 2011), o projeto é atualizado automaticamente para a versão atual. Se o projeto foi criado com a novembro de 2011 a versão e essa versão ainda estiver instalada, o projeto será aberto nessa versão.
2. No Gerenciador de soluções, abra o menu de atalho do nó do projeto, escolha **propriedades**e, em seguida, escolha o **aplicativo** guia da caixa de diálogo que aparece.
   
    O **aplicativo** guia mostra a versão das ferramentas que está associada com o projeto. Se for exibida a versão atual das ferramentas do Azure, o projeto já foi atualizado. Se você tiver instalado uma versão mais recente das ferramentas que mostra que a guia, uma **atualizar** botão é exibido.
3. Escolha o **atualizar** botão para atualizar um projeto para a versão atual das ferramentas.
4. Compile o projeto e resolva os erros resultantes das alterações de API. Para obter informações sobre como modificar seu código para a nova versão, consulte a documentação da API específica.

