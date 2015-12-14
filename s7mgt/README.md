1. Build 'netconf-subsystem' from github.com/OpenClovis/OpenYuma
2. Build docker image and push to docker hub
   $docker build -t s7mgt .
   $docker run -i -p 5000:22 -p 5001:830 s7mgt
   $docker push

3. Verify port 22:
$ssh root@127.0.0.1 -p 5000 -> pass:clovis
scp -P 5000 test.txt root@127.0.0.1:./ 

3. Verify port 830 (netconf service):
$ssh root@127.0.0.1 -p 5001 -> pass:clovis


Note:
1/ Docker host having linux kernel version > 3.16

