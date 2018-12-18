---
title: Alterações consideráveis na extensibilidade do Visual Studio 2017 | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1a7ed5322c131bd9f3b758b31169676865880fd7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49826486"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Alterações na extensibilidade do Visual Studio 2017

Com o Visual Studio 2017, estamos oferecendo uma [experiência de instalação mais rápida e leve do Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2016/04/01/faster-leaner-visual-studio-installer) que reduz o impacto do Visual Studio em sistemas de usuário, ao mesmo tempo, dando aos usuários maior preferência sobre os recursos e cargas de trabalho que são instalados. Para dar suporte a esses aprimoramentos, fez alterações para o modelo de extensibilidade e fez algumas alterações para extensibilidade do Visual Studio. Este documento descreve os detalhes técnicos dessas alterações e que pode ser feito para resolvê-los. Observe que algumas informações são detalhes de implementação de point-in-time e podem ser alteradas posteriormente.

## <a name="changes-affecting-vsix-format-and-installation"></a>Alterações que afetam a instalação e formato VSIX

Estamos introduzindo o VSIX v3 formato (versão 3) para dar suporte a experiência de instalação leve.

Alterações no formato VSIX incluem:

* Declaração de pré-requisitos de instalação. Para cumprir a promessa de uma leve, fast-instalação do Visual Studio, o instalador agora oferece mais opções de configuração para os usuários. Como resultado, para garantir que os recursos e componentes necessários para uma extensão estiverem instalados, serão necessário extensões declarar suas dependências.
  * O instalador do Visual Studio 2017 oferecerá automaticamente para adquirir e instalar os componentes necessários para o usuário como parte da instalação de sua extensão.
  * Os usuários também serão avisados ao tentar instalar uma extensão que não foi criada usando o novo formato VSIX v3, mesmo que elas tenham sido marcadas em seu manifesto como direcionamento de versão 15.0.
* Recursos avançados para o formato VSIX. Para fornecer um [instalação de baixo impacto](https://blogs.msdn.microsoft.com/visualstudio/2016/04/25/anatomy-of-a-low-impact-visual-studio-install) do Visual Studio que também dá suporte a instalações lado a lado, podemos não salvar a maioria dos dados de configuração no registro do sistema e foram movidos assemblies específicos do Visual Studio fora do GAC. Também aumentamos os recursos do formato VSIX e mecanismo de instalação de VSIX, permitindo que você usá-la em vez de um MSI ou EXE para instalar as extensões para alguns tipos de instalação.

  Os novos recursos incluem:

  * Registro para a instância especificada do Visual Studio.
  * Instalação fora do [pasta extensões](set-install-root.md).
  * Detecção da arquitetura do processador.
  * Dependência de pacotes de idiomas separados por idioma.
  * Instalação com [suporte para NGEN](ngen-support.md).

## <a name="building-an-extension-for-visual-studio-2017"></a>Criando uma extensão do Visual Studio 2017

Designer de ferramentas para a criação do novo formato de manifesto do VSIX v3 agora está disponível no Visual Studio 2017. Consulte o documento que acompanha este artigo [como: migrar projetos de extensibilidade para o Visual Studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md) para obter detalhes sobre como usar as ferramentas de designer ou fazer atualizações manuais ao projeto e o manifesto para desenvolver extensões do VSIX v3.

## <a name="change-visual-studio-user-data-path"></a>Alteração: Caminho de dados de usuário de Visual Studio

Anteriormente, apenas uma instalação de cada versão principal do Visual Studio pode existir em cada computador. Para dar suporte a instalações lado a lado do Visual Studio 2017, vários caminhos de dados de usuário para o Visual Studio podem existir no computador do usuário.

O código em execução dentro do processo do Visual Studio deve ser atualizado para usar o Gerenciador de configurações do Visual Studio. O código em execução fora do processo do Visual Studio pode encontrar o caminho do usuário de uma instalação específica do Visual Studio [seguindo as diretrizes aqui](locating-visual-studio.md).

## <a name="change-global-assembly-cache-gac"></a>Alteração: Cache de Assembly Global (GAC)

A maioria dos assemblies de núcleo do Visual Studio não são mais instalados no GAC. As seguintes alterações foram feitas para que o código em execução no processo do Visual Studio ainda pode encontrar os assemblies necessários no tempo de execução.

> [!NOTE]
> [INSTALLDIR] refere-se abaixo para o diretório raiz de instalação do Visual Studio. *VSIXInstaller.exe* preencher isso automaticamente, mas para escrever código de implantação personalizada, leia [localizando o Visual Studio](locating-visual-studio.md).

* Assemblies que só foram instalados no GAC:
  * Agora, esses assemblies são instalados sob <em>[INSTALLDIR] \Common7\IDE\*, * [INSTALLDIR] \Common7\IDE\PublicAssemblies</em> ou *\Common7\IDE\PrivateAssemblies [INSTALLDIR]*. Essas pastas são parte dos caminhos de investigação do processo do Visual Studio.

* Assemblies que foram instalados em um caminho de investigação não e no GAC:
  * A cópia no GAC foi removida da instalação.
  * Um *pkgdef* arquivo foi adicionado ao especificar uma entrada de base de código para o assembly.

    Por exemplo:

    ```xml
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```
    Em tempo de execução, o subsistema do Visual Studio pkgdef mesclará essas entradas no arquivo de configuração de tempo de execução do processo do Visual Studio (sob *[VSAPPDATA]\devenv.exe.config*) como [ `<codeBase>` ](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element) elementos. Essa é a maneira recomendada para permitir que o processo do Visual Studio encontrar o assembly, porque ele evita a pesquisa por meio de caminhos de investigação.

### <a name="reacting-to-this-breaking-change"></a>Reagir a essa alteração interruptiva

* Se sua extensão está em execução dentro do processo do Visual Studio:
  * Seu código será capaz de localizar assemblies de núcleo do Visual Studio.
  * Considere o uso de um *pkgdef* arquivo para especificar um caminho para os assemblies, se necessário.
* Se sua extensão está em execução fora do processo do Visual Studio:
  * Considere procurando assemblies de núcleo do Visual Studio sob <em>[INSTALLDIR] \Common7\IDE\*, * [INSTALLDIR] \Common7\IDE\PublicAssemblies</em> ou *[INSTALLDIR] \Common7\IDE\PrivateAssemblies*usando o resolvedor de assembly ou arquivo de configuração.

## <a name="change-reduce-registry-impact"></a>Alteração: Reduzir o impacto do registro

### <a name="global-com-registration"></a>Registro global de COM

* Anteriormente, o Visual Studio instalado várias chaves do registro para os hives HKEY_CLASSES_ROOT e HKEY_LOCAL_MACHINE para dar suporte ao registro de COM nativo. Para eliminar esse impacto, o Visual Studio agora usa [ativação sem registro para componentes COM](https://msdn.microsoft.com/library/ms973913.aspx).
* Como resultado, a maioria das cargas de TLB / OLB / arquivos DLL em % ProgramFiles (x86) %\Common Files\Microsoft Shared\MSEnv não são mais instalados por padrão pelo Visual Studio. Agora, esses arquivos são instalados sob [INSTALLDIR] com correspondentes manifestos COM sem registro usados pelo processo de host do Visual Studio.
* Como resultado, o código externo que se baseia no registro global de COM para interfaces COM do Visual Studio não encontrará esses registros. O código em execução dentro do processo do Visual Studio não verá uma diferença.

### <a name="visual-studio-registry"></a>Registro do Visual Studio

* Anteriormente, o Visual Studio instalado várias chaves do registro para o sistema **HKEY_LOCAL_MACHINE** e **HKEY_CURRENT_USER** hives sob uma chave específica do Visual Studio:
  * **HKLM\Software\Microsoft\VisualStudio\{versão}**: chaves do Registro criadas pelos instaladores MSI e extensões de por máquina.
  * **HKCU\Software\Microsoft\VisualStudio\{versão}**: chaves do Registro criadas pelo Visual Studio para armazenar configurações específicas do usuário.
  * **HKCU\Software\Microsoft\VisualStudio\{versão} _Config**: uma cópia da chave em HKLM do Visual Studio acima, além de chaves do registro mesclado de *pkgdef* arquivos pelas extensões.
* Para reduzir o impacto sobre o registro, o Visual Studio agora usa o [RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya) função para armazenar as chaves do registro em um arquivo binário privado sob *[VSAPPDATA]\privateregistry.bin*. Somente um número muito pequeno de chaves específicas do Visual Studio permanecem no registro do sistema.

* O código existente em execução dentro do processo do Visual Studio não é afetado. Visual Studio redirecionará todas as operações de registro na chave específicas do HKCU Visual Studio para o registro privado. Lendo e gravando em outros locais do registro continuarão a usar o registro do sistema.
* Código externo será necessário carregar e ler esse arquivo para entradas de registro do Visual Studio.

### <a name="reacting-to-this-breaking-change"></a>Reagir a essa alteração interruptiva

* Código externo deve ser convertido para usar a ativação sem registro para componentes COM também.
* Componentes externos podem encontrar o local do Visual Studio [seguindo as diretrizes aqui](https://blogs.msdn.microsoft.com/heaths/2016/09/15/changes-to-visual-studio-15-setup).
* É recomendável que componentes externos usam a [Gerenciador de configurações externas](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager) em vez de ler/gravar diretamente para chaves de registro do Visual Studio.
* Verifique se os componentes de que sua extensão está usando podem ter implementado outra técnica para o registro. Por exemplo, as extensões do depurador podem ser capazes de tirar proveito dos novos [msvsmon registro do arquivo JSON COM](migrate-debugger-COM-registration.md).
