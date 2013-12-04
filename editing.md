# Editing the website

Editing the mrumrocks.org website is fairly easy. Here are some guides to show you specifically what to do.

## In general
You'll almost always want to restrain your editing to the `#content` div. You can use pretty much any HTML here that you want.

Note that the pages are stored all named `index.html` in separate folders. This is to create nicer URLs:

    Before: http://mrumrocks.org/portfolio.html
    After:  http://mrumrocks.org/portfolio/

To keep the style of the site constant, you should probably:

 * use `h1` for titles only
 * use `h2` for headings and `h3` for subheadings
 * use `p` tags for body text (don't just put the text in by itself)

To have a consistent HTML document, also do the following:

 * **Use four spaces, not tabs, for indentation.**
   * In Notepad++ (Windows), select *Settings* &rarr; *Preferences*; under the *Language Menu/Tab Settings* tab, check the *Replace by space* checkbox and ensure that *Tab size* is set to `4`.   
   * In gedit (Linux), select *Edit* &rarr; *Preferences*; under the *Editor* tab, check the *Insert spaces instead of tabs* checkbox and ensure that *Tab width* is set to `4`.
 * **Keep body text at 80 characters or fewer in width.** Most text editors will tell your your current column number. Try to keep it at or below 80. Just break a new line when you need to. Exceptions include `a` tags and other places where it would be sillier to break a line.


Also, isolate your paragraph tags as follows:

    <p>
    Some text
    </p>
    <p>
    More text
    </p>

## The home and contact pages
The home and contact pages don't have any special content, so you can edit them (inside the `#content` div) as normal web pages.

## The tutorials page

To add a new project, you'll need to add two things: a project selector and the project contents.

You'll need to pick a unique project name. For this example, we'll use `project-name`.

### The project selector
The code for a project selector for a Java project looks like this:

    <a class="pselect java" href="#project-name">Some Project</a>

You should place this code within the `#project-selector` div near the top of the `#content` div. Make sure to place it above the "clear" button.

You can modify this appropriately for different project types. I've included `java`, `flash`, and `blender` by default. You can add more by modifying this page's CSS. To do so, add a line as follows (example given for Premiere):

    .premiere { background-image: url("../rsc/project-premiere.png");

Insert this code next to the other project indicators, under the line commented `/* Project indicator icons */`.

The relevant selector would then have `class="pselect premiere"`.

### The project contents

You'll need to add a new div below the existing projects. The minimal syntax is as follows:

    <div class="project" id="project-name">
        <a href="#" class="close">Close</a>
    </div>

It is recommended to follow the general layout as follows:

    <div class="project" id="project-name">
        <h2>Project Name</h2>
        
        <div class="sub">
            <!-- left side pane -->
            <h3>Project Description</h3>
        </div>
        
        <div class="sub">
            <!-- right side pane -->
            <h3>Lessons</h3>
            <p>
            Watch as a playlist
            <a href="link to playlist">here</a>,
            or watch individual lessons below.
            </p>
            <ul>
                <li>Lesson 1 (<a href="link to video">here</a)</li>
                <li>Lesson 2 (<a href="link to video">here</a)</li>
            </ul>
        </div>
        
        <a href="#" class="close">Close</a>
        
    </div>

Note that the div's `id` must match the `href` value of the selector. For example, if the div has `id="project-name"`, the selector must have `href="#project-name"` (with a pound sign).

To add lessons, just update the `ul`.

After adding a project, you may wish to update the relevant course.

## The courses page

To add a new course called `course-name`, add the following block of code to the `#content` div:

    <div class="modal">
        <a href="#course-name"><h2>Course Name</h2></a>
        
        <div class="modal-info" id="course-name">
            <h3>Description</h3>
            <p>
            Course description goes here
            </p>
            
            <!-- If you have any projects, include them here -->
            <!-- Otherwise, omit this section -->
            <h3>Projects</h3>
            <ul class="projects">
                <li><a href="../tutorials/#project-name">Some Cool Project</a></li>
            </ul>
            <a href="#" class="close">Close</a>
            
            <!-- If this course has a portfolio, link to it here -->
            <!-- Otherwise, omit this section -->
            <h3>Portfolio</h3>
            <p>Visit the portfolio <a href="../portfolio/#course-name">here</a>.</p>
            
            <!-- If this course has a syllabus, link to it here -->
            <!-- Otherwise, omit this section -->
            <h3>Syllabus</h3>
            <p>View the course syllabus <a href="path/to/syllabus.pdf">here</a>.</p>
            
            <a href="#" class="close">Close</a>
        </div>
    </div>

Again, note that the `href` property of the anchor tag must match the `id` property of the div, with an added pound sign.

If you link to a tutorial or portfolio, the target (the portion after the pound sign) must match the `id` of the tutorial or portfolio that you're linking to.

You shouldn't need to modify the CSS of this page at all.

## The portfolios page
To add a new portfolio, add the following block of code to the `#content` div:

    <div class="modal">
        <a href="#course-name"><h2>Some Course</h2></a>
        <div class="modal-info" id="course-name">
            <h3>Pictures</h3>
            <p>
                <a class="fancybox" href="img/course-name/full/01.png" data-fancybox-group="course-name-s" title="Caption">
                    <img src="img/course-name/thumb/01.png" title="Thumbnail caption" alt="" /></a>
                <a class="fancybox" href="img/course-name/full/02.png" data-fancybox-group="advanim-s" title="Caption">
                    <img src="img/course-name/thumb/02.png" title="Thumbnail caption" alt="" /></a>
            </p>
            
            <h3>Videos</h3>
            <p>
                <a class="fancybox-media" href="link to youtube video" data-fancybox-group="course-name-v">
                    <img src="img/course-name/thumb/03.png" title="Video thumbnail caption" alt="" /></a>
            </p>
            
            <a class="close" href="#">Close</a>
        </div>
    </div>

Let's focus on the image setup.

The setup is as follows:

 * An anchor (`a`) tag with the following properties:
   * `class` is `"fancybox"` (this triggers the lightbox)
   * `href` is the path to the full image
   * `data-fancybox-group` is a group identifier for a set of pictures (so that you can use the next/previous buttons). You can have multiple groups in a course, for example `advanim-blender-stills` and `advanim-flash-stills`. The stills group should be different than the video group.
   * `title`, if provided, is the image caption in the popup display
 * An `img` tag inside the `a` tag for the thumbnail 

The directory setup is as follows

    portfolio/
        index.html (the portfolios file)
        img/
            course-name/
                full/ (full-sized images)
                    01.png
                    02.png
                thumb/ (thumbnail images)
                    01.png
                    02.png
            another-course/
                full/  (...)
                thumb/ (...)

For a YouTube (or Vimeo, etc.) link, the format is similar, except that the anchor `class` should be `fancybox-media` instead of `fancybox`, and the `href` should point to the YouTube link. You can use a `title` caption here, too.


That should be pretty much it. Email me if you have questions.  
WC