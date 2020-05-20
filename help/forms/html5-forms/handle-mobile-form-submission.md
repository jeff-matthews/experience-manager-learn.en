---
title: Handle HTML5 Form Submission
description: Create HTML5 Form submission handler
feature: mobile-forms
topics: development
audience: developer
doc-type: article
activity: implement
version: 6.4,6.5
KT: 4418
---

# Submit Handler

HTML5 forms can be submitted to servlet hosted in AEM. The submitted data can be accessed in the servlet as an input stream. To submit your HTML5 form you need to add "HTTP Submit Button" on your form template using AEM Forms Designer

## Create your submit handler

A simple servlet can be created to handle the HTML5 form submission. The submitted data can then be extracted by using the following code. This [servlet](assets/html5-submit-handler.zip) is made available to you as part of this tutorial. Please install the [servlet](assets/html5-submit-handler.zip) using [package manager](http://localhost:4502/crx/packmgr/index.jsp)

```java{.line-numbers}
StringBuffer stringBuffer = new StringBuffer();
String line = null;
java.io.InputStreamReader isReader = new java.io.InputStreamReader(request.getInputStream(), "UTF-8");
java.io.BufferedReader reader = new java.io.BufferedReader(isReader);
while ((line = reader.readLine()) != null) {
    stringBuffer.append(line);
}
System.out.println("The submitted form data is " + stringBuffer.toString());

```


## Configure the Submit URL of the HTML5 form

![submit-url](assets/submit-url.PNG)

* Tap on the xdp and click _Properties_->_Adavanced_
* copy http://localhost:4502/content/AemFormsSamples/handlehml5formsubmission.html and paste this in the Submit URL text field
* Click _SaveAndClose_ button.

### Add entry in the Exclude Paths

* Navigate to [configMgr](http://localhost:4502/system/console/configMgr).
* Search for _Adobe Granite CSRF Filter_
* Add the following entry in the Excluded Paths section
* _/content/AemFormsSamples/handlehml5formsubmission_
* Save your changes

### Test the form

* Tap on the xdp template. 
* Click on _Preview_->Preview as HTML
* Enter some data in the form and click submit
* You should see the submitted data written to your server's stdout.log file

### Additional Reading

This [article](https://docs.adobe.com/content/help/en/experience-manager-learn/forms/document-services/generate-pdf-from-mobile-form-submission-article.html) on generating PDF from HTML5 form submission is also recommended.



