# Online Dictioary Helper (with adding anki note support) 

It's a chrome extension to help grab online dictionary content and pop it up beside selected word. 
It also can help make note in anki desktop (with ankiconnect installed)

# Background
Reading (a lot) is the most importanrt aspect for serious language learner. Inspired by readlang.com and Foosoft/yomichan, I built up a Chinese-English learning chrome extension - Anki Dict Helper one year ago. When users are reading web page online, they can move mouse cursor to the unkown word, press shift key, and then a pop up windows with that word definition will be displayed. It also can help make an anki note with fields, including word, definition and context (the surrounding sentence of selected word).

That extension is running perfectly for Chinese-English language learner. Meanwhile, I also got a lots of requests, asking add other dictionaries and support for other languages, at least for latin alphabet based language which is similar as English as source language.

Well, same reason as Foosoft/yomichan mentioned in his project README page. First off, I have no knowledge of foreign languages other than English. Second, there is no way to get all those dictionaries, convert format and then build it in chrome extension.

But (there is always a 'but' in the end), we are at Internet age right now. There are hundreds of thousands dictionaries online for searching. So, you can just grab the definition from online dictionary, leave word and sentence untouched, make it popup and make a note for anki as usual. Basically, below is the idea 

- anki dict helper: popup window [word, `builtin defintion`, sentence] --> anki 
- anki online dict helper: popup window [word, `online defintion`, sentence] --> anki 

