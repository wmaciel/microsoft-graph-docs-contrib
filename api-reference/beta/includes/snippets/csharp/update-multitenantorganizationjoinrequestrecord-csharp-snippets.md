---
description: "Automatically generated file. DO NOT MODIFY"
---

```csharp

// Code snippets are only available for the latest version. Current version is 5.x

var graphClient = new GraphServiceClient(requestAdapter);

var requestBody = new MultiTenantOrganizationJoinRequestRecord
{
	AddedByTenantId = "1fd6544e-e994-4de2-9f1b-787b51c7d325",
};
var result = await graphClient.TenantRelationships.MultiTenantOrganization.JoinRequest.PatchAsync(requestBody);


```