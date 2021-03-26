---
title: Suporte para configurações de usuário | Microsoft Docs
description: Saiba como habilitar a persistência de categorias de configurações usando as APIs de configurações no SDK do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Custom Settings Points
- user settings [Visual Studio SDK], registering persistence support
- persistence, registering settings
ms.assetid: ad9beac3-4f8d-4093-ad0e-6fb00444a709
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e0128ce1f27674010d1b624457815ddb1016e016
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080639"
---
# <a name="support-for-user-settings"></a>Suporte para configurações de usuário
Um VSPackage pode definir uma ou mais categorias de configurações, que são grupos de variáveis de estado que persistem quando um usuário escolhe o comando **configurações de importação/exportação** no menu **ferramentas** . Para habilitar essa persistência, use as APIs de configurações no [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] .

 Uma entrada de registro que é conhecida como um ponto de configurações personalizado e um GUID define a categoria de configurações de um VSPackage. Um VSPackage pode dar suporte a várias categorias de configurações, cada uma definida por um ponto de configurações personalizado.

- Implementações de configurações baseadas em assemblies de interoperabilidade (usando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings> interface) devem criar um ponto de configurações personalizado editando o registro ou usando um script de registrador (arquivo. rgs). Para obter mais informações, consulte [Criando scripts de registrador](/cpp/atl/creating-registrar-scripts).

- O código que usa a MPF (estrutura de pacote gerenciada) deve criar pontos de configuração personalizados anexando um <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> ao VSPackage para cada ponto de configurações personalizado.

     Se um único VSPackage der suporte a vários pontos de configurações personalizados, cada ponto de configurações personalizado é implementado por uma classe separada e cada um é registrado por uma instância exclusiva da <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> classe. Consequentemente, uma classe de implementação de configurações pode dar suporte a mais de uma categoria de configurações.

## <a name="custom-settings-point-registry-entry-details"></a>Detalhes da entrada do registro do ponto de configurações personalizadas
 Os pontos de configuração personalizados são criados em uma entrada de registro no seguinte local: HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \UserSettings \\ `<CSPName>` , em que `<CSPName>` é o nome do ponto de configurações personalizado ao qual o VSPackage dá suporte e *\<Version>* é a versão do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , por exemplo, 8,0.

> [!NOTE]
> O caminho raiz de HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\ *\<Version>* pode ser substituído por uma raiz alternativa quando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (ambiente de desenvolvimento integrado) é inicializado. Para obter mais informações, consulte [Opções de linha de comando](../../extensibility/command-line-switches-visual-studio-sdk.md).

 A estrutura da entrada do registro está ilustrada abaixo:

 HKLM\Software\Microsoft\VisualStudio \\ *\<Version>* \UserSettings\

 `<CSPName`>= s ' #12345 '

 Package = ' {XXXXXX XXXX XXXX XXXX XXXXXXXXX} '

 Category = ' {YYYYYY YYYY YYYY YYYY YYYYYYYYY} '

 ResourcePackage = ' {ZZZZZZ ZZZZ ZZZZ ZZZZ ZZZZZZZZZ} '

 AlternateParent = CategoryName

| Nome | Type | Dados | Descrição |
|-----------------|--------| - | - |
| (Padrão) | REG_SZ | Nome do ponto de configurações personalizado | O nome da chave, `<CSPName`>, é o nome não local do ponto de configurações personalizado.<br /><br /> Para implementações baseadas no MPF, o nome da chave é obtido pela combinação `categoryName` dos `objectName` argumentos e do <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> Construtor no `categoryName_objectName` .<br /><br /> A chave pode estar vazia ou pode conter a ID de referência para a cadeia de caracteres localizada em uma DLL satélite. Esse valor é obtido do `objectNameResourceID` argumento para o <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> Construtor. |
| Pacote | REG_SZ | GUID | O GUID do VSPackage que implementa o ponto de configurações personalizado.<br /><br /> Implementações baseadas no MPF usando a <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> classe, use o argumento do construtor `objectType` que contém o VSPackage <xref:System.Type> e a reflexão para obter esse valor. |
| Categoria | REG_SZ | GUID | GUID que identifica a categoria de configurações.<br /><br /> Para implementações baseadas em assemblies de interoperabilidade, esse valor pode ser um GUID escolhido arbitrariamente, que o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE passa para os <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ExportSettings%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUserSettings.ImportSettings%2A> métodos e. Todas as implementações desses dois métodos devem verificar seus argumentos GUID.<br /><br /> Para implementações baseadas no MPF, esse GUID é obtido pelo <xref:System.Type> da classe que implementa o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] mecanismo de configurações. |
| ResourcePackage | REG_SZ | GUID | Opcional.<br /><br /> Caminho para a DLL satélite que contém cadeias de caracteres localizadas se o VSPackage de implementação não os fornecer.<br /><br /> O MPF usa a reflexão para obter o recurso correto VSPackage, portanto, a <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> classe não define esse argumento. |
| AlternateParent | REG_SZ | Nome da pasta na página opções de ferramentas que contém este ponto de configurações personalizado. | Opcional.<br /><br /> Você deve definir esse valor somente se uma implementação de configurações oferecer suporte a páginas de **Opções de ferramentas** que usam o mecanismo de persistência no [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] em vez do mecanismo no modelo de automação para salvar o estado.<br /><br /> Nesses casos, o valor na chave AlternateParent é a `topic` seção da `topic.sub-topic` cadeia de caracteres usada para identificar a página **ferramentas** específicas. Por exemplo, para a página **ToolsOptions** , `"TextEditor.Basic"` o valor de AlternateParent seria `"TextEditor"` .<br /><br /> Quando <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> o gera o ponto de configurações personalizadas, ele é o mesmo que o nome da categoria. |
