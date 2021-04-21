---
title: Usar parâmetros de linha de comando para instalar o Visual Studio
titleSuffix: ''
description: Saiba como usar parâmetros de linha de comando para controlar ou personalizar sua instalação do Visual Studio.
ms.date: 4/16/2021
ms.custom: seodec18
ms.topic: conceptual
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 23c83611e7663d35b229517f1e0224eb4ae7bb57
ms.sourcegitcommit: 367a2d9df789aa617abaa09b0cd0a18db7357d0c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107800814"
---
# <a name="use-command-line-parameters-to-install-visual-studio"></a>Usar parâmetros de linha de comando para instalar o Visual Studio

Ao instalar o Visual Studio programaticamente ou em um prompt de comando, você pode usar uma variedade de parâmetros de linha de comando para controlar ou personalizar a instalação para executar as seguintes ações:

- Inicie a instalação no cliente com determinadas opções e comportamentos preselecionados.
- Automatizar o processo de instalação.
- Crie ou mantenha um layout de rede dos arquivos do produto para instalar ou atualizar computadores cliente.

As opções de linha de comando podem ser usadas com o bootstrapper de instalação, que é o arquivo pequeno (~ 1 MB) que inicia o processo de download ou o pacote de atualização do administrador, que é implantado no [catálogo Microsoft Update](https://catalog.update.microsoft.com). 

::: moniker range="vs-2017"

Para obter o bootstrapper para o Visual Studio 2017 versão 15,9, vá para a página [**versões anteriores do Visual Studio**](https://visualstudio.microsoft.com/vs/older-downloads/) e baixe um dos seguintes arquivos bootstrapper:

| Edition | Nome de arquivo |
|-------------|-----------------------|
|Visual Studio Enterprise 2017 versão 15,9 | vs_enterprise.exe |
|Visual Studio Professional 2017 versão 15,9 | vs_professional.exe |
|Ferramentas de Build do Visual Studio 2017 versão 15,9  | vs_buildtools.exe |

::: moniker-end

::: moniker range="vs-2019"

Você pode obter o bootstrapper do Visual Studio 2019 na [página de downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) ou na página de [versões do Visual Studio 2019](https://docs.microsoft.com/visualstudio/releases/2019/history#installing-an-earlier-release) para sua versão e edição escolhidas do Visual Studio. O arquivo de instalação--ou bootstrapper--corresponderá ou será semelhante a um dos seguintes:

| Edition                    | Arquivo                                                                    |
|----------------------------|-------------------------------------------------------------------------|
| Visual Studio 2019 Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019)     |
| Visual Studio 2019 Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019) |
| Ferramentas de Build do Visual Studio 2019   | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019)     |
| Visual Studio 2019 Community    | [vs_community.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2019)  |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>Se você tiver baixado um arquivo bootstrapper anteriormente e quiser verificar qual é a versão dele, veja como fazer isso. No Windows, abra o explorador de arquivos, clique com o botão direito do mouse no arquivo bootstrapper, escolha **Propriedades**, escolha a guia **detalhes** e, em seguida, exiba o número de **versão do produto** . Para corresponder esse número a uma versão do Visual Studio, consulte a página [números de compilação e datas de lançamento do Visual Studio](visual-studio-build-numbers-and-release-dates.md) .

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>Se você tiver baixado anteriormente um arquivo bootstrapper e quiser verificar sua versão, veja como fazer isso. No Windows, abra o explorador de arquivos, clique com o botão direito do mouse no arquivo bootstrapper, escolha **Propriedades**, escolha a guia **detalhes** e, em seguida, exiba o número de **versão do produto** . Para corresponder esse número a uma versão do Visual Studio, consulte a página de [versões do visual studio 2019](https://docs.microsoft.com/visualstudio/releases/2019/history) .

::: moniker-end

Você pode obter a atualização do administrador acessando o [catálogo Microsoft Update](https://catalog.update.microsoft.com), procurar a atualização que deseja instalar e pressionar o botão baixar. As atualizações do administrador presumem que o Visual Studio já está instalado no computador. A aplicação de atualizações do administrador não iniciará uma instalação totalmente nova.

## <a name="bootstrapper-commands-and-command-line-parameters"></a>Comandos de bootstrapper e parâmetros de linha de comando

Ao invocar o bootstrapper do Visual Studio programaticamente para instalar o produto ou para manter um layout, o primeiro parâmetro é o comando (o verbo) que descreve a operação a ser executada. Os parâmetros de linha de comando opcionais subsequentes, que são todos prefixados por dois traços (--), também definem como essa operação deve ocorrer. Todos os parâmetros de linha de comando do Visual Studio não diferenciam maiúsculas de minúsculas e exemplos adicionais podem ser encontrados na página [exemplos de parâmetro de linha de comando](command-line-parameter-examples.md) .

Exemplo de sintaxe: `vs_enterprise.exe [command] <optional parameters>...`

| **Comando** | **Descrição** |
| ----------------------- | --------------- |
| (blank) | O comando padrão instala o produto e é usado para todas as operações de manutenção de layout. |
| `modify` | Modifica um produto instalado. |
| `update` | Atualiza um produto instalado. |
| `repair` | Repara um produto instalado. |
| `uninstall` | Desinstala um produto instalado. |
| `export` | Exporta a seleção da instalação para um arquivo de configuração de instalação. **Observação**: só pode ser usado com vs_installer.exe. |


| **Parâmetros** | **Descrição** |
| ----------------------- | --------------- |
| `--installPath <dir>` | Para o comando de instalação padrão, esse parâmetro é **opcional** e descreve onde a instância será instalada no computador cliente. Para outros comandos como Update ou Modify, esse parâmetro é **necessário** e denota o diretório de instalação para a instância do para agir. |
| `--add <one or more workload or component IDs>` | **Opcional**: durante um comando install ou Modify, esse parâmetro repetível especifica uma ou mais cargas de trabalho ou IDs de componente a serem adicionadas. Os componentes obrigatórios do artefato são instalados, mas não os componentes recomendados ou opcionais. Você pode controlar os componentes adicionais usando os `--includeRecommended` parâmetros e/ou globalmente `--includeOptional` . Para incluir várias cargas de trabalho ou componentes, repita o comando `--add` (por exemplo, `--add Workload1 --add Workload2`). Para ter um controle mais refinado, você pode acrescentar `;includeRecommended` ou `;includeOptional` à ID (por exemplo, `--add Workload1;includeRecommended` ou `--add Workload2;includeRecommended;includeOptional`). Para saber mais, confira a página [IDs de carga de trabalho e de componente](workload-and-component-ids.md). |
| `--remove <one or more workload or component IDs>` | **Opcional**: durante um comando Modify, esse parâmetro repetível especifica uma ou mais cargas de trabalho ou IDs de componente a serem removidas. Ele complementa e se comporta de forma semelhante ao `--add` parâmetro. |
| `--addProductLang <language-locale>` | **Opcional**: durante um comando install ou Modify, esse parâmetro repetível especifica os pacotes de idiomas da interface do usuário que devem ser instalados com o produto. Se não estiver presente, a instalação usará o pacote de idiomas que corresponde à localidade da máquina. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--removeProductLang <language-locale>` | **Opcional**: durante um comando install ou Modify, esse parâmetro repetível determina os pacotes de idiomas da interface do usuário que devem ser removidos do produto.  Ele complementa e se comporta de forma semelhante ao `--addProductLang` parâmetro. |
| `--in <path>` | **Opcional**: o URI ou o caminho para um [arquivo de resposta](automated-installation-with-response-file.md) que pode conter definições de configuração. |
| `--all` | **Opcional**: durante um comando install ou Modify, esse parâmetro faz com que todas as cargas de trabalho e componentes do produto sejam instalados. |
| `--allWorkloads` | **Opcional**: durante um comando install ou Modify, esse parâmetro instala todas as cargas de trabalho e componentes, mas nenhum componente recomendado ou opcional. |
| `--includeRecommended` | **Opcional**: durante um comando install ou Modify, esse parâmetro inclui os componentes recomendados para todas as cargas de trabalho instaladas, mas não os componentes opcionais. As cargas de trabalho são especificadas com `--allWorkloads` ou `--add`. |
| `--includeOptional` | **Opcional**: durante um comando install ou Modify, esse parâmetro inclui os componentes opcionais para todas as cargas de trabalho instaladas, mas não os componentes recomendados. As cargas de trabalho são especificadas com `--allWorkloads` ou `--add`.  |
| `--quiet, -q` | **Opcional**: usado com qualquer comando, esse parâmetro impede que qualquer interface do usuário seja exibida enquanto o comando está sendo executado. |
| `--passive, -p` | **Opcional**: esse parâmetro faz com que a interface do usuário seja exibida de maneira não interativa. Esse parâmetro é mutuamente exclusivo de (e, na verdade, substitui) o `--quiet` parâmetro.  |
| `--norestart` | **Opcional**: esse parâmetro deve ser emparelhado com os `--passive` parâmetros ou `--quiet` .  Durante um comando install, Update ou Modify, a adição do `--norestart` parâmetro atrasará qualquer reinicialização necessária. |
| `--force` | **Opcional**: esse parâmetro força o Visual Studio a fechar mesmo que algum processo do Visual Studio esteja em uso. |
| `--installWhileDownloading` | **Opcional**: durante um comando install, Update ou Modify, esse parâmetro permite que o Visual Studio Baixe e instale o produto em paralelo. É a experiência padrão. |
| `--downloadThenInstall` | **Opcional**: durante um comando install, Update ou Modify, esse parâmetro força o Visual Studio a baixar todos os arquivos antes de instalá-los. É mutuamente exclusivo do `--installWhileDownloading` parâmetro. |
| `--nickname <name>` | **Opcional**: durante um comando de instalação, esse parâmetro define o apelido a ser atribuído a um produto instalado. O apelido não pode ter mais de 10 caracteres.  |
| `--productKey` | **Opcional**: durante um comando de instalação, esse parâmetro define a chave do produto a ser usada para um produto instalado. Ele é composto por 25 caracteres alfanuméricos no formato `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx` ou `xxxxxxxxxxxxxxxxxxxxxxxxx` . |
| `--help, --?, -h, -?` | Exibe uma versão offline desta página. |
| `--config <path>` | **Opcional**: durante uma operação de instalação ou modificação, isso determina as cargas de trabalho e os componentes a serem adicionados com base em um arquivo de configuração de instalação salvo anteriormente. Essa operação é aditiva e não removerá nenhuma carga de trabalho ou componente se elas não estiverem presentes no arquivo. Além disso, os itens que não se aplicam ao produto não serão adicionados. Durante uma operação de exportação, isso determina a localização para salvar o arquivo de configuração de instalação. |


> [!IMPORTANT]
> Ao especificar várias cargas de trabalho ou componentes ou linguagens distintos, você deve repetir a `--add` `--remove` opção de linha de comando ou para cada item.

## <a name="layout-command-and-command-line-parameters"></a>Comando de layout e parâmetros de linha de comando
Todas as operações de gerenciamento de layout pressupõem que o comando é a instalação padrão que está (em branco). Portanto, todas as operações de gerenciamento de layout devem começar com o parâmetro inicial necessário `--layout` .  A tabela a seguir descreve os outros parâmetros que você pode usar para criar ou atualizar um layout usando a linha de comando.

| **Parâmetros de layout** | **Descrição** |
| ----------------------- | --------------- |
| `--layout <dir>` | Especifica um diretório para criar ou atualizar um cache de instalação offline. Para obter mais informações, consulte [Criar uma instalação baseada em rede do Visual Studio](create-a-network-installation-of-visual-studio.md).|
| `--lang <one or more language-locales>` | **Opcional**: usado com `--layout` para preparar um cache de instalação offline com pacotes de recursos com idiomas especificados. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--add <one or more workload or component IDs>` | **Opcional**: uma ou mais IDs de carga de trabalho ou de componente a serem adicionadas. Os componentes obrigatórios do artefato são instalados, mas não os componentes recomendados ou opcionais. Você pode controlar os componentes adicionais globalmente usando `--includeRecommended` e/ou `--includeOptional`. Para ter um controle mais refinado, você pode acrescentar `;includeRecommended` ou `;includeOptional` à ID (por exemplo, `--add Workload1;includeRecommended` ou `--add Workload2;includeOptional`). Para saber mais, confira a página [IDs de carga de trabalho e de componente](workload-and-component-ids.md). <br/>**Observação**: se `--add` for usado, somente as cargas de trabalho especificadas e os componentes e suas dependências serão baixados. Se `--add` não for especificado, todas as cargas de trabalho e componentes serão baixados para o layout.|
| `--includeRecommended` | **Opcional**: inclui os componentes recomendados para todas as cargas de trabalho que estão instaladas, mas não os componentes opcionais. As cargas de trabalho são especificadas com `--allWorkloads` ou `--add`. |
| `--includeOptional` | **Opcional**: inclui os componentes recomendados *e* opcionais para quaisquer cargas de trabalho incluídas no layout. As cargas de trabalho são especificadas com `--add`.  |
| `--keepLayoutVersion` | **Opcional**: aplicar alterações ao layout sem Atualizar a versão do layout. |
| `--verify` | **Opcional**: Verifique o conteúdo de um layout. Todos os arquivos corrompidos ou ausentes são listados. |
| `--fix` | **Opcional**: Verifique o conteúdo de um layout.  Se algum arquivo estiver corrompido ou ausente, ele será baixado novamente. Para corrigir um layout, é necessário acesso à Internet. |
| `--clean <one or more paths to catalogs>` | **Opcional**: remove versões antigas de componentes de um layout que foi atualizado para uma versão mais recente. |

| **Parâmetros de layout avançados** | **Descrição** |
| ----------------------- | --------------- |
| `--channelId <id>` | **Opcional**: a ID do canal para a instância a ser instalada. Isso é necessário para o comando de instalação e ignorado para outros comandos, se `--installPath` for especificado. |
| `--channelUri <uri>` | **Opcional**: o URI do manifesto do canal. Se as atualizações não forem desejadas, `--channelUri` o poderá apontar para um arquivo não existente (por exemplo,--channelUri C:\doesntExist.chman). Isso pode ser usado para o comando de instalação; Ele é ignorado para outros comandos. |
| `--installChannelUri <uri>` | **Opcional**: o URI do manifesto do canal a ser usado para a instalação. O URI especificado por `--channelUri` (que deve ser especificado quando `--installChannelUri` for especificado) é usado para detectar atualizações. Isso pode ser usado para o comando de instalação; Ele é ignorado para outros comandos. |
| `--installCatalogUri <uri>` | **Opcional**: o URI do manifesto do catálogo a ser usado para a instalação. Se especificado, o gerente de canal tenta baixar o manifesto do catálogo desse URI antes de usar o URI no manifesto do canal de instalação. Esse parâmetro é usado para dar suporte a instalação offline, em que o cache de layout será criado com o catálogo de produtos que já foi baixado. Isso pode ser usado para o comando de instalação; Ele é ignorado para outros comandos. |
| `--productId <id>` | **Opcional**: a ID do produto para a instância do que será instalada. Isso é preenchido previamente nas condições normais de instalação. |
| `--wait` | **Opcional**: o processo aguardará até que a instalação seja concluída antes de retornar um código de saída. Isso é útil ao automatizar instalações em que é necessário aguardar a conclusão da instalação para tratar o código de retorno da instalação. |
| `--locale <language-locale>` | **Opcional**: alterar o idioma de exibição da interface do usuário do próprio instalador. A configuração será mantida. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--cache` | **Opcional**: se houver, os pacotes serão mantidos após serem instalados para os reparos subsequentes. Isso substitui a configuração de política global a ser usada para instalações, reparos ou modificações subsequentes. A política padrão é armazenar pacotes em cache. Isso é ignorado para o comando de desinstalação. Leia sobre como [desabilitar ou mover o cache do pacote](disable-or-move-the-package-cache.md) para obter mais informações. |
| `--nocache` | **Opcional**: se houver, os pacotes serão excluídos após serem instalados ou reparados. Eles serão baixados novamente somente se necessário e excluídos novamente após o uso. Isso substitui a configuração de política global a ser usada para instalações, reparos ou modificações subsequentes. A política padrão é armazenar pacotes em cache. Isso é ignorado para o comando de desinstalação. Leia sobre como [desabilitar ou mover o cache do pacote](disable-or-move-the-package-cache.md) para obter mais informações. |
| `--noUpdateInstaller` | **Opcional**: se presente, impede que o instalador se atualize quando Quiet é especificado. O comando do instalador falhará e retornará um código de saída diferente de zero se noUpdateInstaller for especificado como silencioso quando uma atualização do instalador for necessária. |
| `--noWeb` | **Opcional**: se estiver presente, a instalação do Visual Studio usará os arquivos em seu diretório de layout para instalar o Visual Studio. Se um usuário tentar instalar componentes que não estão no layout, a instalação falhará.  Para obter mais informações, consulte [Implantação de uma instalação de rede](create-a-network-installation-of-visual-studio.md). <br/><br/> **Importante**: essa opção não impede que a instalação do Visual Studio Verifique se há atualizações. Para saber mais, confira a página [Controlar atualizações para implantações do Visual Studio baseadas em rede](controlling-updates-to-visual-studio-deployments.md). |
| `--path <name>=<path>` | **Opcional**: usado para especificar caminhos de instalação personalizados para a instalação. Os nomes de caminho com suporte são shared, cache e install. |
| `--path cache=<path>` | **Opcional**: usa o local que você especifica para baixar os arquivos de instalação. Este local só pode ser definido na primeira vez em que o Visual Studio é instalado. Exemplo: `--path cache="C:\VS\cache"` |
| `--path shared=<path>` | **Opcional**: contém arquivos compartilhados para instalações lado a lado do Visual Studio. Algumas ferramentas e SDKs fazem instalações em um local nessa unidade, enquanto outros podem substituir essa configuração e fazer a instalação em outra unidade. Exemplo: `--path shared="C:\VS\shared"` <br/><br/>**Importante**: isso pode ser definido apenas uma vez e na primeira vez que o Visual Studio é instalado. |
| `--path install=<path>` | **Opcional**: equivalente a `–-installPath` . Especificamente, `--installPath "C:\VS"` e `--path install="C:\VS"` são equivalentes. Somente um desses comandos pode ser usado de cada vez. |

## <a name="administrator-update-command-and-command-line-parameters"></a>Comando de atualização do administrador e parâmetros de linha de comando
Se você baixar uma atualização de administrador do [Catálogo de Microsoft Update](https://catalog.update.microsoft.com) para o diretório de instalação no computador cliente, basta clicar duas vezes no arquivo para aplicar a atualização. Você também pode abrir uma janela de comando e passar alguns dos parâmetros abaixo para alterar o comportamento padrão. 

Se você estiver implantando a atualização do administrador por meio do Microsoft Endpoint Manager (SCCM), poderá modificar o pacote para ajustar o comportamento usando os parâmetros abaixo. Você também pode controlar os parâmetros por meio de um arquivo de configuração no computador cliente. Para obter mais informações, consulte [métodos para configurar uma atualização de administrador](../install/applying-administrator-updates.md#methods-for-configuring-an-administrator-update)

Observe que todos os parâmetros de atualização do administrador são executados no contexto de "atualização".

| **Parâmetros de atualização do administrador** | **Descrição** |
| ----------------------- | --------------- |
| `--installerUpdateArgs [optional parameters]` | Esse parâmetro funciona como uma "matriz de passagem" de parâmetros específicos que são relevantes para cenários de atualização do administrador. Os parâmetros opcionais que são habilitados para essa finalidade são: <br/><br/> `--quiet`: Essa é a experiência padrão para atualizações do administrador e está listada aqui para fins de integridade. <br/> `--passive`: Esse parâmetro substitui o `--quiet` parâmetro.  Faz com que a interface do usuário seja exibida de maneira não interativa. <br/>`--norestart`: Esse parâmetro deve ser usado em conjunto com o `--quiet` ou `--passive` e faz com que as reinicializações necessárias sejam atrasadas. <br/>`--noWeb`: Esse parâmetro impede que o Visual Studio Verifique na Internet se há atualizações para o produto. <br/>`--force`: Esse parâmetro força o Visual Studio a fechar, mesmo que o Visual Studio esteja em uso. Use esse parâmetro com cuidado, pois isso pode causar perda de trabalho. Esse parâmetro deve ser usado no contexto do usuário. <br/>`--installWhileDownloading`: Esse parâmetro permite que o Visual Studio Baixe e instale o produto em paralelo. É a experiência padrão para atualizações do administrador e está listada aqui para fins de integridade. <br/>`--downloadThenInstall`: Esse parâmetro força o Visual Studio a baixar todos os arquivos antes de instalá-los. É mutuamente exclusivo do `--installWhileDownloading` parâmetro. |
| `--checkPendingReboot` | A atualização será anulada se houver uma reinicialização pendente no computador, independentemente de qual aplicativo possa tê-lo causado. O padrão é não verificar se há reinicializações pendentes. |


Exemplo de sintaxe: `visualstudioupdate-16.9.0to16.9.4.exe --installerUpdateArgs=--force,--noWeb --checkPendingReboot`

## <a name="list-of-workload-ids-and-component-ids"></a>Lista de IDs de carga de trabalho e IDs de componente

Confira uma lista de IDs de componente e de carga de trabalho classificadas por produto do Visual Studio na página [IDs de componente e de carga de trabalho do Visual Studio](workload-and-component-ids.md).

## <a name="list-of-language-locales"></a>Lista de localidades de idioma

| **Localidade de idioma** | **Idioma** |
| ----------------------- | --------------- |
| Cs-cz | Tcheco |
| De-de | Alemão |
| En-us | Inglês |
| Es-es | Espanhol |
| Fr-fr | Francês |
| It-it | Italiano |
| Ja-jp | Japonês |
| Ko-kr | Coreano |
| Pl-pl | Polonês |
| Pt-br | Português - Brasil |
| Ru-ru | Russo |
| Tr-tr | Turco |
| Zh-cn | Chinês - Simplificado |
| Zh-tw | Chinês - Tradicional |

## <a name="error-codes"></a>Códigos do Erro

Dependendo do resultado da operação, a variável de ambiente `%ERRORLEVEL%` será definida como um dos valores a seguir:

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

Cada operação gera vários arquivos de log no diretório `%TEMP%` que indicam o progresso da instalação. Classifique a pasta por data e procure arquivos começando com `dd_bootstrapper`, `dd_client` e `dd_setup` para o bootstrapper, o aplicativo instalador e o mecanismo de instalação, respectivamente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

- [Exemplos de parâmetros de linha de comando para a instalação do Visual Studio](command-line-parameter-examples.md)
- [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)
- [Automatizar a instalação do Visual Studio com um arquivo de resposta](automated-installation-with-response-file.md)
- [IDs de carga de trabalho e de componente do Visual Studio](workload-and-component-ids.md)
