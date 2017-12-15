---
uid: web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
title: Usando CascadingDropDown com um banco de dados (c#) | Microsoft Docs
author: wenz
description: "O controle CascadingDropDown AJAX Control Toolkit estende um controle DropDownList para que as alterações em uma carga de DropDownList associados valores em anoth..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 06/02/2008
ms.topic: article
ms.assetid: 684f0c28-a490-4e5b-b5e5-5dfb77464b49
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/cascadingdropdown/using-cascadingdropdown-with-a-database-cs
msc.type: authoredcontent
ms.openlocfilehash: 86d6b62259573433cff7054d50cc299da9e4f372
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
<a name="using-cascadingdropdown-with-a-database-c"></a><span data-ttu-id="71594-103">Usando CascadingDropDown com um banco de dados (c#)</span><span class="sxs-lookup"><span data-stu-id="71594-103">Using CascadingDropDown with a Database (C#)</span></span>
====================
<span data-ttu-id="71594-104">por [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="71594-104">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="71594-105">[Baixar o código](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) ou [baixar PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span><span class="sxs-lookup"><span data-stu-id="71594-105">[Download Code](http://download.microsoft.com/download/9/0/7/907760b1-2c60-4f81-aeb6-ca416a573b0d/cascadingdropdown1.cs.zip) or [Download PDF](http://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/cascadingdropdown1CS.pdf)</span></span>

> <span data-ttu-id="71594-106">O controle CascadingDropDown AJAX Control Toolkit estende um controle DropDownList para que as alterações em uma carga de DropDownList associados valores em outra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="71594-106">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="71594-107">Em ordem para este trabalho, um serviço web especial deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="71594-107">In order for this to work, a special web service must be created.</span></span>


## <a name="overview"></a><span data-ttu-id="71594-108">Visão Geral</span><span class="sxs-lookup"><span data-stu-id="71594-108">Overview</span></span>

<span data-ttu-id="71594-109">O controle CascadingDropDown AJAX Control Toolkit estende um controle DropDownList para que as alterações em uma carga de DropDownList associados valores em outra DropDownList.</span><span class="sxs-lookup"><span data-stu-id="71594-109">The CascadingDropDown control in the AJAX Control Toolkit extends a DropDownList control so that changes in one DropDownList loads associated values in another DropDownList.</span></span> <span data-ttu-id="71594-110">(Por exemplo, uma lista fornece uma lista de nós estados e lista seguinte é então preenchida com cidades nesse estado.) Em ordem para este trabalho, um serviço web especial deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="71594-110">(For instance, one list provides a list of US states, and the next list is then filled with major cities in that state.) In order for this to work, a special web service must be created.</span></span>

## <a name="steps"></a><span data-ttu-id="71594-111">Etapas</span><span class="sxs-lookup"><span data-stu-id="71594-111">Steps</span></span>

<span data-ttu-id="71594-112">Em primeiro lugar, uma fonte de dados é necessária.</span><span class="sxs-lookup"><span data-stu-id="71594-112">First of all, a data source is required.</span></span> <span data-ttu-id="71594-113">Este exemplo usa o banco de dados AdventureWorks e o Microsoft SQL Server 2005 Express Edition.</span><span class="sxs-lookup"><span data-stu-id="71594-113">This sample uses the AdventureWorks database and the Microsoft SQL Server 2005 Express Edition.</span></span> <span data-ttu-id="71594-114">O banco de dados é uma parte opcional de uma instalação do Visual Studio (incluindo a edição express) e também está disponível como um download separado em [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span><span class="sxs-lookup"><span data-stu-id="71594-114">The database is an optional part of a Visual Studio installation (including express edition) and is also available as a separate download under [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064).</span></span> <span data-ttu-id="71594-115">O banco de dados AdventureWorks faz parte dos bancos de dados de exemplo e exemplos do SQL Server 2005 (download em [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span><span class="sxs-lookup"><span data-stu-id="71594-115">The AdventureWorks database is part of the SQL Server 2005 Samples and Sample Databases (download at [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)).</span></span> <span data-ttu-id="71594-116">A maneira mais fácil de configurar o banco de dados é usar o Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx? FamilyID = c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang = en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) e conecte o `AdventureWorks.mdf` arquivo de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="71594-116">The easiest way to set the database up is to use the Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) and attach the `AdventureWorks.mdf` database file.</span></span>

<span data-ttu-id="71594-117">Para este exemplo, vamos supor que a instância do SQL Server 2005 Express Edition é chamada `SQLEXPRESS` e reside no mesmo computador que o servidor web; isso também é a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="71594-117">For this sample, we assume that the instance of the SQL Server 2005 Express Edition is called `SQLEXPRESS` and resides on the same machine as the web server; this is also the default setup.</span></span> <span data-ttu-id="71594-118">Se sua configuração for diferente, você precisa se adaptar as informações de conexão para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="71594-118">If your setup differs, you have to adapt the connection information for the database.</span></span>

<span data-ttu-id="71594-119">Para ativar a funcionalidade do ASP.NET AJAX e o Kit de ferramentas de controle, o `ScriptManager` controle deve ser colocado em qualquer lugar na página (mas dentro do &lt; `form` &gt; elemento):</span><span class="sxs-lookup"><span data-stu-id="71594-119">In order to activate the functionality of ASP.NET AJAX and the Control Toolkit, the `ScriptManager` control must be put anywhere on the page (but within the &lt;`form`&gt; element):</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample1.aspx)]

<span data-ttu-id="71594-120">Na próxima etapa, são necessários dois controles DropDownList.</span><span class="sxs-lookup"><span data-stu-id="71594-120">In the next step, two DropDownList controls are required.</span></span> <span data-ttu-id="71594-121">Neste exemplo, usamos as fornecedor e informações de contato da AdventureWorks, portanto, podemos criar uma lista de fornecedores disponíveis e uma para os contatos disponíveis:</span><span class="sxs-lookup"><span data-stu-id="71594-121">In this sample, we use the vendor and contact information from AdventureWorks, thus we create one list for the available vendors and one for the available contacts:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample2.aspx)]

<span data-ttu-id="71594-122">Em seguida, dois extensores de CascadingDropDown devem ser adicionados à página.</span><span class="sxs-lookup"><span data-stu-id="71594-122">Then, two CascadingDropDown extenders must be added to the page.</span></span> <span data-ttu-id="71594-123">Um preenche a primeira lista (fornecedores) e o outro um preenche a segunda lista (contatos).</span><span class="sxs-lookup"><span data-stu-id="71594-123">One fills the first (vendors) list, and the other one fills the second (contacts) list.</span></span> <span data-ttu-id="71594-124">Configure os seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="71594-124">The following attributes must be set:</span></span>

- <span data-ttu-id="71594-125">`ServicePath`: A URL de um serviço web fornecendo as entradas da lista</span><span class="sxs-lookup"><span data-stu-id="71594-125">`ServicePath`: URL of a web service delivering the list entries</span></span>
- <span data-ttu-id="71594-126">`ServiceMethod`: Método da web fornecendo as entradas da lista</span><span class="sxs-lookup"><span data-stu-id="71594-126">`ServiceMethod`: Web method delivering the list entries</span></span>
- <span data-ttu-id="71594-127">`TargetControlID`: A ID da lista suspensa</span><span class="sxs-lookup"><span data-stu-id="71594-127">`TargetControlID`: ID of the dropdown list</span></span>
- <span data-ttu-id="71594-128">`Category`: Informações de categoria que são enviadas ao método da web quando chamado</span><span class="sxs-lookup"><span data-stu-id="71594-128">`Category`: Category information that is submitted to the web method when called</span></span>
- <span data-ttu-id="71594-129">`PromptText`: Texto exibido quando assincronamente Carregando dados de lista do servidor</span><span class="sxs-lookup"><span data-stu-id="71594-129">`PromptText`: Text displayed when asynchronously loading list data from the server</span></span>
- <span data-ttu-id="71594-130">`ParentControlID`: (opcional) pai suspensa lista que o carregamento da lista atual de gatilhos</span><span class="sxs-lookup"><span data-stu-id="71594-130">`ParentControlID`: (optional) parent dropdown list that triggers loading of the current list</span></span>

<span data-ttu-id="71594-131">Dependendo da linguagem de programação usada, o nome do serviço da web em questão é alterado, mas todos os outros valores de atributo são os mesmos.</span><span class="sxs-lookup"><span data-stu-id="71594-131">Depending on the programming language used, the name of the web service in question changes, but all other attribute values are the same.</span></span> <span data-ttu-id="71594-132">Aqui está o elemento CascadingDropDown para a primeira lista suspensa:</span><span class="sxs-lookup"><span data-stu-id="71594-132">Here is the CascadingDropDown element for the first dropdown list:</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample3.aspx)]

<span data-ttu-id="71594-133">Os extensores de controle para a segunda lista precisam definir o `ParentControlID` atributo para que a seleção de uma entrada nos gatilhos de lista de fornecedores carregar associados elementos na lista de contatos.</span><span class="sxs-lookup"><span data-stu-id="71594-133">The control extenders for the second list need to set the `ParentControlID` attribute so that selecting an entry in the vendors list triggers loading associated elements in the contacts list.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample4.aspx)]

<span data-ttu-id="71594-134">O trabalho real, em seguida, é feito no serviço da web, que é definido da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="71594-134">The actual work is then done in the web service, which is set up as follows.</span></span> <span data-ttu-id="71594-135">Observe que o `[ScriptService]` atributo é usado, caso contrário, o ASP.NET AJAX não é possível criar o proxy JavaScript para acessar os métodos da web do código de script do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="71594-135">Note that the `[ScriptService]` attribute is used, otherwise ASP.NET AJAX cannot create the JavaScript proxy to access the web methods from client-side script code.</span></span>

[!code-aspx[Main](using-cascadingdropdown-with-a-database-cs/samples/sample5.aspx)]

<span data-ttu-id="71594-136">A assinatura dos métodos de web chamado pelo CascadingDropDown é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="71594-136">The signature of the web methods called by CascadingDropDown is as follows:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample6.cs)]

<span data-ttu-id="71594-137">Para que o valor de retorno deve ser uma matriz do tipo `CascadingDropDownNameValue` que é definido pelo Kit de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="71594-137">So the return value must be an array of type `CascadingDropDownNameValue` which is defined by the Control Toolkit.</span></span> <span data-ttu-id="71594-138">O `GetVendors()` método é muito fácil de implementar: O código se conecta ao banco de dados AdventureWorks e consulta os 25 primeiros fornecedores.</span><span class="sxs-lookup"><span data-stu-id="71594-138">The `GetVendors()` method is quite easy to implement: The code connects to the AdventureWorks database and queries the first 25 vendors.</span></span> <span data-ttu-id="71594-139">O primeiro parâmetro de `CascadingDropDownNameValue` construtor é a legenda da entrada de lista, o outro valor (atributo de valor em HTML &lt; `option` &gt; elemento).</span><span class="sxs-lookup"><span data-stu-id="71594-139">The first parameter in the `CascadingDropDownNameValue` constructor is the caption of the list entry, the second one its value (value attribute in HTML's &lt;`option`&gt; element).</span></span> <span data-ttu-id="71594-140">Aqui está o código:</span><span class="sxs-lookup"><span data-stu-id="71594-140">Here is the code:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample7.cs)]

<span data-ttu-id="71594-141">Obtendo os contatos associados para um fornecedor (nome do método: `GetContactsForVendor()`) é um pouco mais complicado.</span><span class="sxs-lookup"><span data-stu-id="71594-141">Getting the associated contacts for a vendor (method name: `GetContactsForVendor()`) is a bit trickier.</span></span> <span data-ttu-id="71594-142">Em primeiro lugar, o fornecedor que foi selecionado na lista suspensa primeiro deve ser determinado.</span><span class="sxs-lookup"><span data-stu-id="71594-142">First of all, the vendor which has been selected in the first dropdown list must be determined.</span></span> <span data-ttu-id="71594-143">O Kit de ferramentas define um método auxiliar para a tarefa: O `ParseKnownCategoryValuesString()` método retorna um `StringDictionary` elemento com os dados da lista suspensa:</span><span class="sxs-lookup"><span data-stu-id="71594-143">The Control Toolkit defines a helper method for that task: The `ParseKnownCategoryValuesString()` method returns a `StringDictionary` element with the dropdown data:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample8.cs)]

<span data-ttu-id="71594-144">Por motivos de segurança, esses dados devem ser validados primeiro.</span><span class="sxs-lookup"><span data-stu-id="71594-144">For security reasons, this data must be validated first.</span></span> <span data-ttu-id="71594-145">Portanto, se houver uma entrada de fornecedor (porque o `Category` propriedade do primeiro elemento CascadingDropDown está definida como `"Vendor"`), a ID do fornecedor selecionado pode ser recuperada:</span><span class="sxs-lookup"><span data-stu-id="71594-145">So if there is a Vendor entry (because the `Category` property of the first CascadingDropDown element is set to `"Vendor"`), the ID of the selected vendor may be retrieved:</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample9.cs)]

<span data-ttu-id="71594-146">O restante do método é bastante direta, então.</span><span class="sxs-lookup"><span data-stu-id="71594-146">The rest of the method is fairly straight-forward, then.</span></span> <span data-ttu-id="71594-147">ID do fornecedor é usado como um parâmetro para uma consulta SQL que recupera todos os contatos associados para esse fornecedor.</span><span class="sxs-lookup"><span data-stu-id="71594-147">The vendor's ID is used as a parameter for an SQL query that retrieves all associated contacts for that vendor.</span></span> <span data-ttu-id="71594-148">Uma vez, o método retorna uma matriz do tipo `CascadingDropDownNameValue`.</span><span class="sxs-lookup"><span data-stu-id="71594-148">Once again, the method returns an array of type `CascadingDropDownNameValue`.</span></span>

[!code-csharp[Main](using-cascadingdropdown-with-a-database-cs/samples/sample10.cs)]

<span data-ttu-id="71594-149">Carregar a página do ASP.NET, e depois de um curto tempo a lista de fornecedores é preenchida com 25 entradas.</span><span class="sxs-lookup"><span data-stu-id="71594-149">Load the ASP.NET page, and after a short while the vendor list is filled with 25 entries.</span></span> <span data-ttu-id="71594-150">Selecione uma entrada e observe como a segunda lista suspensa é preenchida com dados.</span><span class="sxs-lookup"><span data-stu-id="71594-150">Pick one entry and notice how the second dropdown list is filled with data.</span></span>


<span data-ttu-id="71594-151">[![A primeira lista é preenchida automaticamente](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="71594-151">[![The first list is filled automatically](using-cascadingdropdown-with-a-database-cs/_static/image2.png)](using-cascadingdropdown-with-a-database-cs/_static/image1.png)</span></span>

<span data-ttu-id="71594-152">A primeira lista é preenchida automaticamente ([clique para exibir a imagem em tamanho normal](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="71594-152">The first list is filled automatically ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image3.png))</span></span>


<span data-ttu-id="71594-153">[![Na segunda lista é preenchida de acordo com a seleção na primeira lista](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="71594-153">[![The second list is filled according to the selection in the first list](using-cascadingdropdown-with-a-database-cs/_static/image5.png)](using-cascadingdropdown-with-a-database-cs/_static/image4.png)</span></span>

<span data-ttu-id="71594-154">Na segunda lista é preenchida de acordo com a seleção na primeira lista ([clique para exibir a imagem em tamanho normal](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="71594-154">The second list is filled according to the selection in the first list ([Click to view full-size image](using-cascadingdropdown-with-a-database-cs/_static/image6.png))</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="71594-155">[Anterior](filling-a-list-using-cascadingdropdown-cs.md)
[Próximo](presetting-list-entries-with-cascadingdropdown-cs.md)</span><span class="sxs-lookup"><span data-stu-id="71594-155">[Previous](filling-a-list-using-cascadingdropdown-cs.md)
[Next](presetting-list-entries-with-cascadingdropdown-cs.md)</span></span>