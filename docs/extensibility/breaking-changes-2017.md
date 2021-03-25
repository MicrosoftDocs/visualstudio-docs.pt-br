---
title: Alterações recentes na extensibilidade do Visual Studio 2017
description: Saiba mais sobre os detalhes técnicos de alterações significativas feitas no modelo de extensibilidade no Visual Studio 2017 e o que você pode fazer para solucioná-los.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 54d5af60-0b44-4ae1-aa57-45aa03f89f3d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c07d48eb63c727701c3b6fcde9d405f9c96abec1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105068187"
---
# <a name="changes-in-visual-studio-2017-extensibility"></a>Alterações na extensibilidade do Visual Studio 2017

O Visual Studio 2017 fornece uma [experiência de instalação mais rápida e leve do Visual Studio](https://devblogs.microsoft.com/visualstudio/faster-leaner-visual-studio-installer) que reduz o impacto do Visual Studio em sistemas de usuário, oferecendo aos usuários mais opções sobre as cargas de trabalho e os recursos que estão instalados. Para dar suporte a esses aprimoramentos, fizemos alterações no modelo de extensibilidade, incluindo algumas alterações significativas. Este artigo descreve os detalhes técnicos dessas alterações e o que pode ser feito para solucioná-las.

> [!NOTE]
> Algumas informações são detalhes de implementação point-in-time e podem ser alteradas posteriormente.

## <a name="changes-affecting-vsix-format-and-installation"></a>Alterações que afetam o formato e a instalação do VSIX

O Visual Studio 2017 introduziu o formato VSIX v3 (versão 3) para dar suporte à experiência de instalação leve.

As alterações no formato VSIX incluem:

* Declaração de pré-requisitos de instalação. Para oferecer a promessa de um Visual Studio simples e de instalação rápida, o instalador agora oferece mais opções de configuração aos usuários. Como resultado, para garantir que os recursos e componentes exigidos por uma extensão estejam instalados, as extensões precisam declarar suas dependências.

  * O instalador do Visual Studio 2017 oferece automaticamente para adquirir e instalar os componentes necessários para o usuário como parte da instalação de sua extensão.
  * Os usuários também são avisados ao tentar instalar uma extensão que não foi criada usando o novo formato VSIX v3, mesmo que elas tenham sido marcadas em seu manifesto como tendo como destino a versão 15,0.

* Recursos aprimorados para o formato VSIX. Para oferecer em uma [instalação de baixo impacto](https://devblogs.microsoft.com/visualstudio/anatomy-of-a-low-impact-visual-studio-install) do Visual Studio que também dá suporte a instalações lado a lado, não salvamos mais a maioria dos dados de configuração no registro do sistema e movemos os assemblies específicos do Visual Studio do GAC. Também aumentamos os recursos do formato VSIX e do mecanismo de instalação do VSIX, permitindo que você o use em vez de um MSI ou EXE para instalar suas extensões para alguns tipos de instalação.

Os novos recursos incluem:

* Registro na instância especificada do Visual Studio.
* Instalação fora da [pasta extensões](set-install-root.md).
* Detecção de arquitetura do processador.
* Dependência de pacotes de idiomas separados por linguagem.
* Instalação com [suporte a NGen](ngen-support.md).

## <a name="build-an-extension-for-visual-studio-2017"></a>Criar uma extensão para o Visual Studio 2017

As ferramentas de designer para a criação do novo formato de manifesto do VSIX v3 estão disponíveis no Visual Studio 2017. Consulte o documento que acompanha [como migrar projetos de extensibilidade para o Visual Studio 2017](how-to-migrate-extensibility-projects-to-visual-studio-2017.md) para obter detalhes sobre como usar as ferramentas de designer ou fazer atualizações manuais para o projeto e o manifesto para desenvolver extensões VSIX v3.

## <a name="change-visual-studio-user-data-path"></a>Alteração: caminho de dados do usuário do Visual Studio

Anteriormente, apenas uma instalação de cada versão principal do Visual Studio poderia existir em cada computador. Para dar suporte a instalações lado a lado do Visual Studio 2017, vários caminhos de dados de usuário para o Visual Studio podem existir no computador do usuário.

O código em execução dentro do processo do Visual Studio deve ser atualizado para usar o Gerenciador de configurações do Visual Studio. O código em execução fora do processo do Visual Studio pode encontrar o caminho do usuário de uma instalação específica do Visual Studio [seguindo as orientações aqui](locating-visual-studio.md).

## <a name="change-global-assembly-cache-gac"></a>Alteração: cache de assembly global (GAC)

A maioria dos assemblies do Visual Studio Core não são mais instalados no GAC. As seguintes alterações foram feitas para que o código em execução no processo do Visual Studio ainda possa encontrar assemblies necessários em tempo de execução.

> [!NOTE]
> [INSTALLDIR] abaixo refere-se ao diretório raiz da instalação do Visual Studio. *VSIXInstaller.exe* preencherá isso automaticamente, mas para escrever código de implantação personalizado, leia [localizando o Visual Studio](locating-visual-studio.md).

* Assemblies que foram instalados apenas no GAC:

  Esses assemblies agora estão instalados em <em>[installdir] \Common7\IDE \* , * [installdir] \Common7\IDE\PublicAssemblies</em> ou *[installdir] \Common7\IDE\PrivateAssemblies*. Essas pastas fazem parte dos caminhos de investigação do processo do Visual Studio.

* Assemblies que foram instalados em um caminho sem investigação e no GAC:

  * A cópia no GAC foi removida da instalação.
  * Um arquivo *. pkgdef* foi adicionado para especificar uma entrada de base de código para o assembly.

    Por exemplo:

    ```
    [$RootKey$\RuntimeConfiguration\dependentAssembly\codeBase\{UniqueGUID}]
    "name"="AssemblyName" "codeBase"="$PackageFolder$\AssemblyName.dll"
    "publicKeyToken"="Public Key Token"
    "culture"="neutral"
    "version"=15.0.0.0
    ```

    Em tempo de execução, o subsistema pkgdef do Visual Studio mescla essas entradas no arquivo de configuração de tempo de execução do processo do Visual Studio (em *[VSAPPDATA] \devenv.exe.config*) como [`<codeBase>`](/dotnet/framework/configure-apps/file-schema/runtime/codebase-element) elementos. Essa é a maneira recomendada para permitir que o processo do Visual Studio Localize seu assembly, pois evita a pesquisa por meio de caminhos de investigação.

### <a name="reacting-to-this-breaking-change"></a>Reagindo a essa alteração significativa

* Se sua extensão estiver sendo executada dentro do processo do Visual Studio:

  * Seu código será capaz de encontrar assemblies do Visual Studio Core.
  * Considere usar um arquivo *. pkgdef* para especificar um caminho para seus assemblies, se necessário.

* Se sua extensão estiver sendo executada fora do processo do Visual Studio:

  Considere a possibilidade de procurar por assemblies do Visual Studio Core em <em>[installdir] \Common7\IDE \* , * [installdir] \Common7\IDE\PublicAssemblies</em> ou *[installdir] \Common7\IDE\PrivateAssemblies* usando o arquivo de configuração ou o resolvedor de assembly.

## <a name="change-reduce-registry-impact"></a>Alteração: reduzir o impacto no registro

### <a name="global-com-registration"></a>Registro COM global

* Anteriormente, o Visual Studio instalou várias chaves do registro no HKEY_CLASSES_ROOT e HKEY_LOCAL_MACHINE Hives para dar suporte ao registro COM nativo. Para eliminar esse impacto, o Visual Studio agora usa [a ativação sem registro para componentes com](/previous-versions/dotnet/articles/ms973913(v=msdn.10)).
* Como resultado, a maioria dos arquivos TLB/OLB/DLL em% ProgramFiles (x86)% \ Shared\MSEnv de Programas\microsoft comum não são mais instalados por padrão pelo Visual Studio. Esses arquivos agora estão instalados em [INSTALLDIR] com manifestos COM Registration-Free correspondentes usados pelo processo de host do Visual Studio.
* Como resultado, o código externo que depende do registro de COM global para interfaces COM do Visual Studio não encontrará mais esses registros. O código em execução dentro do processo do Visual Studio não verá uma diferença.

### <a name="visual-studio-registry"></a>Registro do Visual Studio

* Anteriormente, o Visual Studio instalou várias chaves do registro no **HKEY_LOCAL_MACHINE** do sistema e **HKEY_CURRENT_USER** Hives em uma chave específica do Visual Studio:

  * **HKLM\Software\Microsoft\VisualStudio \{ Version}**: chaves do registro criadas por instaladores msi e extensões por máquina.
  * **HKCU\Software\Microsoft\VisualStudio \{ Version}**: chaves do registro criadas pelo Visual Studio para armazenar configurações específicas do usuário.
  * **HKCU\Software\Microsoft\VisualStudio \{ Version} _Config**: uma cópia da chave do Visual Studio HKLM acima, mais as chaves do registro mescladas de arquivos *. pkgdef* por extensões.

* Para reduzir o impacto no registro, o Visual Studio agora usa a função [RegLoadAppKey](/windows/desktop/api/winreg/nf-winreg-regloadappkeya) para armazenar as chaves do registro em um arquivo binário privado em *[VSAPPDATA] \privateregistry.bin*. Apenas um número muito pequeno de chaves específicas do Visual Studio permanece no registro do sistema.
* O código existente em execução dentro do processo do Visual Studio não é afetado. O Visual Studio redirecionará todas as operações de registro sob a chave específica do Visual Studio do HKCU para o registro privado. A leitura e a gravação em outros locais do registro continuarão a usar o registro do sistema.
* O código externo precisará carregar e ler esse arquivo para entradas de registro do Visual Studio.

### <a name="react-to-this-breaking-change"></a>Reagir a essa alteração significativa

* O código externo deve ser convertido para usar Registration-Free ativação para componentes COM também.
* Os componentes externos podem encontrar o local do Visual Studio [seguindo as orientações aqui](https://devblogs.microsoft.com/setup/changes-to-visual-studio-15-setup).
* Recomendamos que os componentes externos usem o [Gerenciador de configurações externas](/dotnet/api/microsoft.visualstudio.settings.externalsettingsmanager) em vez de ler/gravar diretamente nas chaves do registro do Visual Studio.
* Verifique se os componentes que sua extensão está usando podem ter implementado outra técnica para o registro. Por exemplo, as extensões do depurador podem ser capazes de aproveitar o novo [registro de com do msvsmon JSON-File](migrate-debugger-COM-registration.md).