---
title: spec-format-ocr-hocr
tags: [hocr, ocr, pdf, spec]
created: 2026-01-30T10:44:43.790Z
modified: 2026-01-30T10:44:57.789Z
---

# spec-format-ocr-hocr

# guide

- https://github.com/UB-Mannheim/ocr-fileformat /MIT/202505/python/js
  - https://digi.bib.uni-mannheim.de/ocr-fileformat/
  - Validate and transform between OCR file formats (hOCR, ALTO, PAGE, FineReader)
  - The stylesheets are installed in $PREFIX/share/ocr-fileformat/xslt and can be used directly in your scripts and software. You will need to use an 
  - XSLT 2.0 capable stylesheet transformer.
  - https://github.com/OCR-D/ocrd_fileformat /apache2/python
    - OCR-D wrapper for ocr-fileformat
# spec

- 

## [hOCR - OCR Workflow and Output embedded in HTML](https://kba.github.io/hocr-spec/1.2/)

- resources
  - [hOCR - Wikipedia](https://en.wikipedia.org/wiki/HOCR)

- hOCR is an open standard of data representation for formatted text obtained from optical character recognition (OCR). 
  - The definition encodes text, style, layout information, recognition confidence metrics and other information using Extensible Markup Language (XML) in the form of Hypertext Markup Language (HTML) or XHTML
- The following OCR software can output the recognition result as hOCR file:
  - Tesseract
  - OCRopus
  - ghostscript
  - gImageReader

- The recognized text is stored in normal text nodes of the HTML file. The distribution into separate lines and words is here given by the surrounding span tags. Moreover, the usual HTML entities are used
  - Additional information is given in the properties such as:
  - different layout elements such as "ocr_par", "ocr_line", "ocrx_word"
  - geometric information for each element with a bounding box "bbox"

- The `bbox` - short for "bounding box" - of an element is a rectangular box around this element, which is defined by the upper-left corner (x0, y0) and the lower-right corner (x1, y1).
  - the values are with reference to the top-left corner of the document image and measured in pixels

- The hOCR format is most commonly used in order to make searchable PDF files or as an extracted metadata of the PDF file. In order to create searchable PDF files we can use a scanned document image and a .hocr file of the particular image.

```html
<p class="ocr_par" lang="deu" title="bbox930">
  <span class="ocr_line" title="bbox 348 797 1482 838; baseline -0.009 -6">
    <span class="ocrx_word" title="bbox 348 805 402 832; x_wconf 93">Die</span>
    <span class="ocrx_word" title="bbox 421 804 697 832; x_wconf 90">Darlehenssumme</span>
    <span class="ocrx_word" title="bbox 717 803 755 831; x_wconf 96">ist</span>
    <span class="ocrx_word" title="bbox 773 803 802 831; x_wconf 96">in</span>
    <span class="ocrx_word" title="bbox 821 803 917 830; x_wconf 96">ihrem</span>
    <span class="ocrx_word" title="bbox 935 799 1180 838; x_wconf 95">ursprünglichen</span>
    <span class="ocrx_word" title="bbox 1199 797 1343 832; x_wconf 95">Umfange</span>
    <span class="ocrx_word" title="bbox 1362 805 1399 823; x_wconf 95">zu</span>
    <span class="ocrx_word" title="bbox 1417 x_wconf 96">ver-</span>
  </span>
```

- 
- 
- 
- 

## [ALTO - Analyzed Layout and Text Object - Wikipedia](https://en.wikipedia.org/wiki/Analyzed_Layout_and_Text_Object)

- Analyzed Layout and Text Object (ALTO) is an open XML schema originally developed by the EU-funded METAe project.
  - ALTO files describe the placement, size, and style of text in an image of a digitized document, as well as other elements of the document's layout, such as margins, headings, columns, and illustrations.

```xml
<?xml version="1.0"?>
<alto>
  <Description>
    <MeasurementUnit/>
    <sourceImageInformation/>
    <Processing/>
  </Description>
  <Styles>
    <TextStyle/>
    <ParagraphStyle/>
  </Styles>
  <Layout>
    <Page>
      <TopMargin/>
      <LeftMargin/>
      <RightMargin/>
      <BottomMargin/>
      <PrintSpace/>
    </Page>
  </Layout>
</alto>
```

- Software support
  - ABBYY FineReader
  - Tesseract
  - Kitodo

- 
- 
- 

## spec-more

- ALTO XML
  - Library of Congress standard; detailed layout info, font data, confidence scores at word/character level 
- hOCR HTML/XHTML
  - HTML-based with microformats; preserves visual structure; supported by Tesseract 
- PAGE XML
  - PRImA format; supports region types (text, graphics, tables); polygon coordinates
- OCR-D XML
  - German standard for digitization; strict validation schemas

- 
- 
- 
- 

# faq

- 

# summary

- 

# dev

- 

# discuss-ocr
- ## 

- ## 

- ## 

- ## 
