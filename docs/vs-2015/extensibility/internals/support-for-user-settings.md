---
title: Suporte para configurações do usuário | Microsoft Docs
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
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
caps.latest.revision: 27
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 445f95b1c52b5ada41918cf0f7d8120d912c209f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51759898"
---
# <a name="support-for-user-settings"></a>Suporte para configurações de usuário
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um VSPackage pode definir uma ou mais categorias de configurações, que são grupos de variáveis de estado que persiste quando um usuário escolhe o **configurações de importação/exportação** comando as **ferramentas** menu. Para habilitar essa persistência, você use as APIs de configurações no [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)].  
  
 Uma entrada de registro que é conhecida como um ponto de configurações personalizado e um GUID define a categoria de configurações do VSPackage. Um VSPackage pode dar suporte a várias categorias de configurações, definidos por um ponto de configurações personalizado.  
  
-   Implementações de configurações que se baseiam em assemblies de interoperabilidade (usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings> interface) deve criar o ponto de configurações personalizado editando o registro ou usando um script de registrador (arquivo. rgs). Para obter mais informações, consulte [criação de Scripts do registrador](http://msdn.microsoft.com/library/cbd5024b-8061-4a71-be65-7fee90374a35).  
  
-   Código que usa a estrutura de pacote gerenciado (MPF) deve criar pontos de configurações personalizadas, anexando um <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> o VSPackage para cada ponto de configurações personalizadas.  
  
     Se um único VSPackage dá suporte a vários pontos de configurações personalizadas, cada ponto de configurações personalizado é implementado por uma classe separada e cada um é registrado por uma instância exclusiva do <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> classe. Consequentemente, as configurações de implementação de classe podem dar suporte a mais de uma categoria de configurações.  
  
## <a name="custom-settings-point-registry-entry-details"></a>Detalhes da entrada do registro do ponto de configurações personalizadas  
 Pontos de configurações personalizadas são criados em uma entrada de registro no seguinte local: HKLM\Software\Microsoft\VisualStudio\\*\<versão >* \UserSettings\\`<CSPName>`, onde `<CSPName>` é o nome do ponto de configurações personalizado suporta o VSPackage e  *\<versão >* é a versão do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], por exemplo 8.0.  
  
> [!NOTE]
>  O caminho raiz do HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*\<versão >* pode ser substituído por uma alternativa raiz quando o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é o ambiente de desenvolvimento integrado (IDE) inicializado. Para obter mais informações, consulte [opções de linha de comando](../../extensibility/command-line-switches-visual-studio-sdk.md).  
  
 A estrutura da entrada do registro é ilustrada abaixo:  
  
 HKLM\Software\Microsoft\VisualStudio\\*\<versão >* \UserSettings\  
  
 `<CSPName`> = s '#12345'  
  
 Pacote = '{XXXX XXXXXX XXXX XXXX XXXXXXXXX}'  
  
 Categoria = '{aaaa AAAAAA YYYY YYYY YYYYYYYYY}'  
  
 ResourcePackage = '{ZZZZZZ ZZZZ ZZZZ ZZZZ ZZZZZZZZZ}'  
  
 AlternateParent = CategoryName  
  
|Nome|Tipo|Dados|Descrição|  
|----------|----------|----------|-----------------|  
|(Padrão)|REG_SZ|Nome do ponto de configurações personalizadas|O nome da chave, `<CSPName`>, é o nome não localizado do ponto de configurações personalizado.<br /><br /> Para implementações baseadas em MPF, o nome da chave é obtido pela combinação de `categoryName` e `objectName` argumentos do <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> construtor em `categoryName_objectName`.<br /><br /> A chave pode ser vazia ou pode conter a ID de referência para a cadeia de caracteres localizada em uma DLL satélite. Esse valor é obtido o `objectNameResourceID` argumento para o <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> construtor.|  
|Pacote|REG_SZ|GUID|O GUID do VSPackage que implementa o ponto de configurações personalizadas.<br /><br /> Implementações com base em MPF usando o <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> da classe, use o construtor `objectType` argumento que contém o VSPackage <xref:System.Type> e reflexão para obter esse valor.|  
|Categoria|REG_SZ|GUID|GUID que identifica a categoria de configurações.<br /><br /> Para implementações com base em assemblies de interoperabilidade, esse valor pode ser arbitrariamente escolhido GUID, que o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE passa para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A> e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A> métodos. Todas as implementações desses dois métodos devem verificar seus argumentos GUID.<br /><br /> Para implementações com base em MPF, esse GUID é obtido pela <xref:System.Type> da classe que implementa o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] mecanismo de configurações.|  
|ResourcePackage|REG_SZ|GUID|Opcional.<br /><br /> Caminho para a DLL que contém de satélite localizado cadeias de caracteres se o VSPackage implementação não fornecê-los.<br /><br /> MPF usa a reflexão para obter o recurso correto VSPackage, portanto, o <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> classe não define este argumento.|  
|AlternateParent|REG_SZ|Nome da pasta na página de opções de ferramentas que contém esse ponto de configurações personalizado.|Opcional.<br /><br /> Você deve definir esse valor somente se dá suporte a uma implementação de configurações **opções de ferramentas** páginas que usam o mecanismo de persistência no [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] em vez do mecanismo no modelo de automação para salvar o estado.<br /><br /> Nesses casos, o valor na chave AlternateParent é o `topic` seção o `topic.sub-topic` cadeia de caracteres usada para identificar determinado **ToolsOptions** página. Por exemplo, para o **ToolsOptions** página `"TextEditor.Basic"` o valor de AlternateParent seria `"TextEditor"`.<br /><br /> Quando <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> gera as configurações de ponto personalizado, ele é o mesmo que o nome da categoria.|

