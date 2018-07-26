---
title: Hospedar o ASP.NET Core em um web farm
author: guardrex
description: Saiba como hospedar várias instâncias de um aplicativo ASP.NET Core com recursos compartilhados em um ambiente de web farm.
ms.author: riande
ms.custom: mvc
ms.date: 07/16/2018
uid: host-and-deploy/web-farm
ms.openlocfilehash: 2435c24bc205486331c828337ca81c43e6e60448
ms.sourcegitcommit: 3ca527f27c88cfc9d04688db5499e372fbc2c775
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39096081"
---
# <a name="host-aspnet-core-in-a-web-farm"></a><span data-ttu-id="817ce-103">Hospedar o ASP.NET Core em um web farm</span><span class="sxs-lookup"><span data-stu-id="817ce-103">Host ASP.NET Core in a web farm</span></span>

<span data-ttu-id="817ce-104">Por [Luke Latham](https://github.com/guardrex) e [Chris Ross](https://github.com/Tratcher)</span><span class="sxs-lookup"><span data-stu-id="817ce-104">By [Luke Latham](https://github.com/guardrex) and [Chris Ross](https://github.com/Tratcher)</span></span>

<span data-ttu-id="817ce-105">Um *web farm* é um grupo de dois ou mais servidores web (ou *nós*) que hospedam várias instâncias de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="817ce-105">A *web farm* is a group of two or more web servers (or *nodes*) that host multiple instances of an app.</span></span> <span data-ttu-id="817ce-106">Quando as solicitações de usuários chegam a um web farm, um *balanceador de carga* distribui as solicitações para os nós de farm da web.</span><span class="sxs-lookup"><span data-stu-id="817ce-106">When requests from users arrive to a web farm, a *load balancer* distributes the requests to the web farm's nodes.</span></span> <span data-ttu-id="817ce-107">Os web farms melhoram:</span><span class="sxs-lookup"><span data-stu-id="817ce-107">Web farms improve:</span></span>

* <span data-ttu-id="817ce-108">**Disponibilidade/confiabilidade** &ndash; quando um ou mais nós falham, o balanceador de carga pode rotear solicitações para outros nós em funcionamento para continuar a processar solicitações.</span><span class="sxs-lookup"><span data-stu-id="817ce-108">**Reliability/availability** &ndash; When one or more nodes fail, the load balancer can route requests to other functioning nodes to continue processing requests.</span></span>
* <span data-ttu-id="817ce-109">**Capacidade e desempenho** &ndash; vários nós podem processar mais solicitações que um único servidor.</span><span class="sxs-lookup"><span data-stu-id="817ce-109">**Capacity/performance** &ndash; Multiple nodes can process more requests than a single server.</span></span> <span data-ttu-id="817ce-110">O balanceador de carga equilibra a carga de trabalho ao distribuir as solicitações para os nós.</span><span class="sxs-lookup"><span data-stu-id="817ce-110">The load balancer balances the workload by distributing requests to the nodes.</span></span>
* <span data-ttu-id="817ce-111">**Escalabilidade** &ndash; quando a necessidade da capacidade for maior ou menor, o número de nós ativos pode ser aumentado ou diminuído para corresponder à carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="817ce-111">**Scalability** &ndash; When more or less capacity is required, the number of active nodes can be increased or decreased to match the workload.</span></span> <span data-ttu-id="817ce-112">Tecnologias de plataforma de web farm, como o [Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/), podem adicionar ou remover nós por solicitação do administrador do sistema ou automaticamente sem a intervenção humana.</span><span class="sxs-lookup"><span data-stu-id="817ce-112">Web farm platform technologies, such as [Azure App Service](https://azure.microsoft.com/services/app-service/), can automatically add or remove nodes at the request of the system administrator or automatically without human intervention.</span></span>
* <span data-ttu-id="817ce-113">**Facilidade de manutenção** &ndash; os nós de um web farm podem contar com um conjunto de serviços compartilhados, o que resulta em um gerenciamento mais fácil do sistema.</span><span class="sxs-lookup"><span data-stu-id="817ce-113">**Maintainability** &ndash; Nodes of a web farm can rely on a set of shared services, which results in easier system management.</span></span> <span data-ttu-id="817ce-114">Por exemplo, os nós de um web farm podem contar com um servidor de banco de dados individual e um local de rede comum para recursos estáticos, como imagens e arquivos para download.</span><span class="sxs-lookup"><span data-stu-id="817ce-114">For example, the nodes of a web farm can rely upon a single database server and a common network location for static resources, such as images and downloadable files.</span></span>

<span data-ttu-id="817ce-115">Este tópico descreve as configurações e dependências para aplicativos ASP.NET Core hospedados em um web farm que conta com recursos compartilhados.</span><span class="sxs-lookup"><span data-stu-id="817ce-115">This topic describes configuration and dependencies for ASP.NET core apps hosted in a web farm that rely upon shared resources.</span></span>

## <a name="general-configuration"></a><span data-ttu-id="817ce-116">Configuração geral</span><span class="sxs-lookup"><span data-stu-id="817ce-116">General configuration</span></span>

<xref:host-and-deploy/index>  
<span data-ttu-id="817ce-117">Aprenda como configurar ambientes de hospedagem e implantar aplicativos ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="817ce-117">Learn how to set up hosting environments and deploy ASP.NET Core apps.</span></span> <span data-ttu-id="817ce-118">Configure um gerenciador de processo em cada nó do web farm para automatizar o início e a reinicialização do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="817ce-118">Configure a process manager on each node of the web farm to automate app starts and restarts.</span></span> <span data-ttu-id="817ce-119">Cada nó requer o tempo de execução do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="817ce-119">Each node requires the ASP.NET Core runtime.</span></span> <span data-ttu-id="817ce-120">Para saber mais, confira os tópicos na área [Hospedar e implantar](xref:host-and-deploy/index) da documentação.</span><span class="sxs-lookup"><span data-stu-id="817ce-120">For more information, see the topics in the [Host and deploy](xref:host-and-deploy/index) area of the documentation.</span></span>

<xref:host-and-deploy/proxy-load-balancer>  
<span data-ttu-id="817ce-121">Saiba mais sobre a configuração para aplicativos hospedados por trás de servidores proxy e balanceadores de carga, o que muitas vezes oculta informações de solicitação importantes.</span><span class="sxs-lookup"><span data-stu-id="817ce-121">Learn about configuration for apps hosted behind proxy servers and load balancers, which often obscure important request information.</span></span>

<xref:host-and-deploy/azure-apps/index>  
<span data-ttu-id="817ce-122">[Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/) é um [serviço de plataforma de computação em nuvem da Microsoft](https://azure.microsoft.com/) para hospedar aplicativos Web, incluindo o ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="817ce-122">[Azure App Service](https://azure.microsoft.com/services/app-service/) is a [Microsoft cloud computing platform service](https://azure.microsoft.com/) for hosting web apps, including ASP.NET Core.</span></span> <span data-ttu-id="817ce-123">O Serviço de Aplicativo é uma plataforma totalmente gerenciada que fornece escalabilidade automática, balanceamento de carga, aplicação de patch e implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="817ce-123">App Service is a fully managed platform that provides automatic scaling, load balancing, patching, and continuous deployment.</span></span>

## <a name="app-data"></a><span data-ttu-id="817ce-124">Dados do aplicativo</span><span class="sxs-lookup"><span data-stu-id="817ce-124">App data</span></span>

<span data-ttu-id="817ce-125">Quando um aplicativo é dimensionado para várias instâncias, pode haver um estado do aplicativo que exija o compartilhamento entre os nós.</span><span class="sxs-lookup"><span data-stu-id="817ce-125">When an app is scaled to multiple instances, there might be app state that requires sharing across nodes.</span></span> <span data-ttu-id="817ce-126">Se o estado for transitório, considere a possibilidade de compartilhar um [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache).</span><span class="sxs-lookup"><span data-stu-id="817ce-126">If the state is transient, consider sharing an [IDistributedCache](/dotnet/api/microsoft.extensions.caching.distributed.idistributedcache).</span></span> <span data-ttu-id="817ce-127">Se o estado compartilhado exigir persistência, considere armazenar o estado compartilhado em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="817ce-127">If the shared state requires persistence, consider storing the shared state in a database.</span></span>

## <a name="required-configuration"></a><span data-ttu-id="817ce-128">Configuração necessária</span><span class="sxs-lookup"><span data-stu-id="817ce-128">Required configuration</span></span>

<span data-ttu-id="817ce-129">O serviço de cache e a proteção de dados exigem uma configuração para aplicativos implantados em um web farm.</span><span class="sxs-lookup"><span data-stu-id="817ce-129">Data Protection and Caching require configuration for apps deployed to a web farm.</span></span>

### <a name="data-protection"></a><span data-ttu-id="817ce-130">Proteção de Dados</span><span class="sxs-lookup"><span data-stu-id="817ce-130">Data Protection</span></span>

<span data-ttu-id="817ce-131">O [sistema de proteção de dados do ASP.NET Core](xref:security/data-protection/introduction) é usado por aplicativos para proteger os dados.</span><span class="sxs-lookup"><span data-stu-id="817ce-131">The [ASP.NET Core Data Protection system](xref:security/data-protection/introduction) is used by apps to protect data.</span></span> <span data-ttu-id="817ce-132">A proteção de dados baseia-se em um conjunto de chaves de criptografia armazenados em um *token de autenticação*.</span><span class="sxs-lookup"><span data-stu-id="817ce-132">Data Protection relies upon a set of cryptographic keys stored in a *key ring*.</span></span> <span data-ttu-id="817ce-133">Quando o sistema de Proteção de dados é inicializado, ele aplica [as configurações padrão](xref:security/data-protection/configuration/default-settings) que armazenam localmente o token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="817ce-133">When the Data Protection system is initialized, it applies [default settings](xref:security/data-protection/configuration/default-settings) that store the key ring locally.</span></span> <span data-ttu-id="817ce-134">Sob a configuração padrão, um token de autenticação exclusivo é armazenado em cada nó do web farm.</span><span class="sxs-lookup"><span data-stu-id="817ce-134">Under the default configuration, a unique key ring is stored on each node of the web farm.</span></span> <span data-ttu-id="817ce-135">Consequentemente, cada nó do web farm não pode descriptografar os dados criptografados por um aplicativo em qualquer outro nó.</span><span class="sxs-lookup"><span data-stu-id="817ce-135">Consequently, each web farm node can't decrypt data that's encrypted by an app on any other node.</span></span> <span data-ttu-id="817ce-136">A configuração padrão normalmente não é adequada para hospedagem de aplicativos em um web farm.</span><span class="sxs-lookup"><span data-stu-id="817ce-136">The default configuration isn't generally appropriate for hosting apps in a web farm.</span></span> <span data-ttu-id="817ce-137">Uma alternativa à implementação de um token de autenticação compartilhado é sempre rotear as solicitações do usuário para o mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="817ce-137">An alternative to implementing a shared key ring is to always route user requests to the same node.</span></span> <span data-ttu-id="817ce-138">Para saber mais sobre a configuração do sistema de Proteção de dados para implantações de web farm, confira <xref:security/data-protection/configuration/overview>.</span><span class="sxs-lookup"><span data-stu-id="817ce-138">For more information on Data Protection system configuration for web farm deployments, see <xref:security/data-protection/configuration/overview>.</span></span>

### <a name="caching"></a><span data-ttu-id="817ce-139">Cache</span><span class="sxs-lookup"><span data-stu-id="817ce-139">Caching</span></span>

<span data-ttu-id="817ce-140">Em um ambiente de web farm, o mecanismo de cache deve compartilhar os itens em cache pelos nós do web farm.</span><span class="sxs-lookup"><span data-stu-id="817ce-140">In a web farm environment, the caching mechanism must share cached items across the web farm's nodes.</span></span> <span data-ttu-id="817ce-141">O serviço de cache deve contar com um cache Redis comum, um banco de dados compartilhado do SQL Server ou uma implementação personalizada de cache que compartilha os itens em cache pelo web farm.</span><span class="sxs-lookup"><span data-stu-id="817ce-141">Caching must either rely upon a common Redis cache, a shared SQL Server database, or a custom caching implementation that shares cached items across the web farm.</span></span> <span data-ttu-id="817ce-142">Para obter mais informações, consulte <xref:performance/caching/distributed>.</span><span class="sxs-lookup"><span data-stu-id="817ce-142">For more information, see <xref:performance/caching/distributed>.</span></span>

## <a name="dependent-components"></a><span data-ttu-id="817ce-143">Componentes dependentes</span><span class="sxs-lookup"><span data-stu-id="817ce-143">Dependent components</span></span>

<span data-ttu-id="817ce-144">Os cenários a seguir não exigem configuração adicional, mas dependem de tecnologias que exigem configurações para web farms.</span><span class="sxs-lookup"><span data-stu-id="817ce-144">The following scenarios don't require additional configuration, but they depend on technologies that require configuration for web farms.</span></span>

| <span data-ttu-id="817ce-145">Cenário</span><span class="sxs-lookup"><span data-stu-id="817ce-145">Scenario</span></span> | <span data-ttu-id="817ce-146">Depende de &hellip;</span><span class="sxs-lookup"><span data-stu-id="817ce-146">Depends on &hellip;</span></span> |
| -------- | ------------------- |
| <span data-ttu-id="817ce-147">Autenticação</span><span class="sxs-lookup"><span data-stu-id="817ce-147">Authentication</span></span> | <span data-ttu-id="817ce-148">Proteção de dados (confira <xref:security/data-protection/configuration/overview>).</span><span class="sxs-lookup"><span data-stu-id="817ce-148">Data Protection (see <xref:security/data-protection/configuration/overview>).</span></span><br><br><span data-ttu-id="817ce-149">Para obter mais informações, consulte <xref:security/authentication/cookie> e <xref:security/cookie-sharing>.</span><span class="sxs-lookup"><span data-stu-id="817ce-149">For more information, see <xref:security/authentication/cookie> and <xref:security/cookie-sharing>.</span></span> |
| <span data-ttu-id="817ce-150">Identidade</span><span class="sxs-lookup"><span data-stu-id="817ce-150">Identity</span></span> | <span data-ttu-id="817ce-151">Configuração e autenticação do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="817ce-151">Authentication and database configuration.</span></span><br><br><span data-ttu-id="817ce-152">Para obter mais informações, consulte <xref:security/authentication/identity>.</span><span class="sxs-lookup"><span data-stu-id="817ce-152">For more information, see <xref:security/authentication/identity>.</span></span> |
| <span data-ttu-id="817ce-153">Session</span><span class="sxs-lookup"><span data-stu-id="817ce-153">Session</span></span> | <span data-ttu-id="817ce-154">Proteção de dados (cookies criptografados) (confira <xref:security/data-protection/configuration/overview>) e cache (confira <xref:performance/caching/distributed>).</span><span class="sxs-lookup"><span data-stu-id="817ce-154">Data Protection (encrypted cookies) (see <xref:security/data-protection/configuration/overview>) and Caching (see <xref:performance/caching/distributed>).</span></span><br><br><span data-ttu-id="817ce-155">Para saber mais, confira [Estado de sessão e aplicativo: estado de sessão](xref:fundamentals/app-state#session-state).</span><span class="sxs-lookup"><span data-stu-id="817ce-155">For more information, see [Session and app state: Session state](xref:fundamentals/app-state#session-state).</span></span> |
| <span data-ttu-id="817ce-156">TempData</span><span class="sxs-lookup"><span data-stu-id="817ce-156">TempData</span></span> | <span data-ttu-id="817ce-157">Proteção de dados (cookies criptografados) (confira <xref:security/data-protection/configuration/overview>) ou sessão (confira [Estado de sessão e aplicativo: estado de sessão](xref:fundamentals/app-state#session-state)).</span><span class="sxs-lookup"><span data-stu-id="817ce-157">Data Protection (encrypted cookies) (see <xref:security/data-protection/configuration/overview>) or Session (see [Session and app state: Session state](xref:fundamentals/app-state#session-state)).</span></span><br><br><span data-ttu-id="817ce-158">Para saber mais, consulte [Estado de sessão e aplicativo: TempData](xref:fundamentals/app-state#tempdata).</span><span class="sxs-lookup"><span data-stu-id="817ce-158">For more information, see [Session and app state: TempData](xref:fundamentals/app-state#tempdata).</span></span> |
| <span data-ttu-id="817ce-159">Antifalsificação</span><span class="sxs-lookup"><span data-stu-id="817ce-159">Anti-forgery</span></span> | <span data-ttu-id="817ce-160">Proteção de dados (confira <xref:security/data-protection/configuration/overview>).</span><span class="sxs-lookup"><span data-stu-id="817ce-160">Data Protection (see <xref:security/data-protection/configuration/overview>).</span></span><br><br><span data-ttu-id="817ce-161">Para obter mais informações, consulte <xref:security/anti-request-forgery>.</span><span class="sxs-lookup"><span data-stu-id="817ce-161">For more information, see <xref:security/anti-request-forgery>.</span></span> |

## <a name="troubleshoot"></a><span data-ttu-id="817ce-162">Solução de problemas</span><span class="sxs-lookup"><span data-stu-id="817ce-162">Troubleshoot</span></span>

<span data-ttu-id="817ce-163">Quando a proteção de dados ou cache não está configurada para um ambiente de web farm, erros intermitentes ocorrem quando as solicitações são processadas.</span><span class="sxs-lookup"><span data-stu-id="817ce-163">When Data Protection or Caching isn't configured for a web farm environment, intermittent errors occur when requests are processed.</span></span> <span data-ttu-id="817ce-164">Isso acontece porque os nós não compartilham os mesmos recursos e as solicitações do usuário não são sempre roteadas para o mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="817ce-164">This occurs because nodes don't share the same resources and user requests aren't always routed back to the same node.</span></span>

<span data-ttu-id="817ce-165">Considere um usuário que entra no aplicativo usando a autenticação de cookie.</span><span class="sxs-lookup"><span data-stu-id="817ce-165">Consider a user who signs into the app using cookie authentication.</span></span> <span data-ttu-id="817ce-166">O usuário entra no aplicativo em um nó do web farm.</span><span class="sxs-lookup"><span data-stu-id="817ce-166">The user signs into the app on one web farm node.</span></span> <span data-ttu-id="817ce-167">Se a sua próxima solicitação chegar ao mesmo nó no qual ele se conectou, o aplicativo consegue descriptografar o cookie de autenticação e permite o acesso ao recurso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="817ce-167">If their next request arrives at the same node where they signed in, the app is able to decrypt the authentication cookie and allows access to the app's resource.</span></span> <span data-ttu-id="817ce-168">Se a sua próxima solicitação chegar em um nó diferente, o aplicativo não consegue descriptografar o cookie de autenticação a partir do nó em que o usuário entrou e a autorização do recurso solicitado falhará.</span><span class="sxs-lookup"><span data-stu-id="817ce-168">If their next request arrives at a different node, the app can't decrypt the authentication cookie from the node where the user signed in, and authorization for the requested resource fails.</span></span>

<span data-ttu-id="817ce-169">Quando qualquer um dos seguintes sintomas ocorrem **de forma intermitente**, o problema normalmente é rastreado a configuração incorreta de proteção de dados ou cache para um ambiente de web farm:</span><span class="sxs-lookup"><span data-stu-id="817ce-169">When any of the following symptoms occur **intermittently**, the problem is usually traced to improper Data Protection or Caching configuration for a web farm environment:</span></span>

* <span data-ttu-id="817ce-170">Quebras de autenticação &ndash; o cookie de autenticação está configurado incorretamente ou não pode ser descriptografado.</span><span class="sxs-lookup"><span data-stu-id="817ce-170">Authentication breaks &ndash; The authentication cookie is misconfigured or can't be decrypted.</span></span> <span data-ttu-id="817ce-171">Falha de login OpenIdConnect ou OAuth (Facebook, Microsoft, Twitter) com o erro "Falha de correlação".</span><span class="sxs-lookup"><span data-stu-id="817ce-171">OAuth (Facebook, Microsoft, Twitter) or OpenIdConnect logins fail with the error "Correlation failed."</span></span>
* <span data-ttu-id="817ce-172">Quebras de autorização &ndash; a identidade foi perdida.</span><span class="sxs-lookup"><span data-stu-id="817ce-172">Authorization breaks &ndash; Identity is lost.</span></span>
* <span data-ttu-id="817ce-173">O estado de sessão perde os dados.</span><span class="sxs-lookup"><span data-stu-id="817ce-173">Session state loses data.</span></span>
* <span data-ttu-id="817ce-174">Os itens em cache desaparecem.</span><span class="sxs-lookup"><span data-stu-id="817ce-174">Cached items disappear.</span></span>
* <span data-ttu-id="817ce-175">O TempData falhará.</span><span class="sxs-lookup"><span data-stu-id="817ce-175">TempData fails.</span></span>
* <span data-ttu-id="817ce-176">Os POSTs falham &ndash; a verificação antifalsificação falhará.</span><span class="sxs-lookup"><span data-stu-id="817ce-176">POSTs fail &ndash; The anti-forgery check fails.</span></span>

<span data-ttu-id="817ce-177">Para saber mais sobre a configuração de Proteção de dados para implantações de web farm, confira <xref:security/data-protection/configuration/overview>.</span><span class="sxs-lookup"><span data-stu-id="817ce-177">For more information on Data Protection configuration for web farm deployments, see <xref:security/data-protection/configuration/overview>.</span></span> <span data-ttu-id="817ce-178">Para saber mais sobre a configuração de cache para implantações de web farm, confira <xref:performance/caching/distributed>.</span><span class="sxs-lookup"><span data-stu-id="817ce-178">For more information on Caching configuration for web farm deployments, see <xref:performance/caching/distributed>.</span></span>