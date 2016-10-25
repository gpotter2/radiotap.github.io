---
title: A-MPDU status
categories: [defined]
---
Bit Number
: 20

Structure
: u32 reference number, u16 flags, u8 delimiter CRC value, u8 reserved

Required Alignment
: 4 bytes

The presence of this field indicates that the frame was received as part
of an a-MPDU.

The **reference number** is generated by the capture device and is the
same across each subframe of an A-MPDU. Since the capture device might
be capable of capturing multiple channels or data from multiple
(concurrent) captures could be merged, the reference number is not
guaranteed to be unique across different channels. As a result,
applications should use the channel information together with the
reference number to identify the subframes belonging to the same A-MPDU.

The following **flags** are defined:


| **0x0001** | driver reports 0-length subframes |
| **0x0002** | frame is 0-length subframe (valid only if 0x0001 is set) |
| **0x0004** | last subframe is known (should be set for all subframes in an A-MPDU) |
| **0x0008** | this frame is the last subframe |
| **0x0010** | delimiter CRC error |
| **0x0020** | delimiter CRC value known: the delimiter CRC value field is valid |
| **0xffc0** | reserved |

Within an A-MPDU, the subframe index can be determined by the
application so it is not included, but depending on the driver reporting
this may miss 0-length subframes.