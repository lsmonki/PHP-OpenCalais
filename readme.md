# Open Calais Tags #

Open Calais Tags is a PHP class for extracting entities and tags from text using [Open Calais](http://www.opencalais.com). Calais performs semantic analysis of the text, using natural language processing to identify concepts like people, companies and technologies discussed in the text. These are especially useful for suggesting tags for your content such as website articles or blog posts. You could even automatically tag archived content that would take days to go through manually.

Calais is free for both personal and commercial use, and usage of this class requires a Calais API key. Getting an API key is an easy, automated process. Just click the "Request API Key" link at the top of their site.

## Install via composer ##

Edit your composer.json file to include the following:

```json
{
    "require": {
        "lsmonki/php-open-calais": "2.x"
    }
}
```

## Usage ##

Basic usage is simple. Create an instance of the class with your API key, and call the getEntities method using your content string.

    $oc = new \OpenCalais\OpenCalais('your-api-key');
    $entities = $oc->getEntities($content);

getEntities method accepts two additional arguments: 
* float $relevance - From 0 to 1. Return only elements with greater than or equal relevance value. Default is 0.
* bool $flatten - Return flattened or nested array. Default is false (nested).

### Example input ###

> April 7 (Bloomberg) . Yahoo! Inc., the Internet company that snubbed a $44.6 billion takeover bid from Microsoft Corp., may drop in Nasdaq trading after the software maker threatened to cut its bid if directors fail to give in soon.
> If Yahoo.s directors refuse to negotiate a deal within three weeks, Microsoft plans to nominate a board slate and take its case to investors, Chief Executive Officer Steve Ballmer said April 5 in a statement. He suggested the deal.s value might decline if Microsoft has to take those steps.
> The ultimatum may send Yahoo Chief Executive Officer Jerry Yang scrambling to find an appealing alternative for investors to avoid succumbing to Microsoft, whose bid was a 62 percent premium to Yahoo.s stock price at the time. The deadline shows Microsoft is in a hurry to take on Google Inc., which dominates in Internet search, said analysts including Canaccord Adams.s Colin Gillis.

### Example output ###

    Array
    (
        [topics] => Array
            (
                [0] => Business_Finance
                [1] => Technology_Internet
            )

        [socialTag] => Array
            (
                [0] => Alibaba Group
                [1] => World Wide Web
                [2] => Yahoo!
                [3] => Steve Ballmer
                [4] => Microsoft
                [5] => Ballmer
                [6] => Jerry Yang
                [7] => Canaccord Genuity
            )

        [entities] => Array
            (
                [IndustryTerm] => Array
                    (
                        [0] => software maker
                        [1] => Internet search
                        [2] => Internet
                    )

                [Company] => Array
                    (
                        [0] => Canaccord Adams
                        [1] => Yahoo
                        [2] => Google Inc.
                        [3] => Yahoo! Inc.
                        [4] => Microsoft Corp.
                    )

                [Person] => Array
                    (
                        [0] => Colin Gillis
                        [1] => Steve Ballmer
                        [2] => Jerry Yang
                    )

                [Position] => Array
                    (
                        [0] => Chief Executive Officer
                    )

            )

    )

## Optional Settings ##

A number of settings exist which can be changed through public properties of the OpenCalais object: `contentType` (default: text/html), `outputFormat` (default: application/json). Refer to the OpenCalais documentation for more information.

This code is distributed under the MIT license. See http://www.opensource.org/licenses/mit-license.php
