## Awesome websites built using Hugo, Bootstrap, Google Material Design and Wercker to deploy on AWS S3 

### Prerequisites
*These steps are one time and it is assumed that you are using MacOS*

1. Install Hugo. [https://gohugo.io/](https://gohugo.io/) 
   You might have to first install homebrew (and Ruby, rbenv). Hugo is installed using a simple brew command
    
        brew update && brew install hugo
2. Install Git Cli for Mac from [https://git-scm.com/download/mac](https://git-scm.com/download/mac)
3. Create a GitHub Account if you don't have one [https://github.com](https://github.com)
4. Create a Wercker Account if you don't have one [https://app.wercker.com](https://app.wercker.com)
         


## How to build new websites using this template. 
This template website uses Hugo(https://gohugo.io/), the template engine for fast, static websites. 

*Why Hugo*

For static websites, which change frequently, don't need heavy software like Wordpress or Jenkyll. You can use Hugo which is based on Go Templates. 


### Step 1: Clone the template

   Let's say you are starting a new site `site-1`
    
    $git clone https://github.com/rishabh-parekh/liftoff.git site-1
  
  This will create a local copy of the website template in the folder `site-1` 


Open the Website in **Atom** or any other editor.
The website has the following structure.

*Note: If you don't have tree, install tree using `brew install tree`

    $cd site-1
    $tree -L 1
    .
    ├── archetypes
    ├── config.toml
    ├── content
    ├── data
    ├── layouts
    ├── static
    └── themes

The content for the website is stored in the content folder in **Markdown** [https://daringfireball.net/projects/markdown/] (https://daringfireball.net/projects/markdown/) 

You can create new content in the content folder (more details in later steps) 
The static folder has all the static CSS, Images, Logos, Fonts. 

The site specific layouts are stored in the layout folder. But you can use Themes, which are applied to the content. In the themes folders are different Hugo Themes, we have couple of them downloaded in the template. You can preview and download more themes from the Hugo website. [http://themes.gohugo.io/](http://themes.gohugo.io/)


### Step 2 Start the Hugo Server to serve the website

Let's start the local site from a **terminal** window
In the site-1 folder in the terminal window type 

      $hugo serve

This will start you site and you can go ahead open a browser window to `http://localhost:1313`


### Step 3: Change the config.toml 

Hugo uses a simple top level config file to store all Site related data. You can add new site related data or modify existing one. 

Snippet of the config.toml

      title = "The classroom that is always open"
      baseurl = "http://f9liftoff.io/"
      MetaDataFormat = "toml"
      paginate = 9 # To specify a multiple of 3
      disqusShortname = "" # optional
      copyright = "© Copyright 2016 F9LO, Inc. All Rights Reserved."
      theme="material-design"
      
      #
      # All parameters below here are optional and can be mixed and matched.
      #
      [params]
      # You can use markdown here.
      brand = "F9 LiftOff"
      topline = "Get the Boost"
      footline = "code with <i class='fa fa-heart'></i>"

Edit the config.toml in Atom (or your fav editor) and Go ahead and change the brand name, title, baseurl copyright message etc. 

As soon as you save, Hugo will automatically refresh the website. 

Check the website in the browser window with the new Title, description etc. 

### Step 4: Finalize your layout, images, content with the customer

In this step you will get all the images, content, logo from the customer and finalize the layout with your customer. Assuming you have already done that proceed to Step 5

### Step 5: Change the Logo and Images

The logo and all images are stored in the static/img folder
The logo shown in the front page is based on the config.toml's **customer** parameter

      customer = "lologo"

This is configured in the layouts/partials/header.html file 

      <div class="vert-text">
      <!--logo start-->
         {{if .Site.Params.customer}}
            <a href="#intro"><img src="{{.Site.BaseURL}}/img/{{.Site.Params.customer}}.png" class="logo" alt="logo"> </a>
         {{end}}

Let's say your customer name is petstore (all lowercase). Create a logo file `petstore.png` and drop it in the `img` folder

Similarly all images from the customer which are going to be used throughout the content will be stored in the `img` folder (more later when we build the content)


### Step 6: Change the Top Level Menu

The top level menus are configured in the `layout/partials/header.html`
The menus in the template are `about`, `products`, `approach`, `customers`, `team`, `contact`, `blog`. You can add new menus, delete menus, or change existing existing. 

Each menu has icons. By default the Hugo Icons which are configured in layout/css/hugofont.css

You can use Google Icons from the [Google Material Icons](https://design.google.com/icons/). Uncomment the Menu using Google Style Icons, and comment out Menus using Hugo Style Icon.

The Google Icons use Style Sheets from MaterialCSS which is included at the top of the header.html
[http://materializecss.com/getting-started.html](http://materializecss.com/getting-started.html) 


        <!-- All Google Style Icon Buttons -->
        <!--https://design.google.com/icons/ -->
        <!--
        <a href="#about" class="btn btn-primary btn-lg">About Us <i class="material-icons">account_balance</i></a>
        <a href="#products" class="btn btn-primary btn-lg">Products <i class="material-icons">account_box</i></a>
        <a href="#approach" class="btn btn-info btn-lg">Approach <i class="material-icons">account_circle</i></a>
        <a href="#customers" class="btn btn-info btn-lg">Customers <i class="material-icons">favorite_border</i></a>
        <a href="#team" class="btn btn-dark btn-lg">Team <i class="large material-icons">face</i></a>
        <a href="#contact" class="btn btn-dark btn-lg">Contact <i class="material-icons">group</i></a>
        <a href="#blog" class="btn btn-dark btn-lg">Blog <i class="material-icons">info</i></a>
        <!--- End Google Buttons -->

        <!-- All Hugo Style Icon Buttons -->
        <a href="#about" class="btn btn-dark btn-lg">About Us <i class="icon-idea"></i></a>
        <a href="#products" class="btn btn-dark btn-lg">Products <i class="icon-arrow-down"></i></a>
        <a href="#approach" class="btn btn-dark btn-lg">Approach <i class="icon-rocket2"></i></a>
        <a href="#customers" class="btn btn-dark btn-lg">Customers <i class="icon-talking"></i></a>
        <a href="#team" class="btn btn-dark btn-lg">Team <i class="icon-circlestar"></i></a>
        <a href="#contact" class="btn btn-dark btn-lg">Contact <i class="icon-circlestar"></i></a>
        <a href="#blog" class="btn btn-dark btn-lg">Blog <i class="icon-circlestar"></i></a>


### Step 7: Change the Rest of Header
The header is configured in the `layout/partials/header.html`

### Step 8: Change the Footer
The footer is configured in the `layout/partials/footer.html`
Here you can add the twitter, github, facebook, instagram, snapchat social media icons 

         <li><a href="https://twitter.com/{{.Site.Params.twitter}}" class="icon-twitter icon-2x"></a></li>
         <li><a href="https://github.com/{{.Site.Params.github}}" class="icon-octocat icon-2x"></a></li>

The values for the social media icons are from the config.toml
Edit the config.toml to add social media handles

         twitter = "f9lo" # optional
         github = "f9lo"

The icons for the social media are stored in the hugofont.css 
For icons which are not available in hugofont.css, refer to step 6 for using Google and BootStrap fonts. 

### Step 5: Change and Add new content

### Step 6: Change the Icons

### Step 8: Change the Theme/Colors

### Step 9: Change the Wercker.yml to deploy it automatically

### Step 10: Add the new site to Git

### Step 11: Create a Wercker App and Target

### Step 12: Kick start and watch you website




