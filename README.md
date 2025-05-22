## Understanding How It Works

![alt text](<img/Screenshot 2025-05-22 at 14.45.04.png>)

I injected a println! call right after spawner.spawn() so I could track the order of execution more precisely.

When I ran it, the very first line printed was:
Geordie's Komputer: hey hey
even though that println! sits after the spawn invocation in the code. That’s because spawning a task simply puts it on an executor’s queue—it doesn’t pause or await its completion. The main thread immediately moves on and executes the next statement, producing “hey hey” before the asynchronous task ever starts.

Sometime later, the spawned task finally kicks in. It logs:
Geordie's Komputer: howdy!
then pauses for two seconds via TimerFuture, and finally outputs:
Geordie's Komputer: done!
This sequence highlights how Rust’s futures run independently of the main thread: tasks are queued and executed in the background, allowing the main flow to continue without waiting.