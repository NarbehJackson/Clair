# Clair
Clair
Vulnerability Static Analysis for Containers

Instructions

Step 1: Start clair database

docker run -d -p 5432:5432 --name db arminc/clair-db:latestCopy

Wait for a few seconds till the container is initialized
or
sleep 15

Step 2: Start clair scanner

docker run -d -p 6060:6060 --link db:postgres --name clair arminc/clair-local-scan:v2.0.1

Wait for a few seconds till the container is initialized
or

sleep 10

Step 4: Pull the image to be scanned

docker pull ubuntu:14.04Copy

Step 5: Run Clair scan against the image and generate a json report

Note: $(curl -XGET -s http://checkip.amazonaws.com/) will automatically take your server ip.

clair-scanner --ip $(curl -XGET -s http://checkip.amazonaws.com/) -r clair_report.json ubuntu:14.04
