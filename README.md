
* [HPC Pack REST API 2016](#hpc-pack-rest-api-2016)
   * [Overview](#overview)
      * [Version information](#version-information)
      * [Contact information](#contact-information)
      * [URI scheme](#uri-scheme)
      * [Consumes](#consumes)
      * [Produces](#produces)
   * [Paths](#paths)
      * [Get HPC Pack Version](#get-hpc-pack-version)
      * [Get Active Head Node Name](#get-active-head-node-name)
      * [Get DateTime Format](#get-datetime-format)
      * [Get Node List](#get-node-list)
      * [Get Node by Name](#get-node-by-name)
      * [Get Node Group List](#get-node-group-list)
      * [Get Node Group Members](#get-node-group-members)
      * [Get Job List](#get-job-list)
      * [Create Job](#create-job)
      * [Create Job From XML](#create-job-from-xml)
      * [Get Job](#get-job)
      * [Set Job Properties](#set-job-properties)
      * [Get Job Custom Properties](#get-job-custom-properties)
      * [Set Job Custom Properties](#set-job-custom-properties)
      * [Get Job Environment Variables](#get-job-environment-variables)
      * [Set Job Environment Variables](#set-job-environment-variables)
      * [Submit Job](#submit-job)
      * [Cancel Job](#cancel-job)
      * [Finish Job](#finish-job)
      * [Requeue Job](#requeue-job)
      * [Get Task List](#get-task-list)
      * [Add Task](#add-task)
      * [Get Task](#get-task)
      * [Set Task Properties](#set-task-properties)
      * [Get Task Custom Properties](#get-task-custom-properties)
      * [Set Task Custom Properties](#set-task-custom-properties)
      * [Get Task Environment Variables](#get-task-environment-variables)
      * [Set Task Environment Variables](#set-task-environment-variables)
      * [Cancel Task](#cancel-task)
      * [Finish Task](#finish-task)
      * [Requeue Task](#requeue-task)
      * [Get Subtask](#get-subtask)
      * [Set Subtask Properties](#set-subtask-properties)
      * [Cancel Subtask](#cancel-subtask)
      * [Finish Subtask](#finish-subtask)
      * [Requeue Subtask](#requeue-subtask)
      * [Get Job Templates](#get-job-templates)
   * [Definitions](#definitions)
      * [RestObject](#restobject)
      * [RestProperty](#restproperty)
   * [Security](#security)
      * [basic](#basic)

# HPC Pack REST API 2016


<a name="overview"></a>
## Overview
This is the API spec for Microsoft HPC Pack 2016 Update 3.


### Version information
*Version* : 1.0.0


### Contact information
*Contact Email* : hpcpack@microsoft.com


### URI scheme
*BasePath* : /hpc
*Schemes* : HTTPS


### Consumes

* `application/json`


### Produces

* `application/json`
* `application/xml`




<a name="paths"></a>
## Paths

<a name="getclusterversion"></a>
### Get HPC Pack Version
```
GET /cluster/version
```


#### Description
Get the version of Microsoft HPC Pack installed on the HPC cluster that hosts the web service.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return the installed HPC Pack version.|string|


#### Example HTTP response

##### Response 200
```json
"5.3.6420.0"
```


<a name="getclusteractiveheadnode"></a>
### Get Active Head Node Name
```
GET /cluster/activeHeadNode
```


#### Description
Get the name of the active head node of the HPC Pack cluster.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return the active head node name.|string|


#### Example HTTP response

##### Response 200
```json
"headnode"
```


<a name="getclusterdatetimeformat"></a>
### Get DateTime Format
```
GET /cluster/info/dateTimeFormat
```


#### Description
Get DateTime format for the DateTime objects returned in the API


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return the DateTime format.|string|


#### Example HTTP response

##### Response 200
```json
"M/d/yyyy h:mm:ss tt"
```


<a name="getnodes"></a>
### Get Node List
```
GET /nodes
```


#### Description
Get the values of the specified properties for all of the nodes in an HPC cluster.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string||
|**Query**|**$filter**  <br>*optional*|Filter result by specified filters. A filter is in the form of "{name}20eq%20{value}". Now the only available filter is NodeState.|string||
|**Query**|**properties**  <br>*optional*|A comma-separated list of the names for the properties of the nodes for which you want to get values. If you do not specify the Properties parameter, the response contains values for all of the available properties of the nodes.|string||
|**Query**|**queryId**  <br>*optional*|The value of the x-ms-continuation-queryId header from the previouse response of this operation, used for reading the next page of data.|string||
|**Query**|**rowsPerRead**  <br>*optional*|Specifies how many rows of data to retrieve each time.|integer|`10`|
|**Query**|**sortNodesBy**  <br>*optional*|A node property by which nodes will be sorted. If this parameter is not specified or a property with a specified name does not exist for a node, the result will be sorted by node Id.|string|`"Id"`|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return a list of nodes.  <br>**Headers** :   <br>`x-ms-continuation-queryId` (string) : Enables large sets of data to be returned in smaller responses across a continuation sequence of several requests. The value of this header is to be assigned to the queryId query parameter in the next call of the sequence of calls to this API. The response contains this header as long as additional data remains to be processed. The format of the data in this header is not guaranteed to remain unchanged. You should only copy the data in this header from one operation in a set of multiple operations to the queryId URI parameter for the next operation. You should not use the data in this header or depend on the format of the data in this header in any other way.|< [RestObject](#restobject) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Properties" : [ {
    "Name" : "Id",
    "Value" : "1"
  }, {
    "Name" : "Name",
    "Value" : "WIN2016"
  }, {
    "Name" : "State",
    "Value" : "Online"
  }, {
    "Name" : "Availability",
    "Value" : "AlwaysOn"
  }, {
    "Name" : "Location",
    "Value" : "OnPremise"
  }, {
    "Name" : "OnlineTime",
    "Value" : "7/5/2019 9:05:07 AM"
  } ]
} ]
```


<a name="getnodebyname"></a>
### Get Node by Name
```
GET /nodes/{name}
```


#### Description
Get the values of all of the properties for the specified node.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**name**  <br>*required*|Node name.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all properties of the node.|< [RestProperty](#restproperty) > array|


<a name="getnodegroups"></a>
### Get Node Group List
```
GET /nodes/groups
```


#### Description
Get the names and descriptions for all of the node groups for the HPC cluster.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return a list of node groups.|< [RestObject](#restobject) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Properties" : [ {
    "Name" : "Name",
    "Value" : "HeadNodes"
  }, {
    "Name" : "Description",
    "Value" : "The head nodes in the cluster"
  } ]
}, {
  "Properties" : [ {
    "Name" : "Name",
    "Value" : "ComputeNodes"
  }, {
    "Name" : "Description",
    "Value" : "The compute nodes in the cluster"
  } ]
}, {
  "Properties" : [ {
    "Name" : "Name",
    "Value" : "WCFBrokerNodes"
  }, {
    "Name" : "Description",
    "Value" : "The broker nodes in the cluster"
  } ]
} ]
```


<a name="getnodegroupmembers"></a>
### Get Node Group Members
```
GET /nodes/groups/{name}
```


#### Description
Get the list of the nodes that belong to the specified node group.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**name**  <br>*required*|Node group name.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return a name list of nodes which belong to the node group.|< string > array|


#### Example HTTP response

##### Response 200
```json
[ "CN001", "CN002", "CN003" ]
```


<a name="getjobs"></a>
### Get Job List
```
GET /jobs
```


#### Description
Gets all/filtered jobs for the HPC cluster.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string||
|**Query**|**$filter**  <br>*optional*|Filter jobs by specified filters. A filter is in the form of "{name}20eq%20{value}", and multiple filters can be ANDed like "{filter1}%20and%20{filter2}…". Available filter names are JobState, NodeGroup and ChangeTimeFrom.|string||
|**Query**|**owner**  <br>*optional*|The user who created, submitted, or queued the job.|string||
|**Query**|**properties**  <br>*optional*|A comma-separated list of the names for the properties of the jobs for which you want to get values.|string|`"Id,Owner,Name,State,Priority"`|
|**Query**|**queryId**  <br>*optional*|The value of the x-ms-continuation-queryId header from the previouse response of this operation, used for reading the next page of data.|string||
|**Query**|**rowsPerRead**  <br>*optional*|Specifies how many rows of data to retrieve each time.|integer|`10`|
|**Query**|**sortJobsBy**  <br>*optional*|A job property by which jobs will be sorted. If this parameter is not specified or a property with a specified name does not exist for a job, the result will be sorted by job Id.|string|`"Id"`|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return a list of jobs.  <br>**Headers** :   <br>`x-ms-continuation-queryId` (string) : Enables large sets of data to be returned in smaller responses across a continuation sequence of several requests. The value of this header is to be assigned to the queryId query parameter in the next call of the sequence of calls to this API. The response contains this header as long as additional data remains to be processed. The format of the data in this header is not guaranteed to remain unchanged. You should only copy the data in this header from one operation in a set of multiple operations to the queryId URI parameter for the next operation. You should not use the data in this header or depend on the format of the data in this header in any other way.|< [RestObject](#restobject) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Properties" : [ {
    "Name" : "Id",
    "Value" : "14"
  }, {
    "Name" : "Owner",
    "Value" : "HPC\hpcadmin"
  }, {
    "Name" : "State",
    "Value" : "Finished"
  } ]
}, {
  "Properties" : [ {
    "Name" : "Id",
    "Value" : "11"
  }, {
    "Name" : "Owner",
    "Value" : "HPC\hpcadmin"
  }, {
    "Name" : "State",
    "Value" : "Finished"
  } ]
} ]
```


<a name="createjob"></a>
### Create Job
```
POST /jobs
```


#### Description
Creates a new job on the HPC cluster.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Body**|**properties**  <br>*optional*|Properties of job to create|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|The newly created job id is returned.|integer|


#### Example HTTP response

##### Response 200
```json
19
```


<a name="createjobfromxml"></a>
### Create Job From XML
```
POST /jobs/jobFile
```


#### Description
Create a new job on the HPC cluster by using the information in the specified job XML string.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Body**|**xml**  <br>*optional*|Job properties in XML|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|The newly created job id is returned.|integer|


#### Example HTTP response

##### Response 200
```json
19
```


<a name="getjob"></a>
### Get Job
```
GET /jobs/{jobId}
```


#### Description
Get information about the specified job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Query**|**properties**  <br>*optional*|A comma-separated list of the names for the properties of the job for which you want to get values. If you do not specify this parameter, the response contains values for all of the properties of the job.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified properties of the job.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "Id",
  "Value" : "14"
}, {
  "Name" : "Name",
  "Value" : "My Task"
}, {
  "Name" : "Owner",
  "Value" : "HPC\hpcadmin"
}, {
  "Name" : "State",
  "Value" : "Finished"
} ]
```


<a name="setjobproperties"></a>
### Set Job Properties
```
PUT /jobs/{jobId}
```


#### Description
Set the values for the properties of the specified job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Body**|**properties**  <br>*optional*|Properties of job to set|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="getjobcustomproperties"></a>
### Get Job Custom Properties
```
GET /jobs/{jobId}/customProperties
```


#### Description
Get the values of the specified custom properties for the job, or the values of all of the properties if none are specified.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Query**|**names**  <br>*optional*|A comma-separated list of the names for the custom properties of the job for which you want to get values. If you do not specify the Names parameter, the response contains values for all of the custom properties for the job.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified custom properties of the job.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "c1",
  "Value" : "v1"
}, {
  "Name" : "c2",
  "Value" : "v2"
} ]
```


<a name="setjobcustomproperties"></a>
### Set Job Custom Properties
```
POST /jobs/{jobId}/customProperties
```


#### Description
Set the values of custom properties for a job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Body**|**properties**  <br>*optional*|Custom properties for the job|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="getjobenvironmentvariables"></a>
### Get Job Environment Variables
```
GET /jobs/{jobId}/envVariables
```


#### Description
Get the values of the specified environment variables for the job, or the values of all of the environment variables if none are specified.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Query**|**names**  <br>*optional*|A comma-separated list of the names for the environment variables in the job for which you want to get values. If you do not specify the Names parameter, the response contains values for all of the environment variables for the job. If an environment variable with a specified name does not exist for the job, the response contains an empty string for the value of that environment variable.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified environment variables of the job.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "c1",
  "Value" : "v1"
}, {
  "Name" : "c2",
  "Value" : "v2"
} ]
```


<a name="setjobenvironmentvariables"></a>
### Set Job Environment Variables
```
POST /jobs/{jobId}/envVariables
```


#### Description
Sets the values of environment variables for a job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Body**|**properties**  <br>*optional*|Environment variables for the job|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="submitjob"></a>
### Submit Job
```
POST /jobs/{jobId}/submit
```


#### Description
Submit a job to the HPC Job Scheduler Service so that the HPC Job Scheduler Service can add the job to the queue of jobs to run. If the credentials for the account under which the job should run are not cached on the server, you can set them in the UserName and Password properties. A job that is submitted by this operation is not validated. After the job is submitted, you can get information about the job by using the Get Job operation.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Body**|**properties**  <br>*optional*|Properties of job to submit|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="canceljob"></a>
### Cancel Job
```
POST /jobs/{jobId}/cancel
```


#### Description
Cancel the specified job.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string||
|**Path**|**jobId**  <br>*required*|Job Id|integer||
|**Query**|**forced**  <br>*optional*|Specifies whether to stop the job immediately without using the grace period for canceling the tasks in the job and without running the node release task, if the job contains one. True indicates that the job should stop immediately without using the grace period for canceling the tasks in the job and without running the node release task. False indicates that the job should not stop immediately and should use the grace period for canceling the tasks in the job and run the node release task.|boolean|`"false"`|
|**Body**|**message**  <br>*optional*|A message for the operation.|string||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="finishjob"></a>
### Finish Job
```
POST /jobs/{jobId}/finish
```


#### Description
Finish the specified job. It's silimar to canceling a job, but sets the job state to "Finished" rather than "Canceled".


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Body**|**message**  <br>*optional*|A message for the operation.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="requeuejob"></a>
### Requeue Job
```
POST /jobs/{jobId}/requeue
```


#### Description
Resubmit the specified job to the queue.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="gettasks"></a>
### Get Task List
```
GET /jobs/{jobId}/tasks
```


#### Description
Get the values of the properties for all of the tasks in the specified job.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string||
|**Path**|**jobId**  <br>*required*|Job Id|integer||
|**Query**|**$filter**  <br>*optional*|Filter tasks by specified filters. A filter is in the form of "{name}20eq%20{value}", and multiple filters can be ANDed like "{filter1}%20and%20{filter2}…". Available filter names are TaskState, ChangeTimeFrom, TaskStates, TaskIds and TaskInstanceIds.|string||
|**Query**|**expandParametric**  <br>*optional*|Specifies whether to get properties only for the master task for a parametric sweep task, or for all of the subtasks instead. True indicates that you want to get properties for all of the subtasks. False indicates that you want to get properties only for the master task.|boolean|`"true"`|
|**Query**|**properties**  <br>*optional*|A comma-separated list of the names for the properties of the tasks for which you want to get values.|string|`"TaskId,Name,State,CommandLine,ExitCode,ParentJobId,JobTaskId,InstanceId"`|
|**Query**|**queryId**  <br>*optional*|The value of the x-ms-continuation-queryId header from the previouse response of this operation, used for reading the next page of data.|string||
|**Query**|**rowsPerRead**  <br>*optional*|Specifies how many rows of data to retrieve each time.|integer|`10`|
|**Query**|**sortTasksBy**  <br>*optional*|A task property by which tasks will be sorted. If this parameter is not specified or a property with a specified name does not exist for a task, the result will be sorted by task Id.|string|`"TaskId"`|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return a list of tasks of the job.  <br>**Headers** :   <br>`x-ms-continuation-queryId` (string) : Enables large sets of data to be returned in smaller responses across a continuation sequence of several requests. The value of this header is to be assigned to the queryId query parameter in the next call of the sequence of calls to this API. The response contains this header as long as additional data remains to be processed. The format of the data in this header is not guaranteed to remain unchanged. You should only copy the data in this header from one operation in a set of multiple operations to the queryId URI parameter for the next operation. You should not use the data in this header or depend on the format of the data in this header in any other way.|< [RestObject](#restobject) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Properties" : [ {
    "Name" : "TaskId",
    "Value" : "22.1.1"
  }, {
    "Name" : "Name",
    "Value" : "My Sweep Task"
  }, {
    "Name" : "State",
    "Value" : "Finished"
  }, {
    "Name" : "CommandLine",
    "Value" : "echo 1"
  }, {
    "Name" : "ExitCode",
    "Value" : "0"
  }, {
    "Name" : "ParentJobId",
    "Value" : "22"
  }, {
    "Name" : "JobTaskId",
    "Value" : "1"
  }, {
    "Name" : "InstanceId",
    "Value" : "1"
  } ]
}, {
  "Properties" : [ {
    "Name" : "TaskId",
    "Value" : "22.1.2"
  }, {
    "Name" : "Name",
    "Value" : "My Sweep Task"
  }, {
    "Name" : "State",
    "Value" : "Finished"
  }, {
    "Name" : "CommandLine",
    "Value" : "echo 2"
  }, {
    "Name" : "ExitCode",
    "Value" : "0"
  }, {
    "Name" : "ParentJobId",
    "Value" : "22"
  }, {
    "Name" : "JobTaskId",
    "Value" : "1"
  }, {
    "Name" : "InstanceId",
    "Value" : "2"
  } ]
} ]
```


<a name="addtask"></a>
### Add Task
```
POST /jobs/{jobId}/tasks
```


#### Description
Add a task to a job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Body**|**properties**  <br>*optional*|Properties of task to add.|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|The newly created task id is returned.|integer|


#### Example HTTP response

##### Response 200
```json
1
```


<a name="gettask"></a>
### Get Task
```
GET /jobs/{jobId}/tasks/{taskId}
```


#### Description
Get the values of the specified properties for the specified task, or the values of all of the properties if no properties are specified.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Query**|**properties**  <br>*optional*|A comma-separated list of the names for the properties of the task for which you want to get values. If you do not specify this parameter, the response contains values for all of the properties of the task.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified properties of the task.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "TaskId",
  "Value" : "37.3"
}, {
  "Name" : "JobTaskId",
  "Value" : "3"
}, {
  "Name" : "InstanceId",
  "Value" : "0"
}, {
  "Name" : "State",
  "Value" : "Finished"
}, {
  "Name" : "CommandLine",
  "Value" : "time /t"
} ]
```


<a name="settaskproperties"></a>
### Set Task Properties
```
PUT /jobs/{jobId}/tasks/{taskId}
```


#### Description
Set the values of properties for a task in a job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**properties**  <br>*optional*|Properties of task to set.|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="gettaskcustomproperties"></a>
### Get Task Custom Properties
```
GET /jobs/{jobId}/tasks/{taskId}/customProperties
```


#### Description
Get the values of the specified custom properties for the task, or the values of all of the properties if none are specified.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Query**|**names**  <br>*optional*|A comma-separated list of the names for the custom properties of the task for which you want to get values. If you do not specify the Names parameter, the response contains values for all of the custom properties for the task.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified custom properties of the task.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "c1",
  "Value" : "v1"
}, {
  "Name" : "c2",
  "Value" : "v2"
} ]
```


<a name="settaskcustomproperties"></a>
### Set Task Custom Properties
```
POST /jobs/{jobId}/tasks/{taskId}/customProperties
```


#### Description
Set the values of custom properties for a task.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**properties**  <br>*optional*|Custom properties for the task|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="gettaskenvironmentvariables"></a>
### Get Task Environment Variables
```
GET /jobs/{jobId}/tasks/{taskId}/envVariables
```


#### Description
Get the values of the specified environment variables for the task, or the values of all of the environment variables if none are specified.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Query**|**names**  <br>*optional*|A comma-separated list of the names for the environment variables in the task for which you want to get values. If you do not specify the Names parameter, the response contains values for all of the environment variables for the task. If an environment variable with a specified name does not exist for the task, the response contains an empty string for the value of that environment variable.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified environment variables of the task.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "c1",
  "Value" : "v1"
}, {
  "Name" : "c2",
  "Value" : "v2"
} ]
```


<a name="settaskenvironmentvariables"></a>
### Set Task Environment Variables
```
POST /jobs/{jobId}/tasks/{taskId}/envVariables
```


#### Description
Set the value of one or more environment variables for a task.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**properties**  <br>*optional*|Environment variables for the task|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="canceltask"></a>
### Cancel Task
```
POST /jobs/{jobId}/tasks/{taskId}/cancel
```


#### Description
Cancel the specified task.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string||
|**Path**|**jobId**  <br>*required*|Job Id|integer||
|**Path**|**taskId**  <br>*required*|Task Id|integer||
|**Query**|**forced**  <br>*optional*|Specifies whether to stop the task immediately without using the grace period for canceling a task. True indicates that the task should stop immediately without using the grace period for canceling a task. False indicates that the task should use the grace period for canceling a task.|boolean|`"false"`|
|**Body**|**message**  <br>*optional*|A message for the operation.|string||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="finishtask"></a>
### Finish Task
```
POST /jobs/{jobId}/tasks/{taskId}/finish
```


#### Description
Finish the specified task. It's silimar to canceling a task, but sets the task state to "Finished" rather than "Canceled".


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**message**  <br>*optional*|A message for the operation.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="requeuetask"></a>
### Requeue Task
```
POST /jobs/{jobId}/tasks/{taskId}/requeue
```


#### Description
Move a failed, canceled, or queued task to the configuring state so that the task can be queued again when the job is resubmitted.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**message**  <br>*optional*|A message for the operation.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="getsubtask"></a>
### Get Subtask
```
GET /jobs/{jobId}/tasks/{taskId}/subtasks/{subtaskId}
```


#### Description
Get the values of the specified properties for the specified subtask, or the values of all of the properties if no properties are specified. Only Parameteric Sweep job have subtasks.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**subtaskId**  <br>*required*|Subtask Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Query**|**properties**  <br>*optional*|A comma-separated list of the names for the properties of the subtask for which you want to get values. If you do not specify this parameter, the response contains values for all of the properties of the subtask.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return all/specified properties of the subtask.|< [RestProperty](#restproperty) > array|


#### Example HTTP response

##### Response 200
```json
[ {
  "Name" : "JobTaskId",
  "Value" : "1"
}, {
  "Name" : "TaskId",
  "Value" : "22.1.3"
}, {
  "Name" : "InstanceId",
  "Value" : "3"
}, {
  "Name" : "CommandLine",
  "Value" : "echo 3"
} ]
```


<a name="setsubtaskproperties"></a>
### Set Subtask Properties
```
PUT /jobs/{jobId}/tasks/{taskId}/subtasks/{subtaskId}
```


#### Description
Set the values of properties for a subtask in a job.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**subtaskId**  <br>*required*|Subtask Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**properties**  <br>*optional*|Properties of subtask to set.|< [RestProperty](#restproperty) > array|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="cancelsubtask"></a>
### Cancel Subtask
```
POST /jobs/{jobId}/tasks/{taskId}/subtasks/{subtaskId}/cancel
```


#### Description
Cancel the specified subtask.


#### Parameters

|Type|Name|Description|Schema|Default|
|---|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string||
|**Path**|**jobId**  <br>*required*|Job Id|integer||
|**Path**|**subtaskId**  <br>*required*|Subtask Id|integer||
|**Path**|**taskId**  <br>*required*|Task Id|integer||
|**Query**|**forced**  <br>*optional*|Specifies whether to stop the subtask immediately without using the grace period for canceling a task. True indicates that the subtask should stop immediately without using the grace period for canceling a task. False indicates that the subtask should use the grace period for canceling.|boolean|`"false"`|
|**Body**|**message**  <br>*optional*|A message for the operation.|string||


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="finishsubtask"></a>
### Finish Subtask
```
POST /jobs/{jobId}/tasks/{taskId}/subtasks/{subtaskId}/finish
```


#### Description
Finish the specified subtask.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**subtaskId**  <br>*required*|Subtask Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|
|**Body**|**message**  <br>*optional*|A message for the operation.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="requeuesubtask"></a>
### Requeue Subtask
```
POST /jobs/{jobId}/tasks/{taskId}/subtasks/{subtaskId}/requeue
```


#### Description
Move a failed, canceled, or queued subtask to the configuring state so that the subtask can be queued again when the job is resubmitted.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|
|**Path**|**jobId**  <br>*required*|Job Id|integer|
|**Path**|**subtaskId**  <br>*required*|Subtask Id|integer|
|**Path**|**taskId**  <br>*required*|Task Id|integer|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**204**|OK|No Content|


<a name="getjobtemplates"></a>
### Get Job Templates
```
GET /jobs/templates
```


#### Description
Get a list of the names of the job templates that are available on the HPC cluster.


#### Parameters

|Type|Name|Description|Schema|
|---|---|---|---|
|**Header**|**x-ms-as-user**  <br>*optional*|The name of user whom you want to make request as. You must be an HPC Pack administrator or HPC Pack Job administrator to make it work.|string|


#### Responses

|HTTP Code|Description|Schema|
|---|---|---|
|**200**|Return a list of template names.|< string > array|


#### Example HTTP response

##### Response 200
```json
[ "Default" ]
```




<a name="definitions"></a>
## Definitions

<a name="restobject"></a>
### RestObject

|Name|Schema|
|---|---|
|**properties**  <br>*optional*|< [RestProperty](#restproperty) > array|


<a name="restproperty"></a>
### RestProperty

|Name|Schema|
|---|---|
|**name**  <br>*optional*|string|
|**value**  <br>*optional*|string|




<a name="securityscheme"></a>
## Security

<a name="basic"></a>
### basic
*Type* : basic
