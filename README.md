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
1. Install dependencies (at the top of the Notebook).
2. Load evironment variables in ```helper.py```
3. Prepare your input files. You’ll need:

   * A mapping Excel file (Mapping_Table.xlsx) that defines the fields to extract (extraction schema) and the how these fields will be mapped to the columns in the produced .xlsx file.
     *Column A: (Data source) Field name
     * Column B: (Data source) Field description
     * Column C: (Data source) Field type
     * Column D: Default value - to be populated on every row in the produced excel
     * Column E: (Data target) Transposed column containing the names of the columna that will be available in the produced excel.
   * A source PDF (CatalogueSept2024.pdf) that contains the unstructured data. It should contain field names/labels for the extraction to work reliably.

   Put them in a data/ folder (or update the paths as needed).

4. Run the tool step by step
   * **Step 1:** Generate the schema from Excel. This reads the field definitions and dynamically builds a Pydantic model.<br>
     ```schema = generate_schema_from_excel("data/Mapping_Table.xlsx")```
   * **Step 2:** Extract data from your PDF using LlamaCloud. This extracts structured rows from the document.<br>
     ```result = extract_data_from_pdf("data/CatalogueSept2024.pdf", schema)```
   * **(Optional) Step 3:** Preview and save the raw JSON. Print, if you want to inspect the extracted data.<br>
     ```print_and_save_json(result, "extracted_data.json")```
   * **Step 4:** Map the extracted data to final column names. This step applies the field mapping and outputs a clean Excel file.<br>
     ```map_and_export_to_excel(result, "data/Mapping_Table.xlsx", "import_template.xlsx")```

