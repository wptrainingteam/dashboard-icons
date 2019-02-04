# Dashboard Icons

## Description

In this lesson you will learn about dashboard icons, how they are composed, and how your themes, plugins, and posts benefit from using dashboard icons.

## Prerequisite Skills

This lesson presumes an understanding of and familiarity with:

*   [Creating a child theme](https://make.wordpress.org/training/handbook/theme-school/child-themes/)
*   [functions.php](https://make.wordpress.org/training/handbook/theme-school/what-to-include-in-functions-php/)

## Objectives

After completing this lesson, you will be able to:

*   Identify dashboard icons and explain their purpose,
*   Use dashboard icons when creating posts, themes, and plugins.

## Assets

*   [Twenty Sixteen theme](https://wordpress.org/themes/twentysixteen/)
*   [twentysixteen-child](https://make.wordpress.org/training/files/2014/10/twentysixteen-child.zip)
*   [Developer Resources: Dashicons](https://developer.wordpress.org/resource/dashicons/)

## Screening Questions

*   Have you ever worked on a child theme?
*   Do you have a basic familiarity with CSS/PHP?

## Teacher Notes

*   The recommended approach suggests demonstrating and explaining the process first and then asking students to repeat the actions using their own devices, while you’re available for questions and troubleshooting if something doesn’t work out.
*   A local installation of WordPress is preferred. If possible, plan for some time to assist students with installing WordPress on their computers or, distribute instructions prior to class so they can arrive prepared. For more information on how to install WordPress locally, please visit our [Teacher Resource](https://make.wordpress.org/training/teacher-resources/)s page.
*   The answer to screening questions is “yes.” Participants who reply “no” may require further explanation.
*   Prior to class, the Hands-On Walkthrough can be sent out as a .pdf, in order to preserve links used in the document and keep things green, or printed to be used as a handout in class.

## Hands-on Walkthrough

### Introduction: What are dashboard icons?

Dashboard icons or **dashicons** are a set of fonts, which represent icons used in the new WP-Admin UI. [![das_exemple](https://make.wordpress.org/training/files/2014/10/das_exemple.png)](https://make.wordpress.org/training/files/2014/10/das_exemple.png) The benefits of using font icons over picture icons include:

*   Small file-sizes
*   Good scalability
*   Browser support for old versions of IE
*   Full CSS styling capabilities

**Scenario:** Develop a theme for an online portfolio website. Create a custom post type called “Portfolio” and assign a dashicon<del>s</del> to represent it. Add a “Twitter” dashicon to  the site footer so that visitors can contact us via Twitter. [tip]For the purposes of this training, we will be editing the WordPress [TwentySixteen](https://wordpress.org/themes/twentysixteen/) theme. The WordPress best practice is to modify a [child theme](https://make.wordpress.org/training/handbook/theme-school/child-themes/) of your site's theme.[/tip]

### Using dashicons in your posts

Dashicons are a feature of WordPress that has been included in core since WP 3.8\. Whereas previously this functionality was created via your theme or a plugin, now you can simply add the necessary html directly in the post editor to display dashicons in your posts. To achieve this, create a new post, select the Text tab of the editor, and type the following in the body of the html editor:

> <h2 class="dashicons-before dashicons-smiley">Yay, dashicons!</h2>

[![d1](https://make.wordpress.org/training/files/2014/10/d1.png)](https://make.wordpress.org/training/files/2014/10/d1.png) Switch to “visual” editor by clicking on the Visual tab to see how it looks. [![d2](https://make.wordpress.org/training/files/2014/10/d2.png)](https://make.wordpress.org/training/files/2014/10/d2.png)

### Adding icons for Custom Post Types and CSS

Typically, to use an icon font in your theme you need to: 1\. embed the icon webfont 2\. lookup whatever icon you want to use on the character-map 3\. type that letter or number

#### Enqueueing dashicons

We want our dashicons stylesheet to load before our theme stylesheet does, as our theme stylesheet depends on it. So we will be loading dashicons as a dependency of our theme stylesheet. To achieve this, open your theme’s functions.php and add the following piece of code to the bottom of your functions.php file.

<pre>add_action( 'wp_enqueue_scripts', 'themename_scripts' );
function themename_scripts() {
     wp_enqueue_style( 'themename-style', get_stylesheet_uri(), array( 'dashicons' ), '1.0' );
}</pre>

  [alert]Note that if using the Twenty Sixteen theme, scripts are already enqueued as above, but with _twentysixteen_scripts _in place of _themename_scripts_. Find the function _twentysixteen_scripts()_ in your document and edit it to look like this: [/alert] [![portfolio_code1](https://make.wordpress.org/training/files/2014/10/portfolio_code1.png)](https://make.wordpress.org/training/files/2014/10/portfolio_code1.png)

#### Using dashicons for custom post types: selecting an item to use

Now it’s time to actually implement some icons! At this point it’s you should take a look at the [list of all the current icons](https://developer.wordpress.org/resource/dashicons/). It’s a useful tool to choose the one you need and also to copy the glyph reference for your CSS. Let’s go with our first task. There is a [“portfolio” icon](https://developer.wordpress.org/resource/dashicons/#portfolio) in the set so let’s use it.

#### Using dashicons for custom post types: inserting the icon in the code

1\. Here is how we are going to create and register a new post type. Add the following code to your functions.php. Note that 'menu_icon' => 'dashicons-portfolio' is the indication of the icon to be used.

<pre>add_action( 'init', 'create_portfolio_post_type' );
//creates a custom post type - portfolio
function create_portfolio_post_type() {
   register_post_type( 'portfolio',
   array(
      'labels' => array(
      'name' => __( 'Portfolio items' ),
      'singular_name' => __( 'Portfolio item' )),
      'public' => true,
      'menu_icon' => 'dashicons-portfolio',
   ));
}</pre>

[![portfolio_code2](https://make.wordpress.org/training/files/2014/10/portfolio_code2.png)](https://make.wordpress.org/training/files/2014/10/portfolio_code2.png) 2\. Refresh your site. The portfolio icon is now present in the menu. [![portfolio_result](https://make.wordpress.org/training/files/2014/10/portfolio_result.png)](https://make.wordpress.org/training/files/2014/10/portfolio_result.png)

#### Adding dashicons to theme’s CSS

So, we decided to enhance the standard Twenty Sixteen’s footer by using a twitter logo, so that it would be clear people are welcome to contact theme’s developer via twitter. 1\. Go to dashboard icons list and select twitter icon. Click “Copy CSS’ and then copy text from the pop-up. [![copytwitter](https://make.wordpress.org/training/files/2014/10/copytwitter.png)](https://make.wordpress.org/training/files/2014/10/copytwitter.png) 2\. Open style.css of your theme. 3\. Now you need to apply the code you copied to the :before (or :after) pseudo class of the element you need to be prepended or appended by the icon, and specify that it uses the dashicons font-family. We need the footer, so let’s find in the text and add the following text:

<pre>.site-footer:before {
   font-family: "dashicons";
   content: "\f301";
}</pre>

[![twi_code](https://make.wordpress.org/training/files/2014/10/twi_code.png)](https://make.wordpress.org/training/files/2014/10/twi_code.png) 4\. Save the file and refresh your site. The twitter bird is now right where we wanted it. [![twi_result](https://make.wordpress.org/training/files/2014/10/twi_result.png)](https://make.wordpress.org/training/files/2014/10/twi_result.png) [tip] The icon can now be styled with CSS properties just like any **<span style="color: #ff0000">text:</span>** <del>regular alphabetical letter</del>: if you wish you can change colors, font-weights, rotate it, etc.[/tip]  

## Exercises

Suggested exercises are meant to reinforce the acquired knowledge of performing basic operations with dashicons:

1.  Create a new post featuring some dashicons.
2.  Create a new post type: Video with a suitable dashicon.
3.  Move the bird we inserted in the last part of the lesson to the end of the footer.

## Quiz

**What kind of icons are WordPress dashicons?**

1.  Inline SVG
2.  Icon font
3.  CSS image sprites
4.  Embedded .png files

**Answer:** 2. Icon font

**What is a prerequisite to adding an icon to a custom post via 'menu_icon' => 'dashicons-iconname'?**

1.  Enqueue dashicons with functions.php
2.  Download dashicons to your server
3.  Nothing

**Answer:** 1. Enqueue dashicons with functions.php
