# fill-pdf
***No installations are needed***, just a simple **Google Account**. 

This Jupyter notebook .ipynb **fills automatically custom .PDF file with data from Google Drive Sheets.** 

It is running on Google Colaboratory https://colab.research.google.com/ . 

This specific notebook works only for our use case, but it is nice to see the connection of Google Collaboratory, Google Drive Folder and Google Drive Sheets. 

Prerequisities: Google Drive Sheet (e.g. https://docs.google.com/spreadsheets/d/1DdI_5u6N1cfe71HsWsgpvs-bdJeG9cgllwnFFJgIOzA/edit?usp=sharing) AND this .ipynb notebook uploaded to https://colab.research.google.com/ .

## Walk Through Code
To connect your Google Drive to Google Colaboratory: 
```python
from google.colab import auth
auth.authenticate_user()
```

To work with Google Drive Sheet I used **gspread** library, which I find extremely easy to use. 
```python
import gspread
from google.auth import default
creds, _ = default()

gc = gspread.authorize(creds)
```

In order to work with the sheet you just put the name of the file you want to work with. 
```python
sheet_name = "YouPutHereTheFileNameofYourGoogleDriveSheet"
worksheet = gc.open(sheet_name)
```

To upload a .pdf file which you want to use, you can simply use gdown and id reference (e.g:) : 
```python
! gdown --id 1eWhRtxxxxxxxxxxxx_rPnhN
```
**How to get an Google Drive File ID?** 
![alt text](https://github.com/CesurMurka/fill-pdf/blob/main/Unted.png)


In order to fill .pdf I used fillpdf library  https://pypi.org/project/fillpdf/
```python
!pip install fillpdf
import fillpdf
```

To download a filled out .pdf
```python
from google.colab import files
files.download(output_pdf_path)
```

## **FYI**, if you are interested: 
This .pdf file contains 60 empty boxes. These boxes are filled from the Google Drive sheets. The boxes represents the radiation dose in Grays. 
**TSEI (total skin electron irradiation)** technique was used for skin treatment. 

https://humanhealth.iaea.org/HHW/MedicalPhysics/Radiotherapy/Topicsofspecialinterest/TSEI/index.html

We measured this dose from the 60 TLD (thermoluminiscent dosimeters), which were sticked on the patient during the treatment on linear accelerator. 
