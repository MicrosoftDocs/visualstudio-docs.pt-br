---
title: Como instalar um plug-in de controle do código-fonte | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3f88e4781115fa7a5fac54826304ab32472eeefb
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905364"
---
# <a name="how-to-install-a-source-control-plug-in"></a>Como instalar um plug-in de controle do código-fonte
A criação de um plug-in de controle de origem envolve três etapas:

1. Crie uma DLL com as funções definidas na seção referência da API de plug-in de controle do código-fonte desta documentação.

2. Implemente as funções definidas pela API de plug-in de controle do código-fonte. Quando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] chamadas para ela, torne interfaces e caixas de diálogo disponíveis do plug-in.

3. Registre a DLL fazendo entradas de registro apropriadas.

## <a name="integration-with-visual-studio"></a>Integração com o Visual Studio
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]dá suporte a plug-ins de controle do código-fonte que estão em conformidade com a API de plug-in de controle do código

### <a name="register-the-source-control-plug-in"></a>Registrar o plug-in de controle do código-fonte
 Antes que um IDE (ambiente de desenvolvimento integrado) em execução possa chamar o sistema de controle do código-fonte, primeiro ele deve localizar a DLL de plug-in de controle do código-fonte que exporta a API.

#### <a name="to-register-the-source-control-plug-in-dll"></a>Para registrar a DLL de plug-in de controle do código-fonte

1. Adicione duas entradas sob a chave de **HKEY_LOCAL_MACHINE** na subchave de **software** que especifica a subchave de nome da empresa seguida pela subchave de nome do produto. O padrão é **HKEY_LOCAL_MACHINE \\ \<company name> \\ \<product name> \\ \<entry> **  =  *valor*\Software. As duas entradas são sempre chamadas **SCCServerName** e **SCCServerPath**. Cada uma é uma cadeia de caracteres regular.

    Por exemplo, se o nome da sua empresa for a Microsoft e seu produto de controle do código-fonte for chamado de SourceSafe, esse caminho do registro será **HKEY_LOCAL_MACHINE \software\microsoft\sourcesafe**. Nessa subchave, a primeira entrada, **SCCServerName**, é uma cadeia de caracteres legível pelo usuário que nomeia seu produto. A segunda entrada, **SCCServerPath**, é o caminho completo para a DLL de plug-in de controle do código-fonte à qual o IDE deve se conectar. O seguinte fornece exemplos de entradas do registro:

   |Entrada de registro de exemplo|Valor de exemplo|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|
   |HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\SCCServerPath|*c:\vss\win32\ssscc.dll*|

   > [!NOTE]
   > SCCServerPath é o caminho completo para o plug-in SourceSafe. Seu plug-in de controle do código-fonte usará nomes diferentes da empresa e do produto, mas os mesmos caminhos de entrada do registro.

2. As seguintes entradas de registro opcionais podem ser usadas para modificar o comportamento do seu plug-in de controle do código-fonte. Essas entradas entram na mesma subchave que **SccServerName** e **SccServerPath**.

   - A entrada **HideInVisualStudioregistry** pode ser usada se você não quiser que o plug-in de controle do código-fonte apareça na lista de **seleção de plug-in** de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Essa entrada também afetará a alternância automática para o plug-in de controle do código-fonte. Um possível uso dessa entrada é se você fornecer um pacote de controle do código-fonte que substitua seu plug-in de controle do código-fonte, mas você deseja tornar mais fácil para o usuário migrar do usando o plug-in de controle do código-fonte para o pacote de controle do código-fonte. Quando o pacote de controle do código-fonte é instalado, ele define essa entrada do registro, que oculta o plug-in.

      **HideInVisualStudio** é um valor DWORD e é definido como *1* para ocultar o plug-in ou *0* para mostrar o plug-in. Se a entrada do registro não for exibida, o comportamento padrão será mostrar o plug-in.

   - A entrada de registro **DisableSccManager** pode ser usada para desabilitar ou ocultar a opção de menu ** \<Source Control Server> Iniciar** que normalmente aparece no **File**  >  submenu**controle de origem** de arquivo. A seleção dessa opção de menu chama a função [SccRunScc](../../extensibility/sccrunscc-function.md) . O plug-in de controle do código-fonte pode não dar suporte a um programa externo e, portanto, talvez você queira desabilitar ou até mesmo ocultar a opção de menu **Iniciar** .

      **DisableSccManager** é um valor DWORD e é definido como *0* para habilitar a opção de menu **Iniciar \<Source Control Server> ** , defina como *1* para desabilitar a opção de menu e defina como *2* para ocultar a opção de menu. Se essa entrada de registro não for exibida, o comportamento padrão será mostrar a opção de menu.

   | Entrada de registro de exemplo | Valor de exemplo |
   | - |--------------|
   | HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio | 1 |
   | HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\SourceSafe\DisableSccManager | 1 |

3. Adicione a subchave, **SourceCodeControlProvider**, na chave **HKEY_LOCAL_MACHINE** na subchave **software** .

    Sob essa subchave, a entrada do registro **ProviderRegKey** é definida como uma cadeia de caracteres que representa a subchave que você colocou no registro na etapa 1. O padrão é **HKEY_LOCAL_MACHINE**  =  *software \software\sourcecodecontrolprovider\providerregkey \\<nome da empresa \> \\<nome \> do produto*.

    Veja a seguir o conteúdo de exemplo desta subchave.

   |Entrada de registro|Valor de exemplo|
   |--------------------|------------------|
   |HKEY_LOCAL_MACHINE \SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > O plug-in de controle do código-fonte usará a mesma subchave e nomes de entrada, mas o valor será diferente.

4. Crie uma subchave chamada **InstalledSCCProviders** na subchave **SourceCodeControlProvider** e coloque uma entrada nessa subchave.

    O nome dessa entrada é o nome legível pelo usuário do provedor (o mesmo que o valor especificado para a entrada SCCServerName) e o valor é, mais uma vez, a subchave criada na etapa 1. O padrão é **HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider\installedsccproviders \\<nome \> de exibição**  =  *software \\ \> \\ \><nome da empresa<* nome do produto.

    Por exemplo:

   |Entrada de registro de exemplo|Valor de exemplo|
   |---------------------------|------------------|
   |HKEY_LOCAL_MACHINE \SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|

   > [!NOTE]
   > Pode haver vários plug-ins de controle do código-fonte registrados dessa maneira. É assim que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] localiza todos os plug-ins baseados na API de plug-in de controle do código-fonte instalado.

## <a name="how-an-ide-locates-the-dll"></a>Como um IDE localiza a DLL
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE tem duas maneiras de localizar a DLL de plug-in de controle do código-fonte:

- Localize o plug-in de controle do código-fonte padrão e conecte-se a ele silenciosamente.

- Localiza todos os plug-ins de controle do código-fonte registrados, dos quais o usuário escolhe um.

  Para localizar a DLL da primeira forma, o IDE examina a subchave **HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider** para a entrada **ProviderRegKey**. O valor dessa entrada aponta para outra subchave. Em seguida, o IDE procura uma entrada chamada **SccServerPath** na segunda subchave em **HKEY_LOCAL_MACHINE**. O valor dessa entrada aponta o IDE para a DLL.

> [!NOTE]
> O IDE não carrega DLLs de caminhos relativos (por exemplo, *.\NewProvider.DLL*). Um caminho completo para a DLL deve ser especificado (por exemplo, *c:\Providers\NewProvider.DLL*). Isso reforça a segurança do IDE, impedindo o carregamento de DLLs de plug-in não autorizadas ou representadas.

 Para localizar a DLL da segunda maneira, o IDE examina a subchave **HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider\installedsccproviders** para todas as entradas. Cada entrada tem um nome e um valor. O IDE exibe uma lista desses nomes para o usuário. Quando o usuário escolhe um nome, o IDE localiza o valor para o nome selecionado que aponta para uma subchave. O IDE procura uma entrada chamada **SccServerPath** nessa subchave em **HKEY_LOCAL_MACHINE**. O valor dessa entrada aponta o IDE para a DLL correta.

 Um plug-in de controle do código-fonte precisa dar suporte a ambas as maneiras de localizar a DLL e, consequentemente, define **ProviderRegKey**, substituindo qualquer configuração anterior. Mais importante, ele deve se adicionar à lista de **InstalledSccProviders** para que o usuário possa ter a opção de qual plug-in de controle do código-fonte usar.

> [!NOTE]
> Como a chave de **HKEY_LOCAL_MACHINE** é usada, somente um plug-in de controle do código-fonte pode ser registrado como o plug-in de controle do código-fonte padrão em um determinado computador (no entanto, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] permite que os usuários determinem qual plug-in de controle do código-fonte eles desejam realmente usar para uma solução específica). Durante o processo de instalação, verifique se um plug-in de controle do código-fonte já está definido; Nesse caso, pergunte ao usuário se deseja ou não definir o novo plug-in de controle do código-fonte que está sendo instalado como o padrão. Durante a desinstalação, não remova outras subchaves do registro que são comuns a todos os plug-ins de controle do código-fonte em **HKEY_LOCAL_MACHINE \software\sourcecodecontrolprovider**; Remova apenas sua subchave SCC específica.

## <a name="how-the-ide-detects-version-1213-support"></a>Como o IDE detecta o suporte à versão 1.2/1.3
 Como o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] detecta se um plug-in dá suporte à funcionalidade de API de plug-in de controle de origem versão 1,2 e 1,3? Para declarar a funcionalidade avançada, o plug-in de controle do código-fonte deve implementar a função correspondente:

 Primeiro, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] verifica o valor retornado chamando o [SccGetVersion](../../extensibility/sccgetversion-function.md). Ele deve ser maior ou igual a 1,2.

 Em seguida, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] determina se a nova funcionalidade específica tem suporte examinando o `lpSccCaps` argumento no [SccInitialize](../../extensibility/sccinitialize-function.md).

 Se ambas as condições forem atendidas, as novas funções com suporte nas versões 1,2 e 1,3 poderão ser chamadas.

## <a name="see-also"></a>Confira também
- [Introdução aos plug-ins de controle do código-fonte](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)
