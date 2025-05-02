Create a certificate for your app Granting access via Azure AD App-Only | Microsoft Learn

Check the token to see which permission level of your app, this tool could decode the token: https://jwt.io/
For example:




Tool Graph Explorer | Try Microsoft Graph APIs - Microsoft Graph

A sample if from my cx:




So below are discussions about Site id & library id & item id and the results of the whole api

1. Call a spo site:
method 1: with spo site url:
The graph format set as:
https://graph.microsoft.com/v1.0/sites/m365x88585280.sharepoint.com:/sites/TestSPOSite



method 2: with spo site id: 1a95145b-f6ad-48f0-a1cc-5ee25f4cf005. This is Site Id in Cx api.
And it will provide same results with site url:




2. Call a spo library
We can consider a spo library as a drive, and a folder in a spo library is also a drive.
Refer https://learn.microsoft.com/en-us/graph/api/drive-get?view=graph-rest-1.0&tabs=http#get-the-document-library-for-a-site



And to get the drive id for a specific spo library, we need firstly get all libraries in a spo site with below api, and from now we will start to use site id instead of site url in the api:
https://graph.microsoft.com/v1.0/sites/1a95145b-f6ad-48f0-a1cc-5ee25f4cf005/drives

Then in the results below, we can find our target library and then record id b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy   This is Library Id in Cx api

{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#drives",
    "value": [
        {
            "createdDateTime": "2022-10-08T15:23:03Z",
            "description": "",
            "id": "b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy",
            "lastModifiedDateTime": "2022-10-21T04:52:53Z",
            "name": "Documents",
            "webUrl": "https://m365x88585280.sharepoint.com/sites/TestSPOSite/Shared%20Documents",
            "driveType": "documentLibrary",
            "createdBy": {
                "user": {
                    "displayName": "System Account"
                }
            },
            "lastModifiedBy": {
                "user": {
                    "displayName": "System Account"
                }
            },
            "owner": {
                "group": {
                    "email": "TestSPOSite@M365x88585280.onmicrosoft.com",
                    "id": "c61d5502-bcb4-4477-8cb2-0fdfe6566634",
                    "displayName": "TestSPOSite Owners"
                }
            },
            "quota": {
                "deleted": 0,
                "remaining": 27487788285761,
                "state": "normal",
                "total": 27487790694400,
                "used": 2408639
            }
        }
    ]
}

Then query the api with library id to get details about this library:
https://graph.microsoft.com/v1.0/sites/1a95145b-f6ad-48f0-a1cc-5ee25f4cf005/drives/b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy



{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#drives/$entity",
    "createdDateTime": "2022-10-08T15:23:03Z",
    "description": "",
    "id": "b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy",
    "lastModifiedDateTime": "2022-10-21T04:52:53Z",
    "name": "Documents",
    "webUrl": "https://m365x88585280.sharepoint.com/sites/TestSPOSite/Shared%20Documents",
    "driveType": "documentLibrary",
    "createdBy": {
        "user": {
            "displayName": "System Account"
        }
    },
    "lastModifiedBy": {
        "user": {
            "displayName": "System Account"
        }
    },
    "owner": {
        "group": {
            "email": "TestSPOSite@M365x88585280.onmicrosoft.com",
            "id": "c61d5502-bcb4-4477-8cb2-0fdfe6566634",
            "displayName": "TestSPOSite Owners"
        }
    },
    "quota": {
        "deleted": 0,
        "remaining": 27487788285761,
        "state": "normal",
        "total": 27487790694400,
        "used": 2408639
    }
}

3.Get all items in a spo library:
https://graph.microsoft.com/v1.0/sites/1a95145b-f6ad-48f0-a1cc-5ee25f4cf005/drives/b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy/root/delta

We will get all items in the results and we need to filter and get the target.

And I would like to test with the .xlsx file which name is Exceltest.xlsx, we need to note down the id which is Item Id in Cx api..



        {
            "@odata.type": "#microsoft.graph.driveItem",
            "createdDateTime": "2022-10-21T02:32:42Z",
            "eTag": "\"{7F1C9ACF-070F-40BF-A8F9-C1554F6F8236},11\"",
            "id": "01NFE5UXOPTIOH6DYHX5AKR6OBKVHW7ARW",
            "lastModifiedDateTime": "2022-11-02T08:10:05Z",
            "name": "Exceltest.xlsx",
            "webUrl": "https://m365x88585280.sharepoint.com/sites/TestSPOSite/_layouts/15/Doc.aspx?sourcedoc=%7B7F1C9ACF-070F-40BF-A8F9-C1554F6F8236%7D&file=Exceltest.xlsx&action=default&mobileredirect=true",
            "cTag": "\"c:{7F1C9ACF-070F-40BF-A8F9-C1554F6F8236},11\"",
            "size": 11662,
            "createdBy": {
                "user": {
                    "email": "admin@M365x88585280.OnMicrosoft.com",
                    "id": "f3ee6f6d-b606-4fad-bed8-488f79b5afb9",
                    "displayName": "MOD Administrator"
                }
            },
            "lastModifiedBy": {
                "user": {
                    "email": "AdeleV@M365x88585280.OnMicrosoft.com",
                    "id": "1798dfb0-7c66-47b3-92f3-12ff9df21864",
                    "displayName": "Adele Vance"
                }
            },
            "parentReference": {
                "driveType": "documentLibrary",
                "driveId": "b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy",
                "id": "01NFE5UXN6Y2GOVW7725BZO354PWSELRRZ",
                "path": "/drives/b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy/root:"
            },
            "file": {
                "mimeType": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet",
                "hashes": {
                    "quickXorHash": "t2rV9IUDbgDtRnaQbgnAQqF1HcA="
                }
            },
            "fileSystemInfo": {
                "createdDateTime": "2022-10-21T02:32:42Z",
                "lastModifiedDateTime": "2022-11-02T08:10:05Z"
            },
            "shared": {
                "scope": "users"
            }
        },


c. item id/folder id:
 
用GET 请求在知道文件名和文件夹名还有路径的情况下可以直接去查id:
例如查询 Documents>Test Folder> AstridCreate.docx:
GET https://graph.microsoft.com/v1.0/sites/{site-id}/drives/{drive-id}/root:/Test%20Folder/AliceCreate.docx


4. Call the target item which is Exceltest.xlsx here with item id:
https://graph.microsoft.com/v1.0/sites/1a95145b-f6ad-48f0-a1cc-5ee25f4cf005/drives/b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy/items/01NFE5UXOPTIOH6DYHX5AKR6OBKVHW7ARW


Below are customized parameters from cx side to meet their needs: 
5. Now we can add "analytics/allTime?$expand=activities" as Cx did:
https://graph.microsoft.com/v1.0/sites/1a95145b-f6ad-48f0-a1cc-5ee25f4cf005/drives/b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy/items/01NFE5UXOPTIOH6DYHX5AKR6OBKVHW7ARW/analytics/allTime?$expand=activities


{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#microsoft.graph.itemActivityStat",
    "aggregationInterval": "None",
    "startDateTime": "0001-01-01T00:00:00Z",
    "endDateTime": "0001-01-01T00:00:00Z",
    "isTrending": false,
    "access": {
        "actionCount": 0,
        "actorCount": 0,
        "timeSpentInSeconds": 0
    },
    "incompleteData": {
        "wasThrottled": false,
        "resultsPending": false,
        "notSupported": false
    },
    "activities": [
        {
            "id": "00000",
            "activityDateTime": "2022-11-02T08:09:50Z",
            "edit": {},
            "location": {
                "address": {
                    "city": "",
                    "countryOrRegion": "",
                    "postalCode": "",
                    "state": "",
                    "street": ""
                }
            },
            "actor": {
                "user": {
                    "displayName": "Adele Vance",
                    "email": "adelev@m365x88585280.onmicrosoft.com",
                    "id": "1798dfb0-7c66-47b3-92f3-12ff9df21864",
                    "userType": "Internal"
                }
            }
        },
        {
            "id": "00001",
            "activityDateTime": "2022-11-02T08:09:50Z",
            "edit": {},
            "location": {
                "address": {
                    "city": "",
                    "countryOrRegion": "",
                    "postalCode": "",
                    "state": "",
                    "street": ""
                }
            },
            "actor": {
                "user": {
                    "displayName": "MOD Administrator",
                    "email": "admin@m365x88585280.onmicrosoft.com",
                    "id": "f3ee6f6d-b606-4fad-bed8-488f79b5afb9",
                    "userType": "Internal"
                }
            }
        }
    ]
}


Then Add a filter to filter the results of 'Access':
https://graph.microsoft.com/v1.0/sites/1a95145b-f6ad-48f0-a1cc-5ee25f4cf005/drives/b!WxSVGq328EihzF7iX0zwBUKyOdYTcJlEvv2TELjmxGyJDapLUP3DSaOaOKHnNcJy/items/01NFE5UXOPTIOH6DYHX5AKR6OBKVHW7ARW/analytics/allTime?$expand=activities($filter=access ne null)


{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#microsoft.graph.itemActivityStat",
    "aggregationInterval": "None",
    "startDateTime": "0001-01-01T00:00:00Z",
    "endDateTime": "0001-01-01T00:00:00Z",
    "isTrending": false,
    "access": {
        "actionCount": 0,
        "actorCount": 0,
        "timeSpentInSeconds": 0
    },
    "incompleteData": {
        "wasThrottled": false,
        "resultsPending": false,
        "notSupported": false
    }
}


6. Upload a file to a subfolder while create this subfolder at the same time:

如果想要给一个子文件夹创建一个新的子文件夹的同时传一个新的文件用的graph api格式为：

https://graph.microsoft.com/v1.0/drives/<drive id> /items/{the source of parent folder id}:/{parent folder}/<customize new folder name>/test.txt:/content




7. 关于search query


Based on this document https://learn.microsoft.com/en-us/graph/api/search-query?view=graph-rest-1.0&tabs=http#permissions. If we are using an app to call graph api, we need at least Files.Read.All permission, or we will meet 401 Unthorized error.


To double confirm above information, I did tests below:
1. I granted my app as Site.Selected permission for it can read files of my test site, check the token which indicated my app has site.selected permission:


And I can run GET graph api to get items/drives in my test site with my app successfully.

But when I run search query api, I meet 401 error:


2. Then I grant my app with Files.Read.All permission as the documented recommand, checking the token to make sure the permission has been granted successfully:


Then I run same search query and I can get the file I want successfully:



Therefore, we can conclude that the 401 error we meet is because if we want to running graph search query with app, then the least permission of the app is Files.Read.All and Site.Select cannot work in this scenario.

========================

c. item id/folder id:
 
用GET 请求在知道文件名和文件夹名还有路径的情况下可以直接去查id:
例如查询 Documents>Test Folder> AstridCreate.docx:
GET https://graph.microsoft.com/v1.0/sites/{site-id}/drives/{drive-id}/root:/Test%20Folder/AliceCreate.docx
![image](https://github.com/user-attachments/assets/d1bed1fe-49bb-4e07-b685-bf242d7f827c)

