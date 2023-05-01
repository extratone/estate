---
{"dg-publish":true,"permalink":"/macstories/my-obsidian-setup-part-9-saving-articles-and-music-albums-for-later-with-shortcuts-and-dataview-federico/","created":"","updated":""}
---

# "My Obsidian Setup, Part 9: Saving Articles and Music Albums for Later with Shortcuts and Dataview"

*26-04-2022 07:41* 

> Get help and suggestions for your iOS shortcuts and productivity apps.
Get help and suggestions for your iOS shortcuts and productivity apps.

## [My Obsidian Setup, Part 9: Saving Articles and Music Albums for Later with Shortcuts and Dataview](https://club.macstories.net/posts/my-obsidian-setup-part-9-saving-articles-and-music-albums-for-later-with-shortcuts-and-dataview)

![](https://cdn.macstories.net/friday-08-apr-2022-13-19-01-1649416756624.png)

In Parts 6 and 7 of my Obsidian Setup series, I explained how I created a system to save [Safari webpages](https://club.macstories.net/posts/my-obsidian-setup-part-6-dataview-and-cards-for-recent-notes-and-rich-links) and [YouTube videos](https://club.macstories.net/posts/obsidian-setup-part-7) as ‘rich links’ in Obsidian thanks to a combination of [Dataview](https://github.com/blacksmithgu/obsidian-dataview) and Shortcuts. For this first week of [Automation April](https://www.macstories.net/stories/introducing-automation-april/), I thought I’d add two more examples of content I’ve been tracking in Obsidian via cards in a grid powered by Dataview with interactive buttons: **articles** and **Apple Music albums** saved for later.

Both flavors of this workflow are largely based on the same techniques and structure I [first shared in January](https://club.macstories.net/posts/my-obsidian-setup-part-6-dataview-and-cards-for-recent-notes-and-rich-links); however, the shortcuts that make the creation of these ‘cards’ (i.e. notes in Obsidian) have some unique aspects to them, and I’ve also created additional helper shortcuts to retrieve these items from the Home Screen, so let’s take a look.

## Read Later

The fact that I’ve been struggling to find the ideal read-later app for me should come as no surprise to Club MacStories members, just like it shouldn’t surprise anyone that my latest experiment in this field is trying to track everything I read in Obsidian. I’ve tried everything over the years – from Pocket and Reading List to [converting articles into ‘books’ for a Kindle device](https://appstories.net/episodes/210) to the latest crop of read-later apps [such as Matter and Readwise](https://club.macstories.net/posts/why-are-read-it-later-apps-suddenly-hot). Perhaps the reason I can’t stick to a single read-later service right now is that I don’t *want* to: this market of apps is effectively living its own renaissance right now, and I want to dip my toes into many different waters. I want to try everything because I’m curious. So, obviously, I was *also* curious to see whether I could build my own, private, self-hosted read-later system in Obsidian.

As it turns out, not only was this all possible to create in Obsidian based on techniques I already explored months ago, but it’s also one of the more fun and flexible systems I’ve tried for tracking read-later material in a while.

At a high level, my Obsidian read-later workflow revolves around the same dual Shortcuts+Obsidian setup I wrote about for saving rich links in my Dashboard in January. When I find an article I want to save for later, I can run my Obsidian Read Later shortcut in Safari; doing so creates a new note in a ‘Read Later’ folder in Obsidian that contains YAML metadata for the article. Here’s what these notes look like:

![](https://cdn.macstories.net/cleanshot-2022-04-08-at-1-20-59-2x-1649416870932.png)

A note for an article saved for later.

As you can see, each article becomes a Markdown note with a frontmatter that contains additional metadata for the story: the original URL and title are included, of course, but there’s also a field for the article’s hero image, a timestamp for when it was saved, and the domain name. You’ll also notice that for this read-later-optimized version of this shortcut, I added new metadata fields for information that makes sense to have when you’re browsing a read-later queue.

First, I added a field to see from which device you saved an article into your queue. Sometimes I find it convenient to know whether I’m looking for a story I saved from my iPad or iPhone, but most read-later apps don’t care about this kind of context; from Shortcuts, I just added an additional block of actions to save the current device’s model name to a variable, and that was it.

![](https://cdn.macstories.net/cleanshot-2022-04-08-at-1-22-22-2x-1649416951167.png)

Saving device details in Shortcuts.

I also wanted to save the word count of the article so that I could later sort my queue by word count – a useful option to have if you’re looking for a shorter story to read in a few minutes. This turned out to be more of a challenge than I anticipated since Shortcuts for Mac [cannot run actions based on Safari Reader](https://twitter.com/viticci/status/1512022360118992905), which is what the iPhone and iPad versions of Shortcuts use to get a word count from the article you’re saving.

Don’t just take my word for it though – let’s take a look at the shortcut in action. Here’s how easy it is to turn a URL into an article and get its word count in Shortcuts for iPhone and iPad:

![](https://cdn.macstories.net/cleanshot-2022-04-07-at-12-47-44-2x-1649328481777.png)

Two actions, and that’s it.

And because, for whatever reason, Safari Reader actions are not compatible with macOS despite the fact that, *you know*, Safari and Safari Reader exist on macOS, this is the silly and ugly workaround I had to use when the shortcut runs on a Mac:

![](https://cdn.macstories.net/cleanshot-2022-04-07-at-12-48-38-2x-1649328545693.png)

To get a word count from an article on the Mac, I had to fetch the webpage’s contents as HTML, convert it to Markdown, convert it back to rich text (to eliminate as much HTML garbage as possible), force it into plain text (to get rid of images), *then* count the number of words. Why is this the case? I don’t know. But I hope WWDC 2022 and future OSes will be an opportunity for Apple to focus on Shortcuts bug fixes, performance improvements, and, most of all, feature parity between platforms.

Anyway, back to my read-later system. The shortcut (which you can download at the end of this section) processes Safari webpages in a second and articles are saved in Obsidian right away. The shortcut launches the Obsidian app at the end to force-trigger a sync for the newly created note; if you don’t want to launch Obsidian (perhaps because you’re using iCloud Drive, which always syncs in the background), you can remove this step.

In Obsidian, just like I did for rich links and YouTube videos before, I created a single `Read Later.md` note that uses [Minimal Theme’s Cards layout](https://github.com/kepano/obsidian-minimal) mode and a [DataviewJS](https://blacksmithgu.github.io/obsidian-dataview/data-queries/) snippet to visualize all notes saved in the ‘Read Later’ folder as nice interactive cards.

Here’s what the YAML syntax at the top of this note looks like:

```
```
---
cssClasses: table-max, cards, cards-16-9, cards-align-bottom
---
```
```

And here’s the DataviewJS snippet:

```
<pre class="dataview dataview-error">Evaluation Error: eval code@
eval@[native code]
@
@
asyncEvalInContext@
@
render@
onload@
@capacitor://localhost/app.js:1:869788
@
executeJs@
@
@
Promise@[native code]
__async@
@
fulfilled@</pre>
```

When viewed in preview mode, the final result – especially when viewed on an iPad in portrait mode – is very pretty to look at:

![](https://cdn.macstories.net/friday-08-apr-2022-13-27-17-1649417243892.png)

My read-later queue.

There are a couple of things worth noting here. The ‘Mark as Read’ button is interactive and you can click it to change an article’s `status` field from `unread` to `archived`; when you do that, the article will no longer appear in the Read Later grid, but the note will remain in Obsidian so you can open it later and add notes there if you want to. This is made possible by the [Buttons](https://github.com/shabegom/buttons) plugin, which you’ll have to install from the Community Plugins section of Obsidian.

![](https://cdn.macstories.net/cleanshot-2022-04-08-at-1-28-18-2x-1649417309004.png)

The ‘status’ tag controls whether an article is unread or archived.

Additionally, if you install the [Sortable](https://github.com/alexandru-dinu/obsidian-sortable) plugin, you’ll be able to sort articles in the read later grid by different properties in ascending or descending order. Articles are sorted by saved date (latest to oldest) by default, but you can also sort them by title, word count, platform, and more.

![](https://cdn.macstories.net/cleanshot-2022-04-08-at-1-55-46-2x-1649418958368.png)

Sorting in the read-later queue.

I’ve been using this Dataview-based read-later grid view for the past couple of months, and I like how I can press a button in Obsidian for iPad (thanks to the [Customizable Page Header](https://github.com/kometenstaub/customizable-page-header-buttons) plugin) to quickly return to this note when I’m in the mood for something to read. That said, I also came up with an additional shortcut that lets me pick articles from the Shortcuts widget on the Home Screen.

![](https://cdn.macstories.net/friday-08-apr-2022-13-57-09-1649419034804.png)

Getting unread articles from the Home Screen.

The shortcut is quite simple: it gets all notes from my Read Later folder, filters the ones that contain `status: unread` in their Markdown text, and presents me with a list of titles. When I pick a headline from the list, the shortcut uses RegEx to extract the story’s original link from the note and reopens it in Safari so I can start reading right away. Here’s what the shortcut looks like:

![](https://cdn.macstories.net/friday-08-apr-2022-13-58-00-1649419101864.png)

So this is how I’ve been tracking articles I want to read later in Obsidian. This approach may not have all the bells and whistles of modern startups like Readwise and Matter, but the entire “database” is just a collection of Markdown files that I fully control, can take notes on, and can visualize however I want with Dataview in Obsidian or quickly access from the Shortcuts widget on the Home Screen. To get started with this setup, you can download the two shortcuts below:

-   [Obsidian Read Later](https://www.icloud.com/shortcuts/b8f94476ca99479da663776bceca8db6)
-   [Get Articles](https://www.icloud.com/shortcuts/54a0ce6e0181471ca789370a0360df47)

## Listen Later

Once I had a system for articles, I figured I could adapt the same hybrid Obsidian-Shortcuts techniques for saving albums and singles from Apple Music in Obsidian too. Although I’m expecting I’ll switch to [Marcos Tanaka’s upcoming MusicBox app](https://twitter.com/mactanaka/status/1509596604126408704) as soon as it’s available (I seriously can’t wait for it), in the meantime I’ve been using my own system for keeping track of new music I want to listen later, and it works well enough for me.

Obsidian Listen Later is based on modified versions of the shortcuts and Dataview snippet I covered above. The only difference is that instead of sharing from Safari on your iPhone and iPad, you’ll have to run Obsidian Listen Later from the share sheet in the Music app. Alternatively, you can also run the shortcut manually from the Home Screen or on a Mac; in that case, you’ll be prompted to manually paste the URL of an Apple Music item you want to save.

![](https://cdn.macstories.net/friday-08-apr-2022-13-59-34-1649419196993.png)

Running Obsidian Listen Later from the share sheet (left) and an example of a note created by the shortcut (right).

Obsidian Listen Later works by determining whether you’re saving an album or a single (a feature I adapted from [MusicBot](https://www.macstories.net/ios/introducing-musicbot-the-all-in-one-apple-music-assistant-powered-by-shortcuts/)). Then, it uses Shortcuts’ native iTunes Store actions (are these ever going to be modernized for Apple Music?) to extract relevant metadata, including the album title and artwork URL. Then, just like Obsidian Read Later, a Markdown note is assembled with YAML frontmatter at the top, and the resulting file is saved in a folder of your choosing (mine is called ‘Listen Later’ in my Obsidian vault).

![](https://cdn.macstories.net/friday-08-apr-2022-14-02-36-1649419369846.png)

Getting metadata for Apple Music items.

In Obsidian, I created a `Listen Later.md` note and placed the following YAML frontmatter at the top of it:

```
```
---
cssClasses: table-max, cards, cards-1-1, cards-align-bottom
---
```
```

Then, I dropped in the following DataviewJS snippet:

```
<pre class="dataview dataview-error">Evaluation Error: eval code@
eval@[native code]
@
@
asyncEvalInContext@
@
render@
onload@
@capacitor://localhost/app.js:1:869788
@
executeJs@
@
fulfilled@</pre>
```

And here’s the result:

![](https://cdn.macstories.net/friday-08-apr-2022-14-03-59-1649419445068.png)

My saved albums in Obsidian.

Of course, in the part of the Dataview snippet where it says `dv.pages('"Listen Later"')`, you’ll have to replace ‘Listen Later’ with the name of your Obsidian folder where you’re saving music for later – same as above.

At any point, you can click on the ‘Apple Music’ link in the rich cards to reopen the selected item in Apple Music; you can sort the Dataview grid by all the criteria shown on the cards such as release type and creation date; and you can tap the ‘Mark as Listened’ button to mark an item as ‘Listened’ rather than ‘New’, thus making it disappear from the listen later queue.

Of course, just like I did for articles, I also created a ‘Get Albums’ shortcut to quickly retrieve notes for items marked as ‘New’ in Obsidian on the Home Screen. The shortcut presents me with a list of singles and albums that I can instantly reopen in the Music app, so I don’t have to open Obsidian and the Listen Later note if I don’t want to. That’s the beauty of having an open and customizable system based on a folder of Markdown files that I can choose to view and process however I see fit.

![](https://cdn.macstories.net/friday-08-apr-2022-14-04-46-1649419491811.png)

Accessing saved albums from the Home Screen.

If you want to get started saving albums and singles in Obsidian, you can copy the Dataview snippet I shared above and download the two shortcuts below:

-   [Obsidian Listen Later](https://www.icloud.com/shortcuts/401d85ab0d404ae19a4be3d7aa703fe2)
-   [Get Albums](https://www.icloud.com/shortcuts/baeeb2fd91ed4f80871156b4cbd3c8ee)

And if you’re modifying this setup to track other things that aren’t articles or music, [I’d love to know about it](https://twitter.com/viticci).

[Submit a Shortcut Request](https://docs.google.com/forms/d/e/1FAIpQLSeViYJRP69lNKgbmNWqxY1iEnz851gLE375swzC12Qarm-RxA/viewform?usp=sf_link)
***

==**12585**== Words

- **[My Obsidian Setup, Part 9: Saving Articles and Music Albums for Later with Shortcuts and Dataview](https://club.macstories.net/posts/my-obsidian-setup-part-9-saving-articles-and-music-albums-for-later-with-shortcuts-and-dataview)**