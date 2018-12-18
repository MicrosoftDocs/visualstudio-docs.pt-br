---
title: Configurar a caixa de diálogo de referência de serviço | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- msvse_wcf.dlg.ConfigureServiceReference
helpviewer_keywords:
- WCF services, Configure Service Reference dialog box
- service references [Visual Studio], configuring behavior
- Configure Service Reference dialog box
ms.assetid: 25e4c36b-2db6-4e71-9010-b7068255d09d
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 24da338378739afca6ad228582a29069aebde9f5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49266964"
---
# <a name="configure-service-reference-dialog-box"></a>Caixa de diálogo Configurar Referência de Serviço
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O **Configure Service Reference** caixa de diálogo permite que você configure o comportamento de [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] serviços.  
  
> [!NOTE]
>  As caixas de diálogo e os comandos de menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da sua edição ou das configurações ativas. Para alterar as configurações, escolha Importar e Exportar Configurações no menu Ferramentas. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 Para acessar o **Configure Service Reference** caixa de diálogo, o botão direito do mouse, um serviço de referência na **Gerenciador de soluções** e escolha **configurar referência de serviço**. Você também pode acessar a caixa de diálogo clicando o **Advanced** botão na **Adicionar caixa de diálogo de referência de serviço**.  
  
## <a name="task-list"></a>Lista de Tarefas  
  
-   Para alterar o endereço em que um serviço WCF está hospedado, digite o novo endereço na **endereço** campo.  
  
-   Para alterar o nível de acesso para classes em um cliente WCF, selecione uma palavra-chave de nível de acesso na **nível para as classes geradas de acesso** lista.  
  
-   Para chamar os métodos de um serviço WCF de forma assíncrona, selecione a **gerar operações assíncronas** caixa de seleção.  
  
-   Para gerar tipos de contrato de mensagem em um cliente de WCF, selecione a **sempre gerar contratos de mensagem** caixa de seleção.  
  
-   Para especificar os tipos de coleção de dicionário ou lista para um cliente WCF, selecione os tipos a partir de **tipo de coleção** e **tipo de coleção de dicionário** lista.  
  
-   Para desabilitar o compartilhamento de tipo, desmarque a **reutilizar os tipos em assemblies referenciados** caixa de seleção. Para habilitar o compartilhamento para um subconjunto dos assemblies referenciados de tipo, selecione o **reutilizar tipos em assemblies consultados** caixas de seleção **reutilizar os tipos em assemblies referenciados especificados**e selecione o desejado referências na **lista de assemblies referenciados**.  
  
## <a name="uielement-list"></a>Lista UIElement  
 **Endereço**  
 Usado para atualizar o endereço da Web onde o procura uma referência de serviço para um serviço. Por exemplo, durante o desenvolvimento de serviço pode estar hospedado em um servidor de desenvolvimento e posteriormente movido para um servidor de produção, a necessidade de uma alteração de endereço.  
  
> [!NOTE]
>  O elemento de endereço não está disponível quando o **Configure Service Reference** caixa de diálogo é exibida da **Adicionar caixa de diálogo de referência de serviço**.  
  
 **Nível de acesso para classes geradas**  
 Determina o nível de acesso do código para classes de cliente do WCF.  
  
> [!NOTE]
>  Para projetos de site, essa opção é sempre definida como `Public` e não pode ser alterado. Para obter mais informações, consulte [solução de problemas de referências de serviço](../data-tools/troubleshooting-service-references.md).  
  
 **Gerar operações assíncronas**  
 Determina se os métodos de serviço WCF serão ser chamados de forma síncrona (o padrão) ou assíncrona.  
  
 **Gerar operações baseadas em tarefa**  
 Ao escrever código assíncrono, essa opção permite que você se beneficie da tarefa paralela TPL (biblioteca) que foi introduzido com o .net 4. Ver [(TPL) biblioteca de paralelismo de tarefas](http://msdn.microsoft.com/library/dd460717.aspx).  
  
 **Sempre gerar contratos de mensagem**  
 Determina se os tipos de contrato de mensagem serão gerados para um cliente WCF. Para obter mais informações sobre contratos de mensagem, consulte [contratos de mensagem usando](http://msdn.microsoft.com/library/1e19c64a-ae84-4c2f-9155-91c54a77c249).  
  
 **Tipo de coleção**  
 Especifica o tipo de coleção de lista para um cliente WCF. O tipo padrão é <xref:System.Array>.  
  
 **Tipo de coleção de dicionário**  
 Especifica o tipo de coleção de dicionário para um cliente WCF. O tipo padrão é <xref:System.Collections.Generic.Dictionary%602>.  
  
 **Reutilizar os tipos em assemblies referenciados**  
 Determina se um cliente WCF tenta reutilizar que já existem em assemblies referenciados em vez de gerar novos tipos quando um serviço é adicionado ou atualizado. Por padrão, esta opção estiver marcada.  
  
 **Reutilizar os tipos em todos os assemblies referenciados**  
 Quando selecionada, todos os tipos na **lista de assemblies referenciados** serão reutilizados se possível. Por padrão, essa opção é selecionada.  
  
 **Reutilizar os tipos em assemblies referenciados especificados**  
 Quando selecionada, somente nos tipos selecionados na **lista de assemblies referenciados** será reutilizado.  
  
 **Lista de assemblies referenciados**  
 Contém uma lista de assemblies referenciados para o projeto ou o site da Web. Quando **reutilizar os tipos em assemblies referenciados especificados** for selecionada, assemblies individuais podem ser marcados ou desmarcados.  
  
 **Adicionar referência Web**  
 Exibe a [NIB: caixa de diálogo de referência Web adicionar](http://msdn.microsoft.com/en-us/bdf05776-c591-40af-bfd7-e1e2aa1e87b5).  
  
> [!NOTE]
>  Essa opção deve ser usada somente para projetos que usam a versão 2.0 do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)].  
  
> [!NOTE]
>  O **Add Web Reference** botão está disponível apenas quando o **Configure Service Reference** caixa de diálogo é exibida da **Adicionar caixa de diálogo de referência de serviço**.  
  
## <a name="see-also"></a>Consulte também  
 [Como: adicionar, atualizar ou remover uma referência de serviço](http://msdn.microsoft.com/library/cacc14bd-4455-4a44-be78-d2ac16113dd9)   
 [Como: adicionar uma referência a um serviço Web](http://msdn.microsoft.com/library/952e49a1-567e-4a74-8cd7-f2e7b62c3168)   
 [Serviços do Windows Communication Foundation e WCF Data Services](../data-tools/configure-service-reference-dialog-box.md)

