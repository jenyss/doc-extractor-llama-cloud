# doc-extractor-llama-cloud

This project is a document extraction and transformation pipeline powered by LlamaCloud and Pydantic. It reads a mapping schema from Excel, extracts structured data from documents (Excel, PDF) , transforms it based on predefined rules, and exports it to a clean, import-ready Excel file. Perfect for automating manual data entry and converting messy documents into structured formats.

If you have any questions or would like to collaborate, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/jenya-stoeva-60477249/). You're more than welcome!

## How It Works
1. Loads a field mapping schema from an Excel file.
2. Dynamically generates a Pydantic schema based on the mapping.
3. ❗❗❗ Uses LlamaCloud to extract structured data from a PDF or Excel document. You MUST swap .xlsx format with .pdf for the service to work with Excel since there is some superficial validation which allows only PDFs but the extractor works in fact great with Excel files as well.
4. Maps the extracted JSON data to final column names using a second Excel mapping.
5. Exports the cleaned and transformed data to a ready-to-use Excel template.
6. Ideal for automating document processing and reducing manual data cleanup.

## How-To
coming soon....

