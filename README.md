# Online Dictioary Helper (with anki support) 

It's a chrome extension to be customized to show online dictionary content. It also can help make note in anki desktop (with ankiconnect installed)

# Background

Reading (a lot) is the most importanrt aspect for serious language learner. Inspired by [readlang.com](http://readlang.com/) and [Foosoft/yomichan](https://github.com/FooSoft/yomichan), I built up a English-Chinese learning chrome extension - [Anki Dict Helper](https://github.com/ninja33/anki-dict-helper) in 2016. When users are reading web page online, they can move mouse cursor to the unkown word, press <kbd>shift</kbd> key, and then a pop up windows with that word definition will be displayed. It also can help make an anki note filled fields with **word**, **definition** and **context** (the surrounding sentence of selected word).

# The idea

That extension is running perfectly for English-Chinese language learners. Meanwhile, I also got a lots of requests, asking add other dictionaries and support for other languages, at least for latin alphabet based language which is similar as English as source language.

Well, same reason as Foosoft/yomichan mentioned in his project [FAQ](https://github.com/FooSoft/yomichan#frequently-asked-questions) page. First off, I have no knowledge of foreign languages other than English. Second, there is no way to get all those dictionaries, convert format and then build it in chrome extension.

But (there is always a 'but' in the end), we are at Internet age right now. There are hundreds of thousands dictionaries online for searching. So, you can just scrape the definition from online dictionary, leave word and sentence untouched, make it popup and make a note for anki as usual. Basically, below is the idea.

- anki dict helper: popup window [word, **builtin defintion**, sentence] --> anki 
- anki online dict helper: popup window [word, **online defintion**, sentence] --> anki 

The **online definition** part is driven by customized javascript which could be written by you or your friend, and hosted on Github.com

# How to use

1. Install the extesion first from Chrome Web store. Setup Option if you want. (detail in below option page section)
2. (Optional) Setup anki deck, type and fields names to put your **word**, **definition**, **sentence**.
3. Open some web pages which have English artical (by default option which has English dictionary only).
4. Move mourse cursor to the word, double click to select or press <kbd>shift</kbd> to automatically select word in case it's a link.
5. A popup windows displayed to show the word definition.
6. (Optional) Press top/right green **(+)** icon to add anki note. 
7. (Optional) You need make sure anki desktop was open and ankiconnect addon was installed.

The extension shipped in with two dictionaries as sample,  You can play with these 2 dicntionaries and see if it's what you want.

1. English-Chinese dictionary: youdao.com

![placeholder](https://raw.githubusercontent.com/ninja33/anki-online-dict-helper/master/src/img/icon128.png)

2. English-English dictionary: collins.com

![placeholder](https://raw.githubusercontent.com/ninja33/anki-online-dict-helper/master/src/img/icon128.png)

As for dictionary collins.com, actually it is not built-in dictionary, it is here to show you how to load customized dictionary script.

# The Option Page

The extension option page is devided in three section.

1. General Option: Turn on or turn off the extension if you want.
2. Anki Options: Setup Anki deck/type name, and which fields you are going to put **word**, **definiton**, **sentence**. Currently, the exntension can only output these three most important information. Web page url and audio can be added late.
3. Dictionary Options:
    - Script Repository: Input your own script location here.
    - Selected Dictionary: Here will display all available dictionaries (buildin and customized), and please what current dictionary you want to use.

![placeholder](https://raw.githubusercontent.com/ninja33/anki-online-dict-helper/master/src/img/icon128.png)

# Start your own script

If you want to display your own online dictionary content, you need build the script by yourself, and upload the scipt to Github.com and iput script location in `Repository`.

**Important: You can not directly refer github.com as srcipt location (becasue of [this](https://github.com/rgrove/rawgit/blob/master/FAQ.md) reason), you need change the domian name to rawgit.com**

For example:
1. If you script was uploaded to https://**github**.com/your-name/your-repository/branch/filename.js
2. You need change above address to https://**rawgit**.com/your-name/your-repository/branch/filename.js


## Framework & Workflow

Bacially, the extension will accept your browser word selection as input, pass it to your own dictionary script for online query, then get the returned content and show it on broswer popup windows. (optional)When you click `plus` button, it will add a note for you in anki with `word`,`definition`,`sentence` in those fields defined in option page.

The dictionary script contains three parts:

1. Build an online dictionary query url. In most case, it's just like http(s)://example.online.dictionary.com/search?word={your-word}
2. Perform online query by sending above url, and get the web page content.
3. To clear up the content and return. You may need use Elemenet/CSS selector (getEelementbyXXX or querySelector) to get the definition part you want.

## Coding convention

1. First of all, you need wrap all of your online dictionary scraping code in a Class. To avoid duplicated declaration, you need detect if this Class was declared or not, and then register this Class with a display name (will be displayed in extension option page) at the end of code.

2. Second, in your dictionary Class, you need define at least one function named as `findTerm()` , which accept `word` as function parameter, return a javascript Promise object. That's all.

Below is script template to start your own coding.

```javascript
if (typeof YouClassName == 'undefined') {
    Class YouClassName{
        constructor() {
            // Your code starting here ...
        }

        findTerm(word) {
            return new Promise((resolve, reject){
            // Your code starting here ...
            // resolve(content);   
            // reject(error);
            });
        }
    }
    registerDict('Your Dicionary Display Name', YouClassName);
}
```

# Too Complicated?

Unfortunately, it's not RTG(Ready To Go) package for beginner. The extension already built up a frame work to accept your broswer selection, display popup, create anki note, but the dictionary part is up to you. Ask someone who know javascript programming if you really need help.

# Security issue

Because the extension will dynamically load your own customized script, so, you know what you are doing here.
1. You need explicitly input your script location in option page.
2. The only allowed script source domain is rawgit.com which means all code is public and can be tracked on github.com

# Pull request & script repository

Welcome pull request if you want to enhancement this extension, or put your own script here as central repository.

- the exntension source will go to /src
- the online dictionary script will go to /dicts
