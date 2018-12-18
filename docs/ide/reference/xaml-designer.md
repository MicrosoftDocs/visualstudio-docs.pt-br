---
title: Página de opções do Designer XAML
ms.date: 03/02/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.XAMLDesigner
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 52691c0b49c74bd39fa97ec8d297ffb823ba705c
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388355"
---
# <a name="xaml-designer-options-page"></a>Página de opções do Designer XAML

Use a página de opções do **Designer XAML** para especificar como os elementos e atributos são formatados nos documentos XAML. Para abrir essa página, escolha o menu **Ferramentas** e, em seguida, **Opções**. Para acessar a página de propriedades **XAML Designer**, escolha o nó **XAML Designer**. As configurações para o XAML Designer são aplicadas quando você abre o documento. Portanto, se você alterar as configurações, será necessário fechar e reabrir o Visual Studio para ver as alterações.

> [!NOTE]
> As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, confira [Redefinir as configurações](../environment-settings.md#reset-settings).

## <a name="enable-xaml-designer"></a>Habilitar o XAML Designer

Quando selecionada, essa configuração habilita o XAML Designer. O XAML Designer fornece uma área de trabalho visual para editar documentos XAML. Algumas funcionalidades no Visual Studio, como o IntelliSense para associação de dados e recursos, exigem que o XAML Designer seja habilitado.

As configurações a seguir aplicam-se somente quando o XAML Designer está habilitado. Se você alterar esta opção, será necessário reiniciar o Visual Studio para que a configuração entre em vigor.

## <a name="default-document-view"></a>Exibição de documento padrão

Use essa configuração para controlar se o modo de exibição de Design aparece quando documentos XAML são carregados.

|||
|-|-|
|**Modo de Exibição de Fonte**|Especifica se somente a fonte de XAML aparece no modo de exibição XAML. Isso é útil ao carregar documentos grandes.|
|**Modo de exibição de Design**|Especifica se apenas um XAML Designer visual aparece no modo de exibição XAML.|
|**Modo Divisão**|Especifica se o XAML Designer visual e a fonte de XAML aparecem próximos um do outro no modo de exibição XAML (local com base na configuração **Orientação de Divisão**).|

## <a name="split-orientation"></a>Orientação de Divisão

Use essa configuração para controlar quando e como o XAML Designer aparece ao editar um documento XAML. Essas configurações aplicam-se somente quando a **Exibição do documento padrão** está definida como **Modo Divisão**.

|||
|-|-|
|**Vertical**|A fonte de XAML aparece no lado esquerdo do modo de exibição XAML e o XAML Designer aparece no outro lado.|
|**Horizontal**|O XAML Designer aparece na parte superior do modo de exibição XAML e a fonte de XAML aparece abaixo dele.|
|**Padrão**|O documento XAML usa a orientação de divisão recomendada para a plataforma de destino do projeto do documento. Para a maioria das plataformas, isso é equivalente a **Horizontal**.|

## <a name="zoom-by-using"></a>Aplicar zoom usando

Use essa configuração para determinar o funcionamento de aplicar zoom ao editar um documento XAML.

|||
|-|-|
|**Botão de rolagem do mouse**|Ampliar o XAML Designer ao rolar o botão de rolagem do mouse.|
|**CTRL + botão de rolagem do mouse**|Ampliar o XAML Designer pressionando a tecla CTRL ao rolar o botão de rolagem do mouse.|
|**Alt + botão de rolagem do mouse**|Ampliar o XAML Designer pressionando a tecla ALT ao rolar o botão de rolagem do mouse.|

Essas configurações determinam o comportamento do Designer ao editar um documento XAML.

|||
|-|-|
|**Nomear automaticamente os elementos interativos na criação**|Especifica se um nome padrão é fornecido para um novo elemento interativo ao adicioná-lo no Designer.|
|**Inserir automaticamente as propriedades de layout na criação de elemento**|Especifica se as propriedades de layout são fornecidas a um novo elemento ao adicioná-lo no Designer.|
|**Usar layout baseado em quadrantes**|Especifica se o controle atualmente selecionado alinha-se às bordas do contêiner pai mais próximas. Se essa caixa de seleção estiver desmarcada, os alinhamentos de controle não se alteram durante uma operação de movimentação ou criação.|
|**Popular automaticamente os itens da caixa de ferramentas**|Especifica se os controles de usuário e os controles personalizados na solução atual são mostrados automaticamente na caixa de ferramentas.|

## <a name="settings-blend-only"></a>Configurações (Somente Blend)

Use essas opções para determinar as configurações ao editar arquivos XAML usando o Blend.

|||
|-|-|
|**Aplicar zoom usando**|Ampliar o XAML Designer ao rolar o botão de rolagem do mouse ou pressionando a tecla CTRL ou ALT ao rolar o botão de rolagem do mouse.|
|**Digitar unidades**|Especifica se as medidas no designer são baseadas em pontos ou pixels. Como os Aplicativos Universais do Windows não oferecem suporte a pontos, as unidades serão automaticamente convertidas em pixels se **Pontos** estiver selecionado.|

## <a name="artboard-blend-only"></a>Prancheta (Somente Blend)

Use essas configurações para determinar o comportamento do XAML Designer ao editar documentos XAML no Blend.

### <a name="snapping"></a>Ajustando

|||
|-|-|
|**Mostrar grade de ajuste**|Quando essa opção é selecionada, as linhas de grade aparecem no designer para ajudá-lo a alinhar os controles. Os controles adicionados ao designer ajustam-se a essas linhas de grade quando a opção **Ajustar às linhas de grade** está selecionada.|
|**Ajustar às linhas de grade**|Quando os controles são adicionados ou movidos no designer, eles se encaixam às linhas de grade.|
|**Espaçamento da linha de grade**|Especifica o espaçamento entre linhas de grade em pixels ou pontos (conforme determinado pela configuração **Digitar unidades**).|
|**Ajustar-se às guias de alinhamento**|Especifica se os controles ajustam-se às guias de alinhamento.|
|**Margem padrão**|Quando **Ajustar-se às guias de alinhamento** está habilitado, especifica o espaçamento entre as guias de alinhamento e o controle em pixels ou pontos (conforme determinado pela configuração **Digitar unidades**).|
|**Preenchimento padrão**|Quando **Ajustar-se às guias de alinhamento** está habilitado, especifica o espaçamento adicional entre as guias de alinhamento e o controle em pixels ou pontos (conforme determinado pela configuração **Digitar unidades**).|

### <a name="animation"></a>Animação

Use essa configuração para determinar se um aviso é exibido quando animações dependentes (não aceleradas) estão habilitadas no Blend.

### <a name="effects"></a>Efeitos

Use essas configurações para determinar se efeitos são renderizados ao editar arquivos XAML no XAML Designer usando o Blend.

|||
|-|-|
|**Renderizar efeitos**|Especifica se efeitos renderizam ao editar arquivos XAML no XAML Designer usando o Blend.|
|**Limite de zoom**|Especifica o percentual de ampliação com a qual os efeitos são renderizados quando a caixa de seleção **Renderizar efeitos** está selecionada. Se você aplicar zoom além dessa configuração os efeitos não serão mais renderizados no XAML Designer.|

## <a name="see-also"></a>Consulte também

- [XAML no WPF](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [Passo a passo: Meu primeiro aplicativo da área de trabalho do WPF](/dotnet/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application)