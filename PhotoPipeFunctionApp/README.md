# PhotoPipe — Event-Driven Image Processing
## Akash Nadackanal Vinod (041156265)
## Demo Video
[Lab 04 Youtube Demo](https://youtu.be/YAj_FJNCUyw)

This project implements an event-driven image processing pipeline using Azure Event Grid and Azure Functions. It processes images uploaded to Azure Blob Storage, generating metadata and thumbnails, and logs processing events for auditing.

## Setup Instructions

1. **Deploy Azure Resources**:
   - Create a Resource Group.
   - Create a Storage Account with two blob containers: `image-uploads` (Blob anonymous read access) and `image-results` (Private).
   - Configure Storage Account CORS to allow `*` for GET, PUT, OPTIONS, HEAD.

2. **Deploy the Azure Function**:
   - The code is located in the `PhotoPipeFunctionApp` folder (`function_app.py`).
   - Create a Python Azure Function App.
   - Deploy the project to Azure.
   - Add `STORAGE_CONNECTION_STRING` to your Function App configuration with your Storage Account connection string.
   - Enable CORS with `*` on your Function App.

3. **Configure Event Grid**:
   - Create a System Topic routing from your Blob Storage.
   - Subscription 1 `process-image-sub`: Filter to `/blobServices/default/containers/image-uploads` and extensions `.jpg`/`.png`. Route to `process-image` function.
   - Subscription 2 `audit-log-sub`: Filter to `/blobServices/default/containers/image-uploads`. Route to `audit-log` function.

4. **Client Setup**:
   - Open `client.html`.
   - Update the configuration constants (`Storage Account Name`, `SAS Token`, `Function App URL`).
   - Run the client and upload images.
