Data framing in the context of communication protocols, such as WebSockets, refers to the process of encapsulating a piece of data with additional information, or "framing," that is used to ensure the proper transmission, reception, and interpretation of the data. Data framing is crucial for establishing a structured and reliable communication channel between sender and receiver. Here's how data can be framed:

**1. Message Segmentation:** When data is transmitted over a communication channel, it needs to be divided into smaller units called frames. Frames are typically of fixed or variable size and include the actual data as well as control information.

**2. Start and End Markers:** In some framing methods, frames are marked with special start and end markers. These markers signal the beginning and end of each frame, helping the receiver identify where one frame ends and the next begins.

**3. Length Prefixing:** A common framing technique is to prefix each frame with a length field that indicates the number of bytes in the frame. The receiver reads the length field to determine how many bytes to expect for the data portion of the frame.

**4. Delimiters:** Framing can also involve using specific characters or sequences of characters, known as delimiters, to mark the start and end of frames. For example, a common delimiter-based framing method is using newline characters ('\n') to separate frames.

**5. Byte Stuffing:** In some cases, data within a frame may contain characters that could be confused with frame delimiters. Byte stuffing involves adding extra bytes to the data to distinguish it from actual frame delimiters.

**6. Bit Stuffing:** Similar to byte stuffing, bit stuffing involves adding extra bits to the data at specific positions to ensure that the frame does not match the framing pattern. This is commonly used in synchronous communication protocols.

**7. Checksum or CRC:** Some framing methods include a checksum or a cyclic redundancy check (CRC) value that is calculated over the frame's data. The receiver uses this value to verify the integrity of the received data.

**8. Escape Characters:** Escape characters are used to escape or encode special characters within the data to prevent them from being mistaken as control characters or frame delimiters.

**9. Protocol Headers:** In more complex communication protocols, frames may include header fields that provide information about the frame, such as the source, destination, sequence number, and more.

Proper data framing is essential for reliable communication, especially when dealing with asynchronous communication or situations where data integrity is critical. Different communication protocols and applications may use varying framing techniques based on factors such as data format, error detection, and transmission efficiency.