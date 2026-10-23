# Instagram DM automation: booking with checks

![Appointment checking](https://dxggowrfyirnanabowhr.supabase.co/storage/v1/object/public/site-images/site-instagram-dm-automation-booking-with-checks-1792717872.jpg)

An Instagram booking conversation has more work in it than picking an appointment time. The person has questions, and those questions can lead down many different paths. To me, handling that variety without losing the client is the difficult part of an AI receptionist's job

## Be open about who is answering

The client is a person who can recognise that they are speaking with artificial intelligence. For a complicated exchange, my recommendation is to acknowledge the AI openly. I believe that earns more trust than making a chatbot pose as a human employee

The conversation still needs someone to handle its changing direction. A language model can take that work: responding to different questions and choosing wording that fits the exchange. That conversational responsibility can be separated from checking the details of an appointment

![Appointment discussion](https://images.pexels.com/photos/6809657/pexels-photo-6809657.jpeg)

## Put exact checks in the software

A booking involves prices, calendar dates and available times. I recommend implementing those checks in Python, with code participating alongside the conversational model. It checks the price list when a price is needed and the calendar when the discussion reaches availability

The model can phrase a reply using those checked details. It should not supply appointment facts from memory. This gives the exchange distinct responsibilities: one component handles language, while another checks the business records behind the booking

That division does not mean software can never have bugs. The point is to look up the actual information needed for the appointment rather than treating the conversational model's recollection as a source of prices or free slots

## Review the model's answers

Many possible conversation paths still need boundaries. Define the rules before the receptionist starts talking to clients. A flexible reply remains subject to the restrictions you set for the business

I also recommend a second model with a reviewing role. It compares the first model's proposed answer against those pre-established rules. The conversational model prepares the message; the reviewer examines whether that message stays within the agreed limits

![Phone and diary](https://images.pexels.com/photos/714700/pexels-photo-714700.jpeg)

This review has a different purpose from looking up an appointment slot. One checks compliance with conversation rules, the other checks exact booking data. Both belong in the same workflow without making either responsible for the other's job

I wrote about the relationship between conversation, software checks and answer review on my blog: [Instagram DM automation: booking with checks](https://matintellect.com/en/posts/instagram-dm-automation-booking-with-checks)
