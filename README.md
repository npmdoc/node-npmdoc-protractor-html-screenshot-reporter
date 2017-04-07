# api documentation for  [protractor-html-screenshot-reporter (v0.0.21)](https://github.com/jintoppy/protractor-html-screenshot-reporter)  [![npm package](https://img.shields.io/npm/v/npmdoc-protractor-html-screenshot-reporter.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-protractor-html-screenshot-reporter) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-protractor-html-screenshot-reporter.svg)](https://travis-ci.org/npmdoc/node-npmdoc-protractor-html-screenshot-reporter)
#### An npm module and grunt plugin which generates your Protractor test reports in HTML with screenshots

[![NPM](https://nodei.co/npm/protractor-html-screenshot-reporter.png?downloads=true)](https://www.npmjs.com/package/protractor-html-screenshot-reporter)

[![apidoc](https://npmdoc.github.io/node-npmdoc-protractor-html-screenshot-reporter/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-protractor-html-screenshot-reporter_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-protractor-html-screenshot-reporter/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-protractor-html-screenshot-reporter/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-protractor-html-screenshot-reporter/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Jinto Jose",
        "email": "jintoppy@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/jintoppy/protractor-html-screenshot-reporter/issues"
    },
    "dependencies": {
        "mkdirp": "~0.3.5",
        "underscore": "~1.6.0"
    },
    "description": "An npm module and grunt plugin which generates your Protractor test reports in HTML with screenshots",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "0744988b5720ae67ad2b7653eeb4a669e4710833",
        "tarball": "https://registry.npmjs.org/protractor-html-screenshot-reporter/-/protractor-html-screenshot-reporter-0.0.21.tgz"
    },
    "gitHead": "913be5e06fea093cf8d172a57e21e5c642e82e5e",
    "homepage": "https://github.com/jintoppy/protractor-html-screenshot-reporter",
    "keywords": [
        "screenshot",
        "selenium",
        "protractor",
        "jasmine",
        "reporter",
        "gruntplugin",
        "protractor html report"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "jintoppy",
            "email": "jintoppy@gmail.com"
        }
    ],
    "name": "protractor-html-screenshot-reporter",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/jintoppy/protractor-html-screenshot-reporter.git"
    },
    "scripts": {},
    "version": "0.0.21"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module protractor-html-screenshot-reporter](#apidoc.module.protractor-html-screenshot-reporter)
1.  object <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.</span>jsonparser
1.  object <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.</span>util

#### [module protractor-html-screenshot-reporter.jsonparser](#apidoc.module.protractor-html-screenshot-reporter.jsonparser)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.jsonparser.</span>processJson (jsonData, options)](#apidoc.element.protractor-html-screenshot-reporter.jsonparser.processJson)

#### [module protractor-html-screenshot-reporter.util](#apidoc.module.protractor-html-screenshot-reporter.util)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>addMetaData (metaData, baseName, descriptions, options)](#apidoc.element.protractor-html-screenshot-reporter.util.addMetaData)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>gatherDescriptions (suite, soFar)](#apidoc.element.protractor-html-screenshot-reporter.util.gatherDescriptions)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>generateGuid ()](#apidoc.element.protractor-html-screenshot-reporter.util.generateGuid)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>removeDirectory (dirPath)](#apidoc.element.protractor-html-screenshot-reporter.util.removeDirectory)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>storeMetaData (metaData, file)](#apidoc.element.protractor-html-screenshot-reporter.util.storeMetaData)
1.  [function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>storeScreenShot (data, file)](#apidoc.element.protractor-html-screenshot-reporter.util.storeScreenShot)



# <a name="apidoc.module.protractor-html-screenshot-reporter"></a>[module protractor-html-screenshot-reporter](#apidoc.module.protractor-html-screenshot-reporter)



# <a name="apidoc.module.protractor-html-screenshot-reporter.jsonparser"></a>[module protractor-html-screenshot-reporter.jsonparser](#apidoc.module.protractor-html-screenshot-reporter.jsonparser)

#### <a name="apidoc.element.protractor-html-screenshot-reporter.jsonparser.processJson"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.jsonparser.</span>processJson (jsonData, options)](#apidoc.element.protractor-html-screenshot-reporter.jsonparser.processJson)
- description and source-code
```javascript
function processJson(jsonData, options){
    passCount=0;
    failCount = 0;
    reporterOptions = options;
    var jsonStr = "<ul>";
    formattedJson = [];
    currentFormattedDataIndex = 0;

    _.each(jsonData, function (value) {
        var descArr = value.description.split('|').reverse();
        if (descArr.length > 0) {
            formatData(value, descArr);
        }
    });



    function parseJSON(element) {
        if(element.children){

            jsonStr += '<li>'+element.desc+ '<ul>';
            element.children.forEach(function (child, index, childArr) {
                if (child.children) {
                    parseJSON(child);
                }else{
                    var ss = generateHTML(child);
                    jsonStr += '<li>' + ss +'</li>';
                    if(index === childArr.length-1){
                        jsonStr += '</ul></li>';
                    }
                }
            });
            return jsonStr;
        }

    }

    var tableHtml = "";
    formattedJson.forEach(function (element) {
        jsonStr = "";
        tableHtml += parseJSON(element);
        tableHtml += new Array(element.depth-1).join('</ul></li>');

    });
    tableHtml = '<ul>' + tableHtml + '</ul>';
    tableHtml += "<div><h2><u>Results summary</u></h2>";
    tableHtml += "<b>Total tests passed</b>: "+ passCount +" <br/> <b>Total tests failed</b>: "+ failCount +" <br/> This report
generated on "+new Date()+" </div>";

    // //updating the document title
    // var docTitleRegex = new RegExp('{{reportTitle}}');
    // staticHTMLContentprefix =  staticHTMLContentprefix.replace(docTitleRegex, reporterOptions.docTitle);
    // return staticHTMLContentprefix + tableHtml + staticHTMLContentpostfix;
    var finalHtml = phssr.makeHTMLPage(tableHtml, reporterOptions);
    return finalHtml;
}
```
- example usage
```shell
...

function addHTMLReport(jsonData, baseName, options){
	var basePath = path.dirname(baseName),
		htmlFile = path.join(basePath, options.docName),
		stream;

	stream = fs.createWriteStream(htmlFile);
	stream.write(jsonParser.processJson(jsonData, options));
	stream.end();

}

function addMetaData(metaData, baseName, descriptions, options){
	var json,
		stream,
...
```



# <a name="apidoc.module.protractor-html-screenshot-reporter.util"></a>[module protractor-html-screenshot-reporter.util](#apidoc.module.protractor-html-screenshot-reporter.util)

#### <a name="apidoc.element.protractor-html-screenshot-reporter.util.addMetaData"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>addMetaData (metaData, baseName, descriptions, options)](#apidoc.element.protractor-html-screenshot-reporter.util.addMetaData)
- description and source-code
```javascript
function addMetaData(metaData, baseName, descriptions, options){
	var json,
		stream,
		basePath = path.dirname(baseName),
		file = path.join(basePath, options.combinedJsonFileName);
	try {
		metaData.description = descriptions.join('|');
		json = metaData;
		var currentData;
		try{
			currentData = JSON.parse(fs.readFileSync(file, {
				encoding: 'utf8'
			}));
			if(currentData.length && currentData.length>0){
				currentData.push(json);
			}
			json = currentData;
		}catch(e){
			json = [json];
		}
		stream = fs.createWriteStream(file);
		stream.write(JSON.stringify(json));
		stream.end();

		addHTMLReport(json, baseName, options);
	} catch(e) {
		console.error('Could not save meta data');
	}

}
```
- example usage
```shell
...
				, directory = path.dirname(screenShotPath);

			metaData.screenShotFile = screenShotFile;
			mkdirp(directory, function(err) {
				if(err) {
					throw new Error('Could not create directory ' + directory);
				} else {
					util.addMetaData(metaData, metaDataPath, descriptions, self.finalOptions);
					if(takeScreenshot) {
						util.storeScreenShot(png, screenShotPath);
					}
					if (!self.finalOptions.disableMetaData) {
						util.storeMetaData(metaData, metaDataPath);
					}
				}
...
```

#### <a name="apidoc.element.protractor-html-screenshot-reporter.util.gatherDescriptions"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>gatherDescriptions (suite, soFar)](#apidoc.element.protractor-html-screenshot-reporter.util.gatherDescriptions)
- description and source-code
```javascript
function gatherDescriptions(suite, soFar) {
	soFar.push(suite.description);

	if(suite.parentSuite) {
		return gatherDescriptions(suite.parentSuite, soFar);
	} else {
		return soFar;
	}
}
```
- example usage
```shell
...
	}

	takeScreenshot = !(self.takeScreenShotsOnlyForFailedSpecs && results.passed());

	finishReport = function(png) {

		browser.getCapabilities().then(function (capabilities) {
			var descriptions = util.gatherDescriptions(
					spec.suite
					, [spec.description]
				)


				, baseName = self.pathBuilder(
					spec
...
```

#### <a name="apidoc.element.protractor-html-screenshot-reporter.util.generateGuid"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>generateGuid ()](#apidoc.element.protractor-html-screenshot-reporter.util.generateGuid)
- description and source-code
```javascript
function generateGuid() {
    var buf = new Uint16Array(8);
    buf = crypto.randomBytes(8);
    var S4 = function(num) {
            var ret = num.toString(16);
            while(ret.length < 4){
                    ret = "0"+ret;
            }
            return ret;
    };

    return (
            S4(buf[0])+S4(buf[1])+"-"+S4(buf[2])+"-"+S4(buf[3])+"-"+
            S4(buf[4])+"-"+S4(buf[5])+S4(buf[6])+S4(buf[7])
    );
}
```
- example usage
```shell
...
*                             in-depth information about the Selenium node
*                             which executed the test case.
*
* Returns:
*     (String) containing the built path
*/
function defaultPathBuilder(spec, descriptions, results, capabilities) {
	return util.generateGuid();
}

/** Function: defaultMetaDataBuilder
* Uses passed information to generate a meta data object which can be saved
* along with a screenshot.
* You do not have to add the screenshots file path since this will be appended
* automatially.
...
```

#### <a name="apidoc.element.protractor-html-screenshot-reporter.util.removeDirectory"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>removeDirectory (dirPath)](#apidoc.element.protractor-html-screenshot-reporter.util.removeDirectory)
- description and source-code
```javascript
function removeDirectory(dirPath){
	try { var files = fs.readdirSync(dirPath); }
      catch(e) { return; }
      if (files.length > 0)
        for (var i = 0; i < files.length; i++) {
          var filePath = dirPath + '/' + files[i];
          if (fs.statSync(filePath).isFile())
            fs.unlinkSync(filePath);
          else
            removeDirectory(filePath);
        }
      fs.rmdirSync(dirPath);
}
```
- example usage
```shell
...
		docTitle: this.docTitle,
		docHeader: this.docHeader,
		docName: this.docName,
		cssOverrideFile: this.cssOverrideFile
	};

	if(!this.preserveDirectory){
		util.removeDirectory(this.finalOptions.baseDirectory);
	}
}

/** Function: reportSpecResults
* Called by Jasmine when reporting results for a test spec. It triggers the
* whole screenshot capture process and stores any relevant information.
*
...
```

#### <a name="apidoc.element.protractor-html-screenshot-reporter.util.storeMetaData"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>storeMetaData (metaData, file)](#apidoc.element.protractor-html-screenshot-reporter.util.storeMetaData)
- description and source-code
```javascript
function storeMetaData(metaData, file) {
	var json
		, stream;

	try {
		json = JSON.stringify(metaData);
		stream = fs.createWriteStream(file);

		stream.write(json);
		stream.end();
	} catch(e) {
		console.error('Could not save meta data for ' + file);
	}
}
```
- example usage
```shell
...
					throw new Error('Could not create directory ' + directory);
				} else {
					util.addMetaData(metaData, metaDataPath, descriptions, self.finalOptions);
					if(takeScreenshot) {
						util.storeScreenShot(png, screenShotPath);
					}
					if (!self.finalOptions.disableMetaData) {
						util.storeMetaData(metaData, metaDataPath);
					}
				}
			});
		});

	};
...
```

#### <a name="apidoc.element.protractor-html-screenshot-reporter.util.storeScreenShot"></a>[function <span class="apidocSignatureSpan">protractor-html-screenshot-reporter.util.</span>storeScreenShot (data, file)](#apidoc.element.protractor-html-screenshot-reporter.util.storeScreenShot)
- description and source-code
```javascript
function storeScreenShot(data, file) {
	var stream = fs.createWriteStream(file);

	stream.write(new Buffer(data, 'base64'));
	stream.end();
}
```
- example usage
```shell
...
			metaData.screenShotFile = screenShotFile;
			mkdirp(directory, function(err) {
				if(err) {
					throw new Error('Could not create directory ' + directory);
				} else {
					util.addMetaData(metaData, metaDataPath, descriptions, self.finalOptions);
					if(takeScreenshot) {
						util.storeScreenShot(png, screenShotPath);
					}
					if (!self.finalOptions.disableMetaData) {
						util.storeMetaData(metaData, metaDataPath);
					}
				}
			});
		});
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
