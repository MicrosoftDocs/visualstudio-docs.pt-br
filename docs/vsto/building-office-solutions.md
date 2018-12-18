---
title: Compilar soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- debugging [Office development in Visual Studio]
- debugging Office applications in Visual Studio
- solutions [Office development in Visual Studio], debugging
- Office applications [Office development in Visual Studio], debugging
- application development [Office development in Visual Studio], building
- Office applications [Office development in Visual Studio], building
- projects [Office development in Visual Studio], debugging
- Office solutions [Office development in Visual Studio], building
- solutions [Office development in Visual Studio], building
- Office projects [Office development in Visual Studio], debugging
- projects [Office development in Visual Studio], building
- builds [Office development in Visual Studio]
- Office projects [Office development in Visual Studio], building
- application development [Office development in Visual Studio], debugging
- Office solutions [Office development in Visual Studio], debugging
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 989014bb512ec77af908d823390b1e95b9a7872c
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248225"
---
# <a name="build-office-solutions"></a>Compilar soluções do Office
  Em geral, compilar e depurar projetos do Office é o mesmo que a compilação e depuração de outros tipos de projetos no Visual Studio, como o Windows Forms. Os tópicos nesta seção explicam as diferenças que existem. Para obter informações gerais sobre como criar aplicativos, consulte [compilar e criar no Visual Studio](/visualstudio/ide/compiling-and-building-in-visual-studio).  
  
> [!NOTE]  
>  Interessado em desenvolver soluções que estendem a experiência do Office em toda [várias plataformas](https://dev.office.com/add-in-availability)? Confira a nova [modelo de suplementos do Office](https://dev.office.com/docs/add-ins/overview/office-add-ins). Suplementos do Office têm uma superfície pequena em comparação com soluções e suplementos do VSTO, e você pode criá-los usando quase qualquer tecnologia, como HTML5, JavaScript, CSS3 e XML de programação da web.  
  
## <a name="project-output-for-office-projects"></a>Saída do projeto para projetos do Office  
 É o local de saída para projetos do Office *NomeDoProjeto*\bin\Release. ou *projectname*\bin\debug. Você não pode criar um diretório de implantação.  
  
### <a name="document-level-projects"></a>Projetos de nível de documento  
 Quando você compila um projeto de nível de documento, os itens a seguir estão incluídos na saída do projeto:  
  
-   Uma cópia do documento do projeto.  
  
-   O assembly do projeto e todos os assemblies referenciados que têm suas **Copy Local** propriedade definida como **verdadeiro**.  
  
-   O manifesto do aplicativo, que tem a extensão de nome de arquivo *. manifest*. Para obter mais informações, consulte [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
-   O manifesto de implantação, que tem a extensão de nome de arquivo *VSTO*. Para obter mais informações, consulte [manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md).  
  
-   Um banco de dados do programa (*PDB*) arquivos.  
  
> [!NOTE]  
>  Se você criar uma solução de nível de documento para um local remoto, em vez de no computador local, adicione o caminho totalmente qualificado para a lista de locais confiáveis na Central de confiabilidade do aplicativo. Para obter mais informações, consulte a seção chamada concedendo confiança a documentos nas [soluções do Office Secure](../vsto/securing-office-solutions.md).  
  
### <a name="application-level-projects"></a>Projetos de nível de aplicativo  
 Quando você compila um projeto de suplemento do VSTO, os itens a seguir estão incluídos na saída do projeto:  
  
- O assembly do projeto e todos os assemblies referenciados que têm suas **Copy Local** propriedade definida como **verdadeiro**.  
  
- O manifesto do aplicativo, que tem a extensão de nome de arquivo *. manifest*. Para obter mais informações, consulte [manifestos de aplicativo para soluções do Office](../vsto/application-manifests-for-office-solutions.md).  
  
- O manifesto de implantação, que tem a extensão de nome de arquivo *VSTO*. Para obter mais informações, consulte [manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md).  
  
- Um banco de dados do programa (*PDB*) o arquivo para o assembly do projeto.  
  
  O processo de compilação para projetos de suplemento do VSTO também cria um conjunto de entradas do registro no computador de desenvolvimento que são necessários para carregar o suplemento do VSTO. Para obter mais informações, consulte [entradas do registro para suplementos VSTO](../vsto/registry-entries-for-vsto-add-ins.md).  
  
  Se você criar um projeto de suplemento do VSTO do Outlook que contém regiões de formulário, o processo de build adiciona as seguintes informações adicionais para o registro:  
  
- Uma chave para cada classe de mensagem que está associado uma ou mais regiões de formulário.  
  
- Uma entrada para cada região do formulário e um valor associado que representa o nome do suplemento do VSTO do Outlook.  
  
  Outlook precisa dessas informações para carregar as regiões do formulário.  
  
## <a name="referenced-assemblies"></a>Assemblies referenciados  
 Você pode fazer referência a assemblies (incluindo projetos de biblioteca de classe) do seu projeto compilando soluções do Office. Cada assembly referenciado tem uma propriedade chamada **Copy Local**. **Local da cópia** indica se o assembly é copiado para o diretório de saída. Por padrão, ele é definido como **verdadeira**. Cada assembly referenciado que tenha **Copy Local** definido como **verdadeiro** é copiado para o diretório de saída.  
  
## <a name="security-during-the-build-process"></a>Segurança durante o processo de compilação  
 Visual Studio configura automaticamente as configurações de segurança no computador de desenvolvimento para conceder confiança à solução durante o processo de compilação. Isso permite que a solução seja executado enquanto você depurá-lo.  
  
 Projetos do Office usam certificados para verificar o Editor. Visual Studio automaticamente cria um certificado temporário para identificar soluções do Office e configura o computador de desenvolvimento para confiar no certificado temporário.  
  
 Para obter mais informações, consulte [soluções do Office Secure](../vsto/securing-office-solutions.md).  
  
### <a name="network-projects"></a>Projetos de rede  
 Se o local do assembly ou o documento estiver em um compartilhamento de rede, a atualização de política de segurança (nível de usuário) local não é suficiente para permitir que a solução seja executada. Um administrador deve conceder confiança total no nível do computador para assemblies e documentos que estão em um compartilhamento de rede antes da solução será executada. Para obter mais informações sobre como definir a política de segurança, consulte [soluções do Office Secure](../vsto/securing-office-solutions.md).  
  
 Para projetos de nível de documento, você também deve adicionar o local totalmente qualificado do documento à lista de pastas confiáveis do Office. Para obter mais informações, consulte [conceder confiança a documentos](../vsto/granting-trust-to-documents.md).  
  
## <a name="change-the-platform-target"></a>Alterar a plataforma de destino  
 Por padrão, é o destino da plataforma para projetos do Office **qualquer CPU**. Normalmente, você não deve alterar essa configuração. Soluções do Office que são criadas com o **qualquer CPU** configuração de execução em versões de 32 bits e 64 bits do Microsoft destino da plataforma [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] ou [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)].  
  
 Você deve definir o destino da plataforma x64 somente se você estiver criando uma solução que será executado apenas em versões de 64 bits do Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] ou [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)], e sua solução chama APIs nativas de 64 bits. Para obter mais informações sobre como alterar a configuração de destino da plataforma, consulte [como: Configurar projetos para plataformas de destino](../ide/how-to-configure-projects-to-target-platforms.md).  
  
 Se você definir o destino da plataforma como x64, a solução não será executado em versões de 32 bits do Windows ou do Office. Plataforma de destino requer a solução seja executada em um processo de 64 bits x64.  
  
## <a name="use-the-clean-command"></a>Use o comando limpo  
 Para remover os arquivos de projeto de compilação do computador de desenvolvimento, você pode usar o **Clean** comando o **compilação** menu no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. O **Clean** comando exclui todos os arquivos no local de saída de compilação. Para projetos de nível de aplicativo, o **Clean** comando também remove as entradas do registro que são criadas pelo processo de compilação.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Depurar projetos do Office](../vsto/debugging-office-projects.md)|Apresenta os problemas envolvidos na depuração de projetos do Office.|  
|[Passo a passo: Criar a primeira personalização no nível de documento para Excel](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)|Demonstra como criar uma personalização básica de nível de documento para Excel.|  
|[Como: Reabilitar um suplemento VSTO que tenha sido desabilitado](../vsto/how-to-re-enable-a-vsto-add-in-that-has-been-disabled.md)|Descreve como reabilitar um suplemento VSTO que foi desabilitado rígida ou flexível.|  
|[Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)|Fornece links para informações sobre como criar soluções do Office e sobre a função de assemblies em sua solução.|  
  
  