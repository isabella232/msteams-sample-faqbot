
# Teams FAQ Bot

This project serves as a starting point to developing a Teams FAQ Bot using [QnA Maker](https://www.qnamaker.ai/). Two projects are included in the solution:

* FaqBot.csproj
* FaqMdParser.csproj

### FaqBot
Contains the Teams Bot API that the client interacts with. 

Learn more about building [Teams Bots](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/bots/bots-create).

### FaqMdParser
Contains code for a simple command line application that helps parse out markdown formatted files into a consistent tab structure that can be uploaded to a QnA Maker Knowledge Base. The application will an .md file using # and ## headers in a file into tab separated values output as a .tsv. See [Using FaqMdParser](#using-faqmdparser).

## Getting Started

1. Deploy a [QnA Maker Service]((https://www.qnamaker.ai/))
2. Create a new QnA Maker Knowledge Base
3. [Register and create](https://docs.microsoft.com/en-us/microsoftteams/platform/concepts/bots/bots-create#create-a-bot-for-microsoft-teams) a new Teams Bot application 
4. Update the web.config appSettings inside of the FaqBot.csproj with values obtained from steps 1-3
5. Build and run/deploy the FaqBot
6. Upload content to your Knowledge Base
7. Talk to bot

### Using FaqMdParser
Natively, Knowledge Base doesn't accept .md as a file extension. If you have files written in markdown (ex. an FAQ in GitHub), the files need to be converted into a formation accepted by the Knowledge Base. You could use a tool such as Pandoc to convert the .md file into another format that the Knowledge Base accepts. However, this can lead to imprecise outcomes due to the semi-structure nature of the document. The alternative is to convert the .md files into a structured format so that there's no ambiguity when uploaded tot he Knowledge Base service. THe FaqMdParser, converts the content of an .md file into tab separated key and value pairs by using h1 and h2 header tags (# and ##) as key markers. The value of each pair is the content between headers.

To use the parser, build the project, navigate to the output bin and run the following command:
```
FaqMdParser.dll -f "[input file path]" -p "[output dir]" -n "[output file name]"
```

Two additonal flags are included:
***-o***: Overwrites the output file, if exists. Default behavior is to append to end of output file.
***-h***: Appends bolded headers to the content strings per tab pair.

sample output of :
```
.md file contents:

## Header
content text below header.

output:

***Header***</br>content text below header.
```

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., label, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
