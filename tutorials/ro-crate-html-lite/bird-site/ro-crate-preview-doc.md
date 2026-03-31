# Building plant and animal sites using ro-crate-html-lite

This documentation shows how to create a HTML site for a collection of Indigenous plant and animal content. The process can be adapted to any data collection with adjustments as needed to metadata properties and templates as suits the collection.

In this example, entries have metadata describing the name and description in an Aboriginal language; translations in English; scientific names; images; audio recordings of calls, names and descriptions; along with photographer and speaker credits.

The process of creating HTML previews of data uses the RO-Crate data standard, Crate-O and the ro-crate-html-lite library. An RO-Crate is a method of storing data, in which data files (e.g. audio recordings or images) are stored on disk alongside a metadata file and licence information (REF). Crate-O is a browser-based tool for creating or converting RO-Crates, and in this activity will be used to create a spreadsheet of content into an RO-Crate. The ro-crate-html-lite tool is used to generate HTML preview versions of the RO-Crate.


## Prepare media assets

Convert your media into web-ready formats. Use MP3 for audio, and JPG or PNG for images.

Organise the collection files into folders. We used the following structure of a parent `files` directory, with subdirectories for `audio` and `images`. In the `audio` directory, we used subdirectories to group the `calls`, `names` and `sentences` recordings.

```
files
├── audio
│     ├── calls
│     │     ├── audio-1.mp3
│     │     └── audio-2.mp3
│     ├── names
│     │     ├── audio-3.mp3
│     │     └── audio-4.mp3
│     └── sentences
│           ├── audio-5.mp3
│           └── audio-6.mp3
└── images
      ├── image-1.jpg
      └── image-2.jpg
```


## Prepare data in a spreadsheet

When working with existing content that has been compiled for other publications, the data preparation step involves copying content from source documents into relevant cells in a spreadsheet. For other collections, a spreadsheet may be automatically generated from a database export or content entered into the spreadsheet from scratch.


### Download template spreadsheet

To suit the RO-Crate preview generation process, the spreadsheet must be in an RO-Crate compatible format. A sample, very generic, RO-Crate template spreadsheet is available here [link]. For projects that are similar to this plant and animal project, use this template [link] as a starting point, as the collection properties have been tailored to the content format.


### Enter details

Start with the RootDataset worksheet/tab. Change the name and description information to suit your collection.


##### Entries

Change to the Entries worksheet. For each item in the collection, fill out the name, alternateName, sentence, translation, sentenceTranslation, scientificName, speaker and photographerName properties. These columns are optional, so if your collection doesn't have this information, leave them empty.

The @id, @type, datePublished and licence columns are required by the RO-Crate standard and are mandatory. @id should be automatically generated in the spreadsheet based on the value in the name column. If you don't have name information, you will need to make up IDs for your entries. The ID format is prefixed with a hash character.


#### Licences

If your entries are licenced under a Creative Commons licence, or some other licence that is available via a URL, enter the URL in the licence column, for example `https://creativecommons.org/licenses/by/4.0/`. For guidance on adding licence information for non-URL situations, see the LDaCA guide (https://www.ldaca.edu.au/resources/user-guides/crate-o/convert-spreadsheet/#licenses). 


#### Assets

Enter the respective file paths to each entry's media assets in the columns `image`, `nameAudio` and `sentenceAudio`. For example:

| isRef_custom:image | isRef_custom:nameAudio | isRef_custom:sentenceAudio |
| --- | --- | --- |
| files/images/pulinyMA&DM.JPG | files/audio/names/puliny_VW.mp3 | files/audio/sentences/puliny.mp3 |


#### Files

Now add information about the media assets into the Files worksheet. Make one row per asset file. The `@id` is the path to the file, e.g. `files/audio/calls/audio-1.mp3`. For `@type`, enter `File`. For `isRef_isPartOf`, copy or enter the `@id` of this asset's entry, e.g. `#puliny`. Make sure to paste the value when copying, not the `@id` formula.

Tip: copy the last three columns from Entries into Files and transpose when pasting to get one row per file, then add @type and the @id of the entry that each file is associated with.


## Package as RO-Crate

We used Crate-O, a browser-based tool to convert the spreadsheet into RO-Crate.

Open [Crate-O](https://language-research-technology.github.io/crate-o/#/) in Chrome (Safari isn't supported).

Click `Open directory` and browse to the location where the spreadsheet is saved. This will create an empty RO-Crate in memory.

Click `Bulk Add` and browse to the spreadsheet. Click confirm to load the spreadsheet data. Now the RO-Crate in memory is populated with the data from the spreadsheet. The collection information and entry data should be visible in Crate-O.

Click `Save`. This will write a metadata JSON file and default HTML preview file to your working folder.


## Build HTML

To build template-based HTML preview, we first clone the `ro-crate-html-lite` tool repository and then adjust configuration and template files as needed.


### Install

Clone `ro-crate-html-lite` from https://github.com/Language-Research-Technology/ro-crate-html-lite.

Enter the directory and install the dependencies with `npm install .`


### Prepare project

In the `test_data` folder, duplicate the `birds` folder. Rename it `test_project` or something to suit your content.

Move your `files` directory and `ro-crate-metadata.json` into the `test_project/data` folder. Your project should now look like this—

```
test_project
├── data
│   ├── about
│   ├── files
│   └── ro-crate-metadata.json
├── config.json
└── templates
    ├── about-template.html
    ├── person-template.html
    ├── root-template.html
    └── subobject-template.html

```


### Generate HTML

At this point, if you aren't customising templates, you can build the HTML. Update the paths to the config and data folders in the following command as required for your project, then run the command from the root of the repositry.

```
node index.js -m test_data/test_project/config.json test_data/test_project/data
```

This will result in HTML preview files being built in the data directory. Open the `ro-crate-preview.html` file in a browser to confirm.


### Customise HTML templates

This example uses the multi-page mode of html-lite. Pages can be built according to different types of objects. The template used for each type of object is specified in config.json. In this example, we use one template for the home page, one for entries, one for people, and the about page.

Templates use [Nunjucks template language](https://mozilla.github.io/nunjucks/). In Nunjucks templates, data is loaded 

If you are changing the templates from this example, update template paths in config.json to suit your project.



### Customise OG

Modify the `og` tags in the templates to suit your project. These tags define how the site URL appears when it is shared by social media/SMS etc.

Create an image to be used as the sharing preview. Save it in the `files` directory and update the path in the `og` tags. Note that the `og:image` dimensions are recommended to be 1200 x 630 pixels, with a max file size of 5mb (but should be heaps less than that).


## Publish

After building the HTML, it can be published on a web server. The RO-Crate specification prefers the file name of the generated HTML preview to be `ro-crate-preview.html`. Either update server configs to use that as the default name, or make a redirection from `index.html` to `ro-crate-preview.html`. Adapt this example

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta property="og:url" content="https://bird-apps.com/index.html" />
    <meta property="og:type" content="website" />
    <meta property="og:title" content="Birds" />
    <meta property="og:description" content="Stories about birds" />
    <meta property="og:image" content="http://bird-apps.com/files/og-img.jpg" />
    <meta property="og:image:secure_url" content="https://bird-apps.com/files/og-img.jpg" />
    <meta property="og:image:width" content="1200" />
    <meta property="og:image:height" content="630" />
    <meta http-equiv="refresh" content="0;url=ro-crate-preview.html" />
  <title>Birds</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
  <h1>Birds</h1>
  <p>stories about birds</p>
</body>
</html>
```
