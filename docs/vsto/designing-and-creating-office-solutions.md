---
title: Projetar e criar soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office solutions [Office development in Visual Studio], creating
- Office development in Visual Studio, creating solutions
- solutions [Office development in Visual Studio], creating
- Office project types in Visual Studio
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 05cf317823d4f5853d960109bd97da77ea8a927d
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671232"
---
# <a name="design-and-create-office-solutions"></a>Projetar e criar soluções do Office
  Visual Studio fornece modelos de projeto que você pode usar para criar vários tipos diferentes de soluções do Office. Esta seção da documentação descreve os modelos de projeto e fornece orientação sobre como criar projetos do Office. Para obter informações sobre como implementar personalizações de interface do usuário e código depois de ter criado seu projeto, consulte [soluções do Office desenvolver](../vsto/developing-office-solutions.md).  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="create-office-projects"></a>Criar projetos do Office  
 Antes de começar, você deve determinar os requisitos e descobrir o tipo de solução que oferece a melhor opção. Por exemplo, se sua solução do Office deve ser executado toda vez que o aplicativo é usado, um suplemento do VSTO melhor se ajusta às suas necessidades. Se o código está totalmente integrado com um único documento, crie uma personalização no nível de documento. Esses tipos de projeto estão disponíveis como modelos de projeto do Visual Studio. Para obter mais informações sobre os modelos de projeto do Office que estão incluídos com o Visual Studio, consulte [visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md). Para obter mais informações sobre como criar projetos do Office, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
 Projetos do Office têm recursos e itens de projeto que são diferentes dos outros tipos de projetos no Visual Studio. Por exemplo, quando você cria um projeto de nível de documento, o documento ou pasta de trabalho em seu projeto pode ser aberta e editada no Visual Studio. Para obter mais informações, consulte [projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md).  
  
## <a name="choose-a-net-framework-version"></a>Escolha uma versão do .NET Framework  
 Depois de selecionar o tipo de projeto que melhor atenda às suas necessidades, você pode escolher qual versão do .NET Framework para usar no processo de desenvolvimento. Você pode direcionar as seguintes versões do .NET Framework em projetos do Office:  
  
- [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]  
  
- [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)]  
  
- [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]  
  
  A versão do .NET Framework que você escolher para seu projeto é necessário nos computadores de usuário final para sua solução seja executada. Por exemplo, se o projeto está destinado a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] é necessário nos computadores de usuário final. Neste exemplo, sua solução não será executado se apenas o .NET Framework 3.5 está instalado nos computadores dos usuários finais.  
  
  Se você migrar um projeto de suplemento do VSTO que tem como alvo o .NET Framework 3.5, o Visual Studio altera a estrutura de destino do seu projeto para [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, dependendo da versão do Office que você instalou.  
  
  No entanto, depois que o Visual Studio altera a estrutura de destino, você talvez precise modificar alguns dos códigos em seu projeto se ele usar determinados recursos. Para obter mais informações sobre como alterar a estrutura de destino, consulte [como: uma versão do .NET Framework de destino](../ide/how-to-target-a-version-of-the-dotnet-framework.md). Para obter mais informações sobre as alterações que você talvez precise fazer em seu projeto, consulte [soluções do Office de migrar para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md).  
  
  Se o Visual Studio altera o .NET Framework de destino para o seu projeto e você estiver usando o ClickOnce para implantar sua solução, certifique-se de que você também pode selecionar a versão correspondente do .NET Framework na **pré-requisitos** caixa de diálogo. Essa seleção não será alterada automaticamente quando você altera a estrutura de destino para o seu projeto. Para obter mais informações, consulte [como: instalar pré-requisitos em computadores de usuário final para executar soluções do Office](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98).  
  
> [!NOTE]  
>  Não é possível direcionar o .NET Framework 3.5 ou anterior em projetos do Office que você cria usando [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)]. Projetos do Office que você cria usando [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)] exigem recursos que foram introduzidos primeiro no [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)]  
  
### <a name="understand-when-the-office-pias-are-required-on-end-user-computers"></a>Entenda quando os PIAs do Office são necessários em computadores de usuários finais  
 Por padrão, assemblies de interoperabilidade primários do Office (PIAs) não precisa ser instalado em computadores de usuários finais se a **Embed Interop Types** de cada referência de PIA do Office no projeto estiver definida como **verdadeiro**, qual é o valor padrão. Nesse cenário, as informações de tipo para os tipos PIA que são usados pela sua solução são incorporadas no assembly da solução quando você compila o projeto. Em tempo de execução, as informações de tipo inserido são usadas em vez dos PIAs chamem o modelo de objeto baseado em COM de aplicativo do Office. Para obter mais informações sobre como os tipos de PIAs são inseridos em sua solução, consulte [equivalência de tipos e tipos de interoperabilidade inseridos](/dotnet/framework/interop/type-equivalence-and-embedded-interop-types).  
  
 Se o **Embed Interop Types** de cada referência de PIA do Office no projeto estiver definida como **falso**, PIAs do Office deve ser instalado e registrado no cache de assembly global em cada computador do usuário final que executa a solução. Na maioria dos casos, os PIAs são instalados por padrão com o Office, mas você também pode incluir o PIA redistribuível como um pré-requisito para a sua solução. Para obter mais informações, consulte [pré-requisitos de solução do Office para implantação](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e).  
  
### <a name="understand-the-client-profile"></a>Entender o perfil de cliente  
 O .NET Framework Client Profile é um subconjunto do .NET Framework completo. Se você precisar usar somente os recursos de cliente no .NET Framework e você deseja fornecer uma experiência mais rápida implantação possíveis para sua solução do Office, você pode direcionar o .NET Framework Client Profile. Para obter mais informações, consulte [perfil de cliente do .NET Framework](/dotnet/framework/deployment/client-profile).  
  
 Quando você cria um projeto do Office, que tem como destino o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], o [!INCLUDE[net_client_v40_long](../vsto/includes/net-client-v40-long-md.md)] é afetado por padrão. Se você quiser desenvolver para o completo [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)], você deve definir essa opção após o projeto é criado. Para obter mais informações, consulte [Como direcionar a uma versão do .NET Framework](../ide/how-to-target-a-version-of-the-dotnet-framework.md).  
  
## <a name="create-solutions-for-the-64-bit-edition-of-microsoft-office"></a>Criar soluções para a edição de 64 bits do Microsoft Office  
 Microsoft Office está disponível nas edições de 64 bits e 32 bits. Para criar soluções do Office que podem ser executados em qualquer edição, a configuração de destino de plataforma para seu projeto deve ser definida como **qualquer CPU**. Esse é o valor padrão para projetos do Office. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
 Há versões de 64 bits e 32 bits separadas do [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] que são usados com as edições de 64 bits e 32 bits do Microsoft Office. Para obter mais informações, consulte [Visual Studio Tools for Office runtime overview](../vsto/visual-studio-tools-for-office-runtime-overview.md).  
  
## <a name="assemblies-in-office-solutions"></a>Assemblies em soluções do Office  
 Quando você cria um projeto do Office usando as ferramentas de desenvolvimento do Office no Visual Studio, o código que você escreve, eventualmente, é compilado em um assembly. O assembly é implantado em um servidor compartilhado ou em um diretório no computador cliente.  
  
 Assemblies em soluções do Office são carregados por um aplicativo do Office. Depois que o assembly é carregado, o código no assembly pode responder a eventos que são gerados no aplicativo, por exemplo, quando um usuário clica em um item de menu. O código no assembly também pode chamar o modelo de objeto para automatizar e estender o aplicativo e ele pode usar qualquer uma das classes no [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)]. Para obter mais informações, consulte [arquitetura de personalizações no nível do documento](../vsto/architecture-of-document-level-customizations.md) e [arquitetura do VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md).  
  
 Soluções do Office usam manifestos de aplicativo e manifestos de implantação para identificar o assembly. Os manifestos contêm informações sobre nome do assembly, versão e local, para que o aplicativo pode localizar, vincular e executar o assembly correto. Para obter mais informações, consulte [manifestos do aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md).  
  
 Projetos de nível de documento incluem um documento, além de um assembly. O documento atua como o front-end do aplicativo e é onde ocorre toda a interação de usuário. Cada documento pode ter apenas um assembly de projeto principal associado a ele; No entanto, vários documentos podem apontar para o mesmo assembly.  
  
 Assemblies em projetos de nível de documento não são inseridos no documento. em vez disso, eles são armazenados em outro lugar e são identificados pelo manifesto de aplicativo do documento.  
  
## <a name="security-considerations-for-assemblies"></a>Considerações de segurança para assemblies  
 Para uma solução do Office ser executado em um computador, os assemblies usados pela solução devem ser confiáveis para executar. Para obter mais informações sobre a segurança, consulte [soluções do Office Secure](../vsto/securing-office-solutions.md).  
  
 Por padrão, o assembly da solução e todos os assemblies referenciados que estão na pasta de saída do projeto são confiáveis para execução no computador de desenvolvimento quando você compila o projeto. Para obter mais informações, consulte [soluções do Office compilar](../vsto/building-office-solutions.md).  
  
 Por motivos de segurança, é melhor criar projetos em seu computador local, em vez de desenvolver em um local compartilhado. Para obter mais informações, consulte [desenvolvimento colaborativo de soluções do Office](../vsto/collaborative-development-of-office-solutions.md).  
  
## <a name="referenced-assemblies"></a>Assemblies referenciados  
 O assembly pode referenciar outros assemblies, que são listados nas referências do projeto. No entanto, um assembly de projeto de nível de documento não pode referenciar outro assembly de projeto de nível de documento.  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de modelos de projeto do Office](../vsto/office-project-templates-overview.md)   
 [Como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)   
 [Projetos do Office no ambiente do Visual Studio](../vsto/office-projects-in-the-visual-studio-environment.md)   
 [Propriedades em projetos do Office](../vsto/properties-in-office-projects.md)   
 [Executar soluções em diferentes versões do Microsoft Office](../vsto/running-solutions-in-different-versions-of-microsoft-office.md)   
 [Como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md)   
 [Manifestos de aplicativo e implantação em soluções do Office](../vsto/application-and-deployment-manifests-in-office-solutions.md)   
 [Como: configurar informações de configuração para uma solução do Office](../vsto/how-to-set-up-configuration-information-for-an-office-solution.md)   
 [Usar a funcionalidade do Office no Visual Studio](../vsto/using-office-functionality-inside-of-visual-studio.md)   
 [Implantar uma solução do Office](../vsto/deploying-an-office-solution.md)   
 [Tarefas comuns na programação do Office](../vsto/common-tasks-in-office-programming.md)   
 [Desenvolver soluções do Office](../vsto/developing-office-solutions.md)   
 [Arquitetura de soluções do Office no Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)  
  
  