---
editable: false
---

# FederationService

A set of methods for managing federations.

| Call | Description |
| --- | --- |
| [Get](#Get) | Returns the specified federation. |
| [List](#List) | Retrieves the list of federations in the specified folder. |
| [Create](#Create) | Creates a federation in the specified folder. |
| [Update](#Update) | Updates the specified federation. |
| [Delete](#Delete) | Deletes the specified federation. |
| [AddUserAccounts](#AddUserAccounts) | Adds users to the specified federation. |
| [ListOperations](#ListOperations) | Lists operations for the specified federation. |

## Calls FederationService {#calls}

## Get {#Get}

Returns the specified federation. <br>To get the list of available federations, make a [List](#List) request.

**rpc Get ([GetFederationRequest](#GetFederationRequest)) returns ([Federation](#Federation))**

### GetFederationRequest {#GetFederationRequest}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation to return. To get the federation ID, make a [FederationService.List](#List) request. The maximum string length in characters is 50.


### Federation {#Federation}

Field | Description
--- | ---
id | **string**<br>Required. ID of the federation.  The maximum string length in characters is 50.
folder_id | **string**<br>Required. ID of the folder that the federation belongs to.  The maximum string length in characters is 50.
name | **string**<br>Required. Name of the federation.  Value must match the regular expression ` |[a-z][-a-z0-9]{1,61}[a-z0-9] `.
description | **string**<br>Description of the federation. The maximum string length in characters is 256.
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
cookie_max_age | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**<br>Browser cookie lifetime in seconds. If the cookie is still valid, the management console authenticates the user immediately and redirects them to the home page. Acceptable values are 10m to 12h, inclusive.
auto_create_account_on_login | **bool**<br>Add new users automatically on successful authentication. The user will get the `resource-manager.clouds.member` role automatically, but you need to grant other roles to them. <br>If the value is `false`, users who aren't added to the cloud can't log in, even if they have authenticated on your server. 
issuer | **string**<br>Required. ID of the IdP server to be used for authentication. The IdP server also responds to IAM with this ID after the user authenticates.  The maximum string length in characters is 8000.
sso_binding | enum **BindingType**<br>Single sign-on endpoint binding type. Most Identity Providers support the `POST` binding type. <br>SAML Binding is a mapping of a SAML protocol message onto standard messaging formats and/or communications protocols. <ul><li>`POST`: HTTP POST binding.</li><li>`REDIRECT`: HTTP redirect binding.</li><li>`ARTIFACT`: HTTP artifact binding.</li><ul/>
sso_url | **string**<br>Required. Single sign-on endpoint URL. Specify the link to the IdP login page here.  The maximum string length in characters is 8000.


## List {#List}

Retrieves the list of federations in the specified folder.

**rpc List ([ListFederationsRequest](#ListFederationsRequest)) returns ([ListFederationsResponse](#ListFederationsResponse))**

### ListFederationsRequest {#ListFederationsRequest}

Field | Description
--- | ---
scope | **oneof:** `cloud_id` or `folder_id`<br>
&nbsp;&nbsp;cloud_id | **string**<br>ID of the cloud to list federations in. To get the cloud ID, make a [yandex.cloud.resourcemanager.v1.CloudService.List](/docs/resource-manager/grpc/cloud_service#List) request. The maximum string length in characters is 50.
&nbsp;&nbsp;folder_id | **string**<br>ID of the folder to list federations in. To get the folder ID, make a [yandex.cloud.resourcemanager.v1.FolderService.List](/docs/resource-manager/grpc/folder_service#List) request. The maximum string length in characters is 50.
page_size | **int64**<br>The maximum number of results per page to return. If the number of available results is larger than `page_size`, the service returns a [ListFederationsResponse.next_page_token](#ListFederationsResponse) that can be used to get the next page of results in subsequent list requests. Default value: 100 Acceptable values are 0 to 1000, inclusive.
page_token | **string**<br>Page token. To get the next page of results, set `page_token` to the [ListFederationsResponse.next_page_token](#ListFederationsResponse) returned by a previous list request. The maximum string length in characters is 50.
filter | **string**<br><ol><li>The field name. Currently you can use filtering only on the [Federation.name](#Federation1) field. </li><li>An operator. Can be either `=` or `!=` for single values, `IN` or `NOT IN` for lists of values. </li><li>The value. Must be 3-63 characters long and match the regular expression `^[a-z][-a-z0-9]{1,61}[a-z0-9]$`.</li></ol> The maximum string length in characters is 1000.


### ListFederationsResponse {#ListFederationsResponse}

Field | Description
--- | ---
federations[] | **[Federation](#Federation1)**<br>List of federations. 
next_page_token | **string**<br>This token allows you to get the next page of results for list requests. If the number of results is larger than [ListFederationsRequest.page_size](#ListFederationsRequest1), use the `next_page_token` as the value for the [ListFederationsRequest.page_token](#ListFederationsRequest1) query parameter in the next list request. Each subsequent list request will have its own `next_page_token` to continue paging through the results. 


### Federation {#Federation}

Field | Description
--- | ---
id | **string**<br>Required. ID of the federation.  The maximum string length in characters is 50.
folder_id | **string**<br>Required. ID of the folder that the federation belongs to.  The maximum string length in characters is 50.
name | **string**<br>Required. Name of the federation.  Value must match the regular expression ` |[a-z][-a-z0-9]{1,61}[a-z0-9] `.
description | **string**<br>Description of the federation. The maximum string length in characters is 256.
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
cookie_max_age | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**<br>Browser cookie lifetime in seconds. If the cookie is still valid, the management console authenticates the user immediately and redirects them to the home page. Acceptable values are 10m to 12h, inclusive.
auto_create_account_on_login | **bool**<br>Add new users automatically on successful authentication. The user will get the `resource-manager.clouds.member` role automatically, but you need to grant other roles to them. <br>If the value is `false`, users who aren't added to the cloud can't log in, even if they have authenticated on your server. 
issuer | **string**<br>Required. ID of the IdP server to be used for authentication. The IdP server also responds to IAM with this ID after the user authenticates.  The maximum string length in characters is 8000.
sso_binding | enum **BindingType**<br>Single sign-on endpoint binding type. Most Identity Providers support the `POST` binding type. <br>SAML Binding is a mapping of a SAML protocol message onto standard messaging formats and/or communications protocols. <ul><li>`POST`: HTTP POST binding.</li><li>`REDIRECT`: HTTP redirect binding.</li><li>`ARTIFACT`: HTTP artifact binding.</li><ul/>
sso_url | **string**<br>Required. Single sign-on endpoint URL. Specify the link to the IdP login page here.  The maximum string length in characters is 8000.


## Create {#Create}

Creates a federation in the specified folder.

**rpc Create ([CreateFederationRequest](#CreateFederationRequest)) returns ([operation.Operation](#Operation))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[CreateFederationMetadata](#CreateFederationMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[Federation](#Federation2)<br>

### CreateFederationRequest {#CreateFederationRequest}

Field | Description
--- | ---
folder_id | **string**<br>ID of the folder to create a federation in. To get the folder ID, make a [yandex.cloud.resourcemanager.v1.FolderService.List](/docs/resource-manager/grpc/folder_service#List) request. The maximum string length in characters is 50.
name | **string**<br>Name of the federation. The name must be unique within the cloud. Value must match the regular expression ` [a-z]([-a-z0-9]{0,61}[a-z0-9])? `.
description | **string**<br>Description of the federation. The maximum string length in characters is 256.
cookie_max_age | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**<br>Browser cookie lifetime in seconds. If the cookie is still valid, the management console authenticates the user immediately and redirects them to the home page. The default value is `8h`. Acceptable values are 10m to 12h, inclusive.
auto_create_account_on_login | **bool**<br>Add new users automatically on successful authentication. The user will get the `resource-manager.clouds.member` role automatically, but you need to grant other roles to them. <br>If the value is `false`, users who aren't added to the cloud can't log in, even if they have authenticated on your server. 
issuer | **string**<br>Required. ID of the IdP server to be used for authentication. The IdP server also responds to IAM with this ID after the user authenticates.  The maximum string length in characters is 8000.
sso_binding | enum **BindingType**<br>Single sign-on endpoint binding type. Most Identity Providers support the `POST` binding type. <br>SAML Binding is a mapping of a SAML protocol message onto standard messaging formats and/or communications protocols. <ul><li>`POST`: HTTP POST binding.</li><li>`REDIRECT`: HTTP redirect binding.</li><li>`ARTIFACT`: HTTP artifact binding.</li><ul/>
sso_url | **string**<br>Required. Single sign-on endpoint URL. Specify the link to the IdP login page here.  The maximum string length in characters is 8000.


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[CreateFederationMetadata](#CreateFederationMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[Federation](#Federation2)>**<br>if operation finished successfully. 


### CreateFederationMetadata {#CreateFederationMetadata}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation that is being created. 


### Federation {#Federation}

Field | Description
--- | ---
id | **string**<br>Required. ID of the federation.  The maximum string length in characters is 50.
folder_id | **string**<br>Required. ID of the folder that the federation belongs to.  The maximum string length in characters is 50.
name | **string**<br>Required. Name of the federation.  Value must match the regular expression ` |[a-z][-a-z0-9]{1,61}[a-z0-9] `.
description | **string**<br>Description of the federation. The maximum string length in characters is 256.
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
cookie_max_age | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**<br>Browser cookie lifetime in seconds. If the cookie is still valid, the management console authenticates the user immediately and redirects them to the home page. Acceptable values are 10m to 12h, inclusive.
auto_create_account_on_login | **bool**<br>Add new users automatically on successful authentication. The user will get the `resource-manager.clouds.member` role automatically, but you need to grant other roles to them. <br>If the value is `false`, users who aren't added to the cloud can't log in, even if they have authenticated on your server. 
issuer | **string**<br>Required. ID of the IdP server to be used for authentication. The IdP server also responds to IAM with this ID after the user authenticates.  The maximum string length in characters is 8000.
sso_binding | enum **BindingType**<br>Single sign-on endpoint binding type. Most Identity Providers support the `POST` binding type. <br>SAML Binding is a mapping of a SAML protocol message onto standard messaging formats and/or communications protocols. <ul><li>`POST`: HTTP POST binding.</li><li>`REDIRECT`: HTTP redirect binding.</li><li>`ARTIFACT`: HTTP artifact binding.</li><ul/>
sso_url | **string**<br>Required. Single sign-on endpoint URL. Specify the link to the IdP login page here.  The maximum string length in characters is 8000.


## Update {#Update}

Updates the specified federation.

**rpc Update ([UpdateFederationRequest](#UpdateFederationRequest)) returns ([operation.Operation](#Operation1))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[UpdateFederationMetadata](#UpdateFederationMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[Federation](#Federation3)<br>

### UpdateFederationRequest {#UpdateFederationRequest}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation to update. To get the federation ID, make a [FederationService.List](#List) request. The maximum string length in characters is 50.
update_mask | **[google.protobuf.FieldMask](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/field-mask)**<br>Field mask that specifies which fields of the federation are going to be updated. 
name | **string**<br>Name of the federation. The name must be unique within the cloud. Value must match the regular expression ` |[a-z]([-a-z0-9]{0,61}[a-z0-9])? `.
description | **string**<br>Description of the federation. The maximum string length in characters is 256.
cookie_max_age | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**<br>Browser cookie lifetime in seconds. If the cookie is still valid, the management console authenticates the user immediately and redirects them to the home page. The default value is `8h`. Acceptable values are 10m to 12h, inclusive.
auto_create_account_on_login | **bool**<br>Add new users automatically on successful authentication. The user will get the `resource-manager.clouds.member` role automatically, but you need to grant other roles to them. <br>If the value is `false`, users who aren't added to the cloud can't log in, even if they have authenticated on your server. 
issuer | **string**<br>Required. ID of the IdP server to be used for authentication. The IdP server also responds to IAM with this ID after the user authenticates.  The maximum string length in characters is 8000.
sso_binding | enum **BindingType**<br>Single sign-on endpoint binding type. Most Identity Providers support the `POST` binding type. <br>SAML Binding is a mapping of a SAML protocol message onto standard messaging formats and/or communications protocols. <ul><li>`POST`: HTTP POST binding.</li><li>`REDIRECT`: HTTP redirect binding.</li><li>`ARTIFACT`: HTTP artifact binding.</li><ul/>
sso_url | **string**<br>Required. Single sign-on endpoint URL. Specify the link to the IdP login page here.  The maximum string length in characters is 8000.


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[UpdateFederationMetadata](#UpdateFederationMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[Federation](#Federation3)>**<br>if operation finished successfully. 


### UpdateFederationMetadata {#UpdateFederationMetadata}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation that is being updated. 


### Federation {#Federation}

Field | Description
--- | ---
id | **string**<br>Required. ID of the federation.  The maximum string length in characters is 50.
folder_id | **string**<br>Required. ID of the folder that the federation belongs to.  The maximum string length in characters is 50.
name | **string**<br>Required. Name of the federation.  Value must match the regular expression ` |[a-z][-a-z0-9]{1,61}[a-z0-9] `.
description | **string**<br>Description of the federation. The maximum string length in characters is 256.
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
cookie_max_age | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**<br>Browser cookie lifetime in seconds. If the cookie is still valid, the management console authenticates the user immediately and redirects them to the home page. Acceptable values are 10m to 12h, inclusive.
auto_create_account_on_login | **bool**<br>Add new users automatically on successful authentication. The user will get the `resource-manager.clouds.member` role automatically, but you need to grant other roles to them. <br>If the value is `false`, users who aren't added to the cloud can't log in, even if they have authenticated on your server. 
issuer | **string**<br>Required. ID of the IdP server to be used for authentication. The IdP server also responds to IAM with this ID after the user authenticates.  The maximum string length in characters is 8000.
sso_binding | enum **BindingType**<br>Single sign-on endpoint binding type. Most Identity Providers support the `POST` binding type. <br>SAML Binding is a mapping of a SAML protocol message onto standard messaging formats and/or communications protocols. <ul><li>`POST`: HTTP POST binding.</li><li>`REDIRECT`: HTTP redirect binding.</li><li>`ARTIFACT`: HTTP artifact binding.</li><ul/>
sso_url | **string**<br>Required. Single sign-on endpoint URL. Specify the link to the IdP login page here.  The maximum string length in characters is 8000.


## Delete {#Delete}

Deletes the specified federation.

**rpc Delete ([DeleteFederationRequest](#DeleteFederationRequest)) returns ([operation.Operation](#Operation2))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[DeleteFederationMetadata](#DeleteFederationMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty)<br>

### DeleteFederationRequest {#DeleteFederationRequest}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation to delete. To get the federation ID, make a [FederationService.List](#List) request. The maximum string length in characters is 50.


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[DeleteFederationMetadata](#DeleteFederationMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty)>**<br>if operation finished successfully. 


### DeleteFederationMetadata {#DeleteFederationMetadata}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation that is being deleted. 


## AddUserAccounts {#AddUserAccounts}

Adds users to the specified federation.

**rpc AddUserAccounts ([AddFederatedUserAccountsRequest](#AddFederatedUserAccountsRequest)) returns ([operation.Operation](#Operation3))**

Metadata and response of Operation:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.metadata:[AddFederatedUserAccountsMetadata](#AddFederatedUserAccountsMetadata)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;Operation.response:[AddFederatedUserAccountsResponse](#AddFederatedUserAccountsResponse)<br>

### AddFederatedUserAccountsRequest {#AddFederatedUserAccountsRequest}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation to add users. The maximum string length in characters is 50.
name_ids[] | **string**<br>Name IDs returned by the Identity Provider (IdP) on successful authentication. These may be UPNs or user email addresses. The maximum string length in characters for each value is 1000.


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[AddFederatedUserAccountsMetadata](#AddFederatedUserAccountsMetadata)>**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)<[AddFederatedUserAccountsResponse](#AddFederatedUserAccountsResponse)>**<br>if operation finished successfully. 


### AddFederatedUserAccountsMetadata {#AddFederatedUserAccountsMetadata}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation that is being altered. 


### AddFederatedUserAccountsResponse {#AddFederatedUserAccountsResponse}

Field | Description
--- | ---
user_accounts[] | **[UserAccount](./#UserAccount)**<br>List of users created by [FederationService.AddUsers](./saml/federation_service#AddUsers) request. 


## ListOperations {#ListOperations}

Lists operations for the specified federation.

**rpc ListOperations ([ListFederationOperationsRequest](#ListFederationOperationsRequest)) returns ([ListFederationOperationsResponse](#ListFederationOperationsResponse))**

### ListFederationOperationsRequest {#ListFederationOperationsRequest}

Field | Description
--- | ---
federation_id | **string**<br>ID of the federation to list operations for. The maximum string length in characters is 50.
page_size | **int64**<br>The maximum number of results per page to return. If the number of available results is larger than `page_size`, the service returns a [ListFederationOperationsOperationsResponse.next_page_token] that can be used to get the next page of results in subsequent list requests. Default value: 100. Acceptable values are 0 to 1000, inclusive.
page_token | **string**<br>Page token. To get the next page of results, set `page_token` to the [ListFederationOperationsResponse.next_page_token](#ListFederationOperationsResponse) returned by a previous list request. The maximum string length in characters is 100.


### ListFederationOperationsResponse {#ListFederationOperationsResponse}

Field | Description
--- | ---
operations[] | **[operation.Operation](#Operation4)**<br>List of operations for the specified federation. 
next_page_token | **string**<br>This token allows you to get the next page of results for list requests. If the number of results is larger than [ListFederationOperationsRequest.page_size](#ListFederationOperationsRequest1), use the `next_page_token` as the value for the [ListFederationOperationsRequest.page_token](#ListFederationOperationsRequest1) query parameter in the next list request. Each subsequent list request will have its own `next_page_token` to continue paging through the results. 


### Operation {#Operation}

Field | Description
--- | ---
id | **string**<br>ID of the operation. 
description | **string**<br>Description of the operation. 0-256 characters long. 
created_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>Creation timestamp. 
created_by | **string**<br>ID of the user or service account who initiated the operation. 
modified_at | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**<br>The time when the Operation resource was last modified. 
done | **bool**<br>If the value is `false`, it means the operation is still in progress. If `true`, the operation is completed, and either `error` or `response` is available. 
metadata | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)**<br>Service-specific metadata associated with the operation. It typically contains the ID of the target resource that the operation is performed on. Any method that returns a long-running operation should document the metadata type, if any. 
result | **oneof:** `error` or `response`<br>The operation result. If `done == false` and there was no failure detected, neither `error` nor `response` is set. If `done == false` and there was a failure detected, `error` is set. If `done == true`, exactly one of `error` or `response` is set.
&nbsp;&nbsp;error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**<br>The error result of the operation in case of failure or cancellation. 
&nbsp;&nbsp;response | **[google.protobuf.Any](https://developers.google.com/protocol-buffers/docs/proto3#any)**<br>The normal response of the operation in case of success. If the original method returns no data on success, such as Delete, the response is [google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty). If the original method is the standard Create/Update, the response should be the target resource of the operation. Any method that returns a long-running operation should document the response type, if any. 

