The study in this repo is inspired by Llama Hub's [`EmbeddedTablesUnstructuredRetrieverPack`](https://github.com/run-llama/llama-hub/tree/main/llama_hub/llama_packs/recursive_retriever/embedded_tables_unstructured) and AI Makerspace's [implementation](https://www.youtube.com/watch?v=oa82yoJ6zYc&t=862s) of it.

Although the pack successfully utilizes Llama-Index modules to parse and retrieve HTML content, the accuracy of responses for detailed queries that retrieve table content was open to improvement.

After careful inspection, it is seen that tables with complex structures are not parsed entirely correctly, which causes low accuracy.

The unstructured node parser takes a `llama_index.schema.Document` as input that is read with a LlamaIndex `FlatReader`. Even though this Document contains most of the html tags such as `<span>, <tr>, <td>` , and the `UnstructuredElementNodeParser` does a great job detecting the tables, it fails to extract the full information under some conditions including but not limited to:
* The table has merged cells
* The cell value includes references
* The cell value is a comma seperated list

This situation causes information loss, which can be recovered considering the original data source was an HTML and actually includes all the necessary tags to capture the information of the table perfectly.

Therefore, this notebook aims to follow the pipeline of the `EmbeddedTablesUnstructuredRetrieverPack` but just change the content of the `TextNode` objects that contain the tables with a custom function. The rest of the pipeline is the same but there is a noticeable improvement.

For easy access (and personal interest) the source document used for this study is the [Wikipedia page of UEFA Champions League](https://en.wikipedia.org/wiki/UEFA_Champions_League). However, I downloaded the page and worked locally to prevent changes in the source document from affecting the code.

### To reproduce the results

**Clone the repo**
`git clone ddddd`
**After creating your virtual environment (recommended), install the dependencies**
`git install requirements.txt`
**Run the notebook**