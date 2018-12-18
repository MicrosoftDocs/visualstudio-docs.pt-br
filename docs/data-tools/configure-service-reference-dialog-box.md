---
title: Caixa de diálogo Configurar Referência de Serviço
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: f0cb2737356813a9b637d7f16e9d5cda704c022a
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389494"
---
# <a name="configure-service-reference-dialog-box"></a>Caixa de diálogo Configurar Referência de Serviço

O **Configure Service Reference** caixa de diálogo permite que você configure o comportamento dos serviços do Windows Communication Foundation (WCF).

Para acessar o **Configure Service Reference** caixa de diálogo, o botão direito do mouse, um serviço de referência na **Gerenciador de soluções** e escolha **configurar referência de serviço**. Você também pode acessar a caixa de diálogo clicando o **Advanced** botão na **Adicionar caixa de diálogo de referência de serviço**.

## <a name="task-list"></a>Lista de tarefas

- Para alterar o endereço em que um serviço WCF está hospedado, digite o novo endereço na **endereço** campo.

- Para alterar o nível de acesso para classes em um cliente WCF, selecione uma palavra-chave de nível de acesso na **nível para as classes geradas de acesso** lista.

- Para chamar os métodos de um serviço WCF de forma assíncrona, selecione a **gerar operações assíncronas** caixa de seleção.

- Para gerar tipos de contrato de mensagem em um cliente de WCF, selecione a **sempre gerar contratos de mensagem** caixa de seleção.

- Para especificar os tipos de coleção de dicionário ou lista para um cliente WCF, selecione os tipos a partir de **tipo de coleção** e **tipo de coleção de dicionário** lista.

- Para desabilitar o compartilhamento de tipo, desmarque a **reutilizar os tipos em assemblies referenciados** caixa de seleção. Para habilitar o compartilhamento para um subconjunto dos assemblies referenciados de tipo, selecione o **reutilizar tipos em assemblies consultados** caixas de seleção **reutilizar os tipos em assemblies referenciados especificados**e selecione o desejado referências na **lista de assemblies referenciados**.

## <a name="uielement-list"></a>Lista UIElement

 **Endereço**

 Atualiza o endereço da web onde o procura uma referência de serviço para um serviço. Por exemplo, durante o desenvolvimento, o serviço pode ser hospedado em um servidor de desenvolvimento e posteriormente movido para um servidor de produção, a necessidade de uma alteração de endereço.

> [!NOTE]
> O elemento de endereço não está disponível quando o **Configure Service Reference** caixa de diálogo é exibida da **Adicionar caixa de diálogo de referência de serviço**.

 **Nível de acesso para classes geradas**

 Determina o nível de acesso do código para classes de cliente do WCF.

> [!NOTE]
> Para projetos de site, essa opção é sempre definida como `Public` e não pode ser alterado. Para obter mais informações, consulte [Solucionando problemas de referências de serviço](../data-tools/troubleshooting-service-references.md).

 **Gerar operações assíncronas**

 Determina se os métodos de serviço WCF é chamado de forma síncrona (o padrão) ou assíncrona.

 **Gerar operações baseadas em tarefas**

 Ao escrever código assíncrono, essa opção permite tirar proveito da tarefa paralela TPL (biblioteca) que foi introduzido com o .NET 4. Ver [(TPL) biblioteca de paralelismo de tarefas](/dotnet/standard/parallel-programming/task-parallel-library-tpl).

 **Sempre gerar contratos de mensagem**

 Determina se os tipos de contrato de mensagem são gerados para um cliente WCF. Para obter mais informações sobre contratos de mensagem, consulte [usando os contratos de mensagem](/dotnet/framework/wcf/feature-details/using-message-contracts).

 **Tipo de coleção**

 Especifica o tipo de coleção de lista para um cliente WCF. O tipo padrão é <xref:System.Array>.

 **Tipo de coleção de dicionário**

 Especifica o tipo de coleção de dicionário para um cliente WCF. O tipo padrão é <xref:System.Collections.Generic.Dictionary%602>.

 **Usar novamente os tipos em assemblies consultados**

 Determina se um cliente WCF tenta reutilizar o que já existe em assemblies referenciados em vez de gerar novos tipos quando um serviço é adicionado ou atualizado. Por padrão, esta opção estiver marcada.

 **Usar novamente os tipos em todos os assemblies consultados**

 Quando selecionada, todos os tipos na **lista de assemblies referenciados** são reutilizados se possível. Por padrão, essa opção é selecionada.

 **Usar novamente os tipos em determinados assemblies consultados**

 Quando selecionada, somente nos tipos selecionados na **lista de assemblies referenciados** são reutilizados.

 **Lista de assemblies referenciados**

 Contém uma lista de assemblies referenciados para o projeto ou o site. Quando você seleciona **reutilizar os tipos em assemblies referenciados especificados**, você pode selecionar ou limpar assemblies individuais.

 **Adicionar Referência Web**

 Exibe a **Add Web Reference** caixa de diálogo.

> [!NOTE]
> Essa opção deve ser usada somente para projetos que usam a versão 2.0 do [!INCLUDE[dnprdnshort](../code-quality/includes/dnprdnshort_md.md)].
>
> [!NOTE]
> O **Add Web Reference** botão está disponível apenas quando o **Configure Service Reference** caixa de diálogo é exibida da **Adicionar caixa de diálogo de referência de serviço**.

## <a name="see-also"></a>Consulte também

- [Como adicionar uma referência a um serviço Web](how-to-add-update-or-remove-a-wcf-data-service-reference.md)
- [Serviços do Windows Communication Foundation e WCF Data Services](../data-tools/configure-service-reference-dialog-box.md)