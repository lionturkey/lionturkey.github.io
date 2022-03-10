# Making a personal website
I've spent the past couple days brainstorming and building this website. At least for this first iteration, I wanted to keep it old-school and only use HTML and CSS.
In case it's useful to anyone else, I'll describe the experience and provide tips for newbs like me.
## Learning by example
Since most websites aren't "handmade" these days, I went through dozens of personal websites and blogs to find a few that I could use as examples. Sites using frameworks have a gazillion \<div\>s and CSS rules which isn't super helpful for learning from.

The first good resource I found was [this repo](https://github.com/eviau/htmlfreewrites/tree/main/minimalistart) for a minimalist art website by [eviau](https://eviau.net/). The repo has only 7 CSS rules that are easy to follow. Her own personal site only has 15 rules!

By looking at [Wesley Aptekar-Cassels's blog](https://blog.wesleyac.com/), I learned about [normalize.css](https://github.com/necolas/normalize.css) which is intended to remove styling inconsistencies between different browsers. Since the last time it was updated was 2018, I tried to find a more recent version. Eventually on [Leah Hanson's blog](http://blog.leahhanson.us/) I found a similar [sanitize.css](https://github.com/csstools/sanitize.css) which was last updated a few months ago.

Since I'm writing blog posts, I made an RSS feed as well. For now, this entails manually updating an xml document every time I post... To find examples of formatting, I went to various blogs and just added "/feed.xml" to the url. This works on [Danielle Sucher's](https://www.daniellesucher.com/) site, for instance. It seems that many people just put their entire blog post in the \<description\> section, but you can also just put a short blurb like in this [W3 Schools example](https://www.w3schools.com/XML/xml_rss.asp).
## Tips for others
- Spend most of your time prototyping your website on a sheet of paper. If you don't know exactly what you want, CSS sucks to play around with
- Check out the source for the websites mentioned above as well as this one!
- Use the [\<base\> element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element#document_metadata) to keep links consistent between HTML pages so you can copy and paste the same HTML outline for all your pages (view the source of this page and the home page for examples)
- Do this quick [flexbox froggy](https://flexboxfroggy.com/) tutorial, it'll save you a lot of time centering things on your website. There's also a [css grid tutorial](https://codepip.com/games/grid-garden/) by the same folks, but you need to make an account for it
- Within each CSS rule, put things in alphabetic order for sanity's sake
- Link underlining is ugly, so [turn it off](https://blog.hubspot.com/website/remove-underline-from-links-css) like a light switch
## Next Steps
Clearly there's a good bit more to do here, but at least this is a start. I need to finish some projects and shove them under the projects page and I want to compile lists of my favorite books, webtoons, movies, music, and whatnot for my friends. I should probably also find my own color scheme and buy an actual domain lol.