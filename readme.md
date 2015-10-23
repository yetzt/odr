# Open Data Repository

`Open Data Repository` specifies a git repository structure to store open data. This is version `0.0.1` of the specification.

The intent of this spec is to make open data accessible, portable and easily usable with software. This is achieved with machine readable metadata, univied access via git and strict license requirements.

## Repository

The data, license and metadata must be contained in a git repository and provided via git.

## Data

The data format should comply with the [Open Format Definition](http://opendefinition.org/ofd/)

## License

The repository must contain a file with the full license text. This file must be named `LICENSE` for a plain text formatted license or `LICENSE.md` for a markdown formatted license. 
The license must be an [Open Definition Approved License](http://opendefinition.org/licenses/)

## Readme

The repository must contain a file with a description of the data and it's format. This file must be named `README.md` and it's contents must be markdown formatted text.

## Metadata

The repository must contain a file with meta information on the data. This file must be named `opendata.json` and contain valid JSON formatted data. 

The format is based on [npm's package.json](https://docs.npmjs.com/files/package.json).

### Properties

#### name

You must give your data repository a name. It must be a string and match `/^[a-z0-9][a-z0-9\-]{0,213}$/`.

```
"name": "example"
```

#### version

You must version your data with a [semver](http://semver.org/) compatible version number.

The PATCH version number part must be incremented for added data with the same format. 
The MINOR version number part must be incremented for added data extending the format whilst maintaining backward compatibility.
The MAJOR version number must be incremented if the data format changes breaking backward compatibility.

```
"version": "1.0.0"
```

#### description

You should provide a brief description of your data.

```
"descriptions": "Measurements of Foos in a Bar"
```

#### license

Additionally to providing a [license file](#License) you must specify the used license or licenses within this field. This license must be an [Open Definition Approved License](http://opendefinition.org/licenses/).

This must be an [SPDX license expression syntax version 2.0 string](https://www.npmjs.com/package/spdx) or an object containing `type` and `url` properties.

Valid SPDX license strings are:

* `CC0-1.0` Creative Commons CCZero
* `PDDL-1.0` Open Data Commons Public Domain Dedication and Licence
* `CC-BY-4.0` Creative Commons Attribution 2.0
* `CC-BY-SA-4.0` Creative Commons Attribution Share Alike 4.0
* `ODbL-1.0` Open Data Commons Open Database License
* `CC-BY-1.0` Creative Commons Attribution 1.0
* `CC-BY-2.0` Creative Commons Attribution 2.0
* `CC-BY-2.5` Creative Commons Attribution 2.5
* `CC-BY-3.0` Creative Commons Attribution 3.0
* `CC-BY-SA-1.0` Creative Commons Attribution Share Alike 1.0
* `CC-BY-SA-2.0` Creative Commons Attribution Share Alike 2.0
* `CC-BY-SA-2.5` Creative Commons Attribution Share Alike 2.5
* `CC-BY-SA-3.0` Creative Commons Attribution Share Alike 3.0
* `GFDL-1.1 GNU` Free Documentation License v1.1
* `GFDL-1.2 GNU` Free Documentation License v1.2
* `GFDL-1.3 GNU` Free Documentation License v1.3
* `MirOS` MirOS Licence

For Open Definition Approved Licenses not listed in the SPDX License List, most notably the *Open Data Commons Attribution License (ODC-BY)*, please complain at SPDX and use the object notation

```
"license": { 
	"type": "ODC-By-1.0", 
	"url": "http://opendatacommons.org/licenses/by/1.0/"
}
```

or the SPDX *SEE LICENSE IN* expression.

```
"license": "SEE LICENSE IN LICENSE.md"
```

#### files

An array of files with data in them. 

```
"files": [
	"data.json",
	"data.csv",
	"geodata/data.geojson"
]
```

#### contributors

An array of contributors. Every contributor is an object with `name` and optionally `url` and/or `email` properties or a string `name <email> (url)`.
	
```
"contributors": [
	"Example <mail@example.org> (https://example.org)"
]
```

```
"contributors": [
	{
		"name": "Example",
		"email": "mail@example.org",
		"url": "https://example.org"
	}
]
```

#### repository

The repository where your data lives. Only git is supported right now.

```
"repository": { 
	"type" : "git",
	"url" : "https://github.com/opendata/opendata.git"
}
```

#### keywords

An array of keywords to describe your data

```
"keywords": [
	"geodata", "example"
]
```

#### homepage

Your data's homepage

```
"homepage": "https://example.org"
```

#### bugs

You may specify an url and/or email address, where people can report issues with your data. 

```
{
	"url" : "https://github.com/owner/project/issues",
	"email" : "project@hostname.com"
}
```

#### engines

You must specify the Open Data Repository Spec Version.

```
"engines": { 
	"odr": "0.0.1" 
} 
```

### Example:

``` json
{
	"name": "some-data",
	"version": "0.0.1",
	"description": "some example data",
	"license": "ODbL-1.0",
	"files": {
		"data.json"
	},
	"contributors": {
		"name": "yetzt"
	},
	"repository": {
		"type": "git",
		"url": "https://github.com/yetzt/odr.git"
	},
	"keywords": ["key","words"],
	"homepage": "https://github.com/yetzt/odr",
	"bugs": "https://github.com/yetzt/odr/issues",
	"engines": { "odr": "0.0.1" }
}
```
