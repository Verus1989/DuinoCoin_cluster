# DuinoCoin cluster

Since there is limitation for mining devices on Duco's server, that cluster will let you use all you calculating power,
even if you have already exceeded max connections per account.

To start it you can use any python ide, I suggest pydroid 3 or you can also use termux

File cluster_server.py - is a server for your cluster, it must have file "Cluster_Config.cfg" next to it to parse info (default port is 9090)

File cluster_worker.py - is a miner for cluster, don't forget to change server address and worker name right in the script(WORKER_NAME and CLUSTER_SERVER_ADDRESS). It doesn't need file "Cluster_Config.cfg". it works in 1 process, good for devices with 1/2 cores, or on PC you can run 4 instances of that script.

File cluster_worker_multiprocessing.py - I hope name of that file speaks for itself, THREADS - number of processes, by default 2, I suggets to set it 1 less than number of cores in your device, because of the operating system(unless you are using Windows/Linux/MacOs, they are pretty efficient with cpu usage managment), background processes and lots of other fun stuff. But, I mean, I am not you mum, so feel free to set to something insane, like 4!!!?!?!?!?!

File cluster_worker_nthr.py - Is a worker without threading library. All "asyncronity" is a raw implementation right in the script. When should you use it? for example on 3ds, standart python libs dont support threading and time.sleep()

# ToDo:

Write worker on c++

# Some questions:

I started cluster_worker_multiprocessing.py and it writes nothing in the console! - That is because I ~~am lasy~~ decided it will be more efficient not to write anything to the console.

How do I change algorithm used for mining? - "Cluster_Config.cfg" in that file change line "algorithm = DUCO-S1|XXHASH", by default XXHASH is used.

How many devices can I connect? - As many as you want.

What devices can use those scripts? - Any devices that can run python.

Should devices be the same for mining? - No, I tested it and optimized to mine on devices with different speed efficiently.

Does it has tips for creator? - No, it mines only for your account, if you want to support me, buy me a coffee:                https://buymeacoffee.com/ENotSewerSide.

What happens if one of devices shuts down and stops responding? - Nothing, server will send job of that device to other devices, and if device cant respond to server in 90 seconds, server will forget that device.

What if I connect new device to the server rigth in the middle of calculating hash? - server will send to that device some job, it depends on what jobs have been done and what are been processed right now.

What are those jobs that server sends to devices? - When server receives new job wrom Duino-coin master server, it divides it to different blocks(jobs), by default it will divide to the number of connected device, to change that you can change variable in the file "cluster_server.py" "INC_COEF", so jobs from master server will be divided by len(devices)+INC_COEF.

Will slow devices make cluster work slower? - No, actually they will make it work faster, so the speed depends on the number of devices connected, more=faster.

IS IT SAFE TO USE OVER THE INTERNET? - Not right now, it has some vulnerabilities, which I will fix later.

I don't have a lot of storage memmory on my phone, will cluster_worker.py store something? - Nope it wouldn't.

I want to change difficulty for cluster, what do I do? - "Cluster_Config.cfg" in that file change "requesteddiff" = NET|MEDIUM|LOW (NET is the hardest difficulty, at least that's what I have read in official PC miner)

Do I start server or workers first? - Doesn't matter.

When I connect my PC to cluster of phones produced in 2005 it seems, that only my PC calculating hashes. - That's because of the servers algorithm, it tries to keep cluster always busy with different jobs, so when phone and PC are calculatiing the same block, PC will calculate it faster and server will stop phone's job, so all devices are calculating something, but the fastest interupts slower devices, because there is no need to continue that job on slower devices.

How many devices will calculate the same block? - It depends, can be one, can be all devices in the same time, but that's ok.

# before you start program download some python libraries:
  
  requests
  
  xxhash
  
