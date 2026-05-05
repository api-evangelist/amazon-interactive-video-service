---
title: "Deliver hybrid live video experiences at ultra-low latency with Daily and Amazon IVS"
url: "https://aws.amazon.com/blogs/media/hybrid-live-video-experiences-ultra-low-latency-daily-amazon-ivs/"
date: "Tue, 06 Jul 2021 21:52:38 +0000"
author: "Sathya Balakrishnan"
feed_url: "https://aws.amazon.com/blogs/media/tag/amazon-interactive-video-service/feed/"
---
<p><em>Authored by Francine Boulanger, Marketing Lead @Daily. The content and opinions in this post are those of the third-party author and AWS is not responsible for the content or accuracy of this post.</em></p> 
<p>&nbsp;</p> 
<p><img alt="A video call of a conference panel &quot;Internal Medicine and Primary Care&quot;, showing an active speaker and four additional guests, is also live streamed" class="aligncenter wp-image-8723 size-full" height="629" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/06/Picture1-1.png" width="977" /></p> 
<p>&nbsp;</p> 
<p><a href="https://www.daily.co/" rel="noopener noreferrer" target="_blank">Daily</a> provides WebRTC based real-time video and audio APIs for developers. Here at Daily, we’re excited to share our latest API, Daily Live Streaming, which provides an easy solution for developers seeking to live stream video conversations to large audiences. Part of the challenge for developers building new kinds of live video experiences has been that it’s difficult to bridge between two technologies: WebRTC for real-time conversations, and HLS for large scale broadcast. Daily integration with <a href="https://aws.amazon.com/ivs/" rel="noopener noreferrer" target="_blank">Amazon Interactive Video Service (Amazon IVS)</a> solves this problem. Using Daily Live Streaming with Amazon IVS lets developers easily broadcast videos with up to nine live cameras, high-quality audio, and screen shares, at practically unlimited scale and ultra-low latency.</p> 
<h2>Building on the promise of real-time video</h2> 
<p>Live video has changed the way we work, learn, socialize, play, relax, and exercise. The Daily Live streaming API and Amazon IVS provide two complementary feature sets powering live video.</p> 
<p>Daily APIs, built on WebRTC, provides real-time APIs for interactive video conversations. Use cases include video calls, telehealth, teaching and tutoring, panel discussions, social games, fitness classes, and watch parties. Video and audio connections are real-time with Daily — less than 200ms, with support for up to 1,000 people in a call.</p> 
<p>Amazon IVS enables broadcast-scale delivery of live video with low latency to millions of viewers. Common use cases include concerts, online events, live commerce, influencer streaming and corporate communications.</p> 
<p>Erik Gullestad, CTO of <a href="https://invitepeople.com/en" rel="noopener noreferrer" target="_blank">InvitePeople.com</a> says, “We are excited about using Daily and Amazon IVS together to create hybrid live stream experiences. We are an online events platform, and our customers host events that include seminars, round table discussions, Q&amp;A sessions, and more. Being able to broadcast real-time, multi-participant conversations to large audiences with just 2-3 seconds of latency allows us to scale events to include more people while preserving the interactive and participatory feel of each session.”</p> 
<h2>Where live streaming video can be used at scale</h2> 
<p>The following are examples of use cases that highlight the benefits of using Daily and Amazon IVS together to enable real-time conversations with broadcast-scale streaming distribution. These complementary experiences let developers expand offerings, and better support and engage communities, customers, users, and fans. Companies and creators can build their video brand and also diversify revenue streams.</p> 
<p>Major use cases include:</p> 
<h3>New live music experiences</h3> 
<ul> 
 <li>A new generation of live music platforms are offering both concert experiences and direct interaction between artists and fans at a more intimate level. With Daily, live music platforms can create real-time sessions, like fan meet-and-greets, house parties and after-parties.</li> 
 <li>Combining Daily’s real-time APIs with Amazon IVS’s scalable delivery makes these new concert experiences available to anyone, on any device, anywhere in the world.</li> 
</ul> 
<h3>Fitness and education</h3> 
<ul> 
 <li>Teachers can better guide and engage students with real-time feedback and instruction. With Daily, developers can build applications that let teachers create revenue around personalized instruction.</li> 
 <li>Teachers can stream this real-time class to millions more with Amazon IVS. This different format also can be offered at a different price point.</li> 
 <li>Video-on-demand is also a key Amazon IVS capability. In the class space, companies like <a href="https://www.masterclass.com/" rel="noopener noreferrer" target="_blank">Masterclass</a> and shows like <a href="https://www.fox.com/masterchef/" rel="noopener noreferrer" target="_blank">MasterChef</a> have demonstrated the long-tail of demand for learning experiences. In addition to the real-time call and the live stream, using Daily with Amazon IVS lets developers support a third offering of video-on-demand.</li> 
</ul> 
<p>&nbsp;</p> 
<p><img alt="Live streaming a Yoga class to virtual participants" class="aligncenter wp-image-8724 size-full" height="489" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/06/Picture2-1.png" width="977" /></p> 
<p>&nbsp;</p> 
<h3>Events</h3> 
<ul> 
 <li>Online events have grown in popularity, both as a replacement for and supplement to in-person events. Daily’s customers offer customized live events with experiences such as keynote presentations, small-group sessions, breakout rooms, social and networking hours, and curated content tracks. With Daily, cameras and microphones can be turned on and off during the call, making it easy to create dynamic experiences like “bringing an audience member up to the stage.”</li> 
 <li>Sessions can include streaming of pre-recorded content, and speech-to-text for accessibility and transcription are also possible through the Daily API.</li> 
 <li>These Q&amp;A sessions can then be broadcast to an even bigger audience via Amazon IVS.</li> 
</ul> 
<p>&nbsp;</p> 
<p><img alt="A live stream of four video call participants discussing a beauty product" class="aligncenter wp-image-8725 size-full" height="641" src="https://d2908q01vomqb2.cloudfront.net/fb644351560d8296fe6da332236b1f8d61b2828a/2021/07/06/Picture3.png" width="977" /></p> 
<p>&nbsp;</p> 
<h3>Live ecommerce and live marketing</h3> 
<ul> 
 <li>Video has emerged as the future of e-commerce, with sellers using live streams to connect with buyers. Using Daily and Amazon IVS, developers can build real-time calls into these streaming sales channels, for experiences like live brand collaborations with remote influencers, live auctions, and social commerce.</li> 
</ul> 
<h3>Gaming and e-sports</h3> 
<ul> 
 <li>With real-time video calls, gamers can play with friends and talk with fans; they can compete, or train with coaches. Streaming those sessions lets gamers broadcast multiplayer sessions easily. With Daily and Amazon IVS, it’s just one extra line of code to stream to millions.</li> 
</ul> 
<h2>Building the future of video</h2> 
<p>At <a href="https://www.daily.co/" rel="noopener noreferrer" target="_blank">Daily</a>, we’re powering a new generation of imaginative, flexible, immersive video and audio experiences. Using Daily with Amazon IVS lets developers scale the reach of these experiences by broadcasting to large audiences.</p> 
<p>If you’re building with real-time video and want to expand to live streaming, <a href="https://www.daily.co/" rel="noopener noreferrer" target="_blank">reach out to us here</a>. We’re a developer-first company and glad to hear how we can support you!</p>
