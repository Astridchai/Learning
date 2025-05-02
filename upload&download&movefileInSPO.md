1. Download file test:
KB: Download driveItem content - Microsoft Graph v1.0 | Microsoft Learn

a. https://graph.microsoft.com/v1.0/sites/m365x04199248.sharepoint.com:/sites/RetentionPolicySite to get site id


{
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#sites/$entity",
    "createdDateTime": "2024-09-10T06:50:15.1Z",
    "description": "RetentionPolicySite",
    "id": "m365x04199248.sharepoint.com,0ae5a181-233f-43c4-8811-f0e686072ec3,ae0cf232-7786-4795-b33f-a35fc3be7fad",
    "lastModifiedDateTime": "2024-10-28T09:29:25Z",
    "name": "RetentionPolicySite",
    "webUrl": "https://m365x04199248.sharepoint.com/sites/RetentionPolicySite",
    "displayName": "RetentionPolicySite",
    "root": {},
    "siteCollection": {
        "hostname": "m365x04199248.sharepoint.com"
    }
}

b. https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives
get drive id of 'Documents':

"createdDateTime": "2024-08-18T05:42:23Z",
            "description": "",
            "id": "b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw",
            "lastModifiedDateTime": "2024-10-28T05:49:05Z",
            "name": "Documents",
            "webUrl": "https://m365x04199248.sharepoint.com/sites/RetentionPolicySite/Shared%20Documents",
            "driveType": "documentLibrary",

c. https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/Astrid1.docx

Above can get item id




    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#Collection(driveItem)/$entity",
    "@microsoft.graph.downloadUrl": "https://m365x04199248.sharepoint.com/sites/RetentionPolicySite/_layouts/15/download.aspx?UniqueId=2452b8b5-330d-47e2-af74-a15160b1cb88&Translate=false&tempauth=v1.eyJzaXRlaWQiOiIwYWU1YTE4MS0yMzNmLTQzYzQtODgxMS1mMGU2ODYwNzJlYzMiLCJhcHBfZGlzcGxheW5hbWUiOiJQb3N0bWFuIiwiYXBwaWQiOiI3MTBhNjg0OC01NjA0LTQ5Y2YtOGFhZC1kM2JkNWJmNGI1NTEiLCJhdWQiOiIwMDAwMDAwMy0wMDAwLTBmZjEtY2UwMC0wMDAwMDAwMDAwMDAvbTM2NXgwNDE5OTI0OC5zaGFyZXBvaW50LmNvbUA2NmRmMTFkNy1iODZlLTQ3MzgtOWEyNS01YWE4OTNjMTllMDkiLCJleHAiOiIxNzMwMTg1MzYxIn0.CgoKBHNuaWQSAjY0EgsIqIPtzKr6uz0QBRoMNDAuMTI2LjM1Ljg4Kix6M2x3b1lBSnRKczJFdUdPandwRUlHaVJ6L25Zd3Rkci9INXRBTFlDNXZBPTCWATgBQhChXpC2DpAAYLXYkiKjhMNVShBoYXNoZWRwcm9vZnRva2VuUghbImttc2kiXXIpMGguZnxtZW1iZXJzaGlwfDEwMDMyMDAzYmYxMDIyYTJAbGl2ZS5jb216ATKCARIJ1xHfZm64OEcRmiVaqJPBngmSAQNNT0SaAQ1BZG1pbmlzdHJhdG9yogEjYWRtaW5AbTM2NXgwNDE5OTI0OC5vbm1pY3Jvc29mdC5jb22qARAxMDAzMjAwM0JGMTAyMkEysgEtbXlmaWxlcy53cml0ZSBhbGxzaXRlcy53cml0ZSBhbGxwcm9maWxlcy5yZWFkyAEB.hBYD3AZ2cpwuZwHhBS8GY6gphk9xJjTb7jcm2H8IMhY&ApiVersion=2.0",
    "createdBy": {
        "user": {
            "email": "admin@M365x04199248.onmicrosoft.com",
            "id": "743578c1-df75-4746-9755-98ac56c13d28",
            "displayName": "MOD Administrator"
        }
    },
    "createdDateTime": "2024-09-10T06:51:14Z",
    "eTag": "\"{2452B8B5-330D-47E2-AF74-A15160B1CB88},1\"",
    "id": "01X2JPET5VXBJCIDJT4JD265FBKFQLDS4I",


d. 选择powershell:
-----------------
$tenantId = "66df11d7-b86e-4738-9a25-5aa893c19e09"
$clientId = "710a6848-5604-49cf-8aad-d3bd5bf4b551"
$clientSecret = "
$siteId = "0ae5a181-233f-43c4-8811-f0e686072ec3"
$itemId = "01X2JPET5VXBJCIDJT4JD265FBKFQLDS4I"

# Get Access Token
$body = @{
    client_id     = $clientId
    client_secret = $clientSecret
    scope         = "https://graph.microsoft.com/.default"
    grant_type    = "client_credentials"
}
$response = Invoke-RestMethod -Uri "https://login.microsoftonline.com/$tenantId/oauth2/v2.0/token" -Method POST -Body $body
$accessToken = $response.access_token

# Download File
$downloadUrl = "https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/Astrid1.docx:/content"
Invoke-WebRequest -Uri $downloadUrl -Headers @{Authorization = "Bearer $accessToken"} -OutFile "C:\Users\mengjiechai\Temp\Astrid1.docx"

======================

2. Upload file

Refer: Upload small files - Microsoft Graph v1.0 | Microsoft Learn
Upload Files to SharePoint Online Library using POSTMAN

a. Sample: upload fileb.txt to below location in screenshot:



https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/Test%20Folder/fileb.txt:/content





In postman successful response:



b. Postman can also help upload local file:





Graph api: PUT https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/Test%20Folder/AliceCreate.docx:/content




==================

3. Move file
Ref:
Move a file or folder - Microsoft Graph v1.0 | Microsoft Learn
How can i move a file from one folder to another in SharePoint using Graph Api? - Stack Overflow
Microsoft Graph Mailbag – Copy/Move Files and Folders in SharePoint Online - Microsoft 365 Developer Blog

Use another sample:
GET https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/Cat.jpg

Get item id at first:
    "eTag": "\"{6E66FE54-FB9F-4E9E-9FB6-49BD2F20A7BC},1\"",
    "id": "01X2JPET2U7ZTG5H73TZHJ7NSJXUXSBJ54",


Resource:



Get folder id (my destination) 

GET https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/Test%20Folder


 "createdDateTime": "2024-09-12T03:54:36Z",
    "eTag": "\"{43976F36-59DB-4D85-8605-0239342DA2C4},1\"",
    "id": "01X2JPETZWN6LUHW2ZQVGYMBICHE2C3IWE",




a. Let's try move this picture in same library at first:
PATCH https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/items/01X2JPET2U7ZTG5H73TZHJ7NSJXUXSBJ54

Adding below content type : application/json




Below id is the id of my target destination folder

{
  "parentReference": {
    "id": "01X2JPETZWN6LUHW2ZQVGYMBICHE2C3IWE"
  },
  "name": "Cat.jpg"
}




Succeed:




b. Let's try different drives in same SPO site if possible, KB tells us it is impossible.

--------------------------





Resource:

GET https://graph.microsoft.com/v1.0/sites/0ae5a181-233f-43c4-8811-f0e686072ec3/drives/b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/root:/hack1.png

 "createdDateTime": "2024-10-29T07:44:28Z",
    "eTag": "\"{21E7A07C-2A2D-4526-9DFB-F023E606B79F},1\"",
    "id": "01X2JPET34UDTSCLJKEZCZ367QEPTANN47",





Destination:

Another library which is destination:


"createdDateTime": "2024-10-29T07:39:44Z",
            "description": "",
            "id": "b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f63neW9jqnxfTbhTC3GI3E1R",
            "lastModifiedDateTime": "2024-10-29T07:39:44Z",
            "name": "Astrid Lib",
            "webUrl": "https://m365x04199248.sharepoint.com/sites/RetentionPolicySite/Astrid%20Lib",
            "driveType": "documentLibrary",

Another folder:

    "createdDateTime": "2024-10-29T07:46:08Z",
    "eTag": "\"{79DB2D5F-9905-4CE4-9F0C-9A7915B79484},1\"",
    "id": "01X2JPET27FXNXSBMZ4RGJ6DE2PEK3PFEE",






{
  "parentReference": {
    "driveId": "b!gaHlCj8jxEOIEfDmhgcuwzLyDK6Gd5VHsz-jX8O-f63neW9jqnxfTbhTC3GI3E1R",
    "id": "01X2JPET27FXNXSBMZ4RGJ6DE2PEK3PFEE"
  },
  "name": "hack1.png"
}

Works:



------------------

c. Different site (not support)

Destination:
site id: 70807f23-d07f-4798-91fe-ab01b6743291
Library id: b!I3-AcH_QmEeR_qsBtnQykTLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw

Resource:
item id: 01X2JPET34UDTSCLJKEZCZ367QEPTANN47


=======================================

If you do not want to use any api tool like postman to do test, then you can use below powershell demo to test move a file:
----------------------------------

Destination Folder id: 01DPAL7M5TQZ3CMIQVBJDIOJ5NHUPWENRW


Resource item id: 01DPAL7M6O4YXBVPKQ7VAZAWOQF7CBSAAP


Output: 


:
==================
#'driveId' here is the id of destination drive, driveItemId is the moving-target file item id
$tenantId = "66df11d7-b86e-4738-9a25-5aa893c19e09"
$clientId = "710a6848-5604-49cf-8aad-d3bd5bf4b551"
$clientSecret = "g-88Q~FRQhnzIPu2LE61uyUGmT1k2e9LROrmqdtM"
$driveId = "b!I3-AcH_QmEeR_qsBtnQykTLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw"
$driveItemId = "01DPAL7M6O4YXBVPKQ7VAZAWOQF7CBSAAP"

# Get Access Token
$body = @{
    client_id     = $clientId
    client_secret = $clientSecret
    scope         = "https://graph.microsoft.com/.default"
    grant_type    = "client_credentials"
}
$response = Invoke-RestMethod -Uri "https://login.microsoftonline.com/$tenantId/oauth2/v2.0/token" -Method POST -Body $body
$accessToken = $response.access_token

Connect-Graph -AccessToken ($accessToken | ConvertTo-SecureString -AsPlainText -Force)

#'driveId' here is the id of destination drive
#'id' here is the id of destination folder id, if you do not move to any folder, remove this property
$params = @{
	parentReference = @{
        driveId = 'b!I3-AcH_QmEeR_qsBtnQykTLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw'
		id = '01DPAL7M5TQZ3CMIQVBJDIOJ5NHUPWENRW'
	}
	name = "FullControl2.csv"
}

Update-MgDriveItem -DriveId $driveId -DriveItemId $driveItemId -BodyParameter $params

或者如果要选用HTTP call 的方式，那么可以这么写：
其中move file里面是graph api call, 注意invoke-WebRequest的写法：

$MoveFile = "https://graph.microsoft.com/v1.0/sites/70807f23-d07f-4798-91fe-ab01b6743291/drives/b!I3-AcH_QmEeR_qsBtnQykTLyDK6Gd5VHsz-jX8O-f61IIV862SWzTJgWukhCNwEw/items/01DPAL7M2J6KOZILSMVNEL4KKQCNH5ALJY"

$jsonBody = $params | ConvertTo-Json -Depth 10
$utf8Body = [System.Text.Encoding]::UTF8.GetBytes($jsonBody)

Invoke-WebRequest -Uri $MoveFile -Body $utf8Body -Headers @{Authorization = "Bearer $accessToken"; "Content-Type" = "application/json; charset=utf-8"} -Method PATCH

========================
![image](https://github.com/user-attachments/assets/b791971b-08ce-4110-ad46-168b6c97a0ca)

