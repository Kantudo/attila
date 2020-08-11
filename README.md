#This fork
This is a fork of the [attila](https://github.com/zutrinken/attila), theme for ghost.
It adds a new button for toggling between dark and light mode, reatining user preference via local storage and maintaing the autodetect functionality bases on prefers-color-scheme.

To enable it you have add the following code in the code injection section of Ghost managing page.

```
<script>

function detectColorScheme(){
    var theme="light";    //default to light

    //local storage is used to override OS theme settings
    if(localStorage.getItem("theme")){
        if(localStorage.getItem("theme") == "dark"){
            var theme = "dark";
        }
    } else if(!window.matchMedia) {
        //matchMedia method not supported
        return false;
    } else if(window.matchMedia("(prefers-color-scheme: dark)").matches) {
        //OS theme setting detected as dark
        console.log("yo bae")
        var theme = "dark";
    }
    console.log("yo wasa")
    //dark theme preferred, set document with a `data-theme` attribute
    if (theme=="dark") {
         document.body.setAttribute("data-theme", "dark");
         document.getElementById("dn").checked = true;
    }else{
         document.getElementById("dn").checked = false;
    }
}
detectColorScheme();
   
//identify the toggle switch HTML element
const toggleSwitch = document.querySelector('#dn');

//function that changes the theme, and sets a localStorage variable to track the theme between page loads
function switchTheme(e) {
    if (e.target.checked) {
        localStorage.setItem('theme', 'dark');
        document.body.setAttribute('data-theme', 'dark');
        toggleSwitch.checked = true;
    } else {
        localStorage.setItem('theme', 'light');
        document.body.setAttribute('data-theme', 'light');
        toggleSwitch.checked = false;
    }    
}

//listener for changing themes
toggleSwitch.addEventListener('change', switchTheme, false);

//pre-check the dark-theme checkbox if dark-theme is set
if (document.documentElement.getAttribute("data-theme") == "dark"){
    toggleSwitch.checked = true;
}
</script>
```
You can see a functioning version of this at my blog, [blog.stlarx.com](https://blog.stlarx.com). 

Credits to Benjamin Réthoré for the css toggle switch design. [https://dribbble.com/shots/2360260-AM-PM-Toggle](https://dribbble.com/shots/2360260-AM-PM-Toggle).
Credits to JimmyBanks at stackoverflow for the javascript code. [https://stackoverflow.com/questions/56300132/how-to-override-css-prefers-color-scheme-setting](https://stackoverflow.com/questions/56300132/how-to-override-css-prefers-color-scheme-setting).

# Attila

A content focused responsive theme for [Ghost](https://github.com/tryghost/ghost/). See a demo at: [attila.zutrinken.com](https://attila.zutrinken.com/)

If you like this theme, you can buy me a ~~coffee~~ [beer](https://paypal.me/zutrinken).

## 📷 Screenshots

<table>
<tr>
<td valign="top">
<img src="https://raw.githubusercontent.com/zutrinken/attila/master/src/screenshot-desktop.jpg" />
</td>
<td valign="top">
<img src="https://raw.githubusercontent.com/zutrinken/attila/master/src/screenshot-mobile.jpg" />
</td>
</tr>
</table>

## ⭐️ Features

* Responsive layout
* Dark Mode
* Search & Tag archive
* Post reading progress
* Code highlight including line numbers
* Disqus support

## 🌍 Localization

* __English__
* __German__
* __Spanish__
* __French__ by [robink](https://github.com/robink)
* __Italian__ by [fmaida](https://github.com/fmaida)
* __Norwegian__ by [arthurnoerve](https://github.com/arthurnoerve)
* __Chinese__ by [hao-lee](https://github.com/hao-lee)
* __Indonesian__ by [simplyeazy](https://github.com/simplyeazy)
* __Romanian__ by [cdorin93](https://github.com/cdorin93)
* __Russian__ by [schamberg97](https://github.com/schamberg97)
* __Turkish__ by [cgrgrbz](https://github.com/cgrgrbz)
* __Swedish__ by [martenj77](https://github.com/martenj77)
* __Czech__ by [lunakv](https://github.com/lunakv)
* __Portuguese__ by [matheusvanzan](https://github.com/matheusvanzan)
* __Vietnamese__ by [JustHmmmm](https://github.com/justhmmmm)
* __Greek__ by [thiodordelis](https://github.com/thiodordelis)
* __Danish__ by [jmayntzhusen](https://github.com/jmayntzhusen)
* __Arabic__ by [pop-eax](https://github.com/pop-eax)

## 🎨 Setup custom color

1. Go to __Code injection__.  
2. Add this to __Blog Header__:  
````
<style>
  :root {
    --color-primary: #D95736;
    --color-primary-active: #BF4526;
  }
</style>
````

## 🔠 Setup custom google fonts

1. Go to [fonts.google.com](https://fonts.google.com/) and choose a font.
2. Choose __Embed__ and copy the `<link>` code.
3. Go to __Code injection__.  
4. Add this to __Blog Header__:  
````
<link href="https://fonts.googleapis.com/css2?family=Mukta&display=swap" rel="stylesheet">
<link href="https://fonts.googleapis.com/css2?family=Crimson+Text&display=swap" rel="stylesheet">
<style>
  :root {
    --font-primary: 'Mukta', sans-serif;
    --font-secondary: 'Crimson Text', serif;
  }
</style>
````

## 💬 Setup [Disqus](https://disqus.com/)

1. Go to __Code injection__.  
2. Add this to __Blog Header__:  
````
<script>var disqus = 'YOUR_DISQUS_SHORTNAME';</script>
````

## 🔍 Setup search

The search function is build with [ghostHunter](https://github.com/jamalneufeld/ghostHunter):

1. Go to __Integrations__.  
2. Choose __Add custom integration__, name it `ghostHunter` and choose __Create__. Copy the generated Content API Key.  
3. Go to __Code injection__.  
4. Add this to __Blog Header__:  
````
<script>
  var ghosthunter_key = 'PASTE_THE_GENERATED_KEY_HERE';
  //optional: set your custom ghost_root url, default is "/ghost/api/v2"
  var ghost_root_url = '/ghost/api/v2';
</script>
````
## ⚙️ Development

Install [Grunt](https://gruntjs.com/getting-started/):

	npm install -g grunt-cli

Install Grunt dependencies:

	npm install

Build Grunt project:

	grunt build

The compress Grunt task packages the theme files into `dist/<theme-name>.zip`, which you can then upload to your site.

	grunt compress

## ⚖️ Copyright & License

Copyright (C) 2015-2020 Peter Amende - Released under the [MIT License](https://github.com/zutrinken/attila/blob/master/LICENSE).
