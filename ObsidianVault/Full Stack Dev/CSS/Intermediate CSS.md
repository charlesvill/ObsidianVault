## Default Styles
- Different browsers add basic CSS to elements parsed on the web. Often devlopers will reset these CSS values to have consistent results regardless of the browser. 

## CSS Units

##### Absolute units vs relative units
- the only absolute unit in web projects you should be using is px
- the family of relative units all can change based on their context\
- articles suggest using rem for the font and using px for margins, padding etc. the main difference being that using relative for padding and margins will allow the more accurate scaling as things zoom or are on different size screens, however it may lead to unnecessarily large unused space. 
- long answer is it depends on the priority pendulum leaning towards either functionality or aesthetics wherein the scaling proportions would need to be more tight. 

##### em and rem 
- both are referring to a font size, could be other things, ***prefer rem over em. 
- em is the font size of the element or the element's parent it's multiplied to the font size so 4px font with 4 em equals (4px * 4em == 16px )
- rem is the same except that it uses the root elemtent so it doesn't get changed if parents change or contexts change. better consistency. 
- refer to this article on when to use each one https://codyloyd.com/2021/css-units/
- refer to this article on all available units https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units

##### percentages
- when a percentage is used it  will be relative to some other property, like the parent value. *ex using 30% as width will take 30% of the parent container and font size will be 30% of the parent font.* 

##### Viewports
- vh or vw represent a relative percentage value to the availble viewport space. 
- more information on the various relative properties with respect to sizing things found here https://css-tricks.com/fun-viewport-units/ this also talks about respecting aspect-ratio. should come back to this
##### Choosing the right Units
- here is a video on knowing what units to be using for different contexts https://www.youtube.com/watch?v=N5wpD9Ov_To&ab_channel=KevinPowell


## More Text Styles

