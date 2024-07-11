# ai4doc
Using AI for processing documents at scale


# Notebooks
1. `sec_comments.ipynb`: This notebook scrapes the SEC website to create a list of comments, and downloads all the PDF comments locally.  
2. `memo.ipynb`: This notebooks separates the memos from the rest of the PDF comments.  


# Annotation
To create the annotations, the Annotation Service from Layout Parser was used:
https://github.com/Layout-Parser/annotation-service
1. `git clone https://github.com/Layout-Parser/annotation-service.git`
2. `cd annotation-service`
3. `set DATA=./data CONFIG=labeling-config.xml`
4. `set MODEL=model.py`
5. `docker-compose up --build -d`
6. Wait for the build to finish, then go to to localhost:8080 and start annotating.

# Annotation Categories
1. Address
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
