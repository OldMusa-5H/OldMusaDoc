# FAQ

## What is a channel?
Our system is gerarcical, at the beginning there is a list of sites,
then every site contains a list of sensors, and a sensor contains a list of
channels. Some sensors can measure more than one value, so we divided the
physical location and the measure types. Basically everything that you can group
together in a single physical point can be named a sensor, and then every
measure type that sensor can read has its own channel where the readings will
be fit into.<br>
A channel can not group more sites or sensors together! it is a subdivision of
a sensor.

## Why doesn't android use Retrofit?
You can blame it all on the ignorance of the middleware developer.
Of course I discovered that project only some days after I completed the
client REST code. That wasted some useful times of development but now it offers
a hopefully more customizable library that can support websockets in the
future...<br> ... I hope.
