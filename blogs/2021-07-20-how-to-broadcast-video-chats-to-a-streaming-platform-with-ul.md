---
title: "How to broadcast video chats to a streaming platform with ultra-low latency using Daily and Amazon IVS"
url: "https://aws.amazon.com/blogs/media/how-to-broadcast-video-chats-to-a-streaming-platform-with-ultra-low-latency-using-daily-and-amazon-ivs/"
date: "Tue, 20 Jul 2021 17:56:59 +0000"
author: "Sathya Balakrishnan"
feed_url: "https://aws.amazon.com/blogs/media/tag/amazon-interactive-video-service/feed/"
---
<p><em>Authored by Jessica Mitchell, Engineer, at Daily. The content and opinions in this post are those of the third-party author and AWS is not responsible for the content or accuracy of this post.</em></p> 
<p>At Daily, we build real-time video and audio APIs that let developers embed calls into any site or app, with support for up to 1,000 participants. Recently, there has been a growing demand for a reliable live streaming solution. As more interactions move online, customers who typically rely on WebRTC for real-time conversations now need to host even larger events like webinars, live conferences, fitness classes, concerts, and large meetings on streaming platforms that reach millions.</p> 
<p>To meet this growing demand, Daily offers live streaming of Daily calls via RTMP streaming. This format can be consumed by several existing solutions — most notably <a href="https://aws.amazon.com/ivs/" rel="noopener noreferrer" target="_blank">Amazon Interactive Video Service</a> (Amazon IVS). It also provides ultra-low latency with only a two to five seconds of delay.</p> 
<p>Daily prides itself on offering the simplest solution for video calls and live streaming, requiring only a few lines of code to get started. In addition to ease of use and low latency, Daily provides customizable layouts for live streaming or multi-participant calls, and full HD resolution. Our live streaming accommodates up to nine video feeds on screen at a time and a configurable number of simultaneous streams per account.</p> 
<p>In this post, we show you how to set up a Daily video call in your app, initiate RTMPS live streaming, and have the stream consumed by the Amazon IVS player.</p> 
<h2><strong>Requirements</strong></h2> 
<p>To get started, there are a few requirements you will need to set up:</p> 
<ol> 
 <li>A <a href="https://dashboard.daily.co/signup" rel="noopener noreferrer" target="_blank">Daily paid account</a>&nbsp;(Launch or Scale) to access the live streaming feature.</li> 
 <li>A Daily room, which can be created via the <a href="https://dashboard.daily.co/rooms/create" rel="noopener noreferrer" target="_blank">Daily dashboard</a> or the <a href="https://docs.daily.co/reference#rooms" rel="noopener noreferrer" target="_blank">REST API</a>.</li> 
 <li>A <a href="https://docs.daily.co/reference#create-meeting-token" rel="noopener noreferrer" target="_blank">meeting token</a> for the Daily room, with the property `is_owner` set to `true`.</li> 
 <li>An <a href="https://portal.aws.amazon.com/billing/signup#/start" rel="noopener noreferrer" target="_blank">AWS account</a>&nbsp;to use Amazon IVS.</li> 
 <li>An Amazon IVS <a href="https://docs.aws.amazon.com/ivs/latest/userguide/getting-started-create-channel.html" rel="noopener noreferrer" target="_blank">streaming channel</a>. A channel can be created through the <a href="https://console.aws.amazon.com/" rel="noopener noreferrer" target="_blank">Amazon IVS console</a> or through the <a href="https://docs.aws.amazon.com/ivs/latest/APIReference/API_CreateChannel.html" rel="noopener noreferrer" target="_blank">Amazon IVS API</a>&nbsp;directly.</li> 
</ol> 
<p>Once you have a streaming channel created, keep the following pieces of information provided by Amazon IVS:</p> 
<ol> 
 <li>The ingest server</li> 
 <li>The stream key</li> 
 <li>The playback URL</li> 
</ol> 
<div class="wp-caption aligncenter" id="attachment_8854" style="width: 987px;">
 <img alt="Amazon IVS’s console for a new streaming channel" class="wp-image-8854 size-full" height="654" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/20/2-4.png" width="977" />
 <p class="wp-caption-text" id="caption-attachment-8854"><em>Amazon IVS’s console for a new streaming channel</em></p>
</div> 
<h2><strong>Create a Daily video call</strong></h2> 
<p>Adding a Daily video call to your app is as simple as adding a few lines of code. To demonstrate this, let’s look at Daily’s <a href="https://github.com/daily-demos/prebuilt-ui/tree/live-streaming-demo" rel="noopener noreferrer" target="_blank">prebuilt demo app</a>, which uses our <a href="https://www.daily.co/prebuilt" rel="noopener noreferrer" target="_blank">prebuilt video</a> UI. (Developers also can build their own <a href="https://docs.daily.co/docs/build-a-custom-video-chat-interface" rel="noopener noreferrer" target="_blank">custom video interfaces</a>&nbsp;with our front-end libraries.)</p> 
<p>In `index.html`, there is a script tag to include `daily-js`, Daily’s front-end JavaScript library. There is also a `&lt;div&gt;` element that can be selected in the `index.js` file via its ID. This is where the video iframe is inserted by `daily-js`.</p> 
<p>In `index.js`, there are three main steps to start a live stream. These steps require the Daily and Amazon IVS prerequisite data created earlier, including the RTMPS endpoint as shown by the following.</p> 
<div class="wp-caption aligncenter" id="attachment_8855" style="width: 987px;">
 <img alt="The Daily Prebuilt demo functions required to start live streaming" class="wp-image-8855 size-full" height="914" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/20/3-3.png" width="977" />
 <p class="wp-caption-text" id="caption-attachment-8855"><em>The Daily Prebuilt demo functions required to start live streaming</em></p>
</div> 
<ol> 
 <li>Initialize the Daily iframe with the `createFrame()` Daily <a href="https://docs.daily.co/reference#%EF%B8%8F-createframe" rel="noopener noreferrer" target="_blank">method</a>.</li> 
 <li>Once the Daily call has been initialized, join the Daily room created earlier with the `join()` <a href="https://docs.daily.co/reference#%EF%B8%8F-join" rel="noopener noreferrer" target="_blank">method</a>. This method should be passed an object with the Daily room URL and meeting owner token set, also created earlier.</li> 
 <li>After the room has been joined, start live streaming the Daily call by choosing the demo’s “Start live streaming” button. This triggers the `startLiveStreaming()` Daily <a href="https://docs.daily.co/reference#%EF%B8%8F-startlivestreaming" rel="noopener noreferrer" target="_blank">method</a>, which accepts an object with the RTMP URL set, as well as additional configurable options. In the case of Amazon IVS, this is an RTMPS URL.The RTMPS URL uses two pieces of information provided by the Amazon IVS console (or REST API) from the new channel created earlier: the ingest server and the stream key.</li> 
</ol> 
<p>As soon as `startLiveStreaming` successfully resolves, your Daily call is officially live streaming.</p> 
<div class="wp-caption aligncenter" id="attachment_8856" style="width: 987px;">
 <img alt="Daily’s embedded iframe with two call participants" class="wp-image-8856 size-full" height="758" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/20/4-6.png" width="977" />
 <p class="wp-caption-text" id="caption-attachment-8856"><em>Daily’s embedded iframe with two call participants</em></p>
</div> 
<h2><strong>Viewing your live stream with Amazon IVS</strong></h2> 
<p>Now that you have your Daily video streaming, playing the live stream is as simple as passing the playback URL to the Amazon IVS player, using the player SDK. To test the Daily live stream with the player, use the <a href="https://github.com/aws-samples/amazon-ivs-basic-web-sample)" rel="noopener noreferrer" target="_blank">Amazon IVS basic web sample</a> from the code repository <a href="https://ivs.rocks/examples" rel="noopener noreferrer" target="_blank">list</a>, or follow the player instructions for <a href="https://docs.aws.amazon.com/ivs/latest/userguide/player-web.html" rel="noopener noreferrer" target="_blank">web</a>, Android, or iOS.</p> 
<p>Once you have the player available, use the playback URL supplied by Amazon IVS in the player setup. This playback URL is one of the pieces of information mentioned earlier while creating a new channel.</p> 
<div class="wp-caption aligncenter" id="attachment_8857" style="width: 882px;">
 <img alt="Example code from the Amazon IVS basic web sample repo" class="wp-image-8857 size-full" height="347" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/20/5-4.png" width="872" />
 <p class="wp-caption-text" id="caption-attachment-8857"><em>Example code from the Amazon IVS basic web sample repo</em></p>
</div> 
<p>To confirm that the live stream is available, load the player in the browser and you can see your live stream with the ultra-low latency of only 2–5 seconds.</p> 
<div class="wp-caption aligncenter" id="attachment_8858" style="width: 987px;">
 <img alt="A Daily live stream viewed through the Amazon IVS player" class="wp-image-8858 size-full" height="575" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/20/6-2.png" width="977" />
 <p class="wp-caption-text" id="caption-attachment-8858"><em>A Daily live stream viewed through the Amazon IVS player</em></p>
</div> 
<p>This setup can be <a href="https://docs.daily.co/reference#%EF%B8%8F-startlivestreaming" rel="noopener noreferrer" target="_blank">further customized</a>&nbsp;by using Daily’s various layouts, such as grid, active speaker, screen share, or single participant views.</p> 
<p>Once your live stream content has ended, you can stop live streaming your Daily call by simply calling `<a href="https://github.com/daily-demos/prebuilt-ui/blob/live-streaming-demo/index.js#L260" rel="noopener noreferrer" target="_blank">callFrame.stopLivestreaming()</a>`&nbsp;in your Daily call code.</p> 
<p><strong>About Daily</strong></p> 
<p>At Daily, our goal is to build video and audio APIs that inspire and support developers. We believe that live video is changing how we all live and work — and it should be much simpler, and faster, for developers and product teams to build creatively with video.</p> 
<p>Using Daily with Amazon IVS provides reliable live streaming with ultra-low latency, with only a few lines of code. With Daily and Amazon IVS both being quick and easy to use, we’ve solved the hard parts of live streaming video for developers so they can focus on building better products faster.</p>
