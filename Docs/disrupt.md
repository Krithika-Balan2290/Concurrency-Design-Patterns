#Disruptors

Disruptor is a Java concurrency pattern developed by LMAX Exchange which allows different threads to share data between themselves. The traditional producer-consumer model uses a queue where the producers store the data and the consumers access the data. The Disruptor model users a ring buffer instead of a queue. A ring buffer is a circular array of fixed length which is a power of 2<sup>[7]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>. 

The items stored in a ring buffer are called events and a current sequence number stores the highest event written to the ring buffer. The ring buffer tracks this number and updates it as new events are written to it. The consumers, called event processors also keep track of the highest even that they have consumed. The producer checks with the ring buffer for the next event in the sequence. The ring buffer then not only has to increment the current sequence number, but in case any data has to be overwritten, the ring buffer also checks with all the event processers whether one of them has already read the data to be overwritten. If the sequence number with the event processor highest down the event sequence is greater than the event number being overwritten, then the ring buffer returns the next event number to be written. If the even processors are still not done processing the event being overwritten, the ring buffer waits until at least one event processor is done processing that event. Then, it returns the next event in sequence to the producers<sup>[7]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

Whenever consumers want to read from the ring buffer, they must also access the ring buffer, but they do not access the ring buffer directly. The consumers access the ring buffer through another interface called the consumer barrier. The consumer barrier returns the value of the highest sequence number on the ring buffer at that time. If a consumer is not yet at that event number, it can choose to access the subsequent events until the highest sequence in the ring buffer and process the together as a batch<sup>[7]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>.

![Disruptor Class Diagram]( http://www.turingfinance.com/wp-content/uploads/2013/11/Disruptor.png) 

(Image Reference<sup>[8]( https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/refs.md)</sup>)


[Prev Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/barriers.md) | [Next Page](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Docs/double_lock.md)
 
 [Back to contents](https://github.com/Krithika-Balan2290/Concurrency-Design-Patterns/blob/master/Index.md)
