**The following content is AI generated and might contain incorrect information. Before you use this content, make sure to review for inaccuracies.**    
# Summary    
The purpose of this workflow is to extract specific fields from a document (new_claim.pdf), analyze the content using a custom model (claim-forms-model2), extract relevant information such as form type, claim ID, policy number, etc., and then join this extracted data with the sentiment analysis of the incident description. Finally, the workflow creates a CSV file containing the extracted claim fields and incident sentiment and stores it in a specified Azure Blob Storage container.    
||Workflow Properties|Value|    
|-----|-----|-----|    
|1|Connector type - In App|7|    
|2|Connector type - Shared|3|    
|3|Connector type - Custom|0|    
|4|API Connections|3|    
    
# Workflow Steps    
## How the workflow starts (Triggers)    
 - **Claim_Trigger**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** The Claim_Trigger Trigger is activated when a blob is added or modified in a specific Azure Blob Storage container.    
&ensp;&ensp; - **Trigger Input:** The input parameters include the path of the Azure Blob Storage container where the trigger is monitoring for new blobs.    
&ensp;&ensp; - **Trigger Output:** This trigger does not have any specific outputs.    
    
## How the workflow continues (Actions)    
 - **Get_New_Claim**    
&ensp;&ensp; - **Type:** Shared    
&ensp;&ensp; - **Description:** Retrieve the content of a new claim PDF file from the specified Azure Blob Storage container.    
&ensp;&ensp; - **Action Input:** The input parameters include the connection reference to Azure Blob Storage, method (get), path to get the file content, and query parameters for file path, inferContentType, and queryParametersSingleEncoded.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Extract_claim_fields_Custom_model**    
&ensp;&ensp; - **Type:** Shared    
&ensp;&ensp; - **Description:** Extract fields from the new claim PDF file using a custom model in the Form Recognizer API.    
&ensp;&ensp; - **Action Input:** The input parameters include the connection reference to the Form Recognizer API, method (post), headers with the file URL, path for analyzing document with the custom model, and query parameter for the API version.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Extracted_claim_data**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** Extract various claim-related data fields from the analyzed document using the custom model.    
&ensp;&ensp; - **Action Input:** The input fields consist of data extraction expressions for different fields like form_type, claim_id, policy_number, etc., based on the extracted document content.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Create_csv_in_blob**    
&ensp;&ensp; - **Type:** Shared    
&ensp;&ensp; - **Description:** Create a CSV file containing the extracted claim information and sentiment analysis results and store it in the Azure Blob Storage container.    
&ensp;&ensp; - **Action Input:** The input parameters include the connection reference to Azure Blob Storage, method (post), body with the extracted claim data and sentiment analysis results, headers for metadata retrieval, and queries for folder path and file name.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Join_Claim_and_Inc_Sentiment**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** Combine the extracted claim data and incident sentiment analysis results into a single output for further processing.    
&ensp;&ensp; - **Action Input:** The input parameters include different fields from both the extracted claim data and the incident sentiment analysis result to create a unified dataset.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Extract_Incident_Description**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** Extract the incident description field from the analyzed document using the custom model in Form Recognizer.    
&ensp;&ensp; - **Action Input:** The input parameter is the incident description field extracted from the analyzed document content.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Call_GPT4_Sentiment_analysis**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** Invoke a custom HTTP endpoint to perform sentiment analysis on the extracted incident description using the GPT-4 model.    
&ensp;&ensp; - **Action Input:** The input parameters include the URI for the HTTP request, method (POST), headers with the API key, body with messages and analysis request details.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Extract_GPT-4_output**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** Extract the sentiment analysis output from the response of the GPT-4 sentiment analysis call.    
&ensp;&ensp; - **Action Input:** The input parameter is the content of the sentiment analysis message from the GPT-4 response.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.    
 - **Extract_Incident_Sentiment**    
&ensp;&ensp; - **Type:** In App    
&ensp;&ensp; - **Description:** Extract the sentiment analysis result from the GPT-4 response for further processing and integration with the claim data.    
&ensp;&ensp; - **Action Input:** The input parameter is the sentiment analysis result extracted from the GPT-4 response.    
&ensp;&ensp; - **Action Output:** This action does not have any specific outputs.  