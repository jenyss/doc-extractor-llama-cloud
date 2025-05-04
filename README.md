# doc-extractor-llama-cloud

This project is a document extraction and transformation pipeline powered by LlamaCloud and Pydantic. It reads a mapping schema from Excel, extracts structured data from documents (Excel, PDF) , transforms it based on predefined rules, and exports it to a clean, import-ready Excel file. Perfect for automating manual data entry and converting messy documents into structured formats.

**The fastest way to get started:** <br>
▶️ Run [LlamaCloudExtractor.ipynb on Colab](https://colab.research.google.com/drive/1V2Ylzp4swI1ea7j7dv58PJiSEIDGc_aZ?usp=sharing) <br>
📺 Watch [this video](https://youtu.be/zKinkcvX-pw) for a step-by-step guide.

If you have any questions or would like to collaborate, feel free to reach out to me on [LinkedIn](https://www.linkedin.com/in/jenya-stoeva-60477249/). You're more than welcome!

## How It Works
1. Loads a field mapping schema from an Excel file. See [Mappring_Table.xlsx](https://github.com/jenyss/doc-extractor-llama-cloud/blob/main/data/Mapping_Table.xlsx).
2. Dynamically generates a Pydantic schema based on the mapping.
3. ❗❗❗ Uses LlamaCloud to extract structured data from a PDF or Excel document. You MUST swap .xlsx format with .pdf for the service to work with Excel since there is some superficial validation which allows only PDFs but the extractor works in fact great with Excel files as well.
4. Maps the extracted JSON data to final column names using the Excel mapping.
5. Exports the cleaned and transformed data to a ready-to-use Excel template.

## How-To
1. Install dependencies (at the top of the Notebook).
2. Load evironment variables in ```helper.py```
3. Prepare your input files. You’ll need:

   * A mapping Excel file (Mapping_Table.xlsx) that defines the fields to extract (extraction schema) and how these fields will be mapped to the columns in the produced .xlsx file.
     * **Column A – Source Field Name:**
       The name of the field from the data source. 
     * **Column B – Source Field Description:**
       A brief description of what the field represents in the data source.
     * **Column C – Source Field Type:**
       The data type of the field (e.g., str, float, dict, list, etc).
     * **Column D – Default Value:**
       A default value to populate for every row in the resulting Excel file. Leave blank if not applicable.
     * **Column E – Target Column Name (Transposed):**
       The name of the corresponding column that will appear in the generated Excel file. This column represents the transformed output structure.

   * A source PDF (CatalogueSept2024.pdf) that contains the unstructured data. Put them in a data/ folder (or update the paths in the code as needed).
  
      Example: [CatalogSept2024.xlsx](https://github.com/jenyss/doc-extractor-llama-cloud/blob/main/data/CatalogSept2024.xlsx)<br>
      Example: [Mappring_Table.xlsx](https://github.com/jenyss/doc-extractor-llama-cloud/blob/main/data/Mapping_Table.xlsx)

4. Run the tool step by step
   * **Step 1:** Generate the schema from Excel. This reads the field definitions and dynamically builds a Pydantic model.<br>
     ```schema = generate_schema_from_excel("data/Mapping_Table.xlsx")```<br>
     
   * **Step 2:** Extract data from your PDF using LlamaCloud. This extracts structured rows from the document.You MUST swap .xlsx format with .pdf for the service to work with Excel since there is some superficial   validation which allows only PDFs but the extractor works in fact great with Excel files as well.<br>
     ```result = extract_data_from_pdf("data/CatalogSept2024.pdf", schema)```<br>
     
   * **(Optional) Step 3:** Preview and save the raw JSON. Print, if you want to inspect the extracted data.<br>
     ```print_and_save_json(result, "extracted_data.json")```<br>
     
   * **Step 4:** Map the extracted data to final column names. This step applies the field mapping and outputs a clean Excel file.<br>
     ```map_and_export_to_excel(result, "data/Mapping_Table.xlsx", "import_template.xlsx")```

