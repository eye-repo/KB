# Browser Configuration

## Firefox

## Chrome

## Generic

1. Install chrome extention: [Custom JavaScript for Websites 2](https://chrome.google.com/webstore/detail/custom-javascript-for-web/ddbjnfjiigjmcpcpkmhogomapikjbjdk) 
2. Go to [youtube.com](youtube.com)
3. Open extention and enter:

    $('.ytd-popup-container').hide()

### Bookmarklets

Dark mode
```
javascript:(function(){
      document.body.style.background='black';
      document.body.style.color='white';
 })(); 
```

Get images from site
```
javascript:(function(){
      var items = document.getElementsByTagName("img");
 for ( i = 0; i &lt; items.length ; i++) {
      console.log(items[i].src);
 }
 })(); 
```

```
javascript:(function(){
 var items = performance.getEntriesByType('resource').filter(resource=>resource.initiatorType == 'img');
 for ( i = 0; i &lt; items.length ; i++) {
      console.log(items[i].name);
 }
 })(); 
```

Search for highlighted text
```
javascript:(function(){
      var szu = window.getSelection().toString();
      var google = "https://www.google.pl/search?q=";
      var bing = "https://www.bing.com/search?q=";
      var duck = "https://duckduckgo.com/?q=";
      window.open(google.concat(szu),'_blank');
      window.open(bing.concat(szu),'_blank');
      window.open(duck.concat(szu),'_blank');
 })(); 
```

Based on [sekurak](https://sekurak.pl/skryptozakladki-bookmarklets-jak-z-zakladki-w-przegladarce-zrobic-narzedzie-do-osintu-osint-hints/)

