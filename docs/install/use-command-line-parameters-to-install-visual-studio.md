---
title: Usar parâmetros de linha de comando para instalar o Visual Studio
description: Saiba como usar parâmetros de linha de comando para controlar ou personalizar sua instalação do Visual Studio.
ms.custom: ''
ms.date: 11/14/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
f1_keywords:
- command-line parameters
- switches
- command prompt
ms.assetid: 480f3cb4-d873-434e-a8bf-82cff7401cf2
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e52d61c1226e131c9d989a70f7c8e6432d8f3733
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51768523"
---
# <a name="use-command-line-parameters-to-install-visual-studio-2017"></a>Usar parâmetros de linha de comando para instalar o Visual Studio 2017

Ao instalar o Visual Studio 2017 por meio de um prompt de comando, é possível usar uma variedade de parâmetros de linha de comando para controlar ou personalizar a instalação. Da linha de comando, você pode realizar as seguintes ações:

- Iniciar a instalação com certas opções pré-selecionadas.
- Automatizar o processo de instalação.
- Criar um cache (layout) dos arquivos de instalação para uso posterior.

As opções de linha de comando são usadas em conjunto com o bootstrapper de instalação, que é o arquivo pequeno (aproximadamente 1MB) que inicia o processo de download. O bootstrapper é o primeiro executável iniciado quando você baixa do site do Visual Studio. Use os links a seguir para obter um link direto para o bootstrapper de versão mais recente para a edição do produto que você está instalando:

- [Visual Studio 2017 Enterprise](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=15?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2017)
- [Visual Studio 2017 Professional](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=15?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2017)
- [Comunidade do Visual Studio 2017](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=community&rel=15?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=link+cta&utm_content=download+commandline+parameters+vs2017)

## <a name="list-of-command-line-parameters"></a>Lista de parâmetros de linha de comando

 Os parâmetros da linha de comando do Visual Studio diferenciam maiúsculas de minúsculas.

> Syntax: `vs_enterprise.exe [command] <options>...`

(Substitua `vs_enterprise.exe` conforme apropriado de acordo com a edição do produto que você está instalando.)

>[!TIP]
> Para obter mais exemplos de como usar a linha de comando para instalar o Visual Studio 2017, confira a página [Exemplos de parâmetro de linha de comando](command-line-parameter-examples.md).

| **Comando** | **Descrição** |
| ----------------------- | --------------- |
| (blank) | Instala o produto. |
| `modify` | Modifica um produto instalado. |
| `update` | Atualiza um produto instalado. |
| `repair` | Repara um produto instalado. |
| `uninstall` | Desinstala um produto instalado. |
| `export` | **Novo na 15.9**: exporta a seleção da instalação para um arquivo de configuração de instalação. |

| **Opção de instalação** | **Descrição** |
| ----------------------- | --------------- |
| `--installPath <dir>` | O diretório de instalação no qual a instância deverá agir. Para o comando de instalação, isso é **Opcional** e é onde a instância será instalada. Para outros comandos, isso é **Necessário** e é onde a instância instalada anteriormente foi instalada. |
| `--addProductLang <language-locale>` | **Opcional**: durante a instalação ou operação de modificação, isso determina os pacotes de idiomas de interface do usuário que são instalados no produto. Ele pode aparecer várias vezes na linha de comando para adicionar vários pacotes de idiomas. Se não estiver presente, a instalação usará a localidade do computador. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--removeProductLang <language-locale>` | **Opcional**: durante a instalação ou operação de modificação, isso determina os pacotes de idiomas de interface do usuário que devem ser removidos do produto. Ele pode aparecer várias vezes na linha de comando para adicionar vários pacotes de idiomas. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--add <one or more workload or component IDs>` | **Opcional**: uma ou mais IDs de carga de trabalho ou de componente a serem adicionadas. Os componentes obrigatórios do artefato são instalados, mas não os componentes recomendados ou opcionais. Você pode controlar os componentes adicionais globalmente usando `--includeRecommended` e/ou `--includeOptional`. Para incluir várias cargas de trabalho ou componentes, repita o comando `--add` (por exemplo, `--add Workload1 --add Workload2`). Para ter um controle mais refinado, você pode acrescentar `;includeRecommended` ou `;includeOptional` à ID (por exemplo, `--add Workload1;includeRecommended` ou `--add Workload2;includeRecommended;includeOptional`). Para saber mais, confira a página [IDs de carga de trabalho e de componente](workload-and-component-ids.md). Você pode repetir esta opção conforme necessário.|
| `--remove <one or more workload or component IDs>` | **Opcional**: uma ou mais IDs de carga de trabalho ou de componente a serem removidas. Para obter mais informações, consulte nossa página [IDs de carga de trabalho e de componente](workload-and-component-ids.md). Você pode repetir esta opção conforme necessário.|
| `--in <path>` | **Opcional**: o URI ou o caminho para um arquivo de resposta.  |
| `--all` | **Opcional**: se todas as cargas de trabalho e todos os componentes de um produto serão instalados. |
| `--allWorkloads` | **Opcional**: instala todas as cargas de trabalho e componentes, mas nenhum componente recomendado ou opcional. |
| `--includeRecommended` | **Opcional**: inclui os componentes recomendados para as cargas de trabalho que estão instaladas, mas não os componentes opcionais. As cargas de trabalho são especificadas com `--allWorkloads` ou `--add`. |
| `--includeOptional` | **Opcional**: inclui os componentes opcionais para as cargas de trabalho que estão instaladas, mas não os componentes recomendados. As cargas de trabalho são especificadas com `--allWorkloads` ou `--add`.  |
| `--quiet, -q` | **Opcional**: não exibir nenhuma interface do usuário durante a instalação. |
| `--passive, -p` | **Opcional**: exibir a interface do usuário, mas não solicitar nenhuma interação do usuário. |
| `--norestart` | **Opcional**: se essa opção estiver presente, comandos com `--passive` ou `--quiet` não reiniciarão o computador automaticamente (se necessário).  Isso será ignorado se `--passive` e `--quiet` não forem especificados.  |
| `--nickname <name>` | **Opcional**: define o apelido a ser atribuído a um produto instalado. O apelido não pode ter mais de 10 caracteres.  |
| `--productKey` | **Opcional**: define a chave do produto (Product Key) a ser usada para um produto instalado. Ele é composto de 25 caracteres alfanuméricos no formato `xxxxx-xxxxx-xxxxx-xxxxx-xxxxx` ou `xxxxxxxxxxxxxxxxxxxxxxxxx`. |
| `--help, --?, -h, -?` | Exibir uma versão offline desta página. |
| `--config <path>` | **Opcional** e **Novo na 15.9**: durante uma instalação ou operação de modificação, isso determina as cargas de trabalho e componentes a serem adicionados com base em um arquivo de configuração de instalação salvo anteriormente. Essa operação é aditiva e não removerá nenhuma carga de trabalho nem componente se ele não estiver presente no arquivo. Além disso, os itens que não se aplicarem ao produto não serão adicionados. Durante uma operação de exportação, isso determina a localização para salvar o arquivo de configuração de instalação. |

> Observação: ao especificar várias cargas de trabalho e vários componentes, é necessário repetir a opção de linha de comando `--add` ou `--remove` para cada item.

| **Opções de layout** | **Descrição** |
| ----------------------- | --------------- |
| `--layout <dir>` | Especifica um diretório para criar um cache de instalação offline. Para obter mais informações, consulte [Criar uma instalação baseada em rede do Visual Studio](create-a-network-installation-of-visual-studio.md).|
| `--lang <one or more language-locales>` | **Opcional**: usado com `--layout` para preparar um cache de instalação offline com pacotes de recursos com idiomas especificados. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--add <one or more workload or component IDs>` | **Opcional**: uma ou mais IDs de carga de trabalho ou de componente a serem adicionadas. Os componentes obrigatórios do artefato são instalados, mas não os componentes recomendados ou opcionais. Você pode controlar os componentes adicionais globalmente usando `--includeRecommended` e/ou `--includeOptional`. Para ter um controle mais refinado, você pode acrescentar `;includeRecommended` ou `;includeOptional` à ID (por exemplo, `--add Workload1;includeRecommended` ou `--add Workload2;includeOptional`). Para saber mais, confira a página [IDs de carga de trabalho e de componente](workload-and-component-ids.md). <br/>**Observação**: se `--add` for usado, somente as cargas de trabalho especificadas e os componentes e suas dependências serão baixados. Se `--add` não for especificado, todas as cargas de trabalho e componentes serão baixados para o layout.|
| `--includeRecommended` | **Opcional**: inclui os componentes recomendados para as cargas de trabalho que estão instaladas, mas não os componentes opcionais. As cargas de trabalho são especificadas com `--allWorkloads` ou `--add`. |
| `--includeOptional` | **Opcional**: inclui os componentes recomendados *e* opcionais para quaisquer cargas de trabalho incluídas no layout. As cargas de trabalho são especificadas com `--add`.  |
| `--keepLayoutVersion` | **Novo no 15.3, opcional**: aplique as alterações no layout sem atualizar a versão do layout. |
| `--verify` | **Novo no 15.3, opcional**: verifique o conteúdo de um layout. Todos os arquivos corrompidos ou ausentes são listados. |
| `--fix` | **Novo no 15.3, opcional**: verifique o conteúdo de um layout.  Se algum arquivo estiver corrompido ou ausente, ele será baixado novamente. Para corrigir um layout, é necessário acesso à Internet. |
| `--clean <one or more paths to catalogs>` | **Novo no 15.3, opcional**: remove versões antigas dos componentes de um layout que foi atualizado para uma versão mais recente. |

| **Opções de instalação avançadas** | **Descrição** |
| ----------------------- | --------------- |
| `--channelId <id>` | **Opcional**: a ID do canal para a instância a ser instalada. Isso é necessário para o comando de instalação, ignorado para outros comandos se `--installPath` está especificado. |
| `--channelUri <uri>` | **Opcional**: o URI do manifesto do canal. Se as atualizações não forem desejadas, `--channelUri` poderá apontar para um arquivo inexistente. por exemplo, --channelUri C:\doesntExist.chman. Isso pode ser usado para o comando de instalação e é ignorado para outros comandos. |
| `--installChannelUri <uri>` | **Opcional**: o URI do manifesto do canal a ser usado para a instalação. O URI especificado por `--channelUri` (que deve ser especificado quando `--installChannelUri` for especificado) é usado para detectar atualizações. Isso pode ser usado para o comando de instalação e é ignorado para outros comandos. |
| `--installCatalogUri <uri>` | **Opcional**: o URI do manifesto do catálogo a ser usado para a instalação. Se especificado, o gerente de canal tenta baixar o manifesto do catálogo desse URI antes de usar o URI no manifesto do canal de instalação. Esse parâmetro é usado para dar suporte a instalação offline, em que o cache de layout será criado com o catálogo de produtos que já foi baixado. Isso pode ser usado para o comando de instalação e é ignorado para outros comandos. |
| `--productId <id>` | **Opcional** A ID do produto para a instância que será instalada. Isso será populado previamente em condições normais de instalação. |
| `--wait` | **Opcional**: o processo aguardará até que a instalação seja concluída antes de retornar um código de saída. Isso é útil ao automatizar instalações em que é necessário aguardar a conclusão da instalação para tratar o código de retorno da instalação. |
| `--locale <language-locale>` | **Opcional**: alterar o idioma de exibição da interface do usuário do próprio instalador. A configuração será mantida. Para obter mais informações, consulte a seção [Lista de localidades de idioma](#list-of-language-locales) nesta página.|
| `--cache` | **Novo em 15.2, opcional**: caso presentes, os pacotes serão mantidos após a instalação para reparos subsequentes. Isso substitui a configuração de política global a ser usada para instalações, reparos ou modificações subsequentes. A política padrão é armazenar pacotes em cache. Isso é ignorado para o comando de desinstalação. Leia sobre como [desabilitar ou mover o cache do pacote](disable-or-move-the-package-cache.md) para obter mais informações. |
| `--nocache` | **Novo em 15.2, opcional**: caso presentes, os pacotes serão ser excluídos depois de serem instalados ou reparados. Serão baixados novamente apenas se for necessário e excluídos após o uso. Isso substitui a configuração de política global a ser usada para instalações, reparos ou modificações subsequentes. A política padrão é armazenar pacotes em cache. Isso é ignorado para o comando de desinstalação. Leia sobre como [desabilitar ou mover o cache do pacote](disable-or-move-the-package-cache.md) para obter mais informações. |
| `--noUpdateInstaller` | **Novidade no 15.2, opcional**: se existir, impede que instalador atualize a si próprio quando o modo silencioso é especificado. O comando do instalador falhará e retornará um código de saída diferente de zero se noUpdateInstaller for especificado como silencioso quando uma atualização do instalador for necessária. |
| `--noWeb` | **Novo no 15.3, opcional**: agora, a instalação baixará qualquer conteúdo que estiver sendo instalado da Internet.  Todo o conteúdo sendo instalado deve estar disponível em um layout offline.  Se algum conteúdo estiver ausente do layout, a instalação falhará.  Para obter mais informações, consulte [Implantação de uma instalação de rede](create-a-network-installation-of-visual-studio.md). |
| `--path <name>=<path>` | **Novo no 15,7, opcional**: usado para especificar caminhos de instalação personalizados para a instalação. Os nomes de caminho com suporte são shared, cache e install. |
| `--path cache=<path>` | **Novo no 15,7, opcional**: usa o local especificado para baixar os arquivos de instalação. Este local só pode ser definido na primeira vez em que o Visual Studio é instalado. Exemplo: `--path cache="C:\VS\cache"` |
| `--path shared=<path>` | **Novo no 15,7, opcional**: contém arquivos compartilhados para instalações do Visual Studio lado a lado. Algumas ferramentas e SDKs fazem instalações em um local nessa unidade, enquanto outros podem substituir essa configuração e fazer a instalação em outra unidade. Exemplo: `--path shared="C:\VS\shared"` <br><br>Importante: isso pode ser definido apenas uma vez e na primeira vez que o Visual Studio é instalado. |
| `--path install=<path>` | **Novo no 15,7, opcional**: equivalente a `–-installPath`. Especificamente, `--installPath "C:\VS"` e `--path install="C:\VS"` são equivalentes. Apenas um deles pode ser usado por vez. |

## <a name="list-of-workload-ids-and-component-ids"></a>Lista de IDs de carga de trabalho e IDs de componente

Para obter uma lista de IDs de componente e de carga de trabalho classificadas por produto do Visual Studio, consulte a página [IDs de componente e de carga de trabalho do Visual Studio 2017](workload-and-component-ids.md).

## <a name="list-of-language-locales"></a>Lista de localidades de idioma

| **Localidade de idioma** | **Linguagem** |
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
| Zh-cn | Chinês – Simplificado |
| Zh-tw | Chinês – Tradicional |

## <a name="error-codes"></a>Códigos de erro

Dependendo do resultado da operação, a variável de ambiente `%ERRORLEVEL%` será definida como um dos valores a seguir:

| **Valor** | **Result** |
| --------- | ---------- |
| 0 | A operação foi concluída com êxito |
| 1602 | A operação foi cancelada |
| 3010 | A operação foi concluída com êxito, mas a instalação requer a reinicialização antes de ser usada |
| 5004 | A operação foi cancelada |
| 5007 | A operação foi bloqueada – o computador não atende aos requisitos |
| Outros | Condição de falha ocorreu. Verifique os logs para obter mais informações |

Cada operação gera vários arquivos de log no diretório `%TEMP%` que indicam o progresso da instalação. Classifique a pasta por data e procure arquivos começando com `dd_bootstrapper`, `dd_client` e `dd_setup` para o bootstrapper, o aplicativo instalador e o mecanismo de instalação, respectivamente.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

- [Exemplos de parâmetros de linha de comando para a instalação do Visual Studio 2017](command-line-parameter-examples.md)
- [Criar uma instalação offline do Visual Studio 2017](create-an-offline-installation-of-visual-studio.md)
- [Automatizar a instalação do Visual Studio com um arquivo de resposta](automated-installation-with-response-file.md)
- [IDs de carga de trabalho e de componente do Visual Studio 2017](workload-and-component-ids.md)