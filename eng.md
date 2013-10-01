We all know that there are a number of ways we can modify layout based on CSS
media queries -- hell, we can even [animate properties between media queries][1].
One bit of outside the box thinking with media queries is deals with
[pointer-events][2]. Using the `pointer-events` property, we can also enable 
and disable some functionality with CSS based on media query state!

The scenario is one that's present in the current implementation of the MDN
redesign. On the left you see article content, on the right you see a table of 
contents:

![MDN Redesign Desktop][3]

When pushed into the tablet media query, the table of contents should move
above the content:

![MDN Redesign Tablet][4]

When on desktop, the table of contents *should not* be toggleable when the
title is clicked. On tablet or other mobile device, however, the table of 
contents should toggle (slide up) when clicked to free up critical space, so as 
to avoid (possibly) loads of scrolling. I didn't want to use JavaScript to 
enable/disable the toggler, because...well...that would be inefficient. Instead 
I paired the`pointer-events` property with the tablet media query:

    /* disable by default */
    #toc .heading {
        pointer-events: none;
    }
    #toc i {
        display: none;
    }
    
    /* enable for tablet! */
    @media only screen and (max-width: 760px) {
        #toc .heading {
            pointer-events: auto;
        }
        #toc i {
            display: block;
        }   
    }
    
I absolutely adore `pointer-events` because it even prevents click events from
firing, thus the JavaScript I use to trigger the [slide up/down][5] doesn't
occur. While I wouldn't say what I've done is overly clever, I would like to say
that you should think about modifying more than just layout within different 
media queries. Oh, and also,`pointer-events` is awesome!

[1]: http://davidwalsh.name/animate-media-queries
[2]: http://davidwalsh.name/pointer-events
[3]: img/mdn-redesign-desktop.jpg "MDN Redesign Desktop"
[4]: img/mdn-redesign-tablet.jpg "MDN Redesign Tablet"
[5]: http://davidwalsh.name/css-slide
