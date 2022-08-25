# Avisynth ClipProperties to Frame Properties Parser
Avisynth Clip Properties to Frame Properties parser for FFAStrans internal use.
<br>
<br>
**Brief Explanation**
<br>
The parser will try to populate Avisynth streams with frame properties that can be used by third party programs like FFAStrans' filter_builder to have an idea about what is being delivered and encode the stream accordingly. If there are NO frame properties (legacy Avisynth or legacy indexer or maybe the user used propClearAll() or for some other reason), the parser will try to use some of the clip properties to assume frame properties (but it's largely based on guess-work) while if there are SOME frame properties, it will preserve those but it will also try to see whether it has all the ones that are needed and it will try to fill the gap either by using what it has got as frame properties OR by using the same guess-work it would have used if it didn't have anything in the first place.
<br>
<br>
The result of this is a series of conditional and try-catch statement that try to prevent the function from erroring out.
<br>
<br>
**Non FFAStrans users, beware!**
<br>
Even though the function is publicly available, this is made for FFAStrans' filter_builder internal use cases only, therefore you'll see that the interlacing check doesn't really make sense for a normal user. This is because technically in Avisynth there was no way to know the field order and the exact interlacing from the clip properties alone, so we came up with the idea long ago to use AssumeFieldBased() to carry frames in a progressive fashion and AssumeFrameBased() to carry interlaced fields so that we could cross-check the clip properties to know whether it was interlaced TFF, interlaced BFF or progressive 'cause there were no frame properties in the past and now this thing has come back to bite us, but anyway, this is just the reason why the interlacing check wouldn't make sense for a normal user.
<br>
<br>
**Stream delivered without the properties parser**
<br>
![image](https://user-images.githubusercontent.com/18946343/186724566-33c82580-a3cc-46c4-aca8-264ccaff0a13.png)
<br>
<br>
**Stream delivered with the properties parser**
<br>
![image](https://user-images.githubusercontent.com/18946343/186724269-0091b1d4-d38c-42f6-8e30-f62d3fdd33d6.png)
