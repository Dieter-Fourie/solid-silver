# Using the Solid Silver Theme

<p align="center">
<img src="solid-silver.png"
</p>

 * Copy the theme into the `themes/` directory of your SilverStripe project.  If you've named it correctly, there should be a directory called `themes/solid-silver/templates`.
 
 * Change the following in your `mysite/config.yml` file.  Change 'theme: 'simple' to 'solid-silver'.
 
 * Add/Create the following  php files in your `mysite/code` folder: 
 
 - AboutPage.php
 - ContactPage.php
 - Page.php
 - Page_Controller.php
 - PorfoilioPage.php
 - PortfolioItem.php
 



# Add the following to 'Page_Controller.php': 

```php
<?php

class Page_Controller extends ContentController
{
    /**
     * An array of actions that can be accessed via a request. Each array element should be an action name, and the
     * permissions or conditions required to allow the user to access it.
     *
     * <code>
     * array (
     *     'action', // anyone can access this action
     *     'action' => true, // same as above
     *     'action' => 'ADMIN', // you must have ADMIN permissions to access this action
     *     'action' => '->checkAction' // you can only access this action if $this->checkAction() returns true
     * );
     * </code>
     *
     * @var array
     */
    private static $allowed_actions = array(
    );


    
 public function init() {   
  parent::init();
  //Requirements::css("http://fonts.googleapis.com/css?family=Raleway:300,500,900%7COpen+Sans:400,700,400italic");
  Requirements::css($this->ThemeDir()."/css/bootstrap.css");
  Requirements::css($this->ThemeDir()."/css/style.css");
  Requirements::css($this->ThemeDir()."/css/font-awesome.min.css");
  Requirements::javascript($this->ThemeDir()."/js/modernizr.js");
  Requirements::javascript("https://ajax.googleapis.com/ajax/libs/jquery/1.11.0/jquery.min.js");
  Requirements::javascript($this->ThemeDir()."/js/bootstrap.min.js");
  Requirements::javascript($this->ThemeDir()."/js/retina-1.1.0.js");
  Requirements::javascript($this->ThemeDir()."/js/jquery.hoverdir.js");
  Requirements::javascript($this->ThemeDir()."/js/jquery.hoverdir.js");
  Requirements::javascript($this->ThemeDir()."/js/jquery.hoverex.min.js");
  Requirements::javascript($this->ThemeDir()."/js/jquery.prettyPhoto.js");
  Requirements::javascript($this->ThemeDir()."/js/jquery.isotope.min.js");
  Requirements::javascript($this->ThemeDir()."/js/custom.js");   
}
   
    
} ]

```

# Add the following to 'Page.php':

```php
<?php

class Page extends SiteTree
{
    
    private static $db = array(
       
    );

    private static $has_one = array(
    'HomeIntroImg' => 'Image',
    );
    
 
    
public function getCMSFields() {
    
$fields = parent::getCMSFields();
   
    
    $fields->addFieldToTab('Root.Attachments', $HomeIntroImg= UploadField::create('HomeIntroImg'));
    $HomeIntroImg->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $HomeIntroImg->setFolderName('img/home');
    

    
return $fields;
    
}    
    
    
}

```

# Add the following to 'AboutPage.php':

```php
<?php
    
class AboutPage extends Page {
    
private static $db = array(
  'MoreAbout' => 'HTMLText',
  'TeamInfo1' => 'HTMLText',
  'TeamInfo2' => 'HTMLText',
  'TeamInfo3' => 'HTMLText',
  'TeamInfo4' => 'HTMLText',
  'Testimonial1' => 'HTMLText',     
);
    
private static $has_one = array (
    'AboutPhoto' => 'Image',
    'TeamPhoto1' => 'Image',
    'TeamPhoto2' => 'Image',
    'TeamPhoto3' => 'Image',   
    'TeamPhoto4' => 'Image',    
);     
    
public function getCMSFields() {
    
$fields = parent::getCMSFields();
    
    $fields->addFieldToTab('Root.Main', TextareaField::create('MoreAbout','More About'), 'Content'); 
    $fields->addFieldToTab('Root.Main', TextareaField::create('TeamInfo1','Team Info 1'), 'Content'); 
    $fields->addFieldToTab('Root.Main', TextareaField::create('TeamInfo2','Team Info 2'), 'Content'); 
    $fields->addFieldToTab('Root.Main', TextareaField::create('TeamInfo3','Team Info 3'), 'Content'); 
    $fields->addFieldToTab('Root.Main', TextareaField::create('TeamInfo4','Team Info 4'), 'Content');       
    
    $fields->addFieldToTab('Root.Attachments', $AboutPhoto = UploadField::create('AboutPhoto'));
    $AboutPhoto->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $AboutPhoto->setFolderName('img/about');
    
    $fields->addFieldToTab('Root.Attachments', $TeamPhoto1 = UploadField::create('TeamPhoto1'));
    $TeamPhoto1->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $TeamPhoto1->setFolderName('img/about');
    
    $fields->addFieldToTab('Root.Attachments', $TeamPhoto2 = UploadField::create('TeamPhoto2'));
    $TeamPhoto2->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $TeamPhoto2->setFolderName('img/about');    
    
    $fields->addFieldToTab('Root.Attachments', $TeamPhoto3 = UploadField::create('TeamPhoto3'));
    $TeamPhoto3->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $TeamPhoto3->setFolderName('img/about'); 
    
    $fields->addFieldToTab('Root.Attachments', $TeamPhoto4 = UploadField::create('TeamPhoto4'));
    $TeamPhoto4->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $TeamPhoto4->setFolderName('img/about');       
    
    $fields->addFieldToTab('Root.Main', TextareaField::create('Testimonial1','Testimonial'), 'Content');   
    
    
return $fields;
    
}  
    
}

class AboutPage_Controller extends Page_Controller {

}
```


# Add the following to 'PorfoilioPage.php':

```php
<?php
    
class PortfolioPage extends Page {

    private static $allowed_children = array ('PortfolioItem');
    //private static $can_be_root = false;
    
}

class PortfolioPage_Controller extends Page_Controller {

}
```


# Add the following to 'PortfolioItem.php': 

```php
<?php
    
class PortfolioItem extends Page {

private static $db = array(
  'ProjectName' => 'HTMLText',
  'Proposal' => 'HTMLText',
  'ProjectDetail' => 'HTMLText',    

); 

private static $has_one = array (
    'ProjectPhoto' => 'Image',
    'ProjectSlider1' => 'Image',
    'ProjectSlider2' => 'Image',
    'ProjectSlider3' => 'Image',
);  
        
private static $can_be_root = false;
   
public function getCMSFields() {
$fields = parent::getCMSFields();
    
    $fields->addFieldToTab('Root.Main', TextareaField::create('ProjectName','Your project name'), 'Content'); 
    $fields->addFieldToTab('Root.Main', TextareaField::create('Proposal','Proposal'), 'Content');
    $fields->addFieldToTab('Root.Main', TextareaField::create('ProjectDetail','Project detail'), 'Content');
    
    $fields->addFieldToTab('Root.Attachments', $ProjectPhoto = UploadField::create('ProjectPhoto'));
    $ProjectPhoto->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $ProjectPhoto->setFolderName('img/portfolio');
    
    $fields->addFieldToTab('Root.Attachments', $ProjectSlider1= UploadField::create('ProjectSlider1'));
    $ProjectSlider1->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $ProjectSlider1->setFolderName('img/portfolio'); 
    
    $fields->addFieldToTab('Root.Attachments', $ProjectSlider2= UploadField::create('ProjectSlider2'));
    $ProjectSlider2->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $ProjectSlider2->setFolderName('img/portfolio'); 
    
    $fields->addFieldToTab('Root.Attachments', $ProjectSlider3= UploadField::create('ProjectSlider3'));
    $ProjectSlider3->getValidator()->setAllowedExtensions(array('png','gif','jpg','svg'));
    $ProjectSlider3->setFolderName('img/portfolio'); 
    
return $fields;
}  
    
    
    
}

class PortfolioItem_Controller extends Page_Controller {

}
```


# Add the following to 'ContactPage.php': 

```php
<?php
    
class ContactPage extends Page {
    
private static $db = array(
  'ContactFormIntro' => 'HTMLText',    
  'ContactAddress' => 'HTMLText',  
);   
    
    
public function getCMSFields() {
    
    $fields = parent::getCMSFields();
    $fields->addFieldToTab('Root.Main', TextareaField::create('ContactFormIntro','Contact Form Intro'), 'Content'); 
    $fields->addFieldToTab('Root.Main', TextareaField::create('ContactAddress','Our Address'), 'Content'); 


return $fields;
    
}  
    
}



class ContactPage_Controller extends Page_Controller {
    
    private static $allowed_actions = array('Form');
    public function Form() { 
        
        
        
        $fields = new FieldList( 
            new TextField('Name'), 
            new EmailField('Email'), 
            new TextField('Subject'), 
            new TextareaField('Message')
        ); 
        $actions = new FieldList( 
            new FormAction('submit', 'Submit') 
        ); 
     $validator = new RequiredFields('Name', 'Email', 'Message','Subject');
    return new Form($this, 'Form', $fields, $actions, $validator); 
    }
    
    public function submit($data, $form) { 
        $email = new Email(); 

        $email->setTo('info@digitaltree.co.nz'); 
        $email->setFrom($data['Email']); 
        $email->setSubject("Contact Message from {$data["Name"]}"); 

        $messageBody = " 
            <p><strong>Name:</strong> {$data['Name']}</p> 
            <p><strong>Subject:</strong> {$data['Subject']}</p> 
            <p><strong>Message:</strong> {$data['Message']}</p> 
        "; 
        $email->setBody($messageBody); 
        $email->send(); 
        return array(
            'Content' => '<p>Thank you for your feedback.</p>',
            'Form' => '<h3>You message has been sent.</h3>'
        );
    }
    
}
```

# Build Database: 

```
Add this in your browser address bar: http://localhost/yoursite/dev/build/?flush

```

# Setup 'Home Page' on CMS : 

```
Go to the admin page: http://localhost/yoursite/admin to access CMS.

Select 'Home page' > Click on 'Settings' > Select 'Home Page" from 'Page type' dropdown list.

Click on 'Content' > Change 'Page name' to 'Home' > Change 'URL Segment' to 'home'

Add the following in 'Services1':

<i class="fa fa-heart-o"></i>
<h4>Handsomely Crafted</h4>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.</p>
<p><br><a href="about-us" class="btn btn-theme ss-broken">More Info</a></p>.

Add the following in 'Services2':

<i class="fa fa-flask"></i>
<h4>Retina Ready</h4>              
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.</p>
<p><br><a href="portfolio-page" class="btn btn-theme ss-broken">More Info</a></p>

Add the following in 'Services3':

<i class="fa fa-trophy"></i>
<h4>Quality Theme</h4>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.</p>
<p><br><a href="contact-us" class="btn btn-theme ss-broken">More Info</a></p>            

Add the following in 'More About':

<h4>More About Our Agency.</h4>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. </p>
<p><br><a href="about-us" class="btn btn-theme">More Info</a></p>

Add the following in 'FAQ':

<h4>Frequently Asked</h4>
<div class="hline"></div>
<p><a href="#" class="ss-broken">How cool is this theme?</a></p>
<p><a href="#" class="ss-broken">Need a nice good-looking site?</a></p>
<p><a href="#" class="ss-broken">Is this theme retina ready?</a></p>
<p><a href="#" class="ss-broken">Which version of Font Awesome uses?</a></p>
<p><a href="#" class="ss-broken">Free support is integrated?</a></p>

Add the following in 'Latest Posts':

<h4>Latest Posts</h4>
<div class="hline"></div>
<p><a href="single-post.html">Our new site is live now.</a></p>
<p><a href="single-post.html">Retina ready is not an option.</a></p>
<p><a href="single-post.html">Bootstrap 3 framework is the best.</a></p>
<p><a href="single-post.html">You need this theme, buy it now.</a></p>
<p><a href="single-post.html">This theme is what you need.</a></p>

Add the following in 'Content':

<h3>Show your work with this beautiful theme</h3>
<h1>Silverstripe Bootstrap Theme.</h1>
<h5>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</h5>
<h5>More Lorem Ipsum added here too.</h5>

Click on 'Save & Publish'


Click on 'Attachments' > 

'Home Intro Img' - Choose image file 'browser.png' - /themes/solid-silver/img/browser.png

Click on 'Save & Publish'

FYI: 'LATEST WORKS' will be populated when you add portfolio pages.


```

# Setup 'About Page' on CMS : 

```

Select 'About page' > Click on 'Settings' > Select 'About Page" from 'Page type' dropdown list.

Click on 'Content' > Change 'Page name' to 'About' > Change 'URL Segment' to 'about-us'

Add the following in 'More About':

<h4>More About Our Agency.</h4>

<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. </p>

<p>It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.</p>

<p>Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source.</p>

<p><br><a href="contact-us" class="btn btn-theme">Contact Us</a></p>

Add the following in 'Team Info 1':

<h4>Mark Webber</h4>
<h5 class="ctitle">CEO</h5>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</p>

Add the following in 'Team Info 2':

<h4>Paul Jameson</h4>
<h5 class="ctitle">LEAD DESIGNER</h5>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</p>        

Add the following in 'Team Info 3':

<h4>Laura Sommers</h4>
<h5 class="ctitle">LEAD DEVELOPER</h5>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</p>

Add the following in 'Team Info 4':

<<h4>Martin Blunt</h4>
<h5 class="ctitle">MARKETING</h5>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry.</p>

Add the following in 'Testimonial':

<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.</p>

Add the following in 'Content':

<p>You can fill this page out with your own content, or delete it and create your own pages.</p>

Click on 'Save & Publish'


Click on 'Attachments' > 

'About Photo' - Choose image file 'browser.png' - /themes/solid-silver/img/agency.jpg 
'Team Photo1' - Choose image file 'browser.png' - /themes/solid-silver/img/team01.jpg
'Team Photo2' - Choose image file 'browser.png' - /themes/solid-silver/img/team02.jpg
'Team Photo3' - Choose image file 'browser.png' - /themes/solid-silver/img/team03.jpg
'Team Photo4' - Choose image file 'browser.png' - /themes/solid-silver/img/team04.jpg

Click on 'Save & Publish'

```

# Setup 'Portfolio Page' on CMS : 

```
Click 'Add New' on the 'Pages' (Top left on CMS window) section > Select 'TUnder another page" from 'Choose where to create this page' list > Select 'Portfolio Page" from 'Choose page type' list > Click on the create button.

Click on 'Content' > Change 'Page name' to 'Portfolio' > Change 'URL Segment' to 'portfolio-page'

Add the following in 'Content':

<h2>We create awesome designs to standout your site or product. Check some of our latest works.</h2>

Click on 'Save & Publish'

```

# Setup 'Portfolio Item Pages' on CMS : 

```
Click 'Add New' on the 'Pages' (Top left on CMS window) section > Select 'Top level" from 'Choose where to create this page' list & select 'Portfolio"> Select 'Portfolio Item" from 'Portfolio Item' list > Click on the create button.

Click on 'Content' > Change 'Page name' to 'Web Design' > Change 'URL Segment' to 'web-item1'

Add the following in 'Your project name':

<h4>Project Name</h4>

<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.</p>

Add the following in 'Proposal':

<h4>Our Proposal</h4>

<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged.</p>

Add the following in 'Project detail':

<h4>Project Details</h4>

<div class="hline"></div>
<p><b>Date: </b> July, 2017</p>
<p><b>Author: </b>Dieter Fourie</p>
<p><b>Categories: </b> Web Design, Theme, Silverstripe</p>
<p><b>Tagged: </b> Flat, UI, Development</p>
<p><b>Client: </b>Black Tie</p>
<p><b>Website: </b> <a href="http://blacktie.co/2014/05/solid-multipurpose-theme/" target="_blank">Solid Theme</a></p>

Click on 'Save & Publish'

Click on 'Attachments' > 

'Project Photo' - Choose image file 'portfolio-3.jpg' - /themes/solid-silver/img/portfolio/portfolio-3.jpg
'Project Slider1' - Choose image file 'single2.jpg' - /themes/solid-silver/img/portfolio/single01.jpg 
'Project Slider2' - Choose image file 'single02.jpg ' - /themes/solid-silver/img/portfolio/single02.jpg 
'Project Slider3' - Choose image file 'single03.jpg ' - /themes/solid-silver/img/portfolio/single03.jpg  

Click on 'Save & Publish'

FYI: 'LATEST WORKS' will be populated when you add portfolio pages.


```

# Duplicate 'Portfolio Item Pages' on CMS : 

```
Right click on a subpage under the 'portfolio' page you want to duplicate > Select "Duplicate' > 'This page only'.

Change new page 'URL Segment' to a page name that makes sense like "web-item2" etc.

Click on 'Save & Publish'

Do this for each portfolio category - Web Design, Logo Design, Graphic Design, Brand Design & Prin Design (You can change this to your liking)

FYI: For this template 5 pages per portfolio section are optimal for the grid gallery to have equal rows. 

```

# Setup 'Contact Page' on CMS : 

```

Select 'Contact Page' > Click on 'Settings' > Select 'Contact Page" from 'Page type' dropdown list.

Click on 'Content' > Change 'Page name' to 'Contact Page' > Change 'URL Segment' to 'contact-us'

Add the following in 'Contact Form Intro':

<h4>Just Get In Touch!</h4>
<div class="hline"></div>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s.</p>

Add the following in 'Our Address':

<h4>Our Address</h4>
<div class="hline"></div>
<p>
Some Ave, 987,<br>
23890, New York,<br>
United States.<br></p>
<p>
Email: hello@solidtheme.com<br>
Tel: +34 8493-4893
</p>
<p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s.</p>

Add the following in 'Content':

<p>You can fill this page out with your own content, or delete it and create your own pages.</p>

Click on 'Save & Publish'

```

# Setup 'Page not found Page' on CMS : 

```

Select 'Page not found Page'.

Add the following in 'Content':

<h4><img class="center" title="" src="assets/img/home/portfolio-01.jpg" alt="404" width="600" height="450" /></h4>

<h4><a></a>404 Error</h4>
<p>Sorry, it seems you were trying to access a page that doesn't exist.</p>
<p>Please check the spelling of the URL you were trying to access and try again.</p>

FYI: You might need to upload the image that you want to use in this page first.

Click on 'Save & Publish'

```

# Setup 'Page not found Page' on CMS : 

```

Select 'Server error Page'.

Add the following in 'Content':

<h4><img class="center" title="" src="assets/img/home/portfolio-01.jpg" alt="404" width="600" height="450" /></h4>
<h4>Server Error</h4>
<p>Sorry, there was a problem with handling your request.</p>

FYI: You might need to upload the image that you want to use in this page first.

Click on 'Save & Publish'

```
