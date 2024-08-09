# ai4doc
Using AI for processing documents at scale


# Create virtual environment
`conda create -n "py312sec" python=3.12`
`conda create -n "py312test" python=3.12`

# Notebooks
1. `sec_comments.ipynb`: This notebook scrapes the SEC website to create a list of comments, and downloads all the PDF comments locally.  
2. `memo.ipynb`: This notebooks separates the memos from the rest of the PDF comments.  
3. `create_train_val_test_data.ipynb`: This notebook splits the data into train, val, and test data. It creates images and annotations. Annotations are dicts containing ID, text and boundary boxes.  

# Other Notebooks  
1. `fiftyone.ipynb`: This notebook launches a platform for tagging annotations.  
2. `layout_parser.ipynb`: Test notebook. This is just for playing around with `layout_parser` package, and can be ignored.  
3. `pytesseract.ipynb`: Test notebook. This is just for playing around with `pytesseract` package, and can be ignored.  


# Annotation Methodology
https://github.com/DS4SD/DocLayNet?tab=readme-ov-file#download

https://raw.githubusercontent.com/DS4SD/DocLayNet/main/assets/DocLayNet_Labeling_Guide_Public.pdf

https://medium.com/@pierre_guillou/document-ai-processing-of-doclaynet-dataset-to-be-used-by-layout-models-of-the-hugging-face-hub-308d8bd81cdb

# Annotation Tool - FiftyOne + CVAT
https://docs.voxel51.com/

1. Create the dataset using FiftyOne. See notebook `fiftyone.ipynb`.
2. Create an account on CVAT (https://app.cvat.ai/)
3. Set environment variables: 
```
set FIFTYONE_CVAT_USERNAME=...
set FIFTYONE_CVAT_PASSWORD=...
```

# Annotation Tool - Labelbox
https://docs.labelbox.com/reference/import-document-data

# Annotation Tool - Layout Parser
To create the annotations, the Annotation Service aka Label Studio from Layout Parser was used:
https://github.com/Layout-Parser/annotation-service
1. `git clone https://github.com/Layout-Parser/annotation-service.git`
2. `cd annotation-service`
3. Delete the example image in the `data` folder
3. `set DATA=./data`
4. `set CONFIG=labeling-config.xml`
4. `set MODEL=model.py`
5. `docker-compose up --build -d`
6. Wait for the build to finish, then go to to localhost:8080 and start annotating.
7. In the Setup tab, click `Named entity recognition`.
8. In the `Labeling Config`, paste the Labeling Config from the section below, in this README. Click `Save`.

# Annotation Categories
1. Header
2. Address
2. Date
3. Greeting
4. Subject
5. Paragraph
6. Page Number
7. Heading
8. Sub-heading
9. Signature
10. Footnotes
11. Footer
11. Appendix/Attachment
12. Other
13. Whitespace

# Labeling Config
```
<View>
  <Labels name="label" toName="text">
    <Label value="Header" background="rgb(255, 20, 147)"/>
    <Label value="Address" background="red"/>
    <Label value="Date" background="darkorange"/>
    <Label value="Greeting" background="orange"/>
    <Label value="Subject" background="green"/>
    <Label value="Paragraph" background="darkblue"/>
    <Label value="Page Number" background="blue"/>
    <Label value="Heading" background="purple"/>
    <Label value="Sub-heading" background="#842"/>
    <Label value="Signature" background="#428"/>
    <Label value="Footnotes" background="#482"/>
    <Label value="Footer" background="rgba(0,0,0,0.8)"/>
    <Label value="Appendix/Attachment" background="rgb(143, 188, 143)"/>
  </Labels>

  <Text name="text" value="$text"/>
</View>
```
