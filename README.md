# Pdf-Text-Extraction
import re
from pdfminer.high_level import extract_pages, extract_text
text = extract_text("ACHEMISTRY FINAL ASSIGNMENT.pdf")
print(text)

pattern = re.compile(r"[a-zA-Z]+,{1}\s{1}")
matches = pattern.findall(text)
names = [n[:-2] for n in matches]
print(names)

import fitz
import PIL.Image
import io
pdf = fitz.open("ACHEMISTRY FINAL ASSIGNMENT.pdf")
counter=1
for i in range(len(pdf)):
    page = pdf[i]
    images = page.get_images()
    for image in images:
        base_img =pdf.extract_image(image[0])
        image_data = base_img["image"]
        img = PIL.Image.open(io.BytesIO(image_data))
        extension = base_img["ext"]
        img.save(open(f"image{counter}.{extension}", "wb"))
        counter += 1
import tabula

tables = tabula.read_pdf("ACHEMISTRY FINAL ASSIGNMENT.pdf", pages="all")
df = tables[0]
print(df[df.Age > 30])
