
  

# wallet-server-sdk-server-backend Changelog

  

Summary of custom sdk customizations

  

### <span id="#current-version">Current SDK version : 9.6.35</span>

  

## Versiones

  

- [1.0.1](#v1.0.1)

- [1.0.2](#v1.0.2)

- [1.0.3](#v1.0.3)

  

<a  id="1.0.1"></a>

## 1.0.1 (2023-03-24)

  

<details>

<summary>Features</summary>

  

- Added an anti spoofing validation in [Match3D2DIDScanResponse](/facetec-servers/FaceTecSDK-custom-server-[version]/src/main/java/com/facetec/customserver/jsonObjects/responses/Match3D2DIDScanResponse.java)

```java

FaceTecLogging.info("Value for digitalIDSpoofStatusEnumInt " + this.digitalIDSpoofStatusEnumInt);

FaceTecLogging.info("Value for faceOnDocumentStatusEnumInt " + this.faceOnDocumentStatusEnumInt);

if(this.digitalIDSpoofStatusEnumInt == 1 && this.faceOnDocumentStatusEnumInt != 1) {

// Consider FORCED RETRY if Facetec Determines that the document is FAKE or NOT enough legible

FaceTecLogging.info("Entered in AntiSpoof Custom validation");

this.scanResultBlob = match3D2DIDScanResult.getScanResultBlob(FaceTecMatch3D2DIDScanResult.ResultBehaviorOverride.FORCE_RETRY);

}

```

  

</details>

  

<details>

<summary>Bug Fixes</summary>

  

- Removed a line from [MongoDatabase](/facetec-servers/FaceTecSDK-custom-server-[version]/src/main/java/com/facetec/customserver/database/MongoDatabase.java) in order to hide the value of mongoDBURI from the logs

  

```java

FaceTecLogging.info("MongoDB URI: " + serverConfig.mongoDBURI);

```

  

- Added a parameter to skipping OCR Confirmation screen in [Match3D2DIDScanResponse](/facetec-servers/FaceTecSDK-custom-server-[version]/src/main/java/com/facetec/customserver/jsonObjects/responses/Match3D2DIDScanResponse.java)

```java

this.scanResultBlob = match3D2DIDScanResult.getScanResultBlob(FaceTecMatch3D2DIDScanResult.ResultBehaviorOverride.SKIP_USER_CONFIRMATION);

```

  

</details>

  

<a  id="1.0.2"></a>

## 1.0.2 (2023-04-03)

  

<details>

<summary>Minor changes</summary>

  

- Added FaceTecLogging [Match3D2DIDScanResponse](/facetec-servers/FaceTecSDK-custom-server-[version]/src/main/java/com/facetec/customserver/jsonObjects/responses/Match3D2DIDScanResponse.java)

```java

try {

String  ocrData = match3D2DIDScanResult.ocrResults;

FaceTecLogging.info("Match3D2DIDScanResponse: Template name = " + ocrData.substring(ocrData.indexOf("templateName") + 15, ocrData.indexOf("templateType") - 3));

} catch (Exception  e) {

FaceTecLogging.info("Match3D2DIDScanResponse: Template name not found");

}

```

- Added FaceTecLogging [NewEnrollmentResponse](/facetec-servers/FaceTecSDK-custom-server-[version]/src/main/java/com/facetec/customserver/jsonObjects/responses/NewEnrollmentResponse.java)

```java

if(fraudUserListSearchResult != null && fraudUserListSearchResult.searchResults.size() > 0) {

FaceTecLogging.info("NewEnrollmentResponse: fraudUserListSearchResult.searchResults.size() = " + fraudUserListSearchResult.searchResults);

FaceTecLogging.info("NewEnrollmentResponse: fraudUserListSearchResult.searchResults.get(0).getScore() = " + fraudUserListSearchResult.searchResults);

}

else {

FaceTecLogging.info("NewEnrollmentResponse: fraudUserListSearchResult.searchResults.size() = 0");

}

```

</details>

<a  id="1.0.3"></a>
## 1.0.3 (2023-04-10)


<details>

<summary>Minor changes</summary>

-  Add lines of code, for the API response and code refactor [Match3D2DIDScanResponse](/facetec-servers/FaceTecSDK-custom-server-[version]/src/main/java/com/facetec/customserver/jsonObjects/responses/Match3D2DIDScanResponse.java) class:

  ++ Added code to extract the template name and type from the OCR results of the ID scan and store it in the response object for later use.
  ++ Added code to set the `isFakeImage` variable of the response object based on certain conditions.

```java
String ocrData = match3D2DIDScanResult.ocrResults;
String templateNameAndType = "";

try {
    templateNameAndType = ocrData.substring(ocrData.indexOf("templateName") + 15, ocrData.indexOf("templateType") - 3);

    FaceTecLogging.info("Match3D2DIDScanResponse: Template name = " + templateName);

} catch (Exception e) {
    FaceTecLogging.info("Match3D2DIDScanResponse: Template name not found");
}

// Assign the extracted template name and type to the response object
this.templateName = templateNameAndType;

....

// Set the isFakeImage variable based on certain conditions
this.isFakeImage = false; // Add line of code
try {
    if (this.digitalIDSpoofStatusEnumInt == 1 || this.faceOnDocumentStatusEnumInt != 1) {
        this.isFakeImage = true; // Add line of code
    }
}

```

</details>

  
  

## Java file links

Remember to replace [version] with your current sdk server [version](#current-version) on the links below
