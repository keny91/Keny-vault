#transport-protocol

HTTP DASH stands for "HTTP Dynamic Adaptive Streaming over HTTP" or simply "Dynamic Adaptive Streaming over HTTP." It is a streaming protocol used for delivering multimedia content, such as video and audio, over the internet. DASH is designed to provide a high-quality streaming experience by dynamically adapting the video quality to match the viewer's network conditions and device capabilities.

Key features of HTTP DASH include:

1.  **Adaptive Bitrate Streaming:** DASH supports adaptive bitrate streaming, which means that the quality of the video stream can change during playback based on the viewer's available network bandwidth. This helps ensure smooth playback even in varying network conditions.
    
2.  **Segmented Content:** Videos in DASH are divided into small segments, typically a few seconds in duration. Each segment is available in multiple quality levels (bitrates). This segmentation allows for efficient streaming and switching between different quality levels.
    
3.  **Manifest Files:** DASH uses manifest files (such as MPEG-DASH MPD files) that provide information about available video segments, their qualities, and other metadata. Clients use these manifest files to request and download the appropriate segments.
    
4.  **Client-Side Adaptation:** DASH relies on the client (viewer's device) to determine which video segments to request and play based on its assessment of the network conditions. The client can dynamically switch between different bitrates to maintain smooth playback.
    
5.  **Standardization:** DASH is an international standard developed by organizations like the Moving Picture Experts Group (MPEG) and the Internet Engineering Task Force (IETF). It is designed to be interoperable and widely supported across different devices and platforms.
    
6.  **Supported Media Formats:** DASH is not tied to a specific video or audio codec. It supports a wide range of media formats, allowing content providers to choose the most suitable codec for their content.
    
7.  **Content Protection:** DASH can be used with various digital rights management (DRM) solutions to protect copyrighted content from unauthorized access.
    

HTTP DASH is similar in concept to other adaptive streaming technologies like Apple's HLS (HTTP Live Streaming) and Microsoft's Smooth Streaming. It is used by streaming platforms, content providers, and broadcasters to deliver high-quality video content to a variety of devices, including computers, smartphones, tablets, smart TVs, and more. By adapting the streaming quality to the viewer's network conditions, DASH aims to provide a seamless and enjoyable streaming experience across different devices and network environments.