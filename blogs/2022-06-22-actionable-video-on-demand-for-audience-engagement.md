---
title: "Actionable video on demand for audience engagement"
url: "https://aws.amazon.com/blogs/media/actionable-video-on-demand-for-audience-engagement/"
date: "Wed, 22 Jun 2022 16:56:19 +0000"
author: "Katherine Kelshaw"
feed_url: "https://aws.amazon.com/blogs/media/tag/amazon-interactive-video-service/feed/"
---
<p>As viewers shift from passively viewing into actively engaging with content during video playback, content providers can design and build interactive and actionable experiences for their audiences. Actionable video is context-aware and time-specific, allowing the viewer to respond to prompts about a person, place, or object while watching and interacting with video as it plays.</p> 
<p>Examples of actionable video prompts include: add this product to cart, send me more information, deliver the ingredients in this recipe, or show me directions to this location. These are just some examples of creative possibilities that enhance the viewing experience and drive audience engagement through actionable video.</p> 
<p>Content providers with existing video-on-demand (VOD) archives, and new VOD productions can create actionable video experiences using managed services from Amazon Web Services (AWS). This blog post describes the framework, and architecture for building actionable video for VOD content on AWS.</p> 
<h3><strong>Actionable is a type of interactive video</strong></h3> 
<p>In actionable video experiences, a prompt displays that is time-aligned and context-aware of the people, places, objects, or sentiment of a scene. Each actionable prompt is assigned to a timestamp range where it should be synchronized to the video.</p> 
<p><img alt="" class="aligncenter wp-image-11125 size-large" height="457" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2022/03/29/actionable-vod-image1-1024x457.png" width="1024" /></p> 
<p>Actionable prompts can be rendered as a video player overlay, in a sidebar, or as a second-screen experience. As video playback progresses, the visible actionable prompt changes as it is synchronized and updated to match the content by timestamp. Both the visual design and synchronization of the prompt to the video timestamp is developed in the front-end technologies of a website, mobile app, and video player.</p> 
<p>An interactive video producer identifies, prepares, and produces the content for the timed actionable prompts in advance of publishing the VOD asset to a website or mobile app. AWS AI/ML managed services can accelerate this workflow by analyzing the video and generating metadata and timestamps about people, places, objects, and sentiment of a scene.</p> 
<h3><strong>Actionable video on-demand through embedded or extra metadata</strong></h3> 
<p>Actionable experiences can be achieved through embedded or extra timed video metadata (or an architecture that combines both). The video player and browser, or mobile app, receives events during playback when timed metadata aligns with the video. The front-end application parses and renders metadata into an actionable prompt.</p> 
<p><img alt="" class="aligncenter wp-image-11126 size-large" height="481" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2022/03/29/acitonable-vod-image2-1024x481.png" width="1024" /></p> 
<p>Embedded timed video metadata is persistent and inserted into the video asset during transcoding. Once inserted, embedded metadata is immutable. For HLS, embedded timed metadata is inserted into the video segments as timed ID3 tags. ID3, developed by the <a href="https://id3.org/">ID3 organization</a>, is a standard for embedding metadata into media to describe the media. The ID3 standard originated in 1996 to describe mp3 audio. ID3 version 2 introduced support for streaming media, with <a href="https://id3.org/id3v2.4.0-frames">ID3v2.4.0</a> being the latest specification.</p> 
<p>There are two extra metadata approaches. Persistent extra metadata uses WebVTT metadata files that requires video player support for mobile apps and browser support for HTML5 players. Dynamic extra metadata is provided by a GraphQL API where a mobile app or browser requests the required metadata parameters aligned by timestamp, or upon an ID3 metadata parsed or WebVTT cue change event.</p> 
<p>Extra timed video metadata is flexible and mutable and is retrieved separately from the video asset. Extra metadata can be dynamic and personalized when it is retrieved in real time for each viewer.</p> 
<h3><strong>The actionable mechanism</strong></h3> 
<p>The most impactful viewing experiences combine metadata sources to create dynamic and personalized actionable experiences. The persistent approach uses embedded ID3 or extra WebVTT metadata files to trigger time-aligned events for actionable opportunities. These time-specific events can query dynamic, extra metadata from a <a href="https://docs.aws.amazon.com/appsync/latest/devguide/designing-a-graphql-api.html">GraphQL API</a> to augment and personalize metadata for each viewer during playback.</p> 
<p>Choosing the persistent approach is also influenced by your VOD content. For existing transcoded assets, you would create metadata in extra WebVTT metadata files as these can be created and maintained separately to the VOD asset.</p> 
<p>Embedded ID3 metadata must be inserted during VOD transcode with <a href="https://aws.amazon.com/mediaconvert/">AWS Elemental MediaConvert</a>, so the embedded approach is suited to new content productions.</p> 
<p>For a broader perspective about how embedded ID3 is used in other streaming media contexts, <a href="https://aws.amazon.com/ivs/">Amazon Interactive Video Service</a> (Amazon IVS) uses the ID3 standard for <a href="https://docs.aws.amazon.com/ivs/latest/userguide/metadata.html">embedding metadata into live video streams</a>. When Amazon IVS live streams are recorded to <a href="https://aws.amazon.com/s3/">Amazon Simple Storage Service</a> (Amazon S3) for VOD playback, the timed metadata persists into the recorded asset.</p> 
<table border="2" cellpadding="2" cellspacing="0" style="border-color: #7d7d7d;"> 
 <thead> 
  <tr style="background-color: #cccccc;"> 
   <td><strong>Mechanism</strong></td> 
   <td><strong>Lifespan</strong></td> 
   <td><strong>Timed metadata format</strong></td> 
   <td><strong>Playback event<br /> </strong>(video player / browser)</td> 
  </tr> 
 </thead> 
 <tbody> 
  <tr> 
   <td>Embedded</td> 
   <td>Persistent</td> 
   <td>ID3</td> 
   <td>Provided by video player in metadata parsed event (or similar).<br /> The Amazon IVS player defines this event as TEXT_METADATA_CUE.</td> 
  </tr> 
  <tr> 
   <td>Extra</td> 
   <td>Persistent</td> 
   <td>WebVTT metadata file</td> 
   <td> <p>Provided by video player in cue change event (or similar).</p> <p>The Amazon IVS player does not currently support WebVTT metadata.</p></td> 
  </tr> 
  <tr> 
   <td>Extra</td> 
   <td>Dynamic *</td> 
   <td>GraphQL API</td> 
   <td>– time update (observing media timestamp)<br /> OR<br /> – lookup event triggered from ID3 or WebVTT metadata</td> 
  </tr> 
 </tbody> 
</table> 
<p style="text-align: right;">* can aggregate multiple data sources for each viewer</p> 
<p>Timed metadata events are triggered differently, depending on the metadata format and the video player and browser/mobile app for playback:</p> 
<ul> 
 <li>Timed embedded ID3 tags are reported by the video player in an event name defined by the video player (like metadata parsed). The Amazon IVS video player reports the event <a href="https://docs.aws.amazon.com/ivs/latest/userguide/metadata.html">TEXT_METADATA_CUE</a>.</li> 
 <li>Timed WebVTT metadata files must be supported by the web browser (for HTML5 video players) and/or the video player (for mobile apps). Video players typically report WebVTT timed metadata events as cue change events. The Amazon IVS video player does not currently support WebVTT metadata.</li> 
 <li>Extra metadata defined by a GraphQL API by media timestamp requires a web browser or mobile app to monitor the time update event of the current playback time and render the actionable prompt when timestamps align.</li> 
</ul> 
<h3><strong>Actionable video on AWS</strong></h3> 
<p>The following architecture demonstrates how actionable video can be achieved on AWS.</p> 
<p><img alt="" class="aligncenter wp-image-11127 size-large" height="623" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2022/03/29/actionable-vod-image3-1024x623.png" width="1024" /></p> 
<p>Interactive producers can identify actionable opportunities with the <a href="https://aws.amazon.com/solutions/implementations/aws-content-analysis/">AWS Content Analysis</a> solution to analyze video content and generate timed metadata about the people, places, objects, sentiment, scene detection, and audio transcription. AWS Content Analysis uses pre-trained AI/ML services such as <a href="https://docs.aws.amazon.com/rekognition/latest/dg/what-is.html">Amazon Rekognition</a>, <a href="https://docs.aws.amazon.com/transcribe/latest/dg/transcribe-whatis.html">Amazon Transcribe</a>, <a href="https://docs.aws.amazon.com/translate/latest/dg/what-is.html">Amazon Translate</a>, and <a href="https://docs.aws.amazon.com/comprehend/latest/dg/what-is.html">Amazon Comprehend</a> to provide ready-made intelligence and accelerate editing and production of impactful actionable prompts.</p> 
<p><strong><u>Diagram Summary</u></strong></p> 
<ol> 
 <li>Content providers upload video assets into Amazon S3 using the <a href="https://aws.amazon.com/solutions/implementations/aws-content-analysis/">AWS Content Analysis</a> solution web UI. Alternatively, assets can be uploaded directly to an Amazon S3 bucket by creating an <a href="https://github.com/aws-solutions/aws-content-analysis#starting-workflows-from-an-s3-trigger">S3 trigger</a> with <a href="https://aws.amazon.com/lambda/">AWS Lambda</a> to initiate the AWS Content Analysis workflow.</li> 
 <li>The AWS Content Analysis workflow is initiated for each asset to analyze content with <a href="https://aws.amazon.com/rekognition/video-features/">Amazon Rekognition Video</a>, Amazon Comprehend, Amazon Transcribe, and Amazon Translate. Results are stored as JSON metadata with timestamps in <a href="https://aws.amazon.com/dynamodb/">Amazon DynamoDB</a>.</li> 
 <li>The interactive producer defines timed actionable prompts for each VOD asset. The interactive producer is accelerated by the metadata and timestamps generated by the AWS AI/ML services used by the AWS Content Analysis solution to detect people, places, objects, sentiment, and scenes.</li> 
 <li>Persistent actionable metadata is created in the selected format for video delivery. Metadata insertion can be automated using an <a href="https://aws.amazon.com/lambda/">AWS Lambda</a> function to generate a WebVTT file in the correct format, or insert embedded ID3 metadata using AWS Elemental MediaConvert. 
  <ul> 
   <li>Embedded persistent metadata is specified by timestamp and ID3 tag in the job template and inserted during video asset transcode using <a href="https://docs.aws.amazon.com/mediaconvert/latest/ug/what-is.html">AWS Elemental MediaConvert</a>. 
    <ul> 
     <li>Use the AWS Console to create a <a href="https://docs.aws.amazon.com/mediaconvert/latest/apireference/creating-your-json-job-specification.html">MediaConvert job specification in JSON format</a> with support for embedded, timed ID3 metadata that can be used by the AWS Lambda function using the MediaConvert API.</li> 
     <li>On the “Global processing” page of the MediaConvert console, specify the timestamp and base64 payload of each ID3 tag.</li> 
     <li>For HLS outputs under the “Transport stream settings” of each video output, set “ID3 metadata” to Passthrough and specify a Program ID (PID) for the ID3 metadata (or leave blank for a default value of 502).</li> 
     <li>For DASH or CMAF outputs, under the “CMAF container settings” of each video output, set “ID3 metadata” to Passthrough.</li> 
     <li>Full-formed ID3 messages in Base64 format can be generated using an external tool. One option is the ID3 tag generator provided in <a href="https://developer.apple.com/documentation/http_live_streaming/using_apple_s_http_live_streaming_hls_tools">Apple’s HTTP Live Streaming (HLS) tools</a> which are provided as a Unix executable. AWS Lambda can <a href="https://aws.amazon.com/blogs/compute/running-executables-in-aws-lambda/">run arbitrary executables in functions</a> to make use of this tool.</li> 
    </ul> </li> 
   <li>Extra persistent metadata is generated as a WebVTT metadata file using <a href="https://docs.aws.amazon.com/lambda/latest/dg/welcome.html">AWS Lambda</a> to query the interactive producer’s time-edited captions for the video asset and generate metadata in the WebVTT file format to save on Amazon S3.</li> 
  </ul> </li> 
 <li>Video on-demand asset delivery includes VOD assets (HLS, DASH, CMAF) and WebVTT files containing actionable, timed-aligned metadata.</li> 
 <li>Extra metadata is retrieved from <a href="https://docs.aws.amazon.com/appsync/latest/devguide/what-is-appsync.html">AppSync</a> using a <a href="https://docs.aws.amazon.com/appsync/latest/devguide/designing-a-graphql-api.html">GraphQL API</a> capable of delivering dynamic data for the viewer by connecting data from multiple sources. AWS services for viewer personalization and targeting include <a href="https://docs.aws.amazon.com/personalize/latest/dg/what-is-personalize.html">Amazon Personalize</a>, <a href="https://docs.aws.amazon.com/location/latest/developerguide/what-is.html">Amazon Location</a>, and <a href="https://docs.aws.amazon.com/pinpoint/latest/userguide/welcome.html">Amazon Pinpoint</a>. The AWS Amplify SDK is optimized to connect easily and securely to AppSync by performing <a href="https://docs.aws.amazon.com/general/latest/gr/signature-version-4.html">Signature Version 4</a> request signing.</li> 
 <li>The video player listens for cue change, metadata parsed, or time update events and renders actionable prompts on the client app or website UI.</li> 
 <li>Actionable VOD assets can also be created when recording an Amazon IVS live stream by using <a href="https://docs.aws.amazon.com/ivs/latest/userguide/record-to-s3.html">auto-record to S3</a>. A recorded Amazon IVS session will contain embedded metadata that was inserted during the IVS live stream using the <a href="https://docs.aws.amazon.com/ivs/latest/userguide/metadata.html">Timed Metadata into Amazon IVS</a></li> 
</ol> 
<h3><strong>Conclusion</strong></h3> 
<p>The creative possibilities for building actionable prompts into your VOD playback experience can be accelerated by using the AWS Content Analysis solution and by selecting the video metadata strategy that supports your desired call-to-actions for viewer engagement.</p> 
<h3><strong>Learn more about AWS media services and video analysis solutions</strong></h3> 
<p>The AWS Content Analysis solution can be installed into your AWS environment within minutes using the one-click cloud formation template on the <a href="https://aws.amazon.com/solutions/implementations/aws-content-analysis/">AWS Content Analysis solution</a> page.</p> 
<p>A video on demand workflow can be installed into your AWS environment within minutes with solutions available at <a href="https://aws.amazon.com/solutions/implementations/video-on-demand-on-aws/">Video On Demand on AWS</a>.</p> 
<p>To create VOD assets with embedded metadata, timed ID3 tags can be inserted into the MediaConvert job by using the AWS console. Transcode jobs can be automated through the AWS API. For more details, refer to the <a href="https://docs.aws.amazon.com/sdk-for-ruby/v2/api/Aws/MediaConvert/Types/Id3Insertion.html">MediaConvert API specification</a> and <a href="https://docs.aws.amazon.com/mediaconvert/latest/apireference/getting-started.html">Getting Started with the MediaConvert API</a>.</p> 
<p>For Amazon IVS live streams recorded to Amazon S3, learn more about events provided by the <a href="https://docs.aws.amazon.com/ivs/latest/userguide/player.html">Amazon IVS player</a> to parse and render Amazon IVS Timed Metadata.</p> 
<p>For building a GraphQL API for Extra Metadata, get started with the <a href="https://docs.aws.amazon.com/appsync/latest/devguide/what-is-appsync.html">AWS AppSync</a> documentation and <a href="https://docs.aws.amazon.com/appsync/latest/devguide/building-a-client-app.html">Building a Client App with AppSync</a> for front-end web and mobile integration with AWS Amplify.</p>
